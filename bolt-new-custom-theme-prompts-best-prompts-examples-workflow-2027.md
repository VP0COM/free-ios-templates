# Bolt.new custom theme prompts: Best Prompts, Examples & Workflow for 2027

By Lawrence Dauchy, Founder of VP0.com  
Published November 2, 2026

A good Bolt.new custom theme prompt should define a visual system, not just ask for a site to “look modern.” Specify the color palette, typography, spacing, border radius, shadows, component behavior, responsive rules, and the visual qualities you do not want. Then apply that system in focused stages instead of repeatedly asking Bolt.new to redesign the entire project.

If you do not yet have a visual direction, [VP0.com](https://vp0.com) can be a useful place to start. Pick a UI direction you like, identify its visual rules, and translate those rules into a reusable Bolt.new theme prompt.

## What should a Bolt.new custom theme prompt include?

A strong Bolt.new theme prompt should describe six things clearly: visual mood, colors, typography, spacing, surfaces, and component behavior.

The mistake is relying on vague adjectives such as “beautiful,” “premium,” or “professional.” These words can help, but they leave too much room for interpretation. A better prompt converts the idea into visible decisions.

Instead of:

> Make this dashboard look premium and modern.

Use:

> Restyle this dashboard using a restrained SaaS design system. Use a warm off-white page background, white cards, dark charcoal text, one cobalt accent color, 12px card radii, thin neutral borders, subtle shadows, generous spacing, compact navigation, and clear typography hierarchy. Avoid gradients, oversized headings, glassmorphism, excessive pills, and decorative illustrations.

The second version gives Bolt.new a system it can apply.

| Theme area | What to specify | Example instruction |
| --- | --- | --- |
| Colors | Background, text, accent, borders | Warm white background with one blue accent |
| Typography | Font style, weight, scale | Compact geometric sans-serif with strong headings |
| Spacing | Density and rhythm | 8px-based spacing with generous section gaps |
| Surfaces | Cards, borders, shadows | White cards with thin gray borders |
| Components | Buttons, inputs, navigation | Medium-radius buttons with clear hover states |
| Restrictions | Styles to avoid | No gradients, glass effects, or giant text |

This works better because each visual choice has a boundary.

## What is the best structure for a Bolt.new theme prompt?

The most reusable structure is:

**Context + visual direction + design tokens + component rules + responsive behavior + preservation rules.**

You can turn that into one reusable template:

> Restyle the existing [product type] using a [visual direction] design system.
>
> Color system:
> - Page background: [color]
> - Surface: [color]
> - Primary text: [color]
> - Secondary text: [color]
> - Accent: [color]
> - Borders: [color]
>
> Typography:
> - Use [font direction]
> - Headings should feel [quality]
> - Body text should prioritize readability
> - Keep the type scale controlled rather than oversized
>
> Components:
> - Cards: [style]
> - Buttons: [style]
> - Inputs: [style]
> - Navigation: [style]
>
> Layout:
> - Use [spacing density]
> - Keep content aligned to a consistent grid
> - Maintain strong hierarchy between sections
>
> Responsive behavior:
> - Preserve hierarchy on mobile
> - Stack dense layouts cleanly
> - Keep touch targets comfortable
>
> Do not change:
> - Existing functionality
> - Content
> - Routes
> - Data logic
>
> Avoid:
> - [unwanted style]
> - [unwanted style]
> - [unwanted style]

The preservation section is particularly important when you are theming an existing project rather than starting from scratch.

## Best Bolt.new custom theme prompt for a modern SaaS app

For a modern SaaS interface, keep the system quiet enough that the product itself stays dominant.

Use this prompt:

> Restyle the existing application with a refined modern SaaS theme.
>
> Use a very light neutral background with white elevated surfaces. Use near-black text for primary content and muted gray for secondary information. Choose one saturated blue accent for primary buttons, selected navigation items, links, focus states, and important data.
>
> Use clean sans-serif typography with compact but readable sizing. Keep headings confident without making them oversized. Use medium font weights for labels and navigation, stronger weights for titles, and comfortable line-height for long text.
>
> Use 10px to 14px corner radii across cards, inputs, dropdowns, and buttons. Keep borders subtle and shadows restrained. Avoid heavy floating-card effects.
>
> Use generous whitespace between major sections but tighter spacing inside functional components.
>
> The interface should feel precise, calm, polished, and production-ready.
>
> Do not add gradients, decorative blobs, glassmorphism, oversized hero typography, random icons, or excessive rounded pills.
>
> Preserve all existing features, routes, copy, and application logic. Change the visual system only.

That gives you a strong baseline without forcing Bolt.new to invent the product again.

## Best dark theme prompt for Bolt.new

Dark themes often fail because everything becomes equally dark. Good dark UI still needs clear layers.

Try:

> Convert the existing interface into a sophisticated dark theme without changing its structure or functionality.
>
> Use a deep charcoal page background rather than pure black. Use slightly lighter surfaces for cards, modals, sidebars, dropdowns, and tables so hierarchy remains visible.
>
> Use soft white for important text and muted cool gray for secondary text.
>
> Use one electric blue accent sparingly for primary actions, selected states, active navigation, links, and focus rings.
>
> Use thin low-contrast borders between adjacent surfaces. Keep shadows extremely subtle.
>
> Preserve the existing spacing system and layout hierarchy.
>
> Buttons should be compact and functional, not glossy. Inputs should have clearly visible boundaries and accessible focus states.
>
> Avoid neon overload, glowing borders, gradients, transparent glass panels, and pure black backgrounds.
>
> Make the final result feel like a serious developer or productivity product.

The key idea is surface separation. A dark theme needs more than swapping white for black.

## Best minimal theme prompt

Minimal does not mean empty. It means reducing visual competition.

> Apply a minimal editorial product theme to the entire interface.
>
> Use an off-white background, nearly black text, subtle warm-gray borders, and one muted accent color.
>
> Remove unnecessary shadows, decorative backgrounds, excessive badges, gradient fills, and redundant dividers.
>
> Use typography as the main hierarchy tool. Make headings moderately large and strongly weighted, while keeping body text compact and readable.
>
> Increase whitespace around major content groups.
>
> Cards should use simple borders instead of pronounced shadows.
>
> Buttons should be straightforward with clear primary, secondary, hover, disabled, and focus states.
>
> Keep the design distinctive through typography, proportions, spacing, and composition instead of visual effects.
>
> Do not alter functionality or content.

This prompt is useful when Bolt.new has produced something that feels visually busy or obviously AI-generated.

## Best luxury theme prompt

Luxury UI usually comes from restraint rather than adding more visual effects.

> Redesign the interface with a quiet luxury visual direction.
>
> Use a warm ivory background, deep graphite text, soft stone-colored secondary text, and a restrained dark bronze accent.
>
> Use an elegant editorial typography hierarchy with large but controlled headings, generous line-height, and refined body text.
>
> Use wide spacing, deliberate alignment, thin borders, very subtle shadows, and low-radius containers.
>
> Avoid colorful gradients, bright SaaS blues, glowing elements, playful illustrations, chunky icons, and excessive cards.
>
> Primary actions should feel confident and understated.
>
> Images should have generous breathing room rather than being surrounded by decorative UI.
>
> Preserve the existing product structure and behavior.
>
> The result should feel expensive because it is controlled, not because it contains more decoration.

## How do you create a custom theme from a reference UI?

Do not tell Bolt.new merely to “make it look like this.” Extract the reusable visual rules first.

For example, suppose you find a screen on VP0.com with the kind of visual hierarchy you want. Rather than copying individual content, identify:

- page background behavior
- card surface color
- accent usage
- heading scale
- body text scale
- radius style
- border strength
- shadow strength
- spacing density
- navigation treatment
- button hierarchy
- information density

Then turn those characteristics into a prompt.

This is more reliable than copying a screenshot blindly because you are creating a system Bolt.new can reuse across screens.

Clone the pattern, not the brand. Do not copy logos, trademarked artwork, proprietary copy, or another product's identity.

## A practical theme extraction prompt

Once you know the reference direction, use:

> I want to reproduce the design language of my reference, not its brand identity or content.
>
> Extract and apply these visual characteristics:
>
> - restrained neutral color palette
> - strong contrast between page and card surfaces
> - medium-radius containers
> - compact navigation
> - bold but controlled headings
> - small muted metadata
> - consistent 8px-based spacing
> - limited accent color usage
> - thin neutral borders
> - minimal shadows
>
> Apply these rules consistently to every existing screen.
>
> Keep all existing content, functionality, routes, and component behavior unchanged.
>
> Do not introduce new sections unless necessary for responsive layout.
>
> Do not imitate logos, brand assets, proprietary copy, or recognizable branded decoration from the reference.

That final boundary matters whenever your inspiration comes from another product.

## Should you create the whole theme in one Bolt.new prompt?

Create the design system in one prompt, but refine the application in focused passes.

Trying to redesign every visual detail and change functionality simultaneously gives the model too many independent decisions.

A more controlled workflow looks like this:

| Pass | Prompt goal | What you inspect |
| --- | --- | --- |
| 1 | Establish theme tokens | Colors, fonts, radius, borders |
| 2 | Apply layout hierarchy | Spacing, containers, grids |
| 3 | Refine components | Buttons, forms, cards, tables |
| 4 | Fix responsive UI | Mobile, tablet, overflow |
| 5 | Polish interaction states | Hover, focus, active, disabled |
| 6 | Consistency pass | Visual drift across screens |

Bolt.new's own [prompting guidance](https://bolt.new/blog/prompting-guide) also emphasizes giving the model clear, scoped instructions instead of repeatedly steering vague requests.

The useful distinction is that one prompt can define the system, while later prompts should correct specific areas.

## What should your second prompt say?

After the initial theme pass, avoid saying:

> Make it better.

Give Bolt.new a design QA prompt instead:

> Review the interface for inconsistencies with the design system we just established.
>
> Check every visible screen for:
>
> - inconsistent border radius
> - incorrect accent colors
> - mismatched card surfaces
> - inconsistent heading sizes
> - uneven spacing
> - buttons that do not follow the primary and secondary hierarchy
> - inputs with inconsistent states
> - unnecessary shadows
> - mobile overflow
>
> Fix only those inconsistencies.
>
> Do not redesign components that already follow the theme correctly. Do not modify features, content, data handling, or routes.

This prevents the common cycle where one successful design gets changed again because a later prompt was too broad.

## How do you stop Bolt.new from destroying an existing design?

Tell it explicitly what is locked.

A useful preservation prompt is:

> Apply the requested visual changes only.
>
> Treat the following as locked:
>
> - page structure
> - component hierarchy
> - copy
> - routes
> - forms and validation behavior
> - data logic
> - authentication
> - API integration
>
> You may change:
>
> - colors
> - typography
> - spacing
> - borders
> - radii
> - shadows
> - decorative styling
> - responsive presentation when required
>
> Before changing a component, preserve its existing purpose and behavior.
>
> Do not replace working components simply to achieve the new visual theme.

This is one of the most useful prompt patterns once the project is functional.

## How should you prompt for typography?

Typography deserves its own pass because it can change the entire perceived quality of a product.

Try:

> Refine the typography system across the project.
>
> Create a consistent hierarchy for:
>
> - display headings
> - page titles
> - section headings
> - card titles
> - body text
> - labels
> - metadata
> - button text
>
> Avoid excessively large headings.
>
> Keep body text highly readable and use consistent line-height.
>
> Use stronger weight differences instead of relying only on dramatic size differences.
>
> Ensure mobile typography scales down naturally without destroying the hierarchy.
>
> Do not change layout, colors, features, or content during this pass.

If your UI still looks generic after the colors are correct, typography is often the next place to look.

## How should you prompt for colors?

Do not provide ten unrelated accent colors. Give every color a job.

A better prompt sounds like this:

> Simplify the color system.
>
> Create semantic roles for:
>
> - page background
> - primary surface
> - secondary surface
> - primary text
> - secondary text
> - border
> - primary accent
> - success
> - warning
> - error
>
> Use the primary accent selectively. Do not use it as decoration on every card.
>
> Maintain sufficient visual contrast between text, controls, and their backgrounds.
>
> Remove colors that do not have a clear semantic purpose.
>
> Keep the existing layout and functionality unchanged.

This makes later design work much easier because Bolt.new has a predictable palette to reuse.

## What workflow works best for Bolt.new custom themes?

For most projects, I would use this sequence:

1. **Choose the direction.** Start from a visual reference, mood, or existing product style.
2. **Extract the design rules.** Identify colors, typography, surfaces, radii, spacing, and density.
3. **Write one master theme prompt.** Define the design system and what Bolt.new must preserve.
4. **Apply it to the shell first.** Navigation, page background, primary containers, and typography establish the visual language.
5. **Refine components separately.** Cards, tables, buttons, forms, and dialogs often need targeted prompts.
6. **Run a mobile pass.** Fix spacing, stacking, navigation, overflow, and touch targets.
7. **Run a consistency pass.** Correct anything that drifted away from the system.
8. **Stop redesigning.** Once the system is coherent, spend your prompts on product behavior rather than endlessly changing aesthetics.

If you want a starting UI before writing the prompt, [VP0.com](https://vp0.com) can help you choose a concrete design direction instead of inventing one from adjectives.

## Where VP0.com fits into the workflow

VP0.com is most useful before the theme prompt is written. A visual reference gives you something concrete to analyze, which is usually easier than starting with “modern,” “minimal,” or “premium” and hoping the model interprets those words the same way you do.

The important part is not blindly duplicating a reference. Extract its system, then adapt that system to your own product, users, and brand.

VP0.com can therefore serve as the inspiration layer, while Bolt.new remains the builder applying your design instructions.

## What is the biggest limitation of custom theme prompting?

A theme prompt cannot replace design judgment.

Bolt.new can apply a well-described system quickly, but you still need to decide whether that system actually suits the product. A dense analytics dashboard, a consumer wellness application, and a luxury commerce site should not automatically share the same typography, spacing, or component density.

A reference library also does not solve the rest of the application. VP0.com can help you find a visual starting point, while your builder and connected services still handle the product's behavior, data, authentication, integrations, and deployment.

Treat prompting as a way to communicate design decisions, not as a substitute for making them.

## Key takeaways

The best Bolt.new custom theme prompts are specific enough to behave like a lightweight design system.

Define the visual mood, semantic colors, typography hierarchy, spacing, radii, surfaces, component rules, and responsive behavior. Add explicit preservation instructions whenever you are modifying an existing project.

Start with one master theme prompt, then refine typography, components, mobile behavior, and consistency in focused passes.

Avoid repeatedly asking Bolt.new to “make it more premium” or “make it look better.” Tell it what should actually change and what must remain untouched.

And when you cannot describe the theme yet, start from a real visual reference and extract the rules you want rather than forcing the model to invent an aesthetic from scratch.

## Frequently asked questions

### What is the best Bolt.new custom theme prompt?

The best Bolt.new custom theme prompt defines the complete visual system while protecting the existing product. Specify colors, typography, spacing, border radius, surfaces, component styles, responsive behavior, and a clear list of elements that Bolt.new must not change.

### How do I make Bolt.new designs look less generic?

Give Bolt.new concrete design constraints instead of broad adjectives. Define the typography hierarchy, component density, color roles, spacing rhythm, border treatment, and styles to avoid. A strong visual reference can also make those decisions easier.

### Should I use one large theme prompt or several prompts?

Use one prompt to establish the design system, then several focused prompts to refine individual areas. Separate passes for typography, components, responsiveness, and consistency are easier to inspect and correct than one uncontrolled redesign request.

### Can Bolt.new copy a design from another app?

You can recreate general interface patterns and visual principles, but avoid copying another company's branding, proprietary content, logos, trademarked assets, or proprietary code. Extract the design language and adapt it to your own product.

### Where can I find inspiration for a Bolt.new custom theme?

VP0.com is a practical starting point when you need a concrete interface direction before writing your theme prompt. Study the visual hierarchy and design rules of a reference, then convert those characteristics into instructions that fit your own application.
