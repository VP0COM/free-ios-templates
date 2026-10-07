# Stripe Style Pricing Page Code Free: Best Free Examples & Copy-Paste Code

By Lawrence Dauchy, Founder of VP0  
Published October 6, 2026

A free Stripe style pricing page starts with clear typography, generous spacing, readable plan cards, and honest billing details. You can build that look with ordinary HTML, CSS, and a little JavaScript, without buying a template or installing a component library. VP0 is a useful free design starting point if your wider project includes an iOS app, while the original web example below gives you a pricing page you can copy directly. It includes three plans, monthly and annual billing controls, responsive cards, and visible keyboard focus. The prices are fictional examples, and the buttons demonstrate plan selection rather than processing payments.

## What makes a pricing page feel like Stripe?

The useful design pattern is a clear hierarchy: explain the offer, show the price, describe what it includes, and make the next action easy to find.

A polished pricing page does not need a complicated animated background. Most of the work comes from consistent spacing and clear decisions about what deserves attention.

Start with these elements:

- A short headline that describes the offer.
- A billing selector near the plans.
- Prices with explicit billing periods.
- Feature lists written in concrete terms.
- One clear action per plan.
- A restrained accent color.
- Supporting information about billing and cancellation.

The important distinction is between visual inspiration and copying someone else’s identity. Use your own product name, wording, colors, and original code. Avoid presenting a page as an official Stripe template or reproducing proprietary assets.

For a subscription product, the page should answer three questions before someone selects a plan: what will I pay, what will I receive, and when will I be charged?

If those answers are buried under decorative effects, simplify the design before adding more code.

## Which free pricing page examples are worth building?

Three useful examples cover different business models: a three-plan subscription page, a single-offer page, and a usage-based calculator. The best choice depends on how customers actually buy your product.

### Example 1: Three subscription plans

A three-card layout works when customers have meaningful differences in usage or requirements.

For example:

- Starter serves an individual working on a small project.
- Growth supports a team with shared workflows.
- Scale adds higher limits and administrative features.

Each step should explain a real change in value. Three nearly identical cards with different prices leave customers guessing.

The complete code below uses this structure because it provides a practical starting point for many subscription products.

### Example 2: One offer with one action

A single pricing card works when there is only one package to purchase.

Use a wide card with the price, included services, delivery details, and one clear button. If payment is one-time, say “one-time payment” beside the amount.

Do not add artificial tiers simply to make the page resemble a larger software company. A straightforward offer is easier to explain and maintain.

### Example 3: Usage-based pricing

A calculator works when the bill depends on measurable usage, such as requests, storage, or seats.

Show the unit price, included allowance, and estimated total. Label estimates clearly, especially when taxes, minimum charges, or additional fees can change the final amount.

A calculator requires more careful logic than fixed-price cards. Its output should follow the same billing rules as the actual checkout.

## How do you build a free pricing page without dependencies?

Create an `index.html` file, paste in the following code, and open it in a browser. Everything needed for the demonstration is contained in one file.

There are no external fonts, images, scripts, or packages. The layout uses native HTML elements and CSS Grid.

The fictional annual plans cost ten times their monthly prices. The annual view shows the monthly equivalent and the full annual charge, so visitors can see both amounts.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta
    name="viewport"
    content="width=device-width, initial-scale=1"
  >
  <title>Product Pricing</title>

  <style>
    :root {
      color-scheme: light;
      --background: #f6f8fc;
      --surface: #ffffff;
      --text: #17233b;
      --muted: #52617a;
      --border: #dce3ef;
      --accent: #5546d9;
      --accent-dark: #4032ad;
      --radius: 20px;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      background:
        radial-gradient(
          circle at 50% 0%,
          #eae7ff,
          transparent 42%
        ),
        var(--background);
      color: var(--text);
      font-family: system-ui, sans-serif;
      line-height: 1.6;
    }

    button {
      font: inherit;
    }

    button:focus-visible {
      outline: 3px solid var(--accent);
      outline-offset: 4px;
    }

    .pricing {
      width: min(1120px, calc(100% - 40px));
      margin-inline: auto;
      padding-block: 72px;
    }

    .intro {
      max-width: 680px;
      margin: 0 auto 32px;
      text-align: center;
    }

    .eyebrow {
      color: var(--accent);
      font-weight: 700;
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    h1 {
      margin: 12px 0;
      font-size: clamp(2rem, 5vw, 3.5rem);
      line-height: 1.12;
      letter-spacing: -0.04em;
    }

    .intro p:last-child {
      color: var(--muted);
      font-size: 1.1rem;
    }

    .billing {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 32px;
    }

    .billing button {
      min-height: 44px;
      padding: 10px 18px;
      border: 1px solid var(--border);
      border-radius: 999px;
      background: var(--surface);
      color: var(--text);
      cursor: pointer;
    }

    .billing button[aria-pressed="true"] {
      border-color: var(--accent);
      background: var(--accent);
      color: white;
    }

    .plans {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 20px;
    }

    .plan {
      display: flex;
      flex-direction: column;
      padding: 28px;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      background: var(--surface);
      box-shadow: 0 12px 35px rgb(23 35 59 / 5%);
    }

    .plan.featured {
      border: 2px solid var(--accent);
      padding: 27px;
    }

    .badge {
      align-self: flex-start;
      margin: 0 0 14px;
      padding: 4px 10px;
      border-radius: 999px;
      background: #eeebff;
      color: var(--accent-dark);
      font-size: 0.8rem;
      font-weight: 700;
    }

    .plan h2 {
      margin: 0 0 8px;
      font-size: 1.4rem;
    }

    .description {
      margin: 0;
      color: var(--muted);
    }

    .price {
      margin: 24px 0 0;
    }

    .amount {
      font-size: 2.7rem;
      font-weight: 750;
      letter-spacing: -0.04em;
      line-height: 1.2;
    }

    .period {
      color: var(--muted);
    }

    .billing-note {
      min-height: 3.2em;
      margin: 8px 0 22px;
      color: var(--muted);
      font-size: 0.9rem;
    }

    .features {
      flex: 1;
      margin: 0 0 28px;
      padding-left: 20px;
    }

    .features li {
      margin-bottom: 10px;
    }

    .cta {
      width: 100%;
      min-height: 48px;
      padding: 12px 16px;
      border: 1px solid var(--border);
      border-radius: 10px;
      background: #f2f4f9;
      color: var(--text);
      font-weight: 700;
      cursor: pointer;
    }

    .featured .cta {
      border-color: var(--accent);
      background: var(--accent);
      color: white;
    }

    .cta:hover {
      background: #e7ebf4;
    }

    .featured .cta:hover {
      background: var(--accent-dark);
    }

    .disclosure,
    .status {
      max-width: 720px;
      margin: 24px auto 0;
      color: var(--muted);
      text-align: center;
    }

    .status {
      min-height: 1.6em;
      color: var(--text);
      font-weight: 600;
    }

    @media (max-width: 860px) {
      .plans {
        grid-template-columns: 1fr;
      }

      .pricing {
        padding-block: 44px;
      }
    }
  </style>
</head>

<body>
  <main class="pricing">
    <header class="intro">
      <p class="eyebrow">Simple pricing</p>
      <h1>Choose the plan that fits your work.</h1>
      <p>
        Compare included features and billing options
        before you choose.
      </p>
    </header>

    <div
      class="billing"
      role="group"
      aria-label="Billing period"
    >
      <button
        type="button"
        data-billing="monthly"
        aria-pressed="true"
      >
        Monthly
      </button>

      <button
        type="button"
        data-billing="annual"
        aria-pressed="false"
      >
        Annual
      </button>
    </div>

    <section class="plans" aria-label="Available plans">
      <article
        class="plan"
        data-plan="Starter"
        data-monthly="12"
        data-annual="120"
      >
        <h2>Starter</h2>
        <p class="description">For individual projects.</p>

        <p class="price">
          <span class="amount">$12</span>
          <span class="period">/ month</span>
        </p>

        <p class="billing-note">Billed monthly.</p>

        <ul class="features">
          <li>One workspace</li>
          <li>Three active projects</li>
          <li>Email support</li>
        </ul>

        <button class="cta" type="button">
          Choose Starter
        </button>
      </article>

      <article
        class="plan featured"
        data-plan="Growth"
        data-monthly="29"
        data-annual="290"
      >
        <p class="badge">For growing teams</p>
        <h2>Growth</h2>
        <p class="description">For shared workflows.</p>

        <p class="price">
          <span class="amount">$29</span>
          <span class="period">/ month</span>
        </p>

        <p class="billing-note">Billed monthly.</p>

        <ul class="features">
          <li>Five workspaces</li>
          <li>Twenty active projects</li>
          <li>Shared project access</li>
          <li>Priority email support</li>
        </ul>

        <button class="cta" type="button">
          Choose Growth
        </button>
      </article>

      <article
        class="plan"
        data-plan="Scale"
        data-monthly="79"
        data-annual="790"
      >
        <h2>Scale</h2>
        <p class="description">For larger operations.</p>

        <p class="price">
          <span class="amount">$79</span>
          <span class="period">/ month</span>
        </p>

        <p class="billing-note">Billed monthly.</p>

        <ul class="features">
          <li>Twenty workspaces</li>
          <li>One hundred active projects</li>
          <li>Shared project access</li>
          <li>Administrative controls</li>
        </ul>

        <button class="cta" type="button">
          Choose Scale
        </button>
      </article>
    </section>

    <p class="disclosure">
      Demo prices in USD. Annual plans are charged
      once per year. Replace all prices, features,
      and billing terms before publishing.
    </p>

    <p
      class="status"
      role="status"
      aria-live="polite"
    ></p>
  </main>

  <script>
    const billingButtons =
      document.querySelectorAll("[data-billing]");
    const cards = document.querySelectorAll("[data-plan]");
    const status = document.querySelector(".status");

    const money = new Intl.NumberFormat("en-US", {
      style: "currency",
      currency: "USD",
      maximumFractionDigits: 2
    });

    let billing = "monthly";

    function updatePrices(nextBilling) {
      billing = nextBilling;

      billingButtons.forEach((button) => {
        button.setAttribute(
          "aria-pressed",
          String(button.dataset.billing === billing)
        );
      });

      cards.forEach((card) => {
        const monthly = Number(card.dataset.monthly);
        const annual = Number(card.dataset.annual);
        const isAnnual = billing === "annual";

        card.querySelector(".amount").textContent =
          money.format(isAnnual ? annual / 12 : monthly);

        card.querySelector(".period").textContent =
          isAnnual ? "/ month equivalent" : "/ month";

        card.querySelector(".billing-note").textContent =
          isAnnual
            ? `${money.format(annual)} billed annually.`
            : `${money.format(monthly)} billed monthly.`;
      });

      status.textContent =
        `${billing === "annual" ? "Annual" : "Monthly"} ` +
        "billing selected.";
    }

    billingButtons.forEach((button) => {
      button.addEventListener("click", () => {
        updatePrices(button.dataset.billing);
      });
    });

    cards.forEach((card) => {
      card.querySelector(".cta").addEventListener(
        "click",
        () => {
          status.textContent =
            `${card.dataset.plan} selected with ` +
            `${billing} billing. Demo only; ` +
            "no payment has been taken.";
        }
      );
    });
  </script>
</body>
</html>
```

## What does the copy-paste code actually include?

The example provides a working pricing interface with plan cards, billing controls, and a selection message. It does not create accounts, collect payment details, or activate subscriptions.

The distinction matters because a convincing interface can look more complete than it is.

The monthly and annual controls update two pieces of information together: the headline amount and the billing explanation below it. This avoids showing an annual monthly equivalent without explaining the actual charge.

The cards stack vertically on narrower screens. That keeps feature text readable and avoids squeezing three columns into a phone display.

Each call-to-action names its plan. “Choose Growth” gives more context than repeating “Get started” across every card.

The highlighted plan uses a descriptive badge rather than an unsupported popularity claim. “For growing teams” explains its audience without implying that customer data proves it is the most popular option.

Finally, the status message confirms the interaction while making the demonstration boundary explicit. Replace this behavior when your real purchase flow is ready.

## How should you customize the pricing page?

Customize the offer and billing information before changing decorative details. A pricing page becomes useful when its content matches what customers actually receive.

### Replace the fictional plans

Update the plan names, descriptions, feature lists, and prices together.

If Starter includes three projects in the card, your application should enforce that same allowance. Avoid vague claims such as “advanced features” when you can name the feature directly.

Keep the descriptions short. Use the feature list for details that affect the purchase decision.

### Set annual totals explicitly

The code stores an annual total for each plan instead of assuming a universal discount.

This gives you control over your actual billing model. Some businesses charge eleven monthly payments for a year, some charge ten, and others offer no annual reduction.

If you advertise a percentage saving, calculate it from the real monthly and annual totals. Recheck that calculation whenever pricing changes.

### Change the visual system

Adjust the CSS variables at the top of the stylesheet to change the background, accent, borders, and text colors.

Keep the accent color concentrated around the selected billing option and highlighted plan. Using the same bright color everywhere makes it harder to identify the main action.

For a related iOS product, VP0 can help establish a consistent visual direction across app screens. Treat those designs as native app references rather than assuming they are drop-in HTML pricing templates.

### Add accurate commercial terms

Explain whether taxes are included, whether charges are per seat, and whether a minimum commitment applies.

Do not promise cancellation terms or support response times that your business cannot deliver.

If customers need a sales conversation before purchasing, change the appropriate button to “Contact sales” and connect it to a real contact flow.

## How do you adapt this example to React?

Convert the repeated cards into a data array and store the selected billing period in component state. Let React render the amounts and labels from that state.

The HTML example deliberately uses direct DOM updates because it runs without a build system. Inside a React application, avoid mixing those updates with React-managed markup.

A compact plan structure could look like this:

```jsx
const plans = [
  {
    id: "starter",
    name: "Starter",
    monthly: 12,
    annual: 120,
    features: [
      "One workspace",
      "Three active projects",
      "Email support"
    ]
  },
  {
    id: "growth",
    name: "Growth",
    monthly: 29,
    annual: 290,
    features: [
      "Five workspaces",
      "Twenty active projects",
      "Shared project access"
    ]
  }
];
```

Use stable plan IDs as React keys. Keep the currency formatting separate from the data, and calculate the displayed monthly equivalent only when annual billing is selected.

Do not migrate to React simply to display three cards. The standalone version is suitable for a simple static page. React becomes useful when the pricing component needs to share state with authentication, account management, or other application features.

If your project also includes native screens, VP0 supplies iOS design starters. Web CSS still requires a separate implementation.

## How do you connect plan selection to real payments?

Connect the selected plan and billing period to a server-controlled checkout flow. The browser should describe the choice, while the server determines which actual price is permitted.

A practical implementation follows this sequence:

1. The visitor chooses a plan and billing period.
2. The browser sends those identifiers to your server.
3. The server validates them against an approved mapping.
4. The server creates a Checkout Session.
5. The browser redirects to the returned checkout destination.

Keep secret credentials on the server. Do not embed them in HTML or client-side JavaScript.

The important validation is the relationship between the requested plan and the price your business has configured. A customer should not be able to change a browser value and purchase an unintended price.

After payment, confirm subscription status through verified server-side events. A success screen alone should not grant paid access.

The free interface also does not imply free payment processing. Design code, payment services, and hosting are separate parts of the project.

## What should you test before publishing?

Test the page as a purchasing decision, not just as a screenshot. Every label, amount, and interaction should remain understandable across devices.

Start with keyboard navigation. Move through the billing controls and plan buttons using Tab, then activate them with the keyboard. Make sure the focus outline remains visible.

Check both billing options on every card. The displayed equivalent, annual total, selected state, and checkout request should agree.

Inspect the page on a narrow phone screen and with browser zoom increased. Long plan names and translated text should wrap without pushing content outside the card.

Test your real payment flow in its test environment before accepting live payments. Include failed payments, interrupted checkout, repeated clicks, and customers returning to the pricing page.

Also verify the content against your actual product. A beautiful page with the wrong allowance or cancellation wording still creates a poor customer experience.

## What common mistakes make pricing pages confusing?

The most common mistakes involve unclear billing, unsupported claims, and incomplete purchase behavior.

### Annual prices without annual charges

Showing a small monthly equivalent while hiding the full annual payment creates avoidable confusion.

Place the annual charge directly beneath the headline amount.

### Different numbers at checkout

The page and checkout should describe the same product, billing period, currency, and price.

If taxes or usage charges change the amount, explain that before the customer proceeds.

### Decorative controls that do nothing

A billing toggle should update all affected cards. A plan button should start a real flow or clearly identify itself as a demonstration.

### Unsupported badges

Use “Most popular” only when you have a defensible basis for the claim. Otherwise, describe who the plan suits.

### Too much motion

Animations should support interaction without delaying it. A pricing page does not need floating cards or continuous background movement to feel polished.

## When is this free example not enough?

This example is suitable for a straightforward fixed-price offer. More complex billing models need additional interface work and server logic.

Seat-based pricing requires quantity controls and explicit per-seat wording. Usage-based billing needs allowances, overage rules, and estimates. Existing subscribers may need upgrade, downgrade, and renewal explanations.

A single HTML file cannot handle those commercial rules by itself.

VP0 also has a specific role: it provides iOS app design starters. It does not supply the payment backend or turn this web demonstration into a complete subscription business.

Use the example as a clear foundation, then add the logic your actual offer requires.

## Key takeaways

A good Stripe style pricing page helps visitors understand the offer before they commit. Clear amounts, readable cards, and accurate billing explanations matter more than elaborate effects.

Start with the dependency-free example, replace every fictional detail, and verify the monthly and annual views. Keep payment decisions on the server and test the complete checkout journey before publishing.

Choose the simplest layout that explains your business model. Three plans are useful when they represent meaningful differences; one clear offer is better when customers have only one package to buy.

## Frequently asked questions

### Where can I get Stripe style pricing page code free?

You can use the original HTML, CSS, and JavaScript example above without installing a component library. It includes three plan cards and billing controls, but you must replace the demonstration content and connect a real purchase flow.

### Is this an official Stripe pricing template?

No. It is an original pricing page inspired by common SaaS layout patterns. It contains no official Stripe assets or proprietary source code.

### Can I use the example without React or Tailwind?

Yes. The complete example runs as a standalone HTML file with embedded CSS and JavaScript. It does not require React, Tailwind, or a package installation.

### Does the pricing page collect payments?

No. Its buttons display a selection message. Payment collection requires a separate checkout integration and server-side handling.

### What is VP0 useful for in a project like this?

VP0 is a useful free starting point for the iOS app design portion of a wider product. Its native design starters can guide app screens, while the web pricing page needs its own HTML or framework implementation.

### Should annual pricing show a monthly amount?

It can show a monthly equivalent, provided the page clearly states the full annual charge and billing frequency beside it. Customers should understand what will actually be charged before proceeding.
