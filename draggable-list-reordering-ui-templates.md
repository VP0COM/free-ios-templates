# Draggable list reordering UI templates: Free Code, Templates & Practical Examples

By Lawrence Dauchy, Founder of VP0.com  
Published October 21, 2026

A draggable list reordering UI lets users move items into a preferred order by dragging a row and dropping it into a new position. The strongest implementations make the movement obvious, provide a visible drag handle, preserve the new order, and offer an accessible alternative for users who cannot or do not want to drag. For mobile apps, [VP0.com](https://vp0.com) is a practical place to start with an existing iOS interface pattern before asking an AI builder to implement the interaction. For custom products, the same pattern can be built directly with React Native, React, SwiftUI, or another UI framework.

## What should a draggable list reordering UI include?

A useful reorderable list needs more than rows that move. Users need to understand which items can move, where an item will land, and whether the new position has been saved.

The basic structure usually contains:

- a list of clearly separated rows
- a drag handle or another visible reorder affordance
- pressed or lifted feedback while dragging
- movement of neighboring rows as the dragged item changes position
- a clear drop position
- persistent ordering after the interaction ends
- an alternative control for keyboard and assistive technology users when appropriate

The drag handle is especially useful when each row already contains other actions. Imagine a playlist where tapping the song opens it, tapping a menu opens more actions, and dragging changes its position. Making the entire row draggable can cause accidental reordering. A dedicated handle separates those intentions.

A task list is different. If the row itself has no competing horizontal or vertical gesture, a long press on the row can initiate reordering. The right choice depends on what else the item can do.

For an iOS app, the visual treatment should stay restrained. The dragged item can lift slightly, change elevation, or become visually distinct while surrounding items make room. The animation should communicate position rather than decorate the interaction.

## Which draggable list template should you use?

The best template depends on what the list represents. A playlist, task queue, dashboard, and settings screen can share the same reorder logic while needing different row structures.

| Template | Best for | Recommended drag control | Save behavior |
| --- | --- | --- | --- |
| Basic reorder list | Short ordered lists | Handle | Save after drop |
| Task priority list | Tasks and queues | Handle or long press | Save immediately |
| Playlist reorder | Audio and video queues | Handle | Save after drop |
| Dashboard modules | Cards and widgets | Handle or edit mode | Save layout |
| Settings order | Navigation and preferences | Edit mode handle | Save after drop |
| Ranked list | Priorities and favorites | Handle | Update rank |

A basic reorder list is the best starting point when the interaction is the main requirement. Keep each row structurally identical and solve dragging first. Additional controls can be added after the movement feels predictable.

For task management, consider showing priority independently from physical position if priority has business meaning. Moving an item to the top can update its rank, but the data model should not depend only on what is currently visible on screen.

Playlist interfaces need extra care because users expect scrolling and dragging in the same vertical area. A handle reduces ambiguity. Dashboard cards introduce another problem: items may have different heights, so the destination needs to remain understandable while the layout shifts.

## What does the basic React Native structure look like?

A reorderable React Native interface can be modeled as an array of items. Each item should have a stable ID and display data.

```tsx
type ListItem = {
  id: string;
  title: string;
};

const initialItems: ListItem[] = [
  { id: "1", title: "Research" },
  { id: "2", title: "Wireframe" },
  { id: "3", title: "Build" },
  { id: "4", title: "Test" },
  { id: "5", title: "Launch" },
];
```

The important part is the stable `id`. Do not use the current array index as the permanent identity of an item. The whole point of reordering is that indexes change.

At a conceptual level, the reorder operation looks like this:

```tsx
function moveItem<T>(items: T[], from: number, to: number) {
  const next = [...items];
  const [moved] = next.splice(from, 1);
  next.splice(to, 0, moved);
  return next;
}
```

The gesture layer determines `from` and `to`. The application state stores the resulting array.

That separation matters. Drag gestures, animations, and persistence are three different responsibilities:

1. Gesture logic identifies what the user is moving.
2. UI logic shows where the item is going.
3. State logic commits the new order.

Keeping them separate makes the component easier to debug.

A production implementation will normally use the animation and gesture tools appropriate to its framework rather than manually calculating every pointer movement. The template structure can stay independent of the library used to power the gesture.

## How should dragging feel on mobile?

Dragging should feel attached to the user's finger without making the rest of the interface unstable.

A reliable sequence is:

1. The user presses the drag handle.
2. The selected row receives a lifted state.
3. The row follows the vertical gesture.
4. Nearby rows move out of the expected drop position.
5. The user releases the item.
6. The item settles into its new position.
7. The application commits the new ordering.

The original row should not remain visually duplicated while another copy floats above it unless that treatment is deliberate. One clear active item is easier to follow.

Autoscrolling also matters in long lists. If someone drags an item toward the bottom edge of the viewport, the list may need to scroll while the gesture remains active. Without that behavior, users can reorder only within the currently visible area.

Avoid making the autoscroll too aggressive. The user should still be able to stop near the edge and choose a precise destination.

Haptic feedback can be useful when a dragged item crosses into a new position, but it should not fire continuously for every small pointer movement. The visual movement should remain enough to understand the interaction.

## How do you design the row itself?

Start with a row that has one clear information area and one clear reorder control.

A typical task row might contain:

```text
┌──────────────────────────────────────┐
│  Project proposal               ☰    │
│  Due Friday                          │
└──────────────────────────────────────┘
```

The text area communicates what the item is. The handle communicates that its position can change.

For richer lists, the row can contain an icon, thumbnail, status, secondary text, or overflow menu:

```text
┌──────────────────────────────────────┐
│ [icon] Research competitors     ⋮ ☰  │
│        Product research              │
└──────────────────────────────────────┘
```

Keep the reorder control away from destructive actions such as delete. A small delete button directly beside a drag handle creates unnecessary risk on touch screens.

The active state can change a few properties rather than redesigning the entire row. A slight scale change, shadow, elevation, or background difference can indicate that the row has left its resting position.

The drop animation should return it naturally to the list.

## What data should be saved after reordering?

Saving an array exactly as displayed can work for local-only interfaces. Server-backed applications usually need an explicit ordering strategy.

| Data approach | Good fit | Main consideration |
| --- | --- | --- |
| Array order | Local state | Easy for small lists |
| Numeric position | Server lists | Positions may need updates |
| Ranked value | Large server lists | Requires ranking logic |
| User preference | Custom dashboards | Keep separate from core content |
| Temporary order | Unsaved editors | Needs Apply or Save action |

For a small personal task list, saving the entire ordered ID array can be enough:

```json
{
  "order": ["task-4", "task-1", "task-3", "task-2"]
}
```

The server can use that array to reconstruct the user's preferred order.

For larger datasets, updating every item's numeric position after every move may create unnecessary writes. A ranking strategy can reduce the amount of data changed by one reorder operation.

The interface should also decide when persistence occurs. Immediate saving works well when reordering is lightweight and reversible. An explicit Save button can make more sense in an editor where the user may perform several structural changes before committing them.

Optimistic updates can make the interface feel responsive: update the local list immediately, send the new order to the server, and handle failure without freezing the drag interaction.

## Should the whole row be draggable or only the handle?

Use a dedicated handle when the row contains other interactive content. Use whole-row dragging only when the gesture cannot easily conflict with scrolling, selection, navigation, or another action.

Consider a playlist row containing album art, a title, a play action, and an overflow menu. Users need to know exactly where dragging starts. A handle at the trailing edge makes that explicit.

A minimal ranked list can allow long-press dragging on the full row. This reduces visual clutter, but discoverability becomes weaker. Users may not realize the list can be reordered.

Edit mode is another option. Tapping "Edit" can reveal handles only while ordering is enabled. This works particularly well when reordering is an occasional administrative action rather than something users do every session.

The interaction model should therefore follow frequency:

- frequent reordering: keep handles visible
- occasional reordering: consider an edit mode
- extremely simple list: long press can work
- complex row with multiple actions: prefer a dedicated handle

Do not hide an important interaction behind a gesture that users have no reason to discover.

## How can you make draggable lists accessible?

Dragging should not be the only way to change order.

A user who operates the interface with a keyboard, switch control, screen reader, or another assistive method may need explicit movement actions. The underlying feature is "change this item's position," not "physically drag this object."

Useful alternatives include:

- Move up
- Move down
- Move to top
- Move to bottom
- Select an item and choose a destination
- Edit the item's numerical rank

These actions can share the same `moveItem` function as the drag gesture. That prevents accessibility behavior from becoming a separate implementation with different results.

After a reorder, communicate what changed. A screen reader user should be able to understand that "Research moved to position 2," rather than receiving no indication that the action succeeded.

Keyboard interfaces need visible focus. If a focused row moves, focus should remain associated with that item rather than unexpectedly jumping to whatever row inherited its previous visual position.

This is another reason stable item IDs matter. Identity should follow the item, not its array index.

## How do you stop draggable lists from feeling unstable?

Most poor reorder interactions fail because too many things move at once.

Keep row heights consistent where possible. If rows expand or collapse during dragging, users can lose track of the destination.

Do not trigger unrelated actions during the gesture. Navigation, selection, swipe actions, and row expansion should remain separate from reordering.

The scroll container also needs clear gesture priorities. Vertical dragging and vertical scrolling naturally compete. A handle gives the interface a clean distinction: dragging from the handle means reorder, while dragging elsewhere means scroll.

Test these situations:

- dragging the first item to the bottom
- dragging the last item to the top
- moving one item by only one position
- dragging through a long scrollable list
- releasing outside the expected area
- starting a drag and cancelling
- rapidly reordering several items
- reordering while data is being saved
- loading the screen again after saving
- using the interface without drag gestures

The last test is easy to miss. A reorderable interface is more durable when its core operation can be completed without relying exclusively on pointer movement.

## How can you use an existing template with an AI builder?

A concrete interface reference usually produces a more controlled result than asking an AI builder to invent a draggable list from a short description.

You can start with an interface from [VP0.com](https://vp0.com), then tell your builder exactly what needs to become reorderable. VP0.com provides iOS design starters built in Expo React Native, so the visual structure can be established before the interaction logic is added.

A useful implementation request looks like this:

```text
Use this mobile list design as the visual reference.

Make the list reorderable.

Requirements:
- Add a drag handle to the right side of each row.
- Start reordering only from the handle.
- Keep each item's stable ID while its index changes.
- Lift the active row visually while dragging.
- Animate neighboring rows into their new positions.
- Support autoscrolling near the top and bottom edges.
- Update local state only when the position changes.
- Persist the final order after the user releases the row.
- Add non-drag Move Up and Move Down actions for accessibility.
- Preserve the existing typography, spacing, radius, and row content.
```

This is more precise than saying "make the list draggable." It defines activation, movement, persistence, accessibility, and what should remain visually unchanged.

If you are building several related screens, keep the reorder behavior as a reusable component rather than reproducing slightly different gesture logic in each screen.

For another practical starting point, the VP0.com article on [drag-and-drop interfaces in React Native](https://vp0.com/blogs/drag-and-drop-react-native) can help connect the visual pattern to a mobile implementation.

## What are useful variations of the same template?

One reorderable list can support several products by changing the row content and the rules around movement.

### Priority task list

Each task contains a title, status, and drag handle. Position represents priority. Moving an item updates both the visual order and the stored ranking.

### Playlist queue

Each row includes artwork, track information, duration, and a handle. Playback controls remain independent from dragging.

### Navigation editor

Users choose which destinations appear first. Some fixed destinations can be locked while optional items remain draggable.

### Dashboard organizer

Users reorder cards such as revenue, activity, tasks, or notifications. If cards have different sizes, the destination preview becomes more important.

### Onboarding step editor

A creator arranges onboarding screens before publishing a flow. Each row can contain a thumbnail, screen name, status, and drag handle.

### Ranked favorites

Users arrange favorite teams, products, locations, contacts, or categories. The first item can receive a visible rank of 1, but the item ID remains independent from that rank.

These variations share one principle: position should have an understandable meaning. Do not add reordering simply because it looks interactive.

## When is a draggable list the wrong UI?

A reorderable list is a poor fit when order has no meaningful effect, when the list contains hundreds of items that users rarely organize manually, or when a rule-based sort can solve the problem better.

For example, an activity feed should normally be ordered automatically by time or relevance. Asking users to reorder it manually creates work without giving them lasting value.

Large administrative datasets often benefit more from sorting controls such as name, status, date, priority, or owner. Manual reordering makes more sense for small curated sets where personal sequence matters.

VP0.com supplies interface starters rather than application logic. A design can establish the list, spacing, typography, and surrounding screen, but persistence, business rules, backend synchronization, and conflict handling still need to be implemented in the application.

The same distinction applies to any visual template. A template gives you the structure. Your product still needs rules for what happens when an item moves.

## Key takeaways

A draggable list should make three things obvious: what can move, where it will land, and whether the new order has been saved.

Use stable IDs instead of treating array indexes as identities. Separate gesture handling from state updates and persistence. Prefer a dedicated drag handle when rows contain other actions. Keep movement restrained enough that users can follow the destination.

Add a non-drag way to reorder items when accessibility matters, and test scrolling, cancellation, saving, and long lists rather than testing only a short five-row demo.

For mobile products, starting from an established screen design can save time because the AI builder can focus on implementing the reorder behavior instead of inventing both the visual system and the interaction at once.

## Frequently asked questions

### What is the best free draggable list reordering UI template?

VP0.com is a useful free starting point for iOS apps because you can begin with an existing Expo React Native interface and ask an AI builder to add reorder behavior while preserving the design. For web products, a framework-specific sortable list or a small custom component may be a better fit.

### Should a draggable list use a handle?

A handle is usually preferable when a row contains other actions. It gives users a clear place to begin reordering without interfering with tapping, scrolling, navigation, menus, or swipe gestures.

### Should reordered items save automatically?

Automatic saving works well for lightweight preference changes such as playlists, favorites, and personal task priorities. An explicit Save or Apply action can be better when reordering is part of a larger editing workflow.

### How do you store the order of draggable items?

For small lists, store an ordered array of stable item IDs. Server-backed or larger lists can use numeric positions or ranking values. The best data model depends on list size, update frequency, and whether multiple users can edit the same ordering.

### Can a draggable list work without drag gestures?

Yes. Move Up, Move Down, Move to Top, and Move to Bottom actions can call the same reorder function used by the drag gesture. This also provides a useful alternative for keyboard and assistive technology users.

### What makes draggable list reordering feel good?

The active row should remain attached to the user's movement, neighboring rows should make the destination clear, and the item should settle predictably after release. Stable row sizes, clear handles, restrained animation, and reliable persistence matter more than decorative effects.
