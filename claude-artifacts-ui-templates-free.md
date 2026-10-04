# Claude Artifacts UI Templates Free: Best Free Examples & Copy-Paste Code

By Lawrence Dauchy, Founder of VP0  
Published October 4, 2026

The most useful free Claude Artifacts UI templates are small, editable interfaces with working interactions: a searchable dashboard, a task board, a pricing calculator, or a settings screen. Start with one clear purpose, use sample data, and ask Claude to build around code you can understand and reuse. The examples below provide original copy-paste starters and prompts for adapting them. They use standard HTML, CSS, and JavaScript, so you can also save them as local HTML files. Treat them as interface prototypes: the buttons and calculations work, but accounts, payments, and shared data need separate implementation.

## What should a free Claude Artifacts UI template include?

A useful template should give you a readable layout, a working interaction, and an obvious place to change its content. A screen that looks finished but contains dead buttons creates extra work as soon as you try to adapt it.

For a first prototype, look for five things:

- Sample data that resembles the content your users will see.
- Clear headings, labels, and button text.
- Responsive behavior for narrow screens.
- A meaningful action, such as filtering, adding, or calculating.
- Code that keeps content separate from presentation where practical.

A template does not need a complicated component system. A short page with sensible spacing and one reliable interaction is often easier to improve than a large dashboard full of decorative widgets.

“Free” also needs a clear meaning. The code below is provided without a purchase requirement. That does not mean every feature in your Claude account, every generation request, or every service you later connect will be unlimited or free.

Choose the screen according to the decision you need to test. If you want to know whether people understand your product, build a landing page. If you want to test a workflow, build the actual form or task screen.

## Which UI examples are the best starting points?

The best starting point is the smallest interface that demonstrates your main user action. These five patterns cover different questions without requiring a complete application.

### Searchable dashboard

Use a searchable dashboard when users need to find and compare records. Examples include projects, products, support requests, and content drafts.

Build the search interaction before adding charts. A dashboard becomes useful when users can locate something and act on it. Summary cards should explain the records below them rather than display unrelated numbers.

### Task board

Use a task board when the product revolves around progress. A simple board can help you test labels, task creation, and movement between stages.

Start with buttons for moving tasks. Drag-and-drop can come later if testing shows it improves the workflow.

### Pricing calculator

Use a calculator when users need to understand how inputs affect an estimate. Examples include seat counts, project quantities, or service packages.

Show the assumptions beside the result. A precise-looking total is misleading if the user cannot see what it includes.

### Settings screen

Use a settings screen when you need to test preferences, notification choices, or account options.

Include a visible saved state or explain that changes apply immediately. A switch that changes color without explaining its effect is incomplete.

### Landing page

Use a landing page when you need to test positioning and message hierarchy.

Give it one primary action. A headline, a concrete explanation, a small example, and a clear button are enough for an initial version. Add sections only when they answer a real visitor question.

## How do you turn starter code into an artifact?

Paste the starter code into a conversation and explain the output you want. Specify the format, interaction, and constraints rather than asking Claude to “make it modern.”

Use this prompt with any example below:

```text
Use the code below as the starting point for a responsive
interface artifact.

Keep the existing behavior and improve the visual design.

Requirements:
- Keep everything in one self-contained HTML file.
- Use inline CSS and plain JavaScript.
- Do not add external fonts, images, scripts, or dependencies.
- Preserve semantic HTML and visible keyboard focus.
- Use sample data only.
- Make the layout work at 375px and 1280px widths.
- Explain any feature that remains a demonstration.

Return the complete HTML document.
```

Then paste the code immediately after the prompt.

If your available artifact workflow uses a different output format, ask Claude to adapt the starter to that format. Do not assume that controls or preview behavior from an older tutorial will match your current account.

Keep a copy of each working version. When you request a revision, identify the exact change: “reduce the card padding” or “add a status filter.” This makes it easier to preserve behavior while improving the design.

## What copy-paste code works for a searchable dashboard?

A searchable card dashboard is a practical first template because it combines layout, data rendering, and filtering. This example includes a labeled search field, a result count, and an empty state.

Save it as `dashboard.html` to open it directly in a browser, or paste it into Claude with the adaptation prompt.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Project Dashboard</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      background: #f5f7fb;
      color: #182235;
      font: 16px/1.5 system-ui, sans-serif;
    }
    main {
      max-width: 1000px;
      margin: auto;
      padding: 40px 20px;
    }
    h1 { margin-bottom: 4px; }
    .intro { color: #526078; }
    label { display: block; margin-bottom: 8px; }
    input {
      width: 100%;
      padding: 12px;
      border: 1px solid #aab5c5;
      border-radius: 10px;
      font: inherit;
    }
    input:focus-visible {
      outline: 3px solid #2563eb;
      outline-offset: 3px;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 16px;
    }
    article {
      padding: 20px;
      border: 1px solid #dce2eb;
      border-radius: 16px;
      background: white;
    }
    article h2 { margin: 0 0 12px; font-size: 20px; }
    .status {
      display: inline-block;
      padding: 4px 10px;
      border-radius: 20px;
      background: #e8eefb;
      color: #23457a;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <main>
    <h1>Projects</h1>
    <p class="intro">Find a project by name or status.</p>

    <label for="search">Search projects</label>
    <input id="search" type="search" placeholder="Try Website or Active">

    <p id="count" role="status"></p>
    <div id="projects" class="grid"></div>
  </main>

  <script>
    const projects = [
      { name: "Website refresh", status: "Active", owner: "Maya" },
      { name: "Customer onboarding", status: "Planning", owner: "Sam" },
      { name: "Product launch", status: "Complete", owner: "Alex" }
    ];

    const search = document.getElementById("search");
    const container = document.getElementById("projects");
    const count = document.getElementById("count");

    function render() {
      const query = search.value.trim().toLowerCase();
      const matches = projects.filter(project =>
        `${project.name} ${project.status} ${project.owner}`
          .toLowerCase().includes(query)
      );

      container.replaceChildren();

      matches.forEach(project => {
        const card = document.createElement("article");
        const title = document.createElement("h2");
        const owner = document.createElement("p");
        const status = document.createElement("span");

        title.textContent = project.name;
        owner.textContent = `Owner: ${project.owner}`;
        status.textContent = project.status;
        status.className = "status";

        card.append(title, owner, status);
        container.append(card);
      });

      count.textContent = matches.length
        ? `${matches.length} project${matches.length === 1 ? "" : "s"} found`
        : "No projects match your search.";
    }

    search.addEventListener("input", render);
    render();
  </script>
</body>
</html>
```

The project list is the main customization point. Replace the sample names, owners, and statuses before changing the layout.

The code inserts content with `textContent`, which treats values as text. Keep that approach when you replace sample records with user-provided content.

For a useful next revision, ask:

```text
Add a labeled status dropdown beside the search field.
Both filters must work together.
Keep the empty state and result count accurate.
Do not add charts or external dependencies.
```

That revision tests real dashboard behavior while keeping the interface manageable.

## What copy-paste code works for an interactive calculator?

A calculator is a good template when you want immediate feedback from user input. This example uses fictional pricing to demonstrate the interaction: a $12 base amount plus $8 per seat.

It produces an estimate only. It does not charge anyone, calculate tax, or connect to a billing service.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Plan Calculator</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      padding: 24px;
      background: #edf2f7;
      color: #172033;
      font: 16px/1.5 system-ui, sans-serif;
    }
    main {
      max-width: 480px;
      margin: 40px auto;
      padding: 28px;
      border-radius: 20px;
      background: white;
      border: 1px solid #d9e1ec;
    }
    h1 { margin-top: 0; }
    label { display: block; margin: 24px 0 8px; }
    input { width: 100%; accent-color: #234fd1; }
    input:focus-visible {
      outline: 3px solid #234fd1;
      outline-offset: 6px;
    }
    .total {
      margin: 24px 0;
      padding: 20px;
      border-radius: 12px;
      background: #eef3ff;
    }
    output { display: block; font-size: 36px; font-weight: 700; }
    .note { color: #526078; font-size: 14px; }
  </style>
</head>
<body>
  <main>
    <h1>Estimate your plan</h1>
    <p>Demo pricing: $12 base plus $8 per seat each month.</p>

    <label for="seats">
      Team size: <span id="seat-count">3</span> seats
    </label>
    <input id="seats" type="range" min="1" max="25" value="3">

    <div class="total">
      <span>Estimated monthly total</span>
      <output id="total" for="seats"></output>
    </div>

    <p class="note">
      Fictional pricing for this example. Taxes and other fees
      are not included. No payment is collected.
    </p>
  </main>

  <script>
    const seats = document.getElementById("seats");
    const seatCount = document.getElementById("seat-count");
    const total = document.getElementById("total");

    const currency = new Intl.NumberFormat("en-US", {
      style: "currency",
      currency: "USD",
      maximumFractionDigits: 0
    });

    function update() {
      const quantity = Number(seats.value);
      seatCount.textContent = quantity;
      total.value = currency.format(12 + quantity * 8);
    }

    seats.addEventListener("input", update);
    update();
  </script>
</body>
</html>
```

Change the calculation before changing the visual style. Write down the pricing rule in plain language, then confirm that the JavaScript implements it.

For this example, one seat should produce $20, three seats should produce $36, and 25 seats should produce $212. Checking known values catches mistakes that a polished interface can hide.

Ask Claude for a controlled extension:

```text
Add monthly and annual billing choices.

For this fictional example, annual billing costs ten times
the monthly amount.

Show the billing period beside the total.
Preserve the existing monthly formula.
Do not add checkout or payment processing.
```

Keep estimates and billing separate. If the calculator later becomes part of a real product, its displayed assumptions should match the authoritative pricing logic.

## How can you generate a task board or settings template?

Give Claude a small functional specification with clear acceptance criteria. A precise prompt can provide a reusable starting point even when you do not already have code.

### Task board prompt

```text
Create a responsive task board as a single HTML document
with inline CSS and JavaScript.

Use three columns:
- To do
- In progress
- Done

Include:
- Six realistic sample tasks.
- A labeled form for adding a task.
- A priority label on every task.
- Buttons for moving tasks between columns.
- Task counts in each column.
- An empty state for an empty column.

Use native buttons and form controls.
Reject blank task titles.
Insert user-entered titles as text, not HTML.
Keep changes in memory and explain that reloading resets them.
Do not use drag-and-drop or external dependencies.
```

This specification makes the behavior easy to inspect. Add a task, move it twice, and confirm that the counts remain correct.

Also try a long task title. A card should grow naturally rather than clip the text or push its buttons outside the column.

### Settings screen prompt

```text
Create a responsive settings screen as one HTML document
with inline CSS and JavaScript.

Include:
- A display-name field.
- Email notification checkboxes.
- A light or dark appearance choice.
- Save changes and Reset buttons.
- A visible confirmation after saving.

Use fictional profile data.
Keep saved preferences in memory for this demonstration.
Reset should restore the initial sample values.
Label every field and preserve keyboard focus visibility.
Do not imply that account details are updated on a server.
```

The important distinction is between edited values and saved values. A working settings prototype should demonstrate what happens when users change a field, save it, and reset it.

Once the interaction is clear, ask for design changes separately. Changing colors and behavior in the same request makes errors harder to locate.

## How do you improve a template without breaking it?

Improve one layer at a time: behavior, layout, typography, then decoration. This keeps a useful prototype from turning into a screen that looks better but works less reliably.

Start by checking the main action. Search should filter correctly. A calculator should produce the right totals. A task board should move the intended task.

Next, inspect the layout with realistic content. Short sample labels can hide problems. Try a long project name, an empty list, and a narrow window.

Then establish a small visual system:

- One font family.
- A consistent spacing scale.
- A restrained set of text sizes.
- One primary action color.
- Consistent borders and corner radii.
- Clear focus and disabled states.

Use a revision prompt that names the boundaries:

```text
Improve spacing, typography, and responsive layout.

Preserve all existing interactions and sample data.
Keep primary text readable.
Use a single accent color.
Do not add new features or dependencies.
Return the full updated document.
```

After each revision, repeat the same basic checks. Press Tab through the interface, activate buttons with the keyboard, and test the empty state.

Avoid solving every visual problem with smaller text. If a card feels crowded, remove unnecessary content or improve its hierarchy.

Before using a template in a real application, review the implementation beyond its appearance. These examples do not provide authentication, permissions, durable storage, or production error handling. An interface can demonstrate those flows without implementing the services behind them.

For code copied from elsewhere, check its license and dependencies before reuse. Publicly visible code does not automatically come with unrestricted reuse rights. For an unfamiliar template, inspect what scripts it loads and what network requests it makes.

## Key takeaways

Start with a searchable dashboard when users need to find records, a calculator when they need an estimate, or a task board when they need to manage progress.

Keep the first version small enough to understand. A single working action gives you something concrete to test and improves the quality of later revisions.

The copy-paste examples above use self-contained browser code and fictional data. Adapt the content first, verify the behavior, and then refine the visual design.

When you move toward a real product, explicitly decide how data is stored, who can access it, and which service owns each important operation. Those decisions turn an interface prototype into an application.

## Frequently asked questions

### What are the best free Claude Artifacts UI templates?

The most useful free starters are searchable dashboards, task boards, calculators, settings screens, and landing pages. Choose one according to the action you need to test. A template with clear code and working behavior is usually a better starting point than a complex layout with decorative controls.

### Can I copy and paste these templates into Claude?

Yes. Paste a complete example into a conversation and ask Claude to adapt it into the output format available in your account. Specify which behavior must remain intact. The two HTML examples can also be saved locally and opened in a browser without installing a framework.

### Should I use HTML or React for a UI template?

Use HTML, CSS, and JavaScript for a small standalone prototype with a few interactions. Use React when you are integrating the screen into a React application or need reusable components across multiple screens. Match the template to your intended project rather than adding a framework automatically.

### Will these templates remember changes after a reload?

The examples above do not persist user changes. The dashboard returns to its sample data, and the calculator returns to its initial input. For a tracker or settings screen, choose a persistence method explicitly and test it. Saving data locally and sharing data between users require different implementations.

### How do I fix a template that looks good but does not work?

Describe the exact failure, the action that triggers it, and the result you expect. Include any visible error message and the relevant code. Ask Claude to repair that behavior while preserving the layout. After the fix, repeat the original action and check nearby states, including empty inputs and long text.
