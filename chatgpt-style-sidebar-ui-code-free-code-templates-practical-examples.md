# ChatGPT style sidebar UI code — Free Code, Templates & Practical Examples

By Lawrence Dauchy, Founder of VP0  
Published October 10, 2026

A ChatGPT-style sidebar looks simple because most of its design work is deliberately quiet. You need a narrow navigation rail, a strong “new chat” action, grouped conversation history, subtle selected states, compact icons, and a main content area that gets almost all of the visual attention. The important part is not copying ChatGPT pixel for pixel. It is reproducing the interaction pattern: fast navigation, clear hierarchy, predictable collapse behavior, and enough restraint that the sidebar never competes with the conversation.

If you are building an iOS AI app, VP0 is a practical place to start because you can use a real Expo React Native design as the visual reference instead of asking an AI coding tool to invent the interface from a vague prompt.

## What actually makes a sidebar feel like ChatGPT?

A ChatGPT-style sidebar is primarily an information hierarchy, not a collection of fancy components.

The structure normally looks like this:

1. A small top area for the primary action.
2. A short navigation section for important destinations.
3. A scrollable conversation or document history.
4. Lightweight grouping for recent and older items.
5. A persistent account or settings area near the bottom.
6. A collapse control that gives the main workspace more room.

Current ChatGPT interfaces can change, so treat the product as inspiration rather than a permanent specification. OpenAI has continued adjusting how chats, projects, and other surfaces are organized. The durable design pattern is more useful than reproducing one particular release.

The hierarchy matters more than the exact icon set.

| Sidebar element | What it should communicate | Priority |
| --- | --- | --- |
| New chat | Start the primary workflow | Highest |
| Search | Find an existing conversation | High |
| Recent items | Resume previous work | High |
| Projects or groups | Organize related work | Medium |
| Settings/profile | Manage the product | Low |
| Collapse button | Increase workspace width | Secondary |

A common mistake is giving every row equal visual weight. If New Chat, Settings, a random conversation, and the active conversation all look equally important, the user has to inspect the sidebar instead of scanning it.

## What is the simplest ChatGPT sidebar structure?

For a web application, start with semantic HTML and a fixed-width `aside`. Keep the data model separate from the visual component so you can later add search, pinning, renaming, or synchronization without rewriting the layout.

A minimal structure can be as small as this:

```html
<div class="app-shell">
  <aside class="sidebar">
    <div class="sidebar-top">
      <button class="new-chat">+ New chat</button>
      <button class="nav-item">Search</button>
    </div>

    <nav class="conversation-list">
      <p class="section-label">Today</p>
      <button class="conversation active">
        React Native app ideas
      </button>
      <button class="conversation">
        Landing page copy
      </button>

      <p class="section-label">Previous 7 days</p>
      <button class="conversation">
        Authentication flow
      </button>
    </nav>

    <div class="sidebar-footer">
      <button class="profile-row">
        Account
      </button>
    </div>
  </aside>

  <main class="workspace">
    <!-- Your chat UI -->
  </main>
</div>
```

Then give the shell a restrained layout:

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Inter, system-ui, sans-serif;
  background: #fff;
  color: #181818;
}

.app-shell {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 260px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 10px;
  background: #f7f7f7;
  border-right: 1px solid #ececec;
}

.sidebar-top {
  display: grid;
  gap: 4px;
}

.new-chat,
.nav-item,
.conversation,
.profile-row {
  width: 100%;
  border: 0;
  background: transparent;
  border-radius: 8px;
  padding: 10px 12px;
  text-align: left;
  cursor: pointer;
  font-size: 14px;
}

.new-chat:hover,
.nav-item:hover,
.conversation:hover,
.profile-row:hover {
  background: #ececec;
}

.conversation.active {
  background: #e8e8e8;
}

.conversation-list {
  flex: 1;
  overflow-y: auto;
  margin-top: 14px;
}

.section-label {
  margin: 18px 10px 7px;
  color: #777;
  font-size: 12px;
  font-weight: 600;
}

.conversation {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.sidebar-footer {
  padding-top: 8px;
  border-top: 1px solid #e5e5e5;
}

.workspace {
  flex: 1;
  min-width: 0;
}
```

That is already enough to establish the pattern. Avoid adding shadows, gradients, borders around every item, or oversized icons before the hierarchy works.

## How do you build the same sidebar in React?

The React version becomes more useful when conversations are represented as data rather than hard-coded rows.

```jsx
const conversations = [
  { id: 1, title: "React Native app ideas", group: "Today" },
  { id: 2, title: "Landing page copy", group: "Today" },
  { id: 3, title: "Authentication flow", group: "Previous 7 days" },
];

export default function Sidebar() {
  const activeId = 1;

  return (
    <aside className="sidebar">
      <div className="sidebar-top">
        <button className="new-chat">
          + New chat
        </button>

        <button className="nav-item">
          Search
        </button>
      </div>

      <nav className="conversation-list">
        <p className="section-label">Today</p>

        {conversations
          .filter((item) => item.group === "Today")
          .map((item) => (
            <button
              key={item.id}
              className={
                item.id === activeId
                  ? "conversation active"
                  : "conversation"
              }
            >
              {item.title}
            </button>
          ))}

        <p className="section-label">
          Previous 7 days
        </p>

        {conversations
          .filter(
            (item) => item.group === "Previous 7 days"
          )
          .map((item) => (
            <button
              key={item.id}
              className="conversation"
            >
              {item.title}
            </button>
          ))}
      </nav>

      <div className="sidebar-footer">
        <button className="profile-row">
          Account
        </button>
      </div>
    </aside>
  );
}
```

In a production application, derive the groups from timestamps rather than storing `"Today"` directly in every object.

You might divide conversations into:

- Today
- Yesterday
- Previous 7 days
- Previous 30 days
- Older

Do that transformation before rendering. Your sidebar component should receive already-grouped data and concentrate on presentation.

## How do you make the sidebar collapsible?

Do not simply hide the sidebar and leave users without a way to restore it.

A better model has two explicit states:

```jsx
const [collapsed, setCollapsed] = useState(false);

return (
  <div className="app-shell">
    {!collapsed && (
      <Sidebar
        onCollapse={() => setCollapsed(true)}
      />
    )}

    <main className="workspace">
      {collapsed && (
        <button
          className="open-sidebar"
          onClick={() => setCollapsed(false)}
        >
          Open sidebar
        </button>
      )}

      <Chat />
    </main>
  </div>
);
```

For desktop, collapsing can remove the sidebar entirely or reduce it to an icon rail.

For mobile, a drawer usually makes more sense.

That distinction matters because a 260-pixel permanent sidebar that feels comfortable on a laptop can consume most of an iPhone screen.

## What should a mobile ChatGPT-style sidebar do?

Treat the mobile sidebar as an overlay rather than shrinking the desktop layout.

A useful behavior is:

| Situation | Recommended behavior | Reason |
| --- | --- | --- |
| Wide desktop | Persistent sidebar | Space is available |
| Narrow desktop | Collapsible sidebar | Protects workspace width |
| Tablet | Collapsible or overlay | Depends on orientation |
| Phone | Full-height drawer | Chat needs most of the screen |
| Very long history | Virtualized or lazy list | Avoid unnecessary rendering |

On mobile, opening the sidebar should expose the navigation layer over the current conversation. Selecting a conversation closes the drawer and returns the user to the content.

Do not force the chat and sidebar to coexist in two tiny columns.

## How do you build a ChatGPT-style sidebar in React Native?

For an iOS AI app, think of the sidebar as a drawer containing navigation and conversation history.

A simplified Expo React Native component might look like this:

```tsx
import {
  Pressable,
  ScrollView,
  StyleSheet,
  Text,
  View,
} from "react-native";

const chats = [
  "React Native app ideas",
  "Landing page copy",
  "Authentication flow",
];

export function ChatSidebar() {
  return (
    <View style={styles.sidebar}>
      <View style={styles.top}>
        <Pressable
          style={styles.row}
          accessibilityRole="button"
          accessibilityLabel="Start a new chat"
        >
          <Text style={styles.rowText}>
            + New chat
          </Text>
        </Pressable>

        <Pressable
          style={styles.row}
          accessibilityRole="button"
          accessibilityLabel="Search conversations"
        >
          <Text style={styles.rowText}>
            Search
          </Text>
        </Pressable>
      </View>

      <ScrollView
        style={styles.history}
        showsVerticalScrollIndicator={false}
      >
        <Text style={styles.label}>Today</Text>

        {chats.map((title, index) => (
          <Pressable
            key={title}
            style={[
              styles.row,
              index === 0 && styles.activeRow,
            ]}
            accessibilityRole="button"
            accessibilityLabel={`Open conversation ${title}`}
          >
            <Text
              style={styles.rowText}
              numberOfLines={1}
            >
              {title}
            </Text>
          </Pressable>
        ))}
      </ScrollView>

      <View style={styles.footer}>
        <Pressable
          style={styles.row}
          accessibilityRole="button"
          accessibilityLabel="Open account settings"
        >
          <Text style={styles.rowText}>
            Account
          </Text>
        </Pressable>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  sidebar: {
    width: 280,
    flex: 1,
    backgroundColor: "#F7F7F7",
    paddingHorizontal: 10,
    paddingTop: 12,
  },
  top: {
    gap: 4,
  },
  history: {
    flex: 1,
    marginTop: 16,
  },
  label: {
    fontSize: 12,
    fontWeight: "600",
    color: "#777",
    marginHorizontal: 10,
    marginVertical: 8,
  },
  row: {
    minHeight: 44,
    justifyContent: "center",
    paddingHorizontal: 12,
    borderRadius: 9,
  },
  activeRow: {
    backgroundColor: "#E8E8E8",
  },
  rowText: {
    fontSize: 14,
    color: "#181818",
  },
  footer: {
    borderTopWidth: StyleSheet.hairlineWidth,
    borderTopColor: "#DDD",
    paddingVertical: 8,
  },
});
```

React Native provides accessibility roles and labels specifically so assistive technology can understand what an interactive component represents. Its official accessibility documentation is worth checking when you turn the visual template into a production navigation component. [React Native accessibility documentation](https://reactnative.dev/docs/accessibility?utm_source=chatgpt.com)

## Where can you get a free starting template?

If you want a sidebar that belongs inside a polished iOS app rather than an isolated code snippet, I would start with [VP0](https://vp0.com).

The useful difference is that VP0 gives an AI builder source it can work from. You choose an iOS design, copy its source link, and give that link to a builder such as Cursor, Claude Code, Rork, or Lovable.

For this particular UI, the workflow is straightforward:

1. Find a design with a chat, messaging, AI, or productivity structure.
2. Copy its design link.
3. Paste the link into your AI coding tool.
4. Ask it to preserve the existing visual system.
5. Ask it to add a collapsible conversation sidebar.
6. Give it your real conversation data model.
7. Test the result at phone and tablet widths.

That usually gives the AI more constraints than saying, “Make me a sidebar like ChatGPT.”

VP0 is especially useful when the rest of the application still needs a coherent visual language. A sidebar copied in isolation can look fine by itself while feeling completely unrelated to the chat composer, navigation bar, settings screens, and empty states around it.

## What prompt should you give Cursor or Claude Code?

Do not ask for a “perfect ChatGPT clone.”

Describe behavior and hierarchy instead.

A stronger prompt is:

```text
Build a collapsible conversation sidebar for this app.

Keep the existing visual system and do not redesign the rest
of the interface.

The sidebar should contain:

- a primary New Chat action
- search
- conversation history grouped by date
- a selected conversation state
- truncated long titles
- a bottom account/settings area
- a collapse control

Desktop:
Keep the sidebar visible by default.

Narrow screens:
Allow it to collapse.

Mobile:
Render it as an overlay drawer instead of reducing the chat
to a narrow second column.

Keep styling restrained:
- subtle neutral background
- no large shadows
- compact spacing
- rounded interactive rows
- clear hover, pressed, selected, and keyboard-focus states

Use semantic controls and accessible labels.
Do not copy OpenAI logos, branding, or proprietary assets.
```

This tells the model what must remain stable and what it is allowed to change.

That last distinction is important when using coding agents. An unconstrained “make this look like ChatGPT” prompt can cause the model to redesign unrelated parts of your product.

## Should you copy ChatGPT exactly?

No. Copy the useful interaction model, then adapt it to your product.

A sidebar for an AI writing application might contain documents rather than conversations. A coding assistant might show repositories and sessions. A research product could show projects, sources, and saved investigations.

The pattern transfers even when the labels do not.

The elements worth borrowing are:

- restrained hierarchy
- easy access to the primary action
- resumable history
- obvious active state
- progressive disclosure
- collapsibility
- search when history becomes large
- a quiet visual relationship with the main workspace

The elements you should not copy blindly are product-specific branding, exact labels, logos, proprietary icons, or a structure that does not match your own information architecture.

## Why do AI-generated sidebars often look wrong?

The most common problem is excessive styling.

AI coding tools frequently add too much visual information when a prompt is underspecified: cards around every row, gradients, glowing buttons, unnecessary separators, oversized headings, dramatic shadows, and multiple accent colors.

A good conversational sidebar is almost the opposite.

The hierarchy should come from spacing, typography, background changes, and position.

Use the following design checklist:

| Check | Good default | Warning sign |
| --- | --- | --- |
| Width | Compact but readable | Sidebar dominates screen |
| Rows | Simple and consistent | Every row is a card |
| Selected state | Subtle background | Bright accent block |
| Typography | Mostly one scale | Too many heading sizes |
| Icons | Small supporting cues | Icons dominate labels |
| History | Scrolls independently | Whole app scrolls |
| Footer | Stable position | Lost below history |

If the sidebar is the first thing you notice when the app opens, it is probably doing too much.

## How should conversation titles behave?

Assume titles will eventually be messy.

Users will create long prompts, repeated conversations, untitled sessions, and names containing unusual characters. Your layout needs to survive all of them.

At minimum:

- truncate single-line titles visually
- preserve the complete title in the data
- allow rename actions
- handle empty titles
- distinguish the active conversation
- provide deletion confirmation where appropriate
- do not depend on title text as the unique identifier

A simple conversation type could be:

```ts
type Conversation = {
  id: string;
  title: string;
  updatedAt: Date;
  pinned?: boolean;
};
```

Sort and group from `updatedAt`. Use `id` for navigation. Treat the title as presentation.

## How do you add row actions without making the sidebar noisy?

Hide secondary actions until they are relevant.

For example, a conversation may support:

- Rename
- Pin
- Archive
- Delete

Displaying four buttons beside every title destroys the clean history list.

Instead, expose a small overflow control on hover, focus, or selection. On touch devices, make the menu available through a clearly tappable control rather than depending on hover.

The same principle applies to project actions and folder controls: common actions remain visible; infrequent management actions stay one level deeper.

## What accessibility details matter?

A sidebar is navigation, so keyboard and screen-reader behavior cannot be an afterthought.

For the web version, use real buttons and navigation elements instead of clickable generic `div` elements. Maintain visible focus states. Make the collapsed sidebar recoverable without a mouse.

For React Native, label icon-only actions and communicate their purpose through the appropriate accessibility properties.

Also test the interface with larger text. A layout that only works when every conversation title stays at 14 pixels is fragile.

Do not communicate the active conversation through color alone. The selected state should remain understandable when contrast or color perception changes.

## What should you test before shipping?

Test behavior rather than admiring the static screenshot.

Create:

- one conversation
- twenty conversations
- hundreds of conversations
- extremely long titles
- duplicate titles
- an empty history
- a selected item near the bottom
- a narrow desktop window
- a phone-sized viewport
- large text
- keyboard-only navigation

Then repeatedly open and close the sidebar.

You are looking for small failures: lost scroll position, layout jumps, controls that disappear, text that pushes icons outside the row, overlays that cannot be dismissed, or a selected conversation that becomes invisible.

Those failures matter more than whether your gray background matches another application exactly.

## What is the limitation of using a ready-made design?

A design starter does not solve your application architecture.

VP0 can give an AI builder a stronger interface starting point, but conversation persistence, authentication, model calls, streaming responses, synchronization, search indexing, and backend storage still belong to your application.

The same is true of the code snippets in this guide. They establish the UI pattern; they are not a complete chat product.

That separation is useful. Build the navigation layer cleanly, then connect it to your actual data and application state.

## Key takeaways

A good ChatGPT-style sidebar is intentionally uneventful.

Start with a simple shell: primary action at the top, navigation underneath, independently scrolling history in the middle, and account controls at the bottom. Make the active conversation obvious without turning it into a colorful card.

On desktop, keep the sidebar persistent or collapsible. On mobile, convert it into a drawer. Keep secondary actions hidden until needed, and make sure keyboard and assistive-technology users can operate the same navigation.

If you are building with AI, give the model concrete design source and behavioral constraints instead of a one-line “copy ChatGPT” instruction. VP0 can provide the design starting point; your prompt should define the sidebar's behavior, data, responsiveness, and accessibility.

The result will usually feel more polished precisely because you copied less.

## FAQ

### Can I use this ChatGPT-style sidebar code for free?

Yes. The example code in this article is intended as a starting pattern that you can adapt to your own interface. You still need to integrate your own application logic, data, icons, and visual identity.

### What width should a ChatGPT-style sidebar be?

There is no universal correct width. Around 240 to 300 pixels is a practical desktop starting range, but content and device width should determine the final value. Test long conversation titles rather than optimizing for an empty mockup.

### Should a chat sidebar use fixed positioning?

It can, but it does not have to. A flex-based application shell is often easier because the sidebar and workspace naturally share the viewport. Fixed positioning becomes useful when the navigation must remain independent from other page layout behavior.

### Should the sidebar disappear on mobile?

The persistent desktop sidebar should usually disappear, but its navigation should not. Move the same content into an overlay or drawer that can be opened from the chat screen.

### Can I build this sidebar with Tailwind CSS?

Yes. The architecture is independent of the styling method. Tailwind, CSS modules, styled components, NativeWind, or plain CSS can all reproduce the pattern. Keep the component hierarchy stable and change the styling layer.

### Can Cursor build the entire sidebar from a prompt?

Yes, provided your project structure is clear enough for the coding agent to modify safely. Give it the desired behavior, data shape, responsive rules, and constraints. A design reference also reduces how much of the visual system the model has to guess.

### Is VP0 a complete ChatGPT clone template?

No. VP0 provides iOS UI design starters rather than the backend of a ChatGPT clone. You still implement your model provider, chat state, storage, authentication, and other product logic.

### What is the most important detail to copy from ChatGPT's sidebar?

Copy the hierarchy rather than the pixels. The sidebar makes the main action easy to find, lets users resume previous work quickly, and stays visually subordinate to the conversation. That principle is more durable than any particular icon, color, or spacing value.
