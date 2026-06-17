---
applyTo: "**/*.ts,**/*.html,**/*.scss"
---

You are an expert in TypeScript, Angular, and scalable web application development. You write functional, maintainable, performant, and accessible code following Angular and TypeScript best practices.

---

## TypeScript

- Use strict type checking
- Prefer type inference when the type is obvious
- Avoid `any`; use `unknown` when the type is uncertain
- Use `readonly` for properties that should not be reassigned

---

## Angular: General Conventions

- Prefer standalone components for all new features; use NgModules only when aligning with existing `ui-components` patterns (e.g., small NgModule wrappers for exports)
- Set `changeDetection: ChangeDetectionStrategy.OnPush` on every component
- Implement lazy loading for feature routes
- For new feature files, use descriptive file names without a `nextech-` prefix (e.g., `input-mask.directive.ts`). Existing `nextech-*` file names are valid and should only be renamed as part of an explicit migration
- Use `NgOptimizedImage` for all static images (`NgOptimizedImage` does not work for inline base64 images)

---

## Components

- Keep components small and focused on a single responsibility
- Prefer inline templates for small components; use external template files for anything complex
- Configure host bindings and host listeners via the `host` object on `@Component` or `@Directive` — do not use `@HostBinding` or `@HostListener` in new code unless a compatibility constraint cannot be addressed otherwise
- Use `class` binding instead of `ngClass` (exception: when binding a `Set`, `ngClass` is appropriate)
- Do not use `ngStyle`; use `style` bindings instead
- When using external templates and styles, use paths relative to the component TS file
- Prefer reactive forms over template-driven forms

---

## Signals and State Management

Signals are the preferred state primitive in Angular. Use them consistently for local and derived state.

- Use `signal()` for local mutable state
- Use `computed()` for derived state — prefer it over `effect()` for transformations
- Use `effect()` only for true side effects (logging, DOM manipulation, syncing to external systems); keep effects simple and focused
- Do not call `.mutate()` on signals; use `.set()` or `.update()` instead
- Use `untracked()` when reading a signal inside an effect or computed without creating a dependency on it

**Two-way binding with signals:** Use `model()` to expose a writable signal that supports two-way binding with a parent component. This replaces the `@Input() value` + `@Output() valueChange` pattern.

**Dependent state:** Use `linkedSignal()` when you need a writable signal that should reset or re-derive its value when a source signal changes (e.g., a selected item that should reset when the list changes). Use `computed()` when the value is purely derived and should never be set externally.

**Signal/Observable interop:**
- Use `toSignal()` to consume an observable as a signal — this is preferred over the async pipe for observables used in computed or effect contexts
- Use `toObservable()` to expose a signal as an observable when an API requires one
- Use `takeUntilDestroyed()` for automatic subscription cleanup; inject `DestroyRef` explicitly when you need to clean up outside of injection context

---

## Signal-Based Queries

Use signal-based query functions instead of decorator-based queries for all new code. These are reactive, composable with other signals, and do not require lifecycle hooks to access results safely.

- `viewChild()` — replaces `@ViewChild` for a single element or component in the template
- `viewChildren()` — replaces `@ViewChildren` for a list
- `contentChild()` — replaces `@ContentChild` for projected content
- `contentChildren()` — replaces `@ContentChildren` for a list of projected content

Signal queries resolve before `ngAfterViewInit`/`ngAfterContentInit` and can be read directly in `computed()` or `effect()` without lifecycle timing concerns.

---

## Component Inputs and Outputs

- Use `input()` and `output()` functions instead of `@Input()` and `@Output()` decorators
- Use `input.required()` for required inputs
- Use `model()` for two-way bindable inputs
- Use `computed()` for values derived from inputs

---

## Async Data Fetching

For async data that should participate in the signals reactive graph, use the `resource()` API:

```ts
userResource = resource({
  request: () => ({ id: this.userId() }),
  loader: ({ request }) => fetch(`/api/users/${request.id}`).then(r => r.json())
});
```

`resource()` exposes `.value()`, `.status()`, and `.error()` as signals. Use it for straightforward data fetching tied to signal inputs. For complex HTTP scenarios requiring interceptors, error handling pipelines, or caching, continue using `HttpClient` with `toSignal()`.

---

## Templates

- Use native control flow — `@if`, `@for`, `@switch` — not `*ngIf`, `*ngFor`, `*ngSwitch`
- Use the async pipe to handle observables in templates; prefer `toSignal()` when the value is used in computed or reactive contexts
- Keep templates simple; avoid complex logic inline
- Do not assume globals like `new Date()` are available in templates
- Use `@defer` to lazily load heavy template blocks that are not needed immediately:

```html
@defer (on viewport) {
  <app-heavy-chart />
} @placeholder {
  <div class="chart-placeholder">Loading…</div>
}
```

---

## Services

- Design services around a single responsibility
- Use `providedIn: 'root'` for singleton services
- Use `inject()` instead of constructor injection — this applies in services, components, directives, guards, and resolvers

---

## Routing

- Use functional guards and resolvers instead of class-based ones:

```ts
export const authGuard: CanActivateFn = () => {
  const auth = inject(AuthService);
  return auth.isAuthenticated() ? true : inject(Router).createUrlTree(['/login']);
};
```

- Enable `withComponentInputBinding()` in `provideRouter()` to automatically bind route params and query params to component inputs
- Implement lazy loading for all feature routes using dynamic `import()`

---

## Accessibility

Every component must pass all AXE checks and meet WCAG 2.1 AA minimums.

- All interactive elements must be keyboard-accessible with visible focus states
- Color contrast: 4.5:1 minimum for body text; 3:1 for large text and UI components
- All images and icons must have `alt` text or `aria-label`; decorative elements get `aria-hidden="true"`
- Form fields must have associated `<label>` elements; error messages must be programmatically associated (e.g., `aria-describedby`)
- Use semantic HTML; reach for ARIA only when native semantics are insufficient
- Manage focus explicitly when dialogs open, routes change, or dynamic content appears
- Never rely solely on color to convey state or information
