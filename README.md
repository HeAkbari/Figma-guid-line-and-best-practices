# Figma Design System Best Practices Guide

## Table of Contents

1. [Naming Conventions](#naming-conventions)
2. [File Structure](#file-structure)
3. [CSS Variables & Design Tokens](#css-variables--design-tokens)
4. [Component Relations](#component-relations)
5. [Layout Structure](#layout-structure)
6. [Component Properties](#component-properties)
7. [References](#references)

---

## Naming Conventions

### General Principles

- Use **PascalCase** for components and frames
- Use **camelCase** for layers and instances
- Use **kebab-case** for CSS variables and tokens
- Be **descriptive** and **consistent** across the design system
- Avoid abbreviations unless universally understood
- Use forward slashes `/` to create hierarchy in component names

### Component Naming

```
✅ Good:
- Button / Primary
- Button / Secondary
- Input / Text
- Card / Product
- Navigation / Header

❌ Bad:
- btn
- input1
- card_v2
- nav-header
```

### Layer Naming

```
✅ Good:
- Container
- Label
- Icon / Leading
- Icon / Trailing
- Helper Text

❌ Bad:
- Frame 1
- Rectangle 2
- Group 3
- Copy
```

### Variant Naming

```
✅ Good:
- Button / Primary / Default
- Button / Primary / Hover
- Button / Primary / Disabled
- Input / Text / Error
- Input / Text / Success

❌ Bad:
- Button-primary
- Button_hover
- Input-error-state
```

### Color Naming

```
✅ Good:
- Color / Primary / 500
- Color / Neutral / 100
- Color / Semantic / Error
- Color / Semantic / Success

❌ Bad:
- Blue
- Gray
- Red
- #FF5733
```

---

## File Structure

### Recommended File Organization

```
📁 Design System File
│
├─ 📄 🎨 Design Tokens
│   ├─ Colors
│   ├─ Typography
│   ├─ Spacing
│   ├─ Shadows
│   └─ Borders
│
├─ 📄 🧩 Components
│   ├─ Primitives (Buttons, Inputs, Icons)
│   ├─ Composites (Cards, Forms, Navigation)
│   └─ Patterns (Headers, Footers, Modals)
│
├─ 📄 📐 Layouts
│   ├─ Grid System
│   ├─ Breakpoints
│   └─ Container Sizes
│
├─ 📄 🎭 Prototypes
│   ├─ User Flows
│   ├─ Interactions
│   └─ Animations
│
├─ 📄 📱 Screens
│   ├─ Mobile
│   ├─ Tablet
│   └─ Desktop
│
└─ 📄 📋 Handoff
    ├─ Developer Notes
    ├─ Specifications
    └─ Assets Export
```

### File Structure Best Practices

#### 1. **Design Tokens Page**

- Centralized color palette
- Typography scale
- Spacing system
- Shadow styles
- Border radius values

#### 2. **Components Page**

- Organized by hierarchy (Primitives → Composites → Patterns)
- Use frames to group related components
- Include component documentation
- Show all variants and states

#### 3. **Prototypes Page**

- Interactive flows
- User journey maps
- Animation demonstrations
- State transitions

#### 4. **Screens Page**

- Organized by device type
- Include responsive breakpoints
- Show real content (not lorem ipsum)
- Include annotations

#### 5. **Handoff Page**

- Developer-friendly specifications
- Export settings
- CSS code snippets
- Asset naming conventions

---

## CSS Variables & Design Tokens

### Design Token Structure

#### Color Tokens

```
✅ Correct Structure:
Color / Primary / 50
Color / Primary / 100
Color / Primary / 500 (Base)
Color / Primary / 600
Color / Primary / 900

Color / Semantic / Error
Color / Semantic / Warning
Color / Semantic / Success
Color / Semantic / Info

Color / Neutral / White
Color / Neutral / Gray-100
Color / Neutral / Gray-900
Color / Neutral / Black
```

#### Typography Tokens

```
✅ Correct Structure:
Typography / Heading / H1
Typography / Heading / H2
Typography / Heading / H3
Typography / Body / Large
Typography / Body / Medium
Typography / Body / Small
Typography / Caption
```

#### Spacing Tokens

```
✅ Correct Structure:
Spacing / 4px
Spacing / 8px
Spacing / 12px
Spacing / 16px
Spacing / 24px
Spacing / 32px
Spacing / 48px
Spacing / 64px
```

### CSS Variable Mapping

When exporting to CSS, map Figma styles to CSS custom properties:

```css
/* Colors */
--color-primary-500: #0066ff;
--color-primary-600: #0052cc;
--color-semantic-error: #dc2626;
--color-semantic-success: #16a34a;

/* Typography */
--font-family-base: 'Inter', sans-serif;
--font-size-h1: 2.5rem;
--font-size-body: 1rem;
--font-weight-bold: 700;

/* Spacing */
--spacing-xs: 4px;
--spacing-sm: 8px;
--spacing-md: 16px;
--spacing-lg: 24px;
--spacing-xl: 48px;

/* Shadows */
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);

/* Borders */
--border-radius-sm: 4px;
--border-radius-md: 8px;
--border-radius-lg: 12px;
```

### Best Practices for Design Tokens

- ✅ Use semantic naming (Primary, Secondary, not Blue, Red)
- ✅ Create a consistent scale (50, 100, 500, 600, 900)
- ✅ Document token usage in component descriptions
- ✅ Use styles for colors, not hex values directly
- ✅ Create text styles for typography
- ✅ Use effect styles for shadows

---

## Component Relations

### Component Hierarchy

```
✅ Correct Component Structure:

🎨 Design Tokens (Base Layer)
│
├─ 🧩 Primitives (Atomic Components)
│   ├─ Icon
│   ├─ Badge
│   ├─ Avatar
│   └─ Divider
│
├─ 🧩 Basic Components
│   ├─ Button (uses: Icon, Badge)
│   ├─ Input (uses: Icon)
│   ├─ Checkbox (uses: Icon)
│   └─ Radio (uses: Icon)
│
├─ 🧩 Composite Components
│   ├─ Form (uses: Input, Button, Checkbox)
│   ├─ Card (uses: Button, Badge, Avatar)
│   ├─ Modal (uses: Button, Icon)
│   └─ Navigation (uses: Button, Icon, Badge)
│
└─ 🧩 Patterns (Page-level)
    ├─ Header (uses: Navigation, Button, Icon)
    ├─ Footer (uses: Navigation, Icon)
    └─ Dashboard (uses: Card, Button, Navigation)
```

### Component Instance Structure

```
✅ UI Button — Correct Component Relations

🟦 Button / Primary (Component)
│
├─ 🟦 Container          ← Auto Layout Frame
│   │
│   ├─ 🟦 Leading Icon   ← Instance of "Icon" component (optional)
│   │   └─ 🖼 Icon / Arrow-Left
│   │
│   ├─ 🅣 Label          ← Text Layer
│   │
│   └─ 🟦 Trailing Icon  ← Instance of "Icon" component (optional)
│       └─ 🖼 Icon / Arrow-Right
│
└─ 🟦 States (Variants)
    ├─ Default
    ├─ Hover
    ├─ Active
    └─ Disabled
```

### Component Properties Best Practices

- ✅ Use **Component Properties** for customizable elements
- ✅ Use **Variants** for different states and sizes
- ✅ Create **Boolean properties** for optional elements (show/hide icons)
- ✅ Use **Text properties** for editable content
- ✅ Use **Instance Swap** for interchangeable elements
- ✅ Document component usage in description

---

## Layout Structure

### Auto Layout Principles

#### Vertical Auto Layout

```
✅ UI Input — Correct Layout Structure (Figma Layers)

🟨 Section: Form Components        (optional, canvas-only)
│
└─ 🟦 Input / Text  (Component)   ← Frame + Auto Layout (Vertical)
   │
   ├─ 🅣 Label
   │
   ├─ 🟦 Field                ← Frame + Auto Layout (Horizontal)
   │   │
   │   ├─ 🟦 Leading Icon     ← Frame (optional)
   │   │   └─ 🖼 Icon (24×24)
   │   │
   │   ├─ 🅣 Text / Placeholder
   │   │
   │   └─ 🟦 Trailing Icon    ← Frame (optional)
   │       └─ 🖼 Icon (20×20)
   │
   └─ 🅣 Helper Text
```

#### Horizontal Auto Layout

```
✅ UI Button — Correct Layout Structure

🟦 Button / Primary (Component)  ← Frame + Auto Layout (Horizontal)
│
├─ 🟦 Leading Icon     ← Frame (24×24, optional)
│   └─ 🖼 Icon / Arrow-Left
│
├─ 🅣 Label            ← Text Layer
│
└─ 🟦 Trailing Icon    ← Frame (24×24, optional)
    └─ 🖼 Icon / Arrow-Right
```

#### Understanding Figma's Building Blocks

At first glance, Figma looks complicated—but it's more simple than it seems. Everything created in Figma uses the same basic building blocks. Even in massive design files with thousands of moving parts, it's still just a bunch of simple pieces expertly glued together.

**Upleveling your layer game**

There's one big difference between text editors like Google Docs and design tools like Figma: **depth**. In Figma, objects can sit on top, underneath, or inside of each other, which means you have to determine the order of those objects.

Since you'll often have hundreds of layers, you'll want to organize them—group them together, nest them under each other, etc. To do that, Figma has **frames**. A frame is a type of layer that acts like a container—you can put other layers inside of it. To create multiple levels of hierarchy, you can (and will frequently) put a frame inside another frame.

That frame-ception is how designers create complex mocks. If you're designing a webpage, the highest level frame might represent the entire page. Inside that huge frame, you might have a separate frame for the top navigation area. Inside that top-nav frame, you'd have more frames for the site logo, nav links, social icons, etc. You get the idea.

**Managing the order of things**

To manage the order of things, Figma uses **layers**. Everything on the canvas is represented by a layer. Shapes? Layers. Lines? Layers. Strings? Yep, layers. (There are a few types of layers, most of which are covered in this guide.)

You'll find layers in the left sidebar, or what we call the **layers panel**. Because everything's a layer, everything you see on the canvas is listed in the layers panel. The order of layers in the panel determines the order of objects on the canvas, with higher layers sitting on top of lower ones.

**TL;DR:**

- Everything is a layer
- The order of layers = the order of objects
- You put layers into frames to organize them and create hierarchy

#### When to Use Frames

**Use frames:**

- If you have multiple related layers, it's always better to combine them into more organized, manageable layers, such as frames.
- If there is any relationship between layers
- To define the resizing behavior of child elements
- To control the frame size independently of its contents
- To apply styles

💡 **Tip:** Frames are suitable for Layout Grids, Auto Layouts, Constraints, Components and Styles.

Multiple objects (made of vector elements or images) that together make up a single symbol can be combined as groups as well, but we recommend using frames instead. Generally speaking, frames can do everything groups can do and contain logic that groups can't.

> **Note:** Too many groups or extra frames, especially nested groups (groups within groups), can complicate your design and code.

#### Card Component Structure

```
✅ UI Card — Correct Layout Structure

🟦 Card / Product (Component)    ← Frame + Auto Layout (Vertical)
│
├─ 🟦 Image Container            ← Frame (Aspect Ratio: 16:9)
│   └─ 🖼 Product Image
│
├─ 🟦 Content                    ← Frame + Auto Layout (Vertical, Padding)
│   │
│   ├─ 🟦 Header                 ← Frame + Auto Layout (Horizontal)
│   │   │
│   │   ├─ 🅣 Title
│   │   │
│   │   └─ 🟦 Badge              ← Instance of "Badge" component
│   │       └─ 🟦 Badge / New
│   │
│   ├─ 🅣 Description
│   │
│   └─ 🟦 Footer                 ← Frame + Auto Layout (Horizontal, Space Between)
│       │
│       ├─ 🅣 Price
│       │
│       └─ 🟦 Button             ← Instance of "Button" component
│           └─ 🟦 Button / Primary
```

#### Dropdown Component Structure

```
✅ UI Dropdown — Correct Layout Structure

🟦 Dropdown / Select (Component)    ← Frame + Auto Layout (Vertical)
│
├─ 🅣 Label                         ← Text Layer (optional)
│
├─ 🟦 Trigger                       ← Frame + Auto Layout (Horizontal)
│   │
│   ├─ 🟦 Selected Value           ← Frame + Auto Layout (Horizontal, Fill)
│   │   │
│   │   ├─ 🟦 Leading Icon         ← Instance of "Icon" component (optional)
│   │   │   └─ 🖼 Icon (20×20)
│   │   │
│   │   └─ 🅣 Selected Text         ← Text Layer
│   │
│   └─ 🟦 Trailing Icon             ← Instance of "Icon" component (20×20)
│       └─ 🖼 Icon / Chevron-Down
│
├─ 🟦 Dropdown Menu                ← Frame + Auto Layout (Vertical, Hidden by default)
│   │                                (Frame only - not a component, specific to Dropdown)
│   │
│   ├─ 🟦 Option                   ← Instance of "Option" component (RECOMMENDED)
│   │   │                            (Component - reusable in List, Autocomplete, etc.)
│   │   ├─ 🟦 Leading Icon         ← Instance of "Icon" component (optional)
│   │   │   └─ 🖼 Icon (20×20)
│   │   │
│   │   ├─ 🅣 Option Text          ← Text Layer
│   │   │
│   │   └─ 🟦 Trailing Icon        ← Instance of "Icon" component (optional, selected state)
│   │       └─ 🖼 Icon / Check
│   │
│   ├─ 🟦 Divider                  ← Instance of "Divider" component (optional)
│   │   └─ 🟦 Divider / Horizontal
│   │
│   └─ 🟦 Option                   ← Instance of "Option" component
│       │
│       ├─ 🟦 Leading Icon         ← Instance of "Icon" component (optional)
│       │   └─ 🖼 Icon (20×20)
│       │
│       └─ 🅣 Option Text          ← Text Layer
│
└─ 🅣 Helper Text                   ← Text Layer (optional)
```

**Component Architecture Decision:**

- ✅ **Option** → **SHOULD be a Component**
    - Reusable across: Dropdown, List Box, Autocomplete, Menu, etc.
    - Consistent styling and behavior
    - Can have variants (Default, Hover, Selected, Disabled)
    - Example: `Option / Default`, `Option / Selected`

- ❓ **Dropdown Menu** → **Frame (NOT a Component)**
    - Specific to Dropdown component only
    - Not reused elsewhere
    - Contains multiple Option instances
    - If you need a reusable menu, create a separate `Menu` component

**Alternative Approach (if Menu is reusable):**

If the menu structure is used in multiple contexts (Dropdown, Context Menu, Popover Menu), then:

```
├─ 🟦 Menu                         ← Instance of "Menu" component (if reusable)
│   │                                (Component - used in Dropdown, Context Menu, etc.)
│   ├─ 🟦 Option                   ← Instance of "Option" component
│   └─ 🟦 Option                   ← Instance of "Option" component
```

### Layout Best Practices

#### Frame Organization

- ✅ Always use **Auto Layout** for flexible components
- ✅ Set **Padding** consistently (use spacing tokens)
- ✅ Use **Gap** for spacing between children
- ✅ Set **Constraints** appropriately (Left & Right, Top & Bottom, etc.)
- ✅ Use **Fill** containers for responsive layouts
- ✅ Set **Min/Max widths** for flexible components

#### Spacing System

```
✅ Consistent Spacing:

Container Padding: 16px / 24px / 32px
Element Gap: 8px / 12px / 16px
Section Spacing: 32px / 48px / 64px
```

#### Constraints

```
✅ Correct Constraint Usage:

- Container: Left & Right (stretches horizontally)
- Fixed Elements: Left & Top (stays in position)
- Centered Content: Center (centers on resize)
- Sticky Elements: Left & Right, Top (stretches and sticks)
```

---

## Component Properties

### Variant Properties

#### Button Component Example

```
✅ Button Component Variants:

Component: Button
├─ Property: Type
│   ├─ Primary
│   ├─ Secondary
│   └─ Tertiary
│
├─ Property: Size
│   ├─ Small (32px height)
│   ├─ Medium (40px height)
│   └─ Large (48px height)
│
└─ Property: State
    ├─ Default
    ├─ Hover
    ├─ Active
    └─ Disabled
```

#### Input Component Example

```
✅ Input Component Variants:

Component: Input
├─ Property: Type
│   ├─ Text
│   ├─ Email
│   ├─ Password
│   └─ Number
│
├─ Property: State
│   ├─ Default
│   ├─ Focus
│   ├─ Error
│   └─ Success
│
└─ Property: Size
    ├─ Small
    └─ Medium
```

### Component Properties Types

#### 1. **Boolean Properties**

```
✅ Use for: Optional elements
Examples:
- Show Leading Icon (true/false)
- Show Helper Text (true/false)
- Show Error State (true/false)
- Is Required (true/false)
```

#### 2. **Text Properties**

```
✅ Use for: Editable content
Examples:
- Label Text
- Placeholder Text
- Helper Text
- Button Label
```

#### 3. **Instance Swap Properties**

```
✅ Use for: Interchangeable components
Examples:
- Icon Type (swap between different icons)
- Avatar Image (swap between different avatars)
- Badge Type (swap between badge variants)
```

#### 4. **Variant Properties**

```
✅ Use for: Different states and styles
Examples:
- Button Type (Primary, Secondary, Tertiary)
- Input State (Default, Error, Success)
- Card Size (Small, Medium, Large)
```

### Component Properties Best Practices

#### ✅ DO:

- Create properties for all customizable elements
- Use descriptive property names
- Group related variants logically
- Document property usage in component description
- Use boolean properties for optional elements
- Set default values appropriately

#### ❌ DON'T:

- Create properties for static elements
- Use vague property names
- Create too many variant combinations
- Forget to document property behavior
- Hard-code values that should be properties

### Component Documentation

```
✅ Component Description Template:

# Button Component

## Usage
Primary action buttons for user interactions.

## Properties
- **Type**: Primary, Secondary, Tertiary
- **Size**: Small (32px), Medium (40px), Large (48px)
- **State**: Default, Hover, Active, Disabled
- **Show Icon**: Boolean (optional leading/trailing icon)

## Spacing
- Padding: 12px 24px (Medium)
- Gap: 8px (when icon present)

## States
- Default: Primary color background
- Hover: Darker shade (+10% opacity)
- Active: Pressed state (slight scale down)
- Disabled: 50% opacity, no interaction

## Accessibility
- Minimum touch target: 44×44px
- Color contrast: WCAG AA compliant
- Keyboard navigation supported
```

---

## References

### All Reference Links

#### Official Figma Resources

1. **Figma Learn: Name and Organize Components**
    - Link: https://help.figma.com/hc/en-us/articles/360038663994-Name-and-organize-components

2. **Figma Learn: Create and Use Variants**
    - Link: https://help.figma.com/hc/en-us/articles/360056440594-Create-and-use-variants

3. **Figma Learn: Build Your Design System** (Includes Auto Layout and component properties)
    - Link: https://help.figma.com/hc/en-us/articles/14548865734679-Lesson-3-Build-your-design-system

4. **Figma Learn: Main Page** (Browse all tutorials)
    - Link: https://help.figma.com/hc/en-us/sections/23691657321239-Courses-and-collections

#### Best Practices & Guides

5. **Anima: Figma Best Practices**
    - Link: https://support.animaapp.com/en/articles/6300035-figma-best-practices

6. **Figma: The UX Writers Guide to Figma**
    - Link: https://www.figma.com/best-practices/the-ux-writers-guide-to-figma/

7. **Figma: Best Practices Hub** (Main best practices page with all guides)
    - Link: https://www.figma.com/best-practices/

8. **Figma: Component Architecture**
    - Link: https://www.figma.com/best-practices/component-architecture/

#### Design System Resources

Check the following link to see the **Layout Structure, Framing, Naming Conventions, etc.** 

9. **PrimeOne: Component Guidelines** - Link: https://www.figma.com/design/G855HjuSyK8viJr0a5ZjRG/Preview-%7C%C2%A0PrimeOne-%7C-3.0.1?node-id=6738-47040&t=1BCMhqcmuOdhiBQv-0

10. **Material Design: Component Guidelines**
    - Link: https://m3.material.io/components

---

## Quick Checklist

### Before Starting Design

- [ ] Set up design tokens (colors, typography, spacing)
- [ ] Create component library structure
- [ ] Define naming conventions
- [ ] Set up file organization
- [ ] Create base components (primitives)

### During Design

- [ ] Use Auto Layout for all components
- [ ] Apply consistent spacing tokens
- [ ] Create component variants for all states
- [ ] Use component properties for customization
- [ ] Document component usage
- [ ] Maintain consistent naming

### Before Handoff

- [ ] Organize all components in library
- [ ] Add developer notes and specifications
- [ ] Export assets with proper naming
- [ ] Create prototype flows
- [ ] Review accessibility (contrast, touch targets)
- [ ] Test responsive behavior
- [ ] Generate CSS variables documentation

---

## Summary

A well-structured Figma design system ensures:

- ✅ **Consistency** across all designs
- ✅ **Efficiency** in design workflow
- ✅ **Scalability** as the system grows
- ✅ **Developer-friendly** handoff process
- ✅ **Maintainability** over time

Follow these best practices to create a professional, production-ready design system that developers can easily implement.
