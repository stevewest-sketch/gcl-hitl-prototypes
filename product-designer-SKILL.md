---
name: product-designer
description: Design and prototype product features using the Gladly design system. Use this skill when creating UI mockups, prototypes, or exploring design concepts. This skill provides patterns, components, and best practices for building interfaces that match the Gladly product.
allowed-tools: Read, Write, Edit, Grep, Glob, Bash
---

# Product Designer

## Purpose

Generate Gladly UI prototypes — complete, working React components that follow the Gladly design system exactly. Use this skill when creating UI mockups, prototypes, or exploring design concepts.

## When to Use

- Visualizing features from PRDs or design specs
- Exploring layout and interaction patterns
- Creating prototypes for user testing or stakeholder demos
- Documenting UI patterns and component usage
- Building design system examples

## Tech Stack

- React 18 + Next.js (App Router, `"use client"` for interactive components)
- styled-components v6 for all styling (NOT Tailwind, NOT CSS modules)
- Radix UI (`@radix-ui/themes`) for accessible primitives (Button, Text, Flex, Table, Checkbox, TextField, Badge, Tooltip, DropdownMenu, etc.)
- TypeScript with explicit prop types

## Styling Rules

- Every styled component must reference the theme object — never hardcode colors, spacing, or font sizes.
- Use the `${(p) => p.theme.___}` pattern to access design tokens.
- Use `$`-prefixed transient props for styled-component-only props: `$isActive`, `$hasError`, etc.
- Wrap Radix primitives with styled-components to apply Gladly styles.

## Design Principles

### No Emojis
Emojis should never appear in the product UI. Use the icon library (`@/components/icons/`) instead. If an element needs a visual indicator — such as a filter pill, status label, or inline marker — use an SVG icon from the existing set (e.g., `SearchIcon`, `InfoIcon`, `Check`, `Cross`) or create a purposeful inline SVG. This applies to all text, labels, buttons, badges, tooltips, and any other visible surface.

### Minimalistic Aesthetic
Color is used sparingly. `green400` is reserved primarily for links, primary buttons, active states, and checkboxes — it should not be used decoratively or for backgrounds outside of hover states (`green100`). The UI relies on whitespace, typography weight, and layout hierarchy to create structure and emphasis rather than color fills, shadows, or decorative elements. Prefer border-only containers over shadowed cards. Let content breathe.

## Design Tokens

Use these exact values via the theme object. Reference `apps/glados/app/defaultTheme.ts` for canonical values.

### Colors

**Primary:**
- `green400`: #009b00 — buttons, links, active states, checkboxes

**Text:**
- `defaultFontBlack`: #111111 — primary text
- `gray700`: #767676 — secondary text, captions

**Borders:**
- `gray300`: #E3E3E3 — borders and dividers

**Backgrounds:**
- `white`: #FFFFFF
- `gray100`: #F6F6F6 — page and card backgrounds
- `gray200`: #F1F1F1 — subtle backgrounds

**Grey Scale (full):**
- `gray100`: #F6F6F6
- `gray200`: #F1F1F1
- `gray300`: #E3E3E3
- `gray400`: #CECECE — alternate backgrounds when gray100 is too light
- `gray500`: #B3B3B3
- `gray600`: #919191 — avatar icons, secondary icons
- `gray700`: #767676
- `gray800`: #484848
- `gray900`: #1A1A1A

**Status Colors:**
- Success: `green100` bg, `green500` icon
- Warning: `yellow100` bg, `yellow500` icon
- Error: `red100` bg, `red500` icon
- Info: `purple100` bg, `purple500` icon

**Interactive States:**
- Hover: `green100` (#D8F4D8) for rows/nav, `green300` for buttons
- Disabled: `gray300` bg, `gray500` text

**Usage:**
```tsx
import defaultTheme from '@/app/defaultTheme';

// In styled-components
background-color: ${(p) => p.theme.colors.gray100};
color: ${(p) => p.theme.colors.defaultFontBlack};
border: 1px solid ${(p) => p.theme.colors.gray300};
```

### Typography

**Font Family:** Inter via `var(--font-inter)`
```tsx
font-family: var(--font-inter), -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
```

**Font Sizes:**
- `small`: 10px
- `reduced`: 12px
- `base`: 13px — body text (default)
- `medium`: 16px
- `large`: 18px
- `larger`: 20px
- `xlarge`: 24px
- `xxlarge`: 36px
- `xxxlarge`: 42px

**Line Height:** 1.62 (base)

**Font Weights:**
- `light`: 300
- `normal`: 400 — body text
- `medium`: 500 — emphasized text, labels
- `mediumHeavy`: 600 — subheadings
- `heavy`: 700 — headings

### Spacing

**Inset (padding):**
- `insetSmall`: 8px
- `insetMedium`: 16px
- `insetLarge`: 24px
- `insetXLarge`: 32px
- `insetXXLarge`: 48px

**Stack (vertical gaps):**
- `stackXSmall`: 4px
- `stackSmall`: 8px
- `stackMedium`: 16px
- `stackLarge`: 24px

### Border Radius

- `xsmall`: 2px
- `small`: 4px — tags, small elements
- `default`: 6px — standard elements
- `large`: 8px — cards, panels
- `xlarge`: 20px — pills, buttons

### Shadows

- `small`: `0 2px 8px 0 rgba(0,0,0,0.08)`
- `medium`: `0 4px 12px 0 rgba(0,0,0,0.08)`

## Component Patterns

### Buttons

**Primary:**
- `green400` bg, white text, border-radius `xlarge` (20px), min-width 80px

**Secondary:**
- White bg, `gray300` border, black text

**Disabled:**
- `gray300` bg, `gray500` text, `cursor: not-allowed`

### Inputs

- Pill-shaped (border-radius `xlarge`), `gray300` border, `gray700` on focus
- Placeholder color: `gray700`

### Tables

- Use Radix `Table.Root`, `Table.Header`, `Table.Body`, `Table.Row`, `Table.Cell`
- Alternating row bg (`gray100`) or border-bottom separators
- Hover: `green100` bg
- Font-size: `base` (13px), header: bold (700)

### Alerts

- Flex row with icon + text + optional close button
- Color-coded by type (success / warning / heads-up / error)
- Border-radius `small` (4px), box-shadow `large`, padding `insetMedium`

### Common UI Patterns

**Cards:**
```tsx
const Card = styled.div`
  background-color: ${(p) => p.theme.colors.gray100};
  border: 1px solid ${(p) => p.theme.colors.gray300};
  border-radius: ${(p) => p.theme.borderRadius.large};
  padding: ${(p) => p.theme.spacing.insetLarge};
`;
```

**Page Background:**
```tsx
const PageWrapper = styled.div`
  background-color: ${(p) => p.theme.colors.gray100};
  min-height: 100vh;
  padding: ${(p) => p.theme.spacing.insetLarge};
`;
```

**White Panel on Grey Background:**
```tsx
const SidePanel = styled.div`
  background-color: ${(p) => p.theme.colors.white};
  padding: ${(p) => p.theme.spacing.insetMedium};
  border-left: 1px solid ${(p) => p.theme.colors.gray300};
`;

// Usage: nest inside a gray100 background container
```

### Layout

- **TopBar**: 60px fixed height, white, shadow, three 33% sections
- **Content**: `calc(100vh - 60px)`, scroll
- **Container**: centered with Radix `Container`, size `"3"`

**Layout Component Selection Guide:**

| Component | Use For |
|-----------|---------|
| `DefaultLayout` | Standard page with TopBar and centered content |
| `FullHeightDefaultLayout` | Full viewport height pages, dashboards |
| `FullWidthDefaultLayout` | Full-width pages, wide tables |
| `TablePageLayout` | Pages primarily featuring a data table |

### Nav Items

- Full-width buttons with left-aligned text
- Active: `gray200` bg, bold, 4px green left border
- Hover: `green100` bg

### Conversation Review UI

For prototypes involving AI conversations, explainability, or conversation review.

**When to use:**
- Showing AI conversation history
- Explaining AI decisions and reasoning
- Reviewing chatbot or agent conversations
- Debugging AI responses

**Key features:**
- Alternating message layout (customer left, system right)
- Expandable explanation panels with direct links to configuration (Edit Guide, View Basics, etc.)
- Visual indicators for warnings/issues in decisions

**Import:**
```tsx
import {
  ConversationMessage,
  CustomerAvatar,
  SystemAvatar
} from '@/components/shared/ConversationReviewer';
```

**Basic Usage:**
```tsx
<div style={{ backgroundColor: '#F6F6F6', padding: '24px' }}>
  <ConversationMessage
    role="system"
    text="How can I help you today?"
    timestamp="Today, 12:58:42 PM"
    explanation={{
      guide: 'Order Support Guide',
      inputs: ['Customer profile', 'Recent orders'],
      decisions: ['Used greeting template', 'Offered help menu']
    }}
  />

  <ConversationMessage
    role="customer"
    text="Cancel my order"
    timestamp="Today, 12:58:53 PM"
  />
</div>
```

**Key Characteristics:**
- **Background**: gray100 (#F6F6F6) for conversation area
- **Customer messages**: Left-aligned, avatar on left, top-left corner radius = 0
- **System messages**: Right-aligned, avatar on right, top-right corner radius = 0
- **Message bubbles**: White background with gray300 border
- **Avatars**: 40px circles
  - Customer: Navy (#1E293B) with white user icon (Font Awesome fa-user)
  - System: White with green phone icon (Font Awesome fa-phone)
- **Metadata**: Above each message, gray700 text, includes phone icon
- **Explanation panel**: Expandable via caret (▼/▲) in metadata line
  - Max-width matches message bubble (650px)
  - Right-aligned for system messages
  - Shows: Guide Used, Key Inputs, Decisions Made, How to Improve links

**Styling Details:**
```tsx
// Customer bubble (left side)
borderRadius: '0 12px 12px 12px'

// System bubble (right side)
borderRadius: '12px 0 12px 12px'

// Avatar sizes
width: 40px, height: 40px

// Message metadata
fontSize: 13px, color: gray700

// Explanation sections
backgroundColor: gray100 (items), white (panel)
```

## Code Style

```tsx
// Example: a new styled component
"use client";

import { Flex, Text } from "@radix-ui/themes";
import styled from "styled-components";

type MyComponentProps = {
  title: string;
  isActive?: boolean;
};

export default function MyComponent({ title, isActive = false }: MyComponentProps) {
  return (
    <Container $isActive={isActive}>
      <StyledTitle>{title}</StyledTitle>
    </Container>
  );
}

const Container = styled(Flex)<{ $isActive?: boolean }>`
  padding: ${(p) => p.theme.spacing.insetMedium};
  background-color: ${(p) => p.$isActive ? p.theme.colors.green100 : p.theme.colors.white};
  border-radius: ${(p) => p.theme.borderRadius.default};
  border: 1px solid ${(p) => p.theme.colors.gray300};
`;

const StyledTitle = styled(Text)`
  font-size: ${(p) => p.theme.fontSize.large};
  font-weight: ${(p) => p.theme.fontWeight.mediumHeavy};
  color: ${(p) => p.theme.colors.defaultFontBlack};
`;
```

## Existing Components (import, don't rebuild)

| Component | Import Path |
|-----------|-------------|
| `PrimaryButton`, `SecondaryButton` | `@/components/shared/GladlyButtonV2` |
| `GladlyText`, `GladlyHeading`, `GladlyLabel` | `@/components/shared/GladlyText` |
| `GladlyLink` | `@/components/shared/GladlyLink` |
| `GladlyBadge` | `@/components/shared/GladlyBadge` |
| `GladlyFilterInput` | `@/components/shared/GladlyFilterInput` |
| `AlertBanner` | `@/components/shared/AlertBanner` (types: success, warning, heads-up, error) |
| `Checkbox` | `@/components/shared/CheckBox` |
| `EmptyState` | `@/components/shared/EmptyState` |
| `CustomTable`, `SimpleTable` | `@/components/shared/GladlyTable` |
| `LoadingSpinner` | `@/components/Spinner/LoadingSpinner` |
| Icons | `@/components/icons/{IconName}` (ChevronDown, SearchIcon, Plus, Cross, InfoIcon, Check, Trash, Pen, etc.) |
| `DefaultLayout` | `@/components/layouts/DefaultLayout` |
| `FullWidthDefaultLayout` | `@/components/layouts/FullWidthDefaultLayout` |
| `FullHeightDefaultLayout` | `@/components/layouts/FullHeightDefaultLayout` |
| `TablePageLayout` | `@/components/layouts/TablePageLayout` |

## Prototype Workflow

### Step 1: Understand Requirements

Read the PRD or design brief. Identify:
- Key screens or views
- User interactions and flows
- Data entities
- Edge cases (empty states, errors, loading)

### Step 2: Check Existing Components

Browse `apps/glados/components/` to understand current patterns. Read theme tokens from `apps/glados/app/defaultTheme.ts` for exact values.

### Step 3: Generate Components

Place components in the appropriate directory under `apps/glados/components/`. Follow all styling rules — never hardcode values, always use theme tokens.

### Step 4: Create Storybook Story

Create a `.stories.tsx` file alongside the component for Storybook preview.

```tsx
import type { Meta, StoryObj } from "@storybook/nextjs-vite";

const meta: Meta = {
  title: "Prototypes/FeatureName",
  parameters: { layout: "fullscreen" },
};

export default meta;
type Story = StoryObj<typeof meta>;

export const Default: Story = {
  render: () => (
    <div style={{ backgroundColor: '#F6F6F6', padding: '24px' }}>
      {/* Your prototype */}
    </div>
  ),
};

export const EmptyState: Story = {
  render: () => (
    <div>{/* Empty state variation */}</div>
  ),
};
```

## Examples

### Dashboard Layout
```tsx
import FullHeightDefaultLayout from '@/components/layouts/FullHeightDefaultLayout';

<FullHeightDefaultLayout navLinks={navLinks} showAgentMenu>
  <div style={{ padding: '24px', backgroundColor: '#F6F6F6' }}>
    {/* Dashboard content */}
  </div>
</FullHeightDefaultLayout>
```

### Table Page
```tsx
import CustomTable from '@/components/shared/GladlyTable/CustomTable';

<CustomTable
  id="feature-table"
  title="Feature List"
  columns={columns}
  dataSet={data}
  defaultSortColumn="name"
/>
```

## What Is Expected

- Complete, working TypeScript React component(s)
- All styling via styled-components + theme tokens (no raw hex values)
- Proper TypeScript types for all props
- Reuse existing Gladly components where possible
- A Storybook story file for visual testing
- Follow the patterns above (Radix wrapper, transient props, theme references)

## Tips & Best Practices

1. **Start with layout**: Choose the right layout component first
2. **Use real data**: Prototypes with realistic data are more convincing
3. **Create multiple stories**: Show default, empty, loading, error states
4. **Match existing patterns**: Check Storybook for similar UIs
5. **Use theme tokens**: Never hardcode colors or spacing values
6. **Keep it interactive**: Use `useState` for user interactions
7. **Document decisions**: Add comments explaining why you chose certain patterns

## Adding New Patterns

To extend this skill with new patterns:

1. **Document the pattern**: Add a new section with component details
2. **Provide code examples**: Show imports and usage
3. **Include visual details**: Describe spacing, colors, layout
4. **Link to implementation**: Reference the actual component files
5. **Add to examples**: Create a Storybook story demonstrating the pattern

**Template for new patterns:**
```markdown
### [Pattern Name]

**When to use:** [Description of use cases]

**Import:**
\```tsx
import { Component } from '@/components/path';
\```

**Usage:**
\```tsx
<Component prop="value">
  {/* Example */}
</Component>
\```

**Styling:**
- Background: [color token]
- Spacing: [spacing values]
- Typography: [font sizes, weights]
- Special considerations: [any unique styling rules]

**Example:**
[Link to Storybook story or reference implementation]
```

## Reference

- **Theme tokens**: `apps/glados/app/defaultTheme.ts`
- **Component source**: `apps/glados/components/shared/`
- **Storybook**: Running locally, navigate to "Prototypes" section for examples
- **Design system docs**: Check `@/components/__docs__/` for component documentation

---

## Skill Maintenance

This skill is living documentation. As you build prototypes:
- Add new patterns you discover
- Document component combinations that work well
- Update with new design system components
- Share examples that demonstrate best practices
