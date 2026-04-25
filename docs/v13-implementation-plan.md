# v13 Implementation Plan — Narrative + Interaction Rewrite

**Source:** `prototype purpose next steps.md` (workshop with Steve, Apr 24)
**Active version becoming archive:** `HITL-Task-Prototype-v12.html`
**New active version:** `HITL-Task-Prototype-v13.html`
**Audience:** Claude Code executing in this repo

---

## 1. Objective

Reconfigure the prototype so the same conversational copilot UI delivers two **clearly different AI capability levels** without any UI divergence:

- **Jordan = Assist behavior.** AI orchestrates a *handoff* and walks the human agent through *understand → evaluate → decide → act*. AI never assumes the decision.
- **Rachel = Operator behavior.** AI has already *prepared* the resolution. The human only confirms or adjusts.

The current prototype shows the right *mechanics* but the copilot panel restates information across opening, context, and recommendation, and Jordan's chip set doesn't progress — it just exposes parallel facets. v13 fixes both.

### The system shift

Replace the current model:

```
Summary → Context → Recommendation   (three views of the same info)
```

With:

```
Handoff → Signal → Decision frame → Interaction
```

Every section must introduce *new* information and move the agent forward. If the agent can already see it elsewhere on screen (profile, timeline, order list), it does not belong in the copilot.

### Out of scope

Anything not covered by the workshop notes. Specifically, do **not**:
- Touch layout, width modes, design tokens, or panel chrome
- Add new CSS components or restructure timeline rendering beyond the one removal called out below
- Change the action card component, the feedback row, or the inbox card structure
- Touch the SMS draft, the recovery product list, or any beat downstream of `useDraft` for Jordan (those land fine today)
- Touch Rachel's `approveCard`, `approveConfirm`, `raise`, `lower`, `addStep`, `handoff`, `revert`, or `updateRecCard` logic — only the surface copy/framing
- Alter the `decisions` model or scenario data shape

---

## 2. Versioning steps (do these first)

Per `CLAUDE.md` "When asked to start a new major version":

1. From repo root: `git pull`.
2. `cp HITL-Task-Prototype-v12.html HITL-Task-Prototype-v13.html`
3. `git mv HITL-Task-Prototype-v12.html archive/`
4. Update `vercel.json` `destination` from `/HITL-Task-Prototype-v12.html` → `/HITL-Task-Prototype-v13.html`.
5. In `CLAUDE.md`, replace every `v12` with `v13` (active file, "When asked to extend" header, archive instruction example).
6. In `README.md`, replace every `v12` with `v13` (active file callouts, deploy instructions, anywhere the canonical file is named).
7. Work on a feature branch (`steve/v13-narrative-rewrite`), not `main`.
8. After all edits below land, push and open a PR.

All file:line references in this document are against **v12 as it exists today** — those are the lines you'll be editing in the freshly-copied v13 file.

---

## 3. Global removals

### 3.1 Delete the timeline AI summary event

The workshop calls this out explicitly: the `aisummary` block in Jordan's timeline restates context the copilot will already cover. It also competes visually with the copilot for the "AI is orchestrating this" moment.

**Two edits:**

**(a) Remove the event from Jordan's timeline data.** v12 line 976:

```js
{ kind: 'aisummary' }
```

Delete this line entirely (and clean up the trailing comma on line 975 as needed so the events array stays valid).

**(b) Remove the renderer.** v12 lines 1408–1428 (the entire `if (e.kind === 'aisummary') { … }` block inside `renderEvent`). Delete the whole block.

**(c) Optional cleanup, only if trivial:** the unused `.ai-summary-wrap`, `.ai-summary-event`, `.ai-summary-bub`, `.asb-*` CSS rules around line 628. Safe to delete; not required for behavior. If anything is shared, leave it.

After this change, Jordan's timeline ends at the `jmsg` "Hang tight" routing message at line 974 and the copilot opening message becomes the *only* AI-orchestration moment on screen.

---

## 4. Jordan flow — Assist rewrite

### 4.1 Copilot opening (Handoff)

**Replace** v12 line 979 `opening` value (currently a 4-clause storytelling sentence that duplicates the customer message and the factsProse):

```js
opening: `Jordan was just escalated to you.

He requested a return on the Clifton 9s — initially declined by policy, then pushed back with additional context.`,
```

**Why:** the current opening narrates the *whole* situation up front, which (a) repeats the customer's own messages a few inches to the left in the timeline and (b) leaves nothing for the chips to discover. The new opening states the situation in two sentences and stops, so the chip-driven flow has somewhere to go.

> Note on the leading wave/`Hey Joseph` greeting: drop it. The opening is now a system-stated handoff, not a colleague greeting.

### 4.2 Signal (replaces `factsProse`)

**Replace** v12 lines 980–987 `factsProse` with a tight, decision-driving list. Strip everything that mirrors the profile pane (LTV, order count, tier — all already visible) and anything that's coaching tone (which moves to the `recommend` beat below):

```js
factsProse: [
  "Bought on our recommendation for the Austin Marathon",
  "Tore his ACL — race no longer happening",
  "Shoes are unworn",
  "First return request in 7 orders"
],
```

**Rules for this list (use as a guardrail if tempted to expand it):**
- Every bullet must be a fact that *changes the call*. If removing it doesn't change the decision, remove it.
- No LTV, no tier name, no historical stats unless directly load-bearing.
- No coaching ("Lead with acknowledgment…") — that lives in a chip response now.
- No citations in this list. Inline `<span class='cite'>` markers move to the `recommend` beat where the policy framing lives.

### 4.3 Decision frame (replaces `rec`)

**Replace** v12 lines 988–992 `rec` block. The current version says "Approve the return — full refund + prepaid label" with execution detail underneath, which makes the AI sound like it's deciding for the agent. The workshop's reframe: AI *frames the type of decision*, doesn't make it.

```js
rec: {
  title: '<span id="rec-title-inner">Decision</span>',
  line1: 'Outside standard policy — within your discretion.',
  line2: 'Clean one-time exception with clear context.'
},
```

Keep the inner `<span id="rec-title-inner">` wrapper — `updateRecCard()` and friends still target it.

### 4.4 Ask (closing prompt)

**Replace** v12 line 993 `ask` value:

```js
ask: "How do you want to handle this?",
```

**Why:** the current ask ("I'd approve this — here's a draft when you're ready.") pre-decides and pre-loads execution. The new ask hands the wheel to the human, which is the entire premise of Assist.

### 4.5 Initial chips — staged progression

**Replace** v12 lines 994–998 chips array with the Stage 1 (Understand) set:

```js
chips: [
  { text: "Show me the conversation", kind: 'primary',   action: 'showConversation' },
  { text: "How is he feeling?",       kind: 'secondary', action: 'sentiment' }
],
```

The chips must now follow a **deliberate three-stage progression**:

| Stage | Purpose | Chips visible |
|---|---|---|
| 1. Understand | Read the situation | `Show me the conversation`, `How is he feeling?` |
| 2. Evaluate | Frame the choice | `What are my options?`, `What would you do?` |
| 3. Act | Execute | `Draft a response` |

This is what makes the flow *feel* like a journey instead of a fact-buffet. Each beat's `nextChips` advances or surfaces the next stage; nothing skips backward unless explicitly relevant.

### 4.6 Script states — full replacement of the `script` object

**Replace** v12 lines 1004–1080 `script` object with the version below. We're deleting `whyRec`, restructuring `sentiment` to be progression-aware, adding new `showConversation`, `options`, and `recommend` beats, keeping `draft`/`warmer`/`useDraft` (with content tweaks), and leaving everything from `recommend` onward (the recovery product flow) **untouched** in shape — only the leading beats change.

> Important: there's a naming collision with existing `recommend`. The current beat at line 1043 named `recommend` is the **product recommendation** beat (recovery products list). The workshop's new `recommend` beat is the **AI advisory** beat that follows `options`. Resolve by renaming the existing product-recommendation beat to `recoverProducts` (and updating the action references — see §4.9).

```js
script: {
  // ── Stage 1: Understand ───────────────────────────────────────
  showConversation: {
    reply: "He bought the Clifton 9 after we recommended it for the Austin Marathon.<br><br>After our system declined the return on policy, he came back with the full picture — torn ACL, race off, shoes never worn — and asked for an exception.",
    nextChips: [
      { text: "How is he feeling?",   kind: 'secondary', action: 'sentiment' },
      { text: "What are my options?", kind: 'primary',   action: 'options' }
    ]
  },
  sentiment: {
    reply: "<strong>Frustrated and disappointed.</strong> Sentiment score <strong>-0.62</strong>, down from neutral at the start.<br><br>This isn't about the shoes — it's about losing something he trained a year for.",
    nextChips: [
      { text: "What are my options?", kind: 'primary',   action: 'options' }
    ]
  },

  // ── Stage 2: Evaluate ─────────────────────────────────────────
  options: {
    reply: "You have two paths:<br><br>• <strong>Enforce policy</strong> — decline the return.<br>• <strong>One-time exception</strong> — approve and refund.<br><br>Given the context, this falls within your discretion<span class='cite' onclick='togglePop(event, 1)'>1</span><span class='cite' onclick='togglePop(event, 3)'>3</span>.",
    nextChips: [
      { text: "What would you do?", kind: 'primary', action: 'recommend' }
    ]
  },
  recommend: {
    reply: "I'd approve the exception.<br><br>We influenced the original purchase, the shoes are unworn, and this is a clean one-time situation. Lead with acknowledgment before the logistics.",
    nextChips: [
      { text: "Draft a response", kind: 'primary', action: 'draft' }
    ]
  },

  // ── Stage 3: Act ──────────────────────────────────────────────
  draft: {
    preface: "Based on approving the exception:",
    draftCard: { label: 'Draft', body: `Hi Jordan — really appreciate you sharing the context, and I'm sorry to hear about the ACL.

I've approved the return on the Clifton 9s. You'll see a full refund of $189.99 to your original payment method in 5–7 business days, and a prepaid UPS return label will land in your email shortly.

Let me know if there's anything else I can help with.` },
    nextChips: [
      { text: "Make it warmer", kind: 'secondary', action: 'warmer' }
    ]
  },
  warmer: {
    preface: "Warmer tone:",
    draftCard: { label: 'Draft · warmer tone', body: `Hi Jordan — really sorry about the ACL. After all the time you put into training, that's incredibly tough.

I've approved the return on your Clifton 9s. You'll see a full refund of $189.99 to your original payment method in 5–7 business days, and a prepaid return label will hit your email shortly.

Wishing you a smooth recovery — when you're ready to lace up again, we'll be here.` },
    nextChips: []
  },

  // ── Post-send (reframed; relationship, not upsell) ────────────
  useDraft: {
    reply: "Sent.<br><br>You handled that well. This might be a good moment to stay connected while he's recovering.",
    sideEffect: 'sendOutboundChat',
    nextChips: [
      { text: "Suggest recovery products", kind: 'primary',   action: 'recoverProducts' },
      { text: "Not now",                   kind: 'secondary', action: 'skipRec' }
    ]
  },

  // ── Downstream (RENAME ONLY — content + structure unchanged) ──
  recoverProducts: { /* paste current `recommend` beat body verbatim */ },
  draftRecSMS:     { /* unchanged */ },
  sendRecSMS:      { /* unchanged */ },
  skipRec:         { /* unchanged */ }
}
```

For the four downstream beats (`recoverProducts`, `draftRecSMS`, `sendRecSMS`, `skipRec`), copy the existing bodies verbatim from v12 lines 1043–1079 with **one change**: the action that triggers `recoverProducts` is now `'recoverProducts'`, so update the `useDraft.nextChips` entry above (already shown) and confirm no other reference to `action: 'recommend'` survives. Search the file for `'recommend'` to make sure nothing downstream still points at the old name.

### 4.7 Citations array

Leave v12 lines 999–1003 `citations` as-is. The new `options` beat references `togglePop(event, 1)` and `togglePop(event, 3)` which are still valid against this array. The `factsProse` no longer has inline cite markers, but the data they referenced now appears via the `options` beat — same citations, repositioned.

### 4.8 Outbound bodies

Update v12 lines 1082–1085 `outboundBodies` to match the new draft copy (or rather, the new `warmer` body, since that's the one Joseph will Use on stage). The procedural `draft` body should also match for fidelity if someone Uses it without warming first:

```js
outboundBodies: {
  draft:  `Hi Jordan — really appreciate you sharing the context, and I'm sorry to hear about the ACL. I've approved the return on the Clifton 9s. You'll see a full refund of $189.99 to your original payment method in 5–7 business days, and a prepaid UPS return label will land in your email shortly. Let me know if there's anything else I can help with.`,
  warmer: `Hi Jordan — really sorry about the ACL. After all the time you put into training, that's incredibly tough. I've approved the return on your Clifton 9s. You'll see a full refund of $189.99 to your original payment method in 5–7 business days, and a prepaid return label will hit your email shortly. Wishing you a smooth recovery — when you're ready to lace up again, we'll be here.`
},
```

### 4.9 Draft preface (UI tweak)

The workshop calls for a small label *above* the draft body that frames it as following from a chosen path: "Based on approving the exception:". This makes it visceral that the AI is *executing the human's decision*, not deciding.

Two changes:

**(a) Add a `preface` field on draft beats.** Already shown in the script object above — `draft` and `warmer` each carry `preface`.

**(b) Wire `preface` through `pushAIMsg`.** v12 line 1867. Add support for `opts.preface` so the draft message renders the label above the draft body. Minimal change inside the function:

```js
function pushAIMsg(text, extraOrOpts) {
  let opts = {};
  if (typeof extraOrOpts === 'string') opts.extra = extraOrOpts;
  else if (extraOrOpts) opts = extraOrOpts;

  const box = document.getElementById('chat-msgs');
  const el = document.createElement('div');
  el.className = 'cm ai';
  const cbClass = opts.draft ? 'cb draft' : 'cb';
  const preface = opts.preface ? `<div class="cb-preface">${opts.preface}</div>` : '';
  const body = text ? `<div class="${cbClass}">${text}</div>` : '';
  const extra = opts.extra || '';
  const actions = (opts.noActions) ? '' : renderMessageActions(!!opts.draft, opts.useAction || 'useDraft');
  el.innerHTML = preface + body + extra + actions;
  box.appendChild(el);
  scrollRP();
  return el;
}
```

Add a small CSS rule alongside existing `.cb` styles (use the existing eyebrow/secondary-text token; do not introduce new colors):

```css
.cb-preface { font-size: 11px; color: #767676; margin-bottom: 6px; letter-spacing: 0.02em; }
```

In `runScript` (the function that consumes the script object and calls `pushAIMsg`), pass `preface: beat.preface` through the options object whenever the beat has one. Look for the call site that pushes draft messages and add this single field.

### 4.10 Inbox card label (do not change)

Keep Jordan's inbox tag as-is (the current `Chat` tag at v12 line 1282). The workshop discussed but rejected adding mode-indicator chrome ("ASSIST MODE"/"READY FOR APPROVAL") because the prototype's premise is that the *same* UI carries different capabilities — visual mode-tags would undermine that. No change here.

---

## 5. Rachel flow — Operator polish

Most of Rachel's structural work landed in v12: the action card already renders inline at copilot-load (v12 lines 1479–1488), the four control chips (raise/lower/addStep/handoff) are already in place, `ask` is already empty. v13's job is to tighten the surface copy so the *operator* read is unmistakable.

### 5.1 Opening

**Replace** v12 line 1151 `opening` value:

```js
opening: `Rachel's cancellation is ready.

Order is still in processing — eligible for a full refund.`,
```

Drops the colleague greeting and the "Just need your call on the thank-you credit" trailing aside. The plan card below speaks for itself.

### 5.2 Signal (replaces `factsProse`)

**Replace** v12 lines 1152–1158 `factsProse`. Strip everything except what determines eligibility and frames the thank-you credit:

```js
factsProse: [
  "Order value: $847.99 — still in processing (no fees)",
  "Trailblazer customer, 12 orders, 0 cancellations",
  "Full refund before ship is covered for Trailblazer<span class='cite' onclick='togglePop(event, 1)'>1</span>",
  "$25 default thank-you credit for $500–$1K orders<span class='cite' onclick='togglePop(event, 2)'>2</span>"
],
```

Keep the two inline citations — they're load-bearing for the policy/credit framing the action card depends on.

### 5.3 Recommendation (no behavior change, sharper line)

**Replace** v12 lines 1159–1163 `rec` (very small change — keep `<span id="rec-title-inner">` wrapper because `updateRecCard()` targets it):

```js
rec: {
  title: '<span id="rec-title-inner">Cancel + $25 thank-you credit</span>',
  line1: 'Refund $847.99 to her original payment method',
  line2: 'Thank-you credit on her account for when she\'s back'
},
```

### 5.4 Operator framing line

**Replace** v12 line 1164 `ask: ""` with the workshop's operator framing line:

```js
ask: "Everything is prepared — you can approve as-is or adjust below.",
```

This restores the `ao-ask` element as the connective line between "what I prepared" and the action card. `renderCopilot` already shows/hides `ao-ask` based on whether `c.ask` is truthy (v12 line 1471–1472), so just supplying the string is enough.

### 5.5 Chips (already correct shape — small label tweak)

Keep v12 lines 1169–1174 chips structure. Optional small label tightening for stage delivery — change `"Bump credit to $50"` to `"Increase credit to $50"` if you want the verb to land cleaner; otherwise leave. No action/arg/handler changes.

### 5.6 Approval output (`copilotReply`)

**Replace** v12 line 1205 `copilotReply` value with the sharper, executive version:

```js
copilotReply: `Done.

Order cancelled, $847.99 refund issued, $${s.creditAmount} credit applied.`,
```

### 5.7 Customer message (`customerReply`)

**Replace** v12 line 1207 `customerReply` value with the tighter version:

```js
customerReply: `Your cancellation is approved, Rachel. A full refund of $847.99 is on its way to your original payment method, and I've added a $${s.creditAmount} thank-you credit to your account.

Wishing you a smooth recovery — we'll be here when you're ready.`,
```

### 5.8 `raise` / `lower` reply lines (small consistency tweak)

v12 lines 1212 and 1217 — Rachel's `raise` and `lower` handlers each emit a `copilotReply` like `"Bumped it to a $X credit. Still within discretion. Go?"`. Tighten to operator framing so the "AI did the work, you're modifying levers" feel stays consistent:

```js
raise: (s, amt) => ({
  copilotReply: `Updated — $${amt} credit applied. Still within policy. Ready when you are.`,
  reAsk: true,
  mutate: { credit: amt }
}),
lower: (s, amt) => ({
  copilotReply: `Updated — $${amt} credit applied. Within policy, slightly more conservative. Ready when you are.`,
  reAsk: true,
  mutate: { credit: amt }
}),
```

No change to the function signatures, `reAsk`, or `mutate` semantics.

---

## 6. Behavioral contrast (validation matrix)

Use this to sanity-check a finished v13 against the workshop's intent. Each column should be true after implementation.

| Dimension | Jordan (Assist) | Rachel (Operator) |
|---|---|---|
| Opening tells you… | What just happened | What's already prepared |
| First chip is… | A discovery question | (No discovery — action card is the surface) |
| AI's stance on the decision | Frames it, doesn't make it | Has already made it |
| Human's job | Decide, then send | Confirm, optionally adjust |
| Number of clicks to act (typical demo) | 4–5 (understand → evaluate → recommend → draft → use) | 1 (Approve & run) |
| Draft is… | Execution support after a chosen path | Not used — action card is the resolution |

---

## 7. QA checklist

### Jordan
- [ ] Timeline ends at the routing message; no AI summary card appears
- [ ] Copilot opening is exactly two sentences and contains no factsProse content
- [ ] `factsProse` has exactly four bullets; none mirror profile pane data
- [ ] `rec.title` reads "Decision" (not "Approve the return…")
- [ ] `ask` reads "How do you want to handle this?"
- [ ] Initial chips: `Show me the conversation`, `How is he feeling?` (no `Draft response` chip on first render)
- [ ] Clicking `Show me the conversation` reveals chips for sentiment + options
- [ ] Clicking `How is he feeling?` (either path) advances toward `What are my options?`
- [ ] `What are my options?` reply ends with `What would you do?` chip
- [ ] `What would you do?` reply ends with `Draft a response` chip
- [ ] Draft message renders with a small "Based on approving the exception:" label above the body
- [ ] `Make it warmer` produces a warmer draft with the same preface treatment
- [ ] `Use` posts the warmer body to the customer timeline (existing behavior)
- [ ] After `Use`, the post-send line reads "Sent. You handled that well…"
- [ ] Recovery products list still appears via `Suggest recovery products` (renamed action `recoverProducts`)
- [ ] No JS console errors; search the file for the string `'recommend'` and confirm zero stale references

### Rachel
- [ ] Action card is visible immediately on Rachel-load (v12 behavior preserved)
- [ ] Opening reads "Rachel's cancellation is ready. / Order is still in processing — eligible for a full refund."
- [ ] `factsProse` is four bullets; the last two carry citations 1 and 2
- [ ] `ask` line "Everything is prepared — you can approve as-is or adjust below." renders below the rec card and above the action card
- [ ] All four control chips present and functional (raise / lower / addStep / handoff)
- [ ] `Bump credit to $50` (or `Increase credit to $50` if relabeled) updates the rec card and emits "Updated — $50 credit applied…" line
- [ ] `Approve & run` on the action card produces the new "Done. Order cancelled, $847.99 refund issued, $X credit applied." copilot reply
- [ ] Customer-facing reply matches the new compressed version
- [ ] Right-aligned `tl-activity` events still post to the timeline (existing behavior unchanged)

### Cross-cutting
- [ ] `vercel.json` redirects `/` → `/HITL-Task-Prototype-v13.html`
- [ ] `CLAUDE.md` and `README.md` reference v13 as the active file; v12 is in `archive/`
- [ ] Manual deploy after push: `vercel --prod --yes` (Vercel git integration is not auto-firing — see PROJECT-MEMORY §1)
- [ ] Verify live URL serves v13 with a browser UA: `curl -sA "Mozilla/5.0" https://gcl-hitl-prototypes.vercel.app/HITL-Task-Prototype-v13.html | head`

---

## 8. Litmus test (workshop's bar)

When someone watches the v13 demo, they should *feel*:

- **Jordan:** "I'd be a better agent with this." The AI didn't decide for me; it walked me through the call.
- **Rachel:** "Why would I ever do this manually again?" The AI already did the work; I just confirmed.

If both lines are true, v13 lands. If either reads as "AI is helping me with returns" generically, the rewrite hasn't bitten hard enough — most likely culprit is the copilot opening or the chip progression on Jordan.

---

## 9. Reference index — exact v12 line numbers being touched

| Edit | v12 file:line | What |
|---|---|---|
| Delete timeline event | 976 | `{ kind: 'aisummary' }` |
| Delete renderer | 1408–1428 | `if (e.kind === 'aisummary')` block |
| Jordan opening | 979 | `opening` value |
| Jordan signal | 980–987 | `factsProse` array |
| Jordan decision frame | 988–992 | `rec` object |
| Jordan ask | 993 | `ask` value |
| Jordan chips | 994–998 | initial `chips` array |
| Jordan script object | 1004–1080 | full replacement (new beats + rename `recommend` → `recoverProducts`) |
| Jordan outbound bodies | 1082–1085 | `outboundBodies.draft` and `outboundBodies.warmer` |
| `pushAIMsg` preface support | 1867–1884 | add `opts.preface` handling |
| `runScript` draft call site | 1663–1675 (function body), specifically line 1675 `pushAIMsg(body, { draft: true, useAction: ... })` | add `preface: beat.preface` to the opts object |
| Rachel opening | 1151 | `opening` value |
| Rachel signal | 1152–1158 | `factsProse` array |
| Rachel rec | 1159–1163 | `rec` object (small wording tweak; keep span wrapper) |
| Rachel ask | 1164 | populate with operator framing line |
| Rachel chips (optional label tweak) | 1169–1174 | `Bump → Increase` if desired |
| Rachel approval | 1205 | `copilotReply` value |
| Rachel customer message | 1207 | `customerReply` value |
| Rachel raise/lower replies | 1212, 1217 | tighter operator wording |

Source workshop: `prototype purpose next steps.md` (root of repo).
