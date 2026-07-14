# Conduit — About Page Changes for the Ad Campaign

From Jason @ The Salt Lick Denver. This is the change list for `conduitforcontractors.com/about` so it lines up with the three video ads. Item numbers match the numbered notes in the annotated markup copy of the page (`conduit-about-page-markup.html`).

## Context for whoever (or whatever) is making these changes

- Three video ads will drive paid Meta traffic to this page. All three sell the same core argument: **it shouldn't cost you $300 to collect a $10,000 payment** — low payment-collection costs, team-size pricing instead of per-seat pricing, easy migration, built by contractors.
- The page has **one goal: free-trial sign-ups** (getting people into the Starter plan). Every button that matters goes to `/sign-up`.
- **Nothing on the page should take the visitor off the page** except the sign-up flow. No external links, no internal detours.
- Most visitors will be **on their phones, coming from Instagram**. The page needs to look great on mobile and be really easy to navigate — short sections, one idea each, nothing that requires mental math.
- The Salt Lick handles the tracking/GTM side (Meta conversion events). The page-side requirements are noted in the relevant items below.

---

## The changes

### 1. Hero headline — CHANGE
Lead with the hook from the scripts: **"It shouldn't cost you $300 to collect a $10,000 payment."**
"The all-in-one platform for contractors" is the category, not the reason they clicked the ad. Leading with payments is right — keep that instinct, use the ad's language.

### 2. "Watch Demos on YouTube" button — REMOVE
Remove any links that take people off the website. Get rid of this button entirely (both in the hero and anywhere else it appears).

### 3. "Book a Free Walkthrough" button — CHANGE
Stop linking out to calendly.com. Instead:
- **Embed the Calendly booking widget at the bottom of the page** (Calendly inline embed, URL: `https://calendly.com/isaac-conduitforcontractors/conduit-intro-session`).
- This button becomes an anchor link that **scrolls the visitor down to the embed**.
- The embed fires an event when a booking completes (`calendly.event_scheduled` via postMessage) — push that to the dataLayer so we can send it to Meta as a conversion. (See item 15.)

### 4. Interactive demos — KEEP
The fully interactive demos are one of the strongest things on the page. Keep them.

### 5. "Payments That Don't Eat Your Profits" section — CHANGE
The demo here should reflect **how the customer sees the invoice**, so the visitor understands the customer gets to choose how to pay. Focus the section on that customer-facing view: two prices (bank transfer / card), the customer picks, and no matter which way they pay, your payment-processing costs are covered — because you can set a different price for credit card than for ACH.

### 6. "See how Conduit lowers card fees →" link — CHANGE
This currently navigates to `/payments`. Lead with the customer-facing demo here instead, and make this an **on-page popup / expandable info box** — it should not move people to another page.

### 7. "Switch in Minutes, Not Weeks" (migration) section — KEEP + MOVE
- Keep the section — it's good, and the ads lean on it.
- **Replace the emoji icons with the actual logos** of the platforms you migrate from (ServiceTitan, Jobber, Housecall Pro, etc.).
- **Move it to sit underneath the Pricing section.**

### 8. Project & Job Management (and the feature sections generally) — CHANGE
Show people **the flow of how one job works** rather than disconnected feature sections: project & job management → the takeoff software → material costs into the bid → team & time tracking → generating the invoice → and some of the customer communication as well. The point: it really is one embedded suite, super easy to use from your phone.

### 9. Takeoff software — ADD
Add a section that **shows off the takeoff software** — that's really cool and worth its own moment. Show the flow: plans loaded in → material costs get added to the invoice → time gets tracked → then generating the invoice.

### 10. "Simple, Transparent Pricing" section — CHANGE
What to highlight here: **this pricing structure is designed not to limit your team's growth.** It shouldn't get more expensive to use the software as your team grows — and on other platforms, it does.

The most compelling thing from a SaaS standpoint: every other SaaS company gates certain features on different tier plans. Here, **the only thing that changes is how many team members you have. That is it — you get every single feature.** Say it that simply.

Remember what this free-trial page is for: just getting people into the Starter plan. Sell confidence in the pricing structure, not a matrix to study.

### 11. "See how we compare" table — CHANGE
- The current list is confusing — it requires a mobile user who was just scrolling Instagram to do a lot of mental math (price ranges, per-user add-ons, footnotes).
- Instead, try: **a dropdown/expander under each Conduit pricing tier** that shows "a team this size would be **$X more per month** on [platform]." One pre-calculated number per platform. Quickly scannable — the takeaway in one glance is that this is the best price per month.
- **Fix the contradiction:** as laid out, ServiceM8 reads as low as $29/mo for a five-person team — lower than Conduit's $65 — while one of our ads says team size shouldn't eat into your FSM budget. Cut that row or reframe it; don't leave a competitor looking cheaper on our own page.

### 12. "Ready to streamline your business?" (closing CTA) — CHANGE
Keep the closing CTA. Same funnel rules as the top of the page: remove the YouTube link, and the walkthrough link scrolls down to the Calendly embed right below it.

### 13. "Meet the Team" section — REMOVE
Not needed on this page. We just want the page to be really clear and funnel people specifically to the free trial.

### 14. "Contractor Resources" section — REMOVE
These links take people off the page. Great for the site and SEO — keep them elsewhere — but on this landing page everything should funnel to the free trial. Footer here should be minimal: terms, privacy, support email.

### 15. Calendly embed — ADD
At the bottom of the page (above the footer): embed the Calendly booking widget inline so booking happens **on the page**. All "Book a Free Walkthrough" buttons scroll here. Push the completed-booking event to the dataLayer so The Salt Lick can send it to Meta:

```js
window.addEventListener('message', function (e) {
  if (e.origin === 'https://calendly.com' &&
      e.data && e.data.event === 'calendly.event_scheduled') {
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({ event: 'walkthrough_scheduled' });
  }
});
```

---

## Suggested section order (after the changes)

1. **Hero** — "It shouldn't cost you $300 to collect a $10,000 payment." One CTA (Get Started Free); walkthrough link scrolls down.
2. **Payments** — customer-facing invoice demo: two prices, the customer picks, your costs are covered either way.
3. **Pricing** — growth never raises your bill; every feature on every plan; per-tier competitor dropdowns.
4. **Migration** — real platform logos; switching takes minutes; your old account stays untouched.
5. **The job flow** — project & job management → takeoff → materials into the bid → time tracking → invoice → customer texts. Existing demos, told as one job, all from your phone.
6. **Closing CTA** — free trial.
7. **Calendly embed** — booking on-page.
8. **Minimal footer** — terms, privacy, support email.
