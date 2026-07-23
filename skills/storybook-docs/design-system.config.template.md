---
# design-system.config.md
# Copy this file to the root of your design-system repo and edit the values.
# The storybook-docs skill reads it on every run.

baseSystem: material3        # material3 | custom | <name of another system>
framework: angular
storybookVersion: 10        # the skill keys version-specific details (e.g. docs-blocks import path) off this
accessibility: WCAG 2.1 AA

paths:
  # Where shared/base-component stories and foundations live (flat files).
  baseStories: projects/ui-components/src/lib/mdc-core/stories
  # Custom components keep Storybook content in a `stories/` subfolder
  # inside the component's own folder. This is the parent that holds them.
  customComponents: projects/ui-components/src/lib/ui-components

# Optional house foundation topics beyond the usual set
# (color, typography, spacing, elevation, shape, motion, iconography, layout).
extraFoundations: []
---

## House notes

Describe how this system diverges from its base. The skill reads this prose to
keep documentation accurate when the house system differs from stock Material 3.

Cover, in plain language: variants you've added or removed, tokens you've renamed
or restyled, patterns you handle differently from the base system, and any brand
or voice rules that should shape the documentation. Anything you write here
overrides the base system's defaults for this repo.

If your Storybook replaces the native show-code toggle with its own code-display
mechanism (a wrapper component, an addon), document it here: what the mechanism
is, how a story attaches code to it, and when a story should or shouldn't show
code. Without this note the skill assumes Storybook's native source display.

If `baseSystem` is `custom`, treat these notes as the primary source of truth and
lean on general design-system best practice rather than Material conventions.
