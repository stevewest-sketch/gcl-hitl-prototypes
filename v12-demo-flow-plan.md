# Plan: v12 — Demo Flow Story & Action Redesign

## Context
Based on April 24 GCL demo feedback (gcl-demo-feedback.md). Create a new `HITL-Task-Prototype-v12.html` copied from v11. Three targeted changes to demo flow and story elements only.

**File to create:** `/Users/steve.westgladly.com/projects/gcl-hitl-prototypes/HITL-Task-Prototype-v12.html`
**Source:** copy of v11 with the changes below applied

---

## Change 1 — Jordan: Remove "Process the Return" entirely

**Feedback:** Actions belong to the HITL story (Rachel). Remove them from the Team Assist story (Jordan) to keep the two acts distinct.

### Remove from `JORDAN.copilot.script`:
- `processReturn` beat
- `approveRun` beat
- `processReturn` from `JORDAN_CHIP_DEFS`
- `{ text: "Process the return", ... }` from `draft.nextChips`
- `{ text: "Process the return", ... }` from `warmer.nextChips`

### Update `useDraft` beat:
```js
useDraft: {
  reply: "Sent. Want to get ahead of his recovery while you have him?",
  sideEffect: 'sendOutboundChat',
  nextChips: [
    { text: "Suggest recovery products", kind: 'primary',   action: 'recommend' },
    { text: "Not now",                   kind: 'secondary', action: 'skipRec' }
  ]
}
```

Jordan's flow now ends: approve → send draft → optionally suggest recovery products → done.

---

## Change 2 — Rachel: Action card surfaces upfront in the opening panel

**Feedback:** Show the full plan upfront ("plan mode"). The agent should see the action card immediately when Rachel loads — not behind a chip click. The action card design/experience is preserved exactly as-is (editable steps, Add a step, Approve & run).

### Current flow:
1. Opening panel: context + rec + "Yes, go ahead" chip
2. Click chip → action card appears in TA chat
3. Click "Approve & run" → execution

### New flow (v12):
1. Opening panel: context + rec + **action card shown inline** (no chip needed)
2. Agent edits steps inline if desired (increase credit, add SMS step, custom step)
3. Click **"Approve & run"** directly on the card → execution
4. Chip tray changes to just: `"No, I'll handle it"` (handoff) — since the card has its own approve button

### Implementation:

**Move action card render into `renderCopilot`** for Rachel:

In `renderCopilot()`, after rendering factsProse/rec/ask for Rachel, call:
```js
if (s.id === 'rachel') {
  const planEl = document.getElementById('rp-plan');
  if (planEl) {
    const card = s.decisions.approveCard(session);
    session.rachelActionCard = card.actionCard;
    planEl.innerHTML = renderActionCard(card.actionCard);
    planEl.style.display = '';
  }
}
```

**New HTML element** in `ai-open` section (after `rec-card`, before `ao-ask`):
```html
<div id="rp-plan" style="display:none"></div>
```

**Update Rachel chips** in `RACHEL.copilot.chips`:
```js
chips: [
  { text: "No, I'll handle it", kind: 'secondary', action: 'handoff' }
]
```

**Remove the `approveCard` branch from `runDecision`** (no longer triggered by a chip — the card is already showing). Keep `approveConfirm` as-is (still triggered by the card's Approve & run button).

**Rachel opening text** — tighten to match the proactive feel:
```
"👋 Hey Joseph — Rachel's cancellation is ready to run. Just need your call on the thank-you credit."
```

**`ask` field** — remove (set to `""`) since the action card below speaks for itself.

### Editing experience (already built, just now visible upfront):
- **Increase credit**: Agent clicks the credit step text → editable inline (existing `ac-step-text` edit behavior) OR uses the chip "Bump to $50" if we surface that. Simpler: keep existing step-preset menu via "Add a step" and let the existing editable step rows handle inline edits.
- **Add "Send SMS" step**: Click "+ Add a step" → preset menu shows "Send SMS recap" → click to add → step appears in the list.
- **Approve & run**: Triggers `approveConfirm` — same execution logic as today (cancel order, issue refund, apply credit, post timeline events, send customer reply).

### Note on `updateRecCard`:
The `updateRecCard()` function currently updates `rec-line2` when credit changes via raise/lower chips. With the inline plan card showing, also re-render `rp-plan` content when credit is modified via chips (if we keep raise/lower chips). For v12, simplest approach: keep the existing raise/lower chip flow for Rachel removed (she won't have those chips now), and rely on inline step editing in the card.

---

## Change 3 — Proactive info: sharper openings

### Jordan `ask` field:
- Current: `"Want me to draft the response?"`
- New: `"I'd approve this — here's a draft when you're ready."`

### Rachel `opening` (already updated above in Change 2).

### Rachel `ask` field: set to `""` (plan card replaces the ask).

---

## Files changed
- New file: `HITL-Task-Prototype-v12.html` (copied from v11, changes applied)
- `vercel.json` — update redirect to point to v12

## Key locations in v11 to change for v12:

| What | Location |
|------|----------|
| Jordan script beats | `JORDAN.copilot.script` (~line 1001) |
| JORDAN_CHIP_DEFS | (~line 1733) |
| Rachel chips/opening/ask | `RACHEL.copilot` (~line 1205) |
| renderCopilot() | (~line 1501) — add Rachel plan card render |
| runDecision() | (~line 1579) — remove approveCard chip branch |
| ai-open HTML | (~line 858) — add `<div id="rp-plan">` |
| vercel.json | root redirect |

## Verification
1. **Jordan**: No "Process the return" chip ever appears at any step. After Use on draft → "Suggest recovery products" / "Not now" chips only.
2. **Rachel**: Panel loads with action card already visible (3 steps: cancel, refund, credit). Click "+ Add a step" → select "Send SMS recap" → step 4 appears. Click step 3 text to edit credit amount. Click "Approve & run" → execution completes, timeline updates, customer reply appears.
3. **Jordan ask**: reads "I'd approve this — here's a draft when you're ready."
4. **Rachel**: No "Yes, go ahead" chip. Only "No, I'll handle it". Plan card is the primary CTA.
