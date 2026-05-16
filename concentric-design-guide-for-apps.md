# Concentric Leadership - Design and Build Standards

**Version:** 1.0
**For use with:** Lovable, ChatGPT, Claude, Cursor, or any AI build tool
**How to use:** Paste or upload this document at the start of every new project. Treat every rule as a hard constraint unless explicitly overridden in the project brief.

---

## 0. Critical project standards (non-negotiable)

These apply to every build, regardless of feature scope.

### Database
- **Always assume an external Supabase database is in use.** Do not create a new local database, mock database, in-memory store, or alternative backend.
- Connect to the existing Supabase instance using the credentials supplied in the project environment.
- If Supabase credentials have not yet been provided, ask for them - do not improvise an alternative or scaffold a temporary backend.
- All authentication, data storage, and row-level security runs through Supabase.

### Code conventions
- TypeScript by default
- Tailwind CSS for styling
- shadcn/ui for component primitives where available
- Lucide React for icons (outline only)

### Language
- Australian English in all UI copy, comments, and documentation
- No ampersands - use "and"
- Short dashes (-), never em dashes

---

## 1. Brand colour palette

Five brand colours plus four semantic colours. **Do not introduce any colour outside this palette.**

### Brand colours

| Role | Name | Hex | HSL | Where it goes |
|---|---|---|---|---|
| Primary | Blue | `#0070AD` | `203 100% 34%` | Primary buttons, links, primary chart series, H2 headings, focus rings |
| Secondary | Teal | `#0097B2` | `189 100% 35%` | Secondary buttons, ghost button text, badge accents, borders on accent elements |
| Structural | Navy | `#082957` | `216 83% 19%` | Top navigation, column headers, dark surfaces, body headings on light bg |
| Tertiary | Light Blue | `#75CAEE` | `200 79% 70%` | Chart series, category pills, secondary blocks. Always with a 1px Navy border when used as a fill on white. Always uses dark text on top, never white. |
| Accent | Yellow | `#F9C51A` | `46 96% 54%` | Sparingly only. Hairline borders, highlight lines, the occasional emphasis moment. Not for buttons or large blocks. |

### Semantic colours

| Role | Hex | HSL | Use |
|---|---|---|---|
| Success | `#0F7A4F` | `155 78% 27%` | Confirmations, success states, positive trends |
| Warning | `#E89611` | `36 86% 49%` | Warnings, "needs attention" states |
| Danger | `#C0392B` | `6 63% 46%` | Errors, destructive actions, overdue alerts |
| Neutral / Info | `#6B7280` | `220 9% 46%` | Muted text, info hints, neutral chart series |

### Tailwind config snippet

```ts
// tailwind.config.ts
extend: {
  colors: {
    brand: {
      blue: 'hsl(203 100% 34%)',
      teal: 'hsl(189 100% 35%)',
      navy: 'hsl(216 83% 19%)',
      'light-blue': 'hsl(200 79% 70%)',
      yellow: 'hsl(46 96% 54%)',
    },
    success: 'hsl(155 78% 27%)',
    warning: 'hsl(36 86% 49%)',
    danger: 'hsl(6 63% 46%)',
    neutral: 'hsl(220 9% 46%)',
  }
}
```

### CSS variables (index.css)

```css
:root {
  /* Page and surfaces */
  --background: 220 20% 97%;        /* Cool light grey page bg */
  --card: 0 0% 100%;                /* White - primary card surface */
  --surface-secondary: 60 13% 90%;  /* #EBEBE1 - sub-panels, side panels */
  --foreground: 222 47% 11%;

  /* Brand */
  --primary: 203 100% 34%;          /* Blue #0070AD */
  --primary-foreground: 0 0% 100%;
  --secondary: 189 100% 35%;        /* Teal #0097B2 */
  --structural: 216 83% 19%;        /* Navy #082957 */
  --tertiary: 200 79% 70%;          /* Light Blue #75CAEE */
  --accent: 46 96% 54%;             /* Yellow #F9C51A */

  /* Semantic */
  --success: 155 78% 27%;
  --warning: 36 86% 49%;
  --destructive: 6 63% 46%;
  --muted: 220 16% 93%;
  --muted-foreground: 220 9% 46%;
  --border: 220 16% 90%;

  /* Radius */
  --radius: 0.5rem;                 /* 8px - buttons, inputs */
  --radius-card: 0.625rem;          /* 10px - cards, panels */
}
```

---

## 2. Surfaces and backgrounds

| Layer | Colour | Use |
|---|---|---|
| Page | `hsl(220 20% 97%)` cool light grey | Main app background |
| Card (primary) | `#FFFFFF` white | Main content cards, forms, primary panels |
| Surface (secondary) | `#EBEBE1` warm grey | Side panels, sub-sections, grouped content, hover backgrounds at low opacity |
| Dark surface | `#082957` Navy | Top nav, column headers |

**Card spec:**
- Background: white
- Border: 1px `hsl(220 16% 90%)`
- Radius: 10px (`var(--radius-card)`)
- Padding: 16px (compact density)
- Shadow: none, or `0 1px 2px rgba(0,0,0,0.04)` for the very subtlest lift

Do not use heavy shadows, gradients, glows, glassmorphism, or coloured tinted backgrounds on cards.

---

## 3. Typography

### Font stack
- **Primary (UI, body, labels, inputs):** Inter, weights 400 and 500 mostly, 600 for emphasis. Range 300-800 available.
- **Secondary (headings, metric values):** DM Sans, weights 400-700
- **Accent (AI-generated comments, call-out boxes, annotations only - never general UI):** Permanent Marker

### Sizes (compact density)

| Element | Size | Weight | Font |
|---|---|---|---|
| H1 (page title) | 1.5rem (24px) | 600 | DM Sans |
| H2 (section) | 1.25rem (20px) | 600 | DM Sans, colour: Primary Blue |
| H3 (subsection) | 1.0625rem (17px) | 600 | DM Sans |
| Body | 0.875rem (14px) | 400 | Inter |
| Label | 0.75rem (12px) | 500 | Inter |
| Metric value (big numbers) | 1.75rem (28px) | 600 | DM Sans |
| Caption / small | 0.75rem (12px) | 400 | Inter |
| Button | 0.875rem (14px) | 500 | Inter |
| Tooltip | 0.8125rem (13px) | 400 | Inter |

### Sentence case everywhere
Buttons, headings, labels - all sentence case. Never Title Case. Never ALL CAPS except for genuine acronyms.

---

## 4. Spacing and density

This is a **compact** density system. Not cramped, not spacious. Sits in the middle - efficient on screen real estate without feeling crammed.

| Token | Value | Use |
|---|---|---|
| Card padding | 16px (12px on mobile) | Inside cards |
| Card-to-card gap | 12px | Between adjacent cards |
| Section spacing | 32px | Between major sections |
| Form field gap | 12px | Between stacked inputs |
| Inline gap | 8px | Between inline elements (icon + label, button + button) |
| Table row height | 36px | Compact rows |
| Button height | 36px | Standard |
| Input height | 36px | Standard |

---

## 5. Components

### Buttons

**Primary button**
- Background: Primary Blue `#0070AD`
- Text: white
- Border: none
- Radius: 8px
- Height: 36px
- Padding: 0 14px
- Hover: darken 10%
- Active: darken 15%
- Disabled: 40% opacity

**Secondary button**
- Background: transparent
- Border: 1px Teal `#0097B2`
- Text: Teal `#0097B2`
- Radius: 8px
- Hover: background Teal at 10% opacity
- Active: background Teal at 15% opacity

**Ghost button**
- Background: transparent
- Border: none
- Text: Teal `#0097B2` (or Mid Grey for less emphasis)
- Hover: background Mid Grey at 5% opacity, or text shifts to Primary Blue
- Use for: empty state CTAs, inline minor actions

**Destructive button**
- Background: Danger Red `#C0392B`
- Text: white
- Same dimensions as primary
- Always require confirmation for irreversible actions

### Inputs

- Border: 1px Mid Grey at 30% opacity
- Background: white
- Radius: 8px
- Height: 36px
- Padding: 0 12px
- Font: Inter 14px, regular
- Focus: 2px Primary Blue ring at 30% opacity, 2px offset (Tailwind: `focus:ring-2 focus:ring-primary/30 focus:ring-offset-2`)
- Disabled: light grey background, Mid Grey text
- Error: 1px Danger Red border, error message below in Danger Red 12px

### Labels and helper text
- Label: 12px, weight 500, Mid Grey, above the input
- Helper text: 12px, weight 400, Mid Grey, below the input
- Required indicator: small asterisk in Danger Red, never the word "required"

### Badges and pills
- Default: background Teal at 15% opacity, Teal text, 12px text, padding 2px 8px, radius 6px
- Destructive: background Danger Red at 12-15% opacity, Danger Red text
- Success: background Success Green at 15% opacity, Success Green text
- Light Blue pills (chart legends, category tags): Light Blue background, dark Navy text, 1px Navy border at 30% opacity

### Tables
- Header row: light grey background `hsl(220 16% 93%)`, 12px label text, Mid Grey, weight 500, padding 8px 12px
- Body rows: 36px height, 14px body text, padding 8px 12px
- Row border: 1px `hsl(220 16% 90%)` between rows
- Hover: row background Mid Grey at 5%
- Selected: row background Primary Blue at 8%, 2px left border in Primary Blue

### Top navigation
- Full-width, white background, 1px bottom border in `hsl(220 16% 90%)`
- Height: 64px
- Logo on left, max-height 36px, 24px from edge
- User avatar on right: 32px circle, Navy background, white initial, 24px from edge

### Column / section headers (Navy strips)
- Background: Navy `#082957`
- Text: white
- Font: Inter 14px, weight 600
- Padding: 12px 16px
- Use at the top of pipeline columns, kanban columns, grouped sections

---

## 6. Iconography

- **Library:** Lucide (lucide-react)
- **Style:** Outline only, 1.5px stroke
- **Default size:** 18-20px
- **Larger contexts (hero, empty states):** 32-48px
- **Colour:** Mid Grey at rest, Primary Blue on hover for interactive icons, Navy for structural icons in dark headers
- **Decorative icons:** `aria-hidden="true"`
- **Interactive-only icons:** must have an `aria-label`

Do not use filled icons. Do not use emoji as UI elements.

---

## 7. Hover and interactive states

**Every interactive element must have a hover state.** If something does something when clicked, it changes on hover. No silent buttons.

| Element | Hover behaviour |
|---|---|
| Primary button | Darken background 10% |
| Secondary button | Fill with accent colour at 10% opacity |
| Ghost button / text link | Underline appears, or background fills with Mid Grey at 5% |
| Clickable cards | Border shifts to 1px Primary Blue at 30%, optional subtle `translateY(-1px)` (no heavy shadows) |
| Table rows | Background fills with Mid Grey at 5% |
| Interactive icons | Colour shifts from Mid Grey to Primary Blue |
| Nav items | Underline appears under label, or text shifts to Primary Blue |

Transition timing: `transition: all 150ms ease-out` on hover changes. No bouncy or playful easings.

---

## 8. Tooltips

Plain-English explanations matter. Use tooltips generously to clarify rather than letting users guess.

**Style:**
- Background: white
- Border: 1px `hsl(220 16% 90%)`
- Text: dark, 13px Inter regular
- Max width: 320px
- Padding: 10px 12px
- Radius: 8px
- Shadow: `0 2px 8px rgba(0,0,0,0.08)` (functional, subtle)
- Arrow: small white triangle pointing to the trigger, with matching border

**Behaviour:**
- Delay before show: 400ms (prevents accidental triggers)
- Position: above or below the trigger depending on space
- Trigger: hover over a small info icon `(i)` placed next to the field label, column header, or term being explained
- Content: 1-3 short sentences of plain English. Explain not just what something is, but why it matters or how it is calculated.

**Info icon trigger:**
- Lucide `info` icon, 14px, Mid Grey
- Sits inline after the label or term
- On hover: colour shifts to Primary Blue, tooltip appears after 400ms

**Example copy:**
- Good: "Last reviewed - when this opportunity was last touched by anyone on the team."
- Bad: "Last reviewed: timestamp of last activity."

---

## 9. Empty states

**Default empty state pattern:**
- Centered in the container
- 14px body text, Mid Grey, single short sentence in plain English
- Below it: small ghost button in Teal, 14px, with the most useful next action
- Optional small Lucide icon above the text, 32px, Mid Grey

**Examples:**
- "No opportunities yet." + ghost button "Add your first opportunity"
- "Nothing assigned to you." + ghost button "Browse open actions"
- "This list is empty." + ghost button "Create an item"

**For high-impact empty states only** (first-login dashboard, brand-new module), upgrade to a blueprint illustration above the text (see Section 11).

---

## 10. Charts and data visualisation

**Series colour order** (for line charts, bar charts, pie charts, multi-series):

1. Primary Blue `#0070AD` - primary series
2. Teal `#0097B2` - secondary series
3. Navy `#082957` - tertiary series
4. Light Blue `#75CAEE` - quaternary (1px Navy border if used as fill, dark text on top)
5. Yellow `#F9C51A` - highlight series only, used sparingly to draw attention to one specific series

**For status-coded charts** (red / amber / green status views):
- Use semantic colours: Success Green, Warning Amber, Danger Red

**Chart styling:**
- Gridlines: 1px Mid Grey at 15% opacity, horizontal only by default
- Axis labels: 12px Inter, Mid Grey
- Axis titles: 13px Inter weight 500, Mid Grey
- Tooltips on data points: same style as Section 8 tooltips
- Legend: 12px Inter, positioned above or below the chart, sentence case
- Series labels: 12px, weight 500

Avoid 3D charts, donut charts with more than 4 segments, or charts where colour is the only differentiator (always add a label or pattern).

---

## 11. Blueprint illustration aesthetic

For custom illustrations - empty states, hero graphics, conceptual diagrams, explainer visuals - default to a **blueprint or architect's-draft style**. This is a signature visual element of the Concentric brand and ties directly to the heavy industry and utilities positioning.

**Visual language:**
- Line drawings only - no solid colour fills
- Lines in Primary Blue `#0070AD`, stroke 1.5px
- Background: pale Light Blue `#75CAEE` at 15-20% opacity, OR a graph-paper grid (1px lines in Light Blue at 20% opacity, 20px grid spacing)
- Hand-drawn or technical-draft feel - clean but with human imperfection rather than vector-perfect
- Optional small annotation labels in Permanent Marker font where call-outs are needed
- No full-colour fills, no gradients, no decorative shading

**When to use:**
- First-login dashboard empty state
- Onboarding screens
- Module hero sections
- Conceptual diagrams explaining a process or model

**When not to use:**
- Standard empty states (use plain text + ghost button)
- Operational dashboards (clean data, no decoration)
- Anywhere requiring a quick visual scan

---

## 12. Imagery and photography

Default policy: **minimal imagery in apps.** Operational tools stay fast and serious. Decorative photography lives on the marketing site, not in apps.

If imagery is needed, it will be supplied on a case-by-case basis. Do not source stock photography. Do not generate AI photographs.

User avatars: initials on a Navy circle by default, photo only if uploaded by the user.

---

## 13. UI voice and copy

**Default voice: neutral and operational.** Clear over clever. Operators in the field do not want personality in their error messages - they want to understand what to do.

| Element | Use this | Avoid |
|---|---|---|
| Save button | "Save" | "Lock it in" |
| Empty state | "No opportunities yet." | "Nothing to see here, friend." |
| Error | "We could not save your changes. Check your connection and try again." | "Oops, something went wrong." |
| Delete confirm | "Delete this item? This cannot be undone." | "Sure? This one is gone for good." |
| Success message | "Changes saved." | "Boom, locked in." |

**Plain English principle:**
- Prefer "Last touched" over "Last activity timestamp"
- Prefer "Who is responsible" over "Owner"
- Prefer "Due by" over "SLA target"
- If a term is industry-specific or has internal meaning, explain it in a tooltip rather than assuming the user knows

A touch of warmth is acceptable in onboarding moments and the first empty state a user encounters. Everywhere else: neutral, helpful, clear.

Avoid absolute or overly certain language ("guaranteed", "always", "never") - prefer honest framing that acknowledges nuance.

---

## 14. Dark mode

**Default: light mode only.** Do not implement a dark mode toggle unless specifically requested for a project.

If dark mode is later needed for a specific project:
- Page background: `hsl(222 47% 6%)`
- Card background: `hsl(222 47% 10%)`
- Foreground text: `hsl(210 40% 96%)`
- Primary Blue lightened: `hsl(203 80% 50%)` for adequate contrast
- Borders: `hsl(220 16% 18%)`

Document the swap at project start - do not retrofit.

---

## 15. Brand assets

All brand assets live in the Concentric Leadership GitHub asset library. Always pull from these URLs. Never improvise placeholders - ask if unsure which to use.

Base URL: `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/`

### Full logos (with text)

| Use | URL |
|---|---|
| Light backgrounds (dark logo) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-dark.svg` |
| Light backgrounds (dark logo PNG) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-dark.png` |
| Dark/Navy backgrounds (white logo) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-white.svg` |
| Dark/Navy backgrounds (white logo PNG) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-white.png` |

### Compact logos (mark above text - for square/small spaces)

| Use | URL |
|---|---|
| Navy background | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-compact-navy.svg` |
| Blue background | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-compact-blue.svg` |
| Transparent background (dark logo) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-compact-transparent.svg` |
| Transparent background (white logo) | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logo-compact-white.svg` |

### Logomark (C icon only - no text)

| Use | URL |
|---|---|
| Teal logomark | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/logos/concentric-logomark-teal.svg` |

### Motifs

| Use | URL |
|---|---|
| Colour circles - primary brand motif, best favicon choice | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/motifs/concentric-circles-colour.svg` |
| Black circles - bullet points, monochrome icons | `https://raw.githubusercontent.com/concentricleaders-coder/concentric-brand-assets/main/motifs/concentric-circles-black.svg` |

### Favicon
Default favicon: use the colour circles motif SVG. It scales sharply at any size and the brand colours read clearly even at 16px.

### Usage guidance
- Top nav on light bg: use `concentric-logo-dark.svg`
- Top nav on Navy bg: use `concentric-logo-white.svg`
- App icon, browser tab: use `concentric-circles-colour.svg`
- Square/compact brand moments: use compact logo variants
- Bullet points and inline icons: use `concentric-circles-black.svg`
- Decorative hero/empty state motif: use `concentric-circles-colour.svg`

---

## 16. Absolute do nots

These rules override any conflicting instructions during a build.

- **Do not** introduce any colour outside the defined palette
- **Do not** use any font outside Inter, DM Sans, or Permanent Marker (and Permanent Marker only in AI comments and call-outs)
- **Do not** use gradients, glassmorphism, neon effects, or heavy shadows
- **Do not** use emoji as UI elements
- **Do not** use Title Case or ALL CAPS in buttons, labels, or headings
- **Do not** use ampersands - use "and"
- **Do not** use em dashes - use short dashes
- **Do not** create a new database, mock backend, or in-memory store - always use the external Supabase database
- **Do not** add hover-less interactive elements - if it does something, it changes on hover
- **Do not** use jargon where plain English will do
- **Do not** introduce dark mode unless specifically requested
- **Do not** use absolute or overly certain language in UI copy

---

## 17. Quick reference - copy and paste tokens

For fast use in any AI builder, the most-used values in copyable form:

```
PAGE BG:          hsl(220 20% 97%)
CARD BG:          #FFFFFF
SUB-PANEL BG:     #EBEBE1
BORDER:           hsl(220 16% 90%)

PRIMARY:          #0070AD  Blue
SECONDARY:        #0097B2  Teal
STRUCTURAL:       #082957  Navy
TERTIARY:         #75CAEE  Light Blue (dark text on top, 1px Navy border)
ACCENT:           #F9C51A  Yellow (sparingly)

SUCCESS:          #0F7A4F
WARNING:          #E89611
DANGER:           #C0392B
NEUTRAL:          #6B7280

RADIUS-BUTTON:    8px
RADIUS-CARD:      10px
CARD-PADDING:     16px
ROW-HEIGHT:       36px
BTN-HEIGHT:       36px
INPUT-HEIGHT:     36px

FONT-UI:          Inter
FONT-HEADING:     DM Sans
FONT-ACCENT:      Permanent Marker (AI comments only)

ICONS:            Lucide outline, 1.5px stroke, 18-20px
FOCUS-RING:       2px Primary Blue at 30% opacity, 2px offset
HOVER-TIMING:     150ms ease-out
TOOLTIP-DELAY:    400ms

LANGUAGE:         Australian English, no ampersands, short dashes only
DATABASE:         Always external Supabase, never local or mock
```

---

*End of guide.*
