# Multi-select dropdown with chips UI code — Free Code, Templates & Practical Examples

By Lawrence Dauchy, Founder of VP0.com  
Published October 20, 2026

A good multi-select dropdown with chips lets users search or browse a list, select several options, see those choices immediately as removable chips, and change the selection without losing context. The interface looks simple, but getting the states, keyboard behavior, overflow, filtering, and mobile layout right takes more work than a normal dropdown.

If you are building the interface from scratch, start with the interaction model before styling it. Decide how users open the menu, select items, remove chips, search a long list, clear everything, and understand disabled or unavailable options.

For app builders who would rather begin from an existing interface direction instead of a blank prompt, [VP0.com](https://vp0.com) is a practical free starting point for iOS UI design. You can choose a design starter and give its source link to an AI coding tool, then adapt the resulting interface to your multi-select use case.

## What is a multi-select dropdown with chips?

A multi-select dropdown combines three ideas:

- a control that opens a list of available options;
- multi-selection, so choosing one option does not replace the previous choice;
- chips or tags that visually represent the current selections.

Imagine a project form with a field called **Skills**. A user chooses React, TypeScript, and Node.js. Instead of showing only “3 selected,” the field displays:

`React ×   TypeScript ×   Node.js ×`

Each chip can be removed independently, while the dropdown remains available for adding more values.

This pattern works particularly well for:

- tags;
- team members;
- categories;
- skills;
- filters;
- locations;
- permissions;
- interests;
- product attributes.

The key question is whether users benefit from seeing their individual selections. If they do, chips are usually more informative than a simple selection count.

## The basic UI structure

A useful multi-select component can be broken into a few predictable pieces.

| Element | Purpose | Typical behavior |
| --- | --- | --- |
| Label | Explains the field | Remains visible above the control |
| Chip area | Shows selected values | Wraps or collapses when crowded |
| Search input | Finds available values | Filters options while typing |
| Dropdown trigger | Opens the options | Indicates open/closed state |
| Options list | Shows choices | Supports mouse and keyboard selection |
| Selected state | Shows existing choices | Checkmark or other clear indicator |
| Remove control | Deletes one chip | Returns the item to available options |
| Clear action | Removes all choices | Best for larger selections |

You do not necessarily need every element. A short list of five options, for example, may not need search.

## A practical React multi-select with chips

Here is a deliberately small implementation that demonstrates the state model without tying the component to a particular UI library.

```jsx
import { useMemo, useState } from "react";

const options = [
  "React",
  "TypeScript",
  "Next.js",
  "Node.js",
  "PostgreSQL",
  "Tailwind CSS",
];

export default function MultiSelect() {
  const [open, setOpen] = useState(false);
  const [query, setQuery] = useState("");
  const [selected, setSelected] = useState([]);

  const filteredOptions = useMemo(() => {
    return options.filter((option) =>
      option.toLowerCase().includes(query.toLowerCase())
    );
  }, [query]);

  function toggleOption(option) {
    setSelected((current) =>
      current.includes(option)
        ? current.filter((item) => item !== option)
        : [...current, option]
    );
  }

  function removeOption(option) {
    setSelected((current) =>
      current.filter((item) => item !== option)
    );
  }

  return (
    <div className="multi-select">
      <label className="label">Skills</label>

      <div
        className="control"
        onClick={() => setOpen(true)}
      >
        {selected.map((option) => (
          <span className="chip" key={option}>
            {option}
            <button
              type="button"
              aria-label={`Remove ${option}`}
              onClick={(event) => {
                event.stopPropagation();
                removeOption(option);
              }}
            >
              ×
            </button>
          </span>
        ))}

        <input
          value={query}
          placeholder={
            selected.length ? "Add more..." : "Select skills..."
          }
          onChange={(event) => {
            setQuery(event.target.value);
            setOpen(true);
          }}
          onFocus={() => setOpen(true)}
        />
      </div>

      {open && (
        <div className="dropdown">
          {filteredOptions.length ? (
            filteredOptions.map((option) => {
              const isSelected = selected.includes(option);

              return (
                <button
                  type="button"
                  className="option"
                  key={option}
                  onClick={() => toggleOption(option)}
                >
                  <span>{option}</span>
                  <span>{isSelected ? "✓" : ""}</span>
                </button>
              );
            })
          ) : (
            <div className="empty">No matching options</div>
          )}
        </div>
      )}
    </div>
  );
}
```

And a simple CSS foundation:

```css
.multi-select {
  position: relative;
  width: 100%;
  max-width: 440px;
  font-family: system-ui, sans-serif;
}

.label {
  display: block;
  margin-bottom: 8px;
  font-size: 14px;
  font-weight: 600;
}

.control {
  min-height: 46px;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 6px;
  padding: 6px 10px;
  border: 1px solid #d0d5dd;
  border-radius: 10px;
  background: white;
}

.control:focus-within {
  outline: 2px solid currentColor;
  outline-offset: 2px;
}

.control input {
  flex: 1;
  min-width: 100px;
  border: 0;
  outline: 0;
  padding: 6px 2px;
  font: inherit;
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 5px 8px;
  border-radius: 999px;
  background: #f2f4f7;
  font-size: 14px;
}

.chip button {
  border: 0;
  background: transparent;
  cursor: pointer;
  font-size: 16px;
}

.dropdown {
  position: absolute;
  z-index: 20;
  top: calc(100% + 6px);
  left: 0;
  right: 0;
  max-height: 240px;
  overflow-y: auto;
  padding: 6px;
  border: 1px solid #d0d5dd;
  border-radius: 10px;
  background: white;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.12);
}

.option {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 9px 10px;
  border: 0;
  border-radius: 7px;
  background: transparent;
  text-align: left;
  cursor: pointer;
}

.option:hover,
.option:focus-visible {
  background: #f2f4f7;
}

.empty {
  padding: 12px 10px;
  font-size: 14px;
}
```

This is a useful visual and state-management starting point, not a complete production accessibility implementation.

## The interaction model matters more than the chips

The most common mistake is spending too much time making the chips attractive while leaving the dropdown behavior ambiguous.

A user should be able to predict what happens after selecting an option.

For most multi-select fields, I would keep the dropdown open after a selection. Closing it after every choice forces users through an unnecessary open-select-close cycle when they want several items.

The selected option should also remain recognizable in the dropdown. A checkmark is usually clearer than simply changing the background color.

For example:

```text
Search skills...

✓ React
  Vue
✓ TypeScript
  Svelte
✓ Node.js
```

That allows users to inspect the complete option set while understanding their current state.

## Should selected options disappear from the dropdown?

Usually, no.

There are two common models.

### Model 1: Keep selected items visible

Selected values remain in the list and receive a selected indicator.

This works well when users might reconsider selections or need to understand which items from the original list they have already chosen.

### Model 2: Remove selected items

After an option becomes a chip, it disappears from the available list.

This makes the remaining list shorter, but it can also make users wonder where an item went.

For most settings, filtering, and form interfaces, I prefer keeping options visible and marking them clearly.

## Search becomes important surprisingly quickly

A dropdown containing six choices can be scanned.

A dropdown containing 60 choices becomes a search problem.

Once the list grows, put a text input directly into the interaction rather than expecting users to scroll through everything.

Filtering should normally be case-insensitive:

```js
const filtered = options.filter((option) =>
  option.label.toLowerCase().includes(query.toLowerCase())
);
```

For structured datasets, you can search multiple properties:

```js
const filtered = options.filter((option) => {
  const searchValue =
    `${option.label} ${option.description}`.toLowerCase();

  return searchValue.includes(query.toLowerCase());
});
```

Avoid overly aggressive fuzzy matching unless users genuinely need it. Predictable search often feels better than clever search.

## How should keyboard interaction work?

This is where a polished visual component can become frustrating if the behavior was never designed.

A searchable dropdown should have a deliberate keyboard model. The [WAI-ARIA Authoring Practices Guide for comboboxes](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/) describes established interaction conventions including arrow-key navigation, Escape for dismissing a popup, and Enter for accepting a suggestion.

A practical target for your component is:

| Key | Expected action |
| --- | --- |
| Down Arrow | Open the menu or move to the next option |
| Up Arrow | Move to the previous option |
| Enter | Select the active option |
| Escape | Close the dropdown |
| Backspace | Remove the last chip when the search field is empty |
| Tab | Continue through the form normally |

Backspace deserves special attention.

If the input contains text, Backspace should edit that text normally. Only when the input is empty should you consider using another Backspace press to remove the last selected chip.

Do not override familiar text-editing behavior just because the component has custom keyboard controls.

## Accessibility needs more than ARIA attributes

Adding `role="combobox"` does not automatically make a custom component accessible.

You need the semantics and interaction behavior to agree.

Depending on your implementation, that may include:

- an accessible field label;
- an expanded/collapsed state;
- a relationship between the input and popup;
- identifiable options;
- a selected state;
- keyboard navigation;
- visible focus;
- meaningful names for chip removal buttons;
- announcements when selections change.

If the chip says “TypeScript,” a remove icon should not be exposed to assistive technology merely as “button” or “x.”

Give it a meaningful name such as:

```jsx
<button aria-label="Remove TypeScript">
  ×
</button>
```

Then test the actual component with keyboard navigation and assistive technology instead of assuming the markup is sufficient.

## How should chips behave when there are many selections?

Wrapping every chip onto additional lines works beautifully with three selections and badly with 30.

There are several reasonable approaches.

### Wrap naturally

Best when users usually choose only a few items.

```text
[React ×] [TypeScript ×] [Next.js ×]
[Node.js ×]
```

This is the simplest model and keeps every selection visible.

### Show a limited number

Display the first few chips and summarize the rest.

```text
[React ×] [TypeScript ×] [+6]
```

Opening `+6` can reveal the complete selection.

This keeps forms compact when selections can become large.

### Use a selection count

For very large filter sets, individual chips may stop being useful.

```text
12 technologies selected
```

This sacrifices immediate visibility for density, so use it only when seeing every selected label is not essential.

## Mobile changes the answer

Desktop dropdowns can depend on generous horizontal space and hover states. Mobile cannot.

For small screens:

- make the entire field easy to tap;
- give removal controls comfortable touch targets;
- avoid extremely tiny chips;
- prevent long labels from breaking the layout;
- keep important options visible above the keyboard;
- consider a bottom sheet or full-screen selector for very large datasets.

A dropdown that extends below a mobile viewport while the software keyboard occupies half the screen quickly becomes unpleasant.

For complex mobile selection, a separate selection surface can be cleaner:

```text
Choose interests

Search interests...

☑ Design
☐ Development
☑ Artificial Intelligence
☐ Marketing
☑ Startups

3 selected

[Done]
```

The collapsed form field can then show chips after the user returns.

## A better AI prompt for generating this component

If you ask an AI coding tool for “a multi-select dropdown,” you leave too many interaction decisions unspecified.

A more useful prompt is:

```text
Build a reusable searchable multi-select field.

Requirements:
- React and TypeScript
- selected values appear as removable chips
- dropdown stays open after each selection
- selected options remain visible with checkmarks
- text input filters options
- arrow keys navigate results
- Enter selects the active option
- Escape closes the menu
- Backspace removes the last chip only when search is empty
- support disabled options
- show an empty-search state
- visible keyboard focus
- accessible labels for remove buttons
- responsive behavior for narrow screens
- no external component library
```

This is much more likely to produce useful code because it describes behavior rather than only appearance.

If the visual direction is still vague, start from a design reference. [VP0.com](https://vp0.com) can provide an iOS-oriented UI starting point that an AI builder can read from source, after which you can tell the builder exactly how the selection behavior should change.

## Useful states to design before coding

A multi-select is not one screen. It is a small state system.

Design at least these states before considering the component finished:

1. Empty and closed.
2. Empty and focused.
3. Dropdown open.
4. Option highlighted.
5. One item selected.
6. Several chips selected.
7. Search query entered.
8. No search results.
9. Disabled option.
10. Long chip label.
11. Many selected items.
12. Validation error.

This catches layout problems much earlier.

A field that looks excellent with “React” and “Vue” might fall apart when a real dataset contains “Customer Relationship Management” or when eight selections need to fit into a narrow form.

## What should the component API look like?

For reusable React code, avoid storing business logic inside the visual component.

A simple controlled API might look like this:

```jsx
<MultiSelect
  label="Skills"
  options={skills}
  value={selectedSkills}
  onChange={setSelectedSkills}
  placeholder="Select skills..."
/>
```

A more flexible option shape could be:

```ts
type MultiSelectOption = {
  value: string;
  label: string;
  disabled?: boolean;
};
```

Then the component accepts:

```ts
type MultiSelectProps = {
  label: string;
  options: MultiSelectOption[];
  value: string[];
  onChange: (value: string[]) => void;
  placeholder?: string;
  searchable?: boolean;
  disabled?: boolean;
  maxSelections?: number;
};
```

This keeps the component reusable for teams, categories, filters, locations, or any other dataset.

## Common mistakes to avoid

### Closing after every selection

This makes repeated selection unnecessarily slow.

### Hiding selection state in the menu

Users should not have to compare the chip row with every option manually.

### Using color as the only selected indicator

Add a checkmark, icon, or another explicit state.

### Letting chips expand forever

Define overflow behavior before real users select 15 values.

### Making the remove target tiny

A beautiful 12-pixel × icon is not useful if it is difficult to activate.

### Deleting chips too aggressively

Backspace should not unexpectedly remove selections while someone is editing search text.

### Ignoring long labels

Test realistic data, not only short placeholder values.

### Treating accessibility as a final patch

Keyboard behavior, focus, selection, and popup semantics affect the component architecture. They are easier to design from the beginning.

## When chips are the wrong pattern

Not every multi-select needs chips.

If users commonly select dozens or hundreds of options, chips create visual noise. A checklist, transfer list, filter panel, or dedicated selection screen may work better.

Likewise, a multi-select dropdown may be unnecessary when the complete set contains only three or four options. Visible checkboxes are often clearer because users can see every choice immediately.

The best control is not the one that uses the most sophisticated UI pattern. It is the one that makes the available choices and current state easiest to understand.

## Where VP0.com fits

VP0.com is most useful here as a design starting point rather than as the selection logic itself. Its designs provide UI source that can be handed to an AI builder, while the multi-select behavior still needs to be implemented for your particular data, validation, accessibility, and state requirements.

That distinction matters. A strong visual reference can stop an AI-generated interface from becoming generic, but it does not replace decisions about keyboard behavior, filtering, option state, or application logic.

The library is also still growing, so you may not find a ready-made design matching this exact component. In that situation, use the closest relevant screen or flow as the visual foundation and specify the multi-select interaction separately.

## A practical implementation checklist

Before shipping your component, check the complete experience:

- Can users understand what the field is asking for?
- Can they see every important selected value?
- Can each chip be removed intentionally?
- Is the selected state also visible inside the dropdown?
- Does search work with realistic data?
- Is there a useful no-results state?
- Does the component handle disabled options?
- Can users operate it without a mouse?
- Is focus always visible?
- Does Escape close the popup predictably?
- Does Backspace preserve normal text editing?
- Do long labels behave correctly?
- Is there a strategy for many selected values?
- Does it remain usable on a narrow mobile screen?
- Are selection changes communicated appropriately to assistive technology?
- Does validation remain understandable when the field has an error?

If several answers are no, the component probably needs another interaction pass rather than more visual polish.

## FAQ

### What is a multi-select dropdown with chips?

It is a form control that allows users to choose multiple options from a dropdown and displays those selections as individual removable chips or tags.

### Should a multi-select dropdown close after each selection?

Usually not. Keeping the dropdown open makes repeated selections faster. Closing can still make sense when users almost always choose a single item despite the field technically supporting several.

### Should selected options stay visible in the dropdown?

Usually yes. Keep them visible and mark them with a clear selected state such as a checkmark. This helps users understand the relationship between the complete option list and their current selections.

### Should a multi-select have search?

Use search when the option set becomes difficult to scan efficiently. Small lists often do not need it; long or dynamic lists usually benefit from filtering.

### What should Backspace do with chips?

When the search input contains text, Backspace should edit the text normally. When the input is empty, Backspace can remove or focus the last chip, provided the behavior is predictable.

### Is a multi-select dropdown accessible by default?

No. Custom dropdowns require deliberate labeling, focus management, keyboard behavior, selection semantics, and testing with assistive technology.

### Should I use chips when users can select many items?

Not necessarily. When selections regularly become large, showing a count, using a checklist, or opening a dedicated selection interface can be easier to understand.

### What is the simplest way to build one with AI?

Give the coding tool explicit requirements for selection, removal, filtering, keyboard controls, overflow, responsive behavior, and accessibility. A visual starting point from VP0.com can define the appearance, while your prompt defines the component behavior.
