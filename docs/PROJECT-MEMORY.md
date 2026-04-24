# HITL × Team Assist Prototype — Project Memory

**Last updated:** Apr 22, 2026 (post-v9 streaming drafts + right-align activity events)
**Owner:** Steve West (Director of Revenue Enablement, Gladly)
**Purpose:** Clickable HTML prototype for the **Gladly Connect Live '26 keynote**, demonstrating how AI and human agents collaborate through one shared surface — Team Assist. The prototype shows two flows on the same UI:
1. **Team Assist demo** — agent in the seat, AI helps (Jordan Rivera · return exception)
2. **HITL demo** — AI in the seat, human approves (Rachel Thompson · VIP cancellation)

Both flows use the same chrome, the same copilot panel, and the same feedback primitives. The keynote narrative: *flip the chair, same product.*

---

## 1. Current production state

- **Live URL:** https://gcl-hitl-prototypes.vercel.app (redirects `/` → `/HITL-Task-Prototype-v9.html`)
- **GitHub:** [`stevewest-sketch/gcl-hitl-prototypes`](https://github.com/stevewest-sketch/gcl-hitl-prototypes) (**private**)
- **Latest commit (HEAD):** `15cf123` — *"v9: right-align activity acknowledgements in timeline"*
- **Vercel team:** `gladly-enablement-site` / project `gcl-hitl-prototypes`
- **Deploy Protection:** disabled (public access)
- **Auto-deploy status:** Vercel Git integration is NOT firing from pushes. Each deploy needs `vercel --prod --yes` from `/Users/steve.westgladly.com/projects/gcl-hitl-prototypes/` after git push. Cause not yet diagnosed — flagged as open issue.

### Landing behavior
- **Default customer:** Jordan Rivera (Team Assist demo — richer story, more beats)
- Rachel is selected by clicking her card in the left list

---

## 2. File map

### Working folder: `/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/hitl-prototypes/`

| File | Purpose |
|---|---|
| `HITL-Task-Prototype-v9.html` | **Current prototype** (~2,100 lines, self-contained HTML) |
| `HITL-Task-Prototype-v8.html` | Apr 21 PM polish pass — facts as prose, panel-weighted layout, chronological tl-events, toned-down rec |
| `HITL-Task-Prototype-v7.html` | Apr 21 AM direction — everything-in-the-copilot, removed task card, Assist chips |
| `HITL-Task-Prototype-v6.html` | Apr 17 direction — expanded customer list, Jordan scenario added, panel-not-tabbed |
| `HITL-Task-Prototype-v5.html` | Baseline reviewed Apr 17 — purple Team Assist tabs, task card with Review Decision |
| `HITL-Task-Prototype-v1.html` – `v4.html` | Earlier iterations |
| `HITL-Task-Prototype-v6-CLAUDECODE-PROMPT.md` | Original kickoff prompt for v6 |
| `HITL-Prototype-v7-Walkthrough.md` | Word-for-word walkthrough of v7 for stakeholders |
| `HITL-Tasks-Analysis-Apr2026.md` | Original research foundation (600 lines) — customer feedback, Gong, Slack, SWOT |
| `HITL-Tasks-Analysis-Apr2026.docx` | Same as above in Word |
| `HITL Feedback.md` | Apr 21 feedback rounds (morning + onsite PM) |
| `PROJECT-MEMORY.md` | This document |
| `SCR-*.png`, `image (26-29).png` | Source screenshots (Aceable, Jordan Rivera mockups) |

### Deploy repo: `/Users/steve.westgladly.com/projects/gcl-hitl-prototypes/`

Contains ONLY the HTML files + `vercel.json` + `.gitignore`. No analysis docs, no images.

| File | Purpose |
|---|---|
| `HITL-Task-Prototype-v1.html` – `v9.html` | All versions live on Vercel at their filename path |
| `vercel.json` | Redirects `/` → `/HITL-Task-Prototype-v9.html` (307) |
| `.gitignore` | Ignores `.vercel/` |

### Demo script folder: `/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/demo-drafts/`

| File | Purpose |
|---|---|
| `GCL_Live_Service_Demo_-_v9.docx` | **Source of truth** for scenario copy, products, beats |
| `GCL_Live_Service_Demo_-_v8.docx` | Prior draft (Team Assist only, pre-HITL) |
| `GCL Live Service Demo - v7.docx` | Earlier HITL iteration |

### Related: `/Users/steve.westgladly.com/.claude/plans/for-the-right-panel-memoized-music.md`

Active plan file — gets rewritten each time Steve requests a new planning cycle.

---

## 3. Customers

### Jordan Rivera — Team Assist demo (default on load)

- **Avatar:** JR, olive green `#6B8E6F`
- **Loyalty tier:** Hoka Trailblazer since 2022
- **Lifetime value:** $4,280.00 · 7 orders, all Hoka
- **Contact:** jordan.rivera@gmail.com · (512) 555-0192 · Austin TX 78701 · Mobile · SMS preferred
- **Visible orders:** Clifton 9 Black/White 10.5 ($189.99, Delivered 02/14) · Bondi 7 Black 10.5 ($159.99) · Mach 5 White/Blue 10.5 ($144.99)
- **Preferences:** Trailblazer · Marathon running · Men's 10.5 · Hoka Clifton · Bondi · Mach

**Customer list pip:** gray chat bubble (he's `type: 'chat'`, not Needs-input)
**Layout:** default proportions (260/320/flex/380) — conversation-forward, not panel-weighted
**Status in timeline header:** `Apr 14 · Return request · Assigned to Joseph`

### Rachel Thompson — HITL demo

- **Avatar:** RT, blue `#5B8DEF`
- **VIP tier** since 2022
- **Lifetime value:** $12,400.00 · 12 Hoka orders, 3% return rate, zero prior cancellations
- **Contact:** rachel.thompson@gmail.com · (212) 555-0147 · 148 Park Pl, Brooklyn NY 11217 · Mobile · Chat preferred
- **Active order:** `ORD-2026-84721 · Hoka Race-Day Pro Pack · Processing · $847.99 · Ordered 04/19/2026`
- **Preferences:** Long-distance running · Women's 8.5 · Hoka Bondi · Clifton · Tecton X

**Customer list pip:** purple sparkle (she's `type: 'assist'`, Needs-input)
**Layout:** panel-weighted (220/280/flex/440) when selected
**Status in timeline header:** `Apr 21 · Cancellation request · Waiting`

### Stub customers (not wired, demo toast on click)

| # | Name | Type | Preview | Channel |
|---|------|------|---------|---------|
| 1 | Sarah Kim | Chat | "Hey, where's my order? It's been a week…" | Chat |
| 4 | Priya Shah | Needs-input | "AI wants your call on a VIP exchange ($380 → $420)." | SMS |
| 5 | Marcus Klein | Chat | "Voice callback — follow-up on shipment." | Voice |
| 6 | Kira Fletcher | Chat | "Question on sizing — jackets run true to size?" | Chat |

---

## 4. Jordan's flow — Team Assist scripted beats

Jordan opens with a pre-populated conversation timeline (Feb 8 prior chat + Apr 14 current return exchange + routing event).

### Timeline (initial state)

**Feb 8 — product consultation (closed)**
- Divider: `Feb 8 · 2 months ago · Product consultation`
- Jordan (chat): *"Hey — thinking about the Clifton 9 for the Austin Marathon in April. I've been in Bondi 7s for the last year. Worth the switch for race day?"*
- Gladly AI (chat): *"Great pick for race day. The Clifton 9 is ~30% lighter than the Bondi 7 with the same cushion DNA… Want me to pull it up in your size?"*
- Jordan (chat): *"Yeah — men's 10.5, black/white."*
- Gladly AI (chat): *"Done — order #GCL-55892, shipping to 2721 Maple. Good luck in Austin."*
- Divider: `Conversation closed — Feb 8, 7:45 PM`

**Apr 14 — today's return request**
- Divider: `Apr 14 · Today · Return request`
- Jordan (chat, 9:02 AM): return request
- Gladly AI (chat, 9:03 AM): policy-based auto-rejection
- Jordan (chat, 9:04 AM): escalation with ACL context
- Jordan (chat, 9:05 AM): further context (unworn, not changing his mind)
- Routing event: `Routed from Gladly AI to Joseph Ansanelli — Apr 14, 9:06 AM`

### Copilot panel (initial state)

Opening AI message (not in the streaming log — structural, no feedback icons):
> 👋 Hey Joseph — AI handed this one over after Jordan pushed back. No recommendation from me yet — ask me anything, or start with one of these.

Chip rail:
- `Catch me up on Jordan` (primary)
- `What's his sentiment?`
- `Can I approve this return?`

### Scripted beats (each click = one agent bubble + one AI response)

| # | Agent chip / phrase | AI response | Side effect |
|---|---|---|---|
| 1 | Catch me up on Jordan | Trailblazer tier since 2022, 7 orders all Hoka, $4,280 LTV. Bought Clifton 9s Feb 10 for marathon. Tore ACL, never wore them. Low risk to approve. | — |
| 2 | What's his sentiment? | Frustrated and disappointed. Lead with acknowledgment. | — |
| 3 | Can I approve this return? | Yes, within your discretion. 37 days past window but agents can approve one-off exceptions ⁽¹⁾. Unworn ⁽²⁾. Trailblazer extends flexibility ⁽³⁾. | — |
| 4 | Draft a response | (draft body directly in the message; green **Use** button inline + feedback icons) | — |
| 5 | Make it warmer | (warmer draft body directly; Use + icons) | — |
| 6 | **Use** (inline button on the draft) | "Sent. Want me to process the return next?" | Posts Joseph's outbound chat to timeline; Jordan's thank-you reply lands ~1.5s later |
| 7 | Process the return | Action card with 3 steps + green `Approve & run` button inline | — |
| 8 | **Approve & run** (inside action card) | Card fills with ✅ completion lines | Appends 3 right-aligned `.tl-activity` events (Joseph approved / Refund issued / Label emailed) |
| 9 | Recommend something for his recovery | Inline 3-product list (Ora Recovery Slide, Bondi 8, Clifton Recovery Socks) with price + one-line reason + hoka.com link. "He prefers SMS. Want me to draft a message?" | — |
| 10 | Draft an SMS | (SMS draft body directly in message; green **Use** button → sendRecSMS) | — |
| 11 | **Use** on SMS draft | "Sent via SMS. Nice finish." | Posts outbound SMS bubble to timeline |

### Drafts (word-for-word, chat-style — no greeting, no sign-off)

**Procedural:**
> Thanks for the context — really sorry about the ACL.
>
> Good news: I can approve the return on your Clifton 9s. Full refund to your original payment method in 5–7 business days, and a prepaid return label will land in your email shortly.
>
> Anything else I can sort out for you?

**Warmer:**
> Really sorry about the ACL — a year of training and then having the race taken away is brutal. Hoping surgery goes smoothly and recovery is quick.
>
> Good news on the shoes: you're all set. Full refund on the Clifton 9s to your original payment method in 5–7 business days, and a prepaid return label will hit your email shortly.
>
> When you're ready to lace up again, we'll be here.

### Action card (Process the return)

```
Process the return
1. Issue refund — $189.99 to his original payment method
2. Generate return label — UPS Ground, Austin
3. Email label + tracking — jordan.rivera@gmail.com

[ Approve & run ]    Edit steps
```

### Post-approve activity (right-aligned tl-activity events)

```
Joseph approved the return exception — just now
Gladly AI issued a $189.99 refund to his original payment method — just now
Gladly AI emailed a prepaid UPS return label to Jordan — just now
```

### SMS draft (still uses "Hey Jordan" / "— Joseph" greeting-signoff per SMS convention)

> Hey Jordan — wishing you a smooth recovery. A few Hokas built for the phase you're in:
>
> • Ora Recovery Slide — hoka.com/ora
> • Bondi 8 — hoka.com/bondi8
> • Clifton Recovery Socks — hoka.com/clifton-socks
>
> No rush — they'll be here when you are.

**Open question:** Steve flagged whether to strip the SMS greeting/signoff. Awaiting confirmation.

### Citations (Jordan)

1. **Return Exceptions** — "Agents may approve one-off return exceptions on a case-by-case basis, even outside the standard 30-day window, when there's a clear hardship reason and the product is unworn."
2. **Return Eligibility** — "Unworn product in original condition is eligible for a full refund to the original payment method."
3. **Loyalty Tier Benefits** — "Trailblazer-tier customers (3+ years, consistent spend) receive extended return flexibility at agent discretion."

---

## 5. Rachel's flow — HITL decision path

### Timeline (initial state)

- Rachel (chat, 2 min ago): *"Hi, I need to cancel my order #ORD-2026-84721 — the Hoka Race-Day Pro Pack. I signed up for the Chicago Marathon this year and picked up the bundle for training, but I just tore a tendon at a training run last weekend. 8–12 weeks off, no race for me. Is there any way to get a refund before it ships?"*
- Gladly AI (chat, 1 min ago): *"Hi Rachel — sorry to hear about the tendon. Let me sort this out for you. I'll be back in just a moment."*

### Copilot panel (structured opening)

**Summary (with inline citations):**
> 👋 Hey Lisa — Rachel's asking to cancel her **Hoka Race-Day Pro Pack ($847.99)**. She's a VIP since 2022 — $12K+ lifetime, 3% return rate, zero prior cancellations. Order's still in processing, so cancelling is clean on our side.⁽¹⁾

**What I know (prose bullets, gray card):**
- Order is still in processing — nothing's shipped yet.
- Rachel's a VIP since 2022 — $12K+ lifetime, zero prior cancellations.
- Our VIP playbook covers this cleanly.⁽¹⁾
- Suggested thank-you credit is $25 for orders in the $500–$1K band.⁽²⁾

**What I'd do (green-rule block):**
- Title: `Cancel the order + $25 thank-you credit`
- Line 1: `$847.99 refund to her original payment method`
- Line 2: `$25 loyalty credit on her account`

**Ask:** *"Want me to handle it, or would you like to tweak it?"*

**Chips:**
- `Yes, go ahead` (primary)
- `Bump credit to $50`
- `Lower credit to $10`
- `No, I'll take it`

### Decision model (Rachel's `decisions` object)

- `approve(s)` → Builds `timelineEvents` array: Lisa approved cancellation → (if modified) Lisa updated credit to $X → Gladly AI cancelled order → Gladly AI issued $847.99 refund. Returns `copilotReply`, `customerReply`, `customerChannel: 'chat'`.
- `raise(s, amt)` → Re-asks with updated chip rail (Yes / Change my mind / No). Mutates rec card inline via `updateRecCard(false)` — shows green `Updated` pill.
- `lower(s, amt)` → Same as raise, lower amount.
- `revert()` → Back to $25 default, restores original 4 chips.
- `handoff(s)` → `timelineEvents`: Lisa took over → Gladly AI stopped responding.

### Post-approve flow

1. `pushAIMsg(copilotReply)` — "Done — order cancelled, $847.99 refund on its way to Rachel's original payment method, and a $X thank-you credit on her account."
2. `timelineEvents` appended as **right-aligned `.tl-activity`** lines (chronological)
3. Outbound AI customer-facing chat message (clean bubble — no badge, no chip)

### Citations (Rachel)

1. **VIP Cancellation Playbook** — "Full refund for VIPs on orders still in processing, no questions asked. A $25–$50 thank-you credit is suggested for $500–$1K orders to encourage a return visit."
2. **Credit Guidelines** — "For orders $500–$1K, $25 is the default thank-you credit. For $1K+, the default is $50. Agents can adjust between $10–$75 without escalation."

---

## 6. UX decisions (established and carried forward)

### Design tokens

- **Green primary:** `#009B00` / `#007A00` hover / `#D8F4D8` fill / `#EAF7EA` surface
- **Navy:** `#0F203C` (AI avatar, task-state pip icon)
- **Purple (Assist tab only):** `#8C69F0` — the single remaining purple in the UI
- **Grays:** `#FAFAFA` → `#767676` scale
- **Red:** `#D50E0E` (destructive only)
- **Typography:** Inter — 13px/1.62 body, 16px h3, 700 bold

### Layout (1440×900)

```
Nav (56, full width)
┌──────────────── Stage ──────────────────────────────┐
│ ┌── Left zone (flex: 1, column) ──┐                 │
│ │ ┌─ Layout (flex: 1) ───────────┐│  Team Assist    │
│ │ │ Customer list │ Profile │ Conv││  (Copilot)     │
│ │ │   220-260     │  280-320│ flex││  380 / 440     │
│ │ │                                ││  / 580         │
│ │ └──────────────────────────────┘│                 │
│ │ Bottom bar (48, flush left)     │  full stage     │
│ └─────────────────────────────────┘  height         │
└──────────────────────────────────────────────────────┘
```

- `.stage` = flex row, height = `calc(100vh - 56px)`
- `.left-zone` = flex column containing `.layout` (flex:1) + `.bottom-bar` (48px)
- `.col-right` (Team Assist) is a sibling of `.left-zone` and gets the full stage height
- Bottom bar stops flush against copilot's left edge

### Width modes

| Mode | Trigger | List | Profile | Conv | Copilot |
|------|---------|------|---------|------|---------|
| Default (chat customer) | Jordan or any `type: 'chat'` | 260 | 320 | flex | 380 |
| Panel-weighted | `type: 'assist'` (Rachel) | 220 | 280 | flex | 440 |
| Focus-copilot | Expand button in copilot gutter | 80 | 280 | flex | 580 |

### Customer list

- Default expanded (260px); collapse button at top reduces to 80px avatar strip
- Filter pills: All / Needs input / Chats
- Card structure: priority dot + 40px avatar + type pip + name + time + 2-line preview + tag (`Needs input` purple / `Chat` gray) + channel label

### Team Assist panel (Copilot)

- 32px vertical gutter with 4 tabs: Expand (top) / Assist (active, purple) / Answers / Library
- Scrolls vertically (newest at bottom)
- Chip rail (suggestion buttons) above the chat input, dynamically refreshed per scripted beat
- Chat input: rounded pill, 1px `#B3B3B3` border, "Chat with Gladly AI" placeholder
- 46×30 attachment thumbnail decorative element to the right of the input

### Streaming chat messages (`.cm.ai`)

- Flex-column (so body + extras + feedback row stack vertically)
- Body = rendered HTML (plain text OR pre-wrap draft)
- Extras = action card / product list (inline under body)
- **Feedback row** on every streaming AI message:
  - Primary **Use** button (drafts only) — fires the beat's `useAction` (default `useDraft`, SMS uses `sendRecSMS`)
  - Regenerate (↻) — toast only
  - Copy (📋) — `navigator.clipboard.writeText` + toast
  - Thumbs up / down — toggleable state, mutually exclusive

### Timeline event types

- `.tl-event` — **centered** · date dividers, routing, state changes, conversation closed
- `.tl-activity` — **right-aligned** · agent decisions, AI-executed actions (post-approve receipts)
- `.msg.inbound` — customer messages with avatar left
- `.msg.outbound` — AI or agent replies with avatar right

### What's explicitly NOT there

- No "task card" in the timeline (killed in v7)
- No Approve/Handoff buttons floating in the conversation — they're all in the copilot
- No modals (everything conversational)
- No purple Assist chips in timeline (v7 removed, replaced with plain `.tl-activity`)
- No "SENT WITH TEAM ASSIST" badge on outbound bubbles
- No "View API call" link
- No credit card references anywhere — all payments say "original payment method"
- No "task" vocabulary ("Needs input" replaces it in the UI)
- No dashed `.draft-card` container — drafts stream as AI messages directly

---

## 7. Data architecture (v9)

### SCENARIOS structure (per customer)

```
{
  id: 'jordan' | 'rachel',
  type: 'chat' | 'assist',                // controls layout + list pip
  wired: true,
  listCard: { name, initials, avatarColor, preview, time, channel, priority },
  profile: { name, customerSince, ltv, contact{…}, preferences[], orders[], conversations[] },
  convHeader: { title, status },
  topic,                                    // bottom-bar topic label
  events: [ { kind: 'cmsg'|'amsg'|'event', … } ],  // initial timeline
  copilot: {
    opening,                                // first AI message (structural, no icons)
    factsProse[],                           // only for HITL (Rachel) — prose bullets
    rec: { title, line1, line2 },           // only for HITL
    ask,                                    // only for HITL
    chips[],                                // initial chip rail
    citations[],                            // 2-3 inline citation sources
    creditDefault, mode,                    // HITL state
    script: { beatName: { reply?, draftCard?, actionCard?, productList?, useAction?, sideEffect?, unlockChips[], nextChips[] } }  // Team Assist
    outboundBodies: { draft, warmer },      // Team Assist — used by sideEffectSendOutbound
    outboundSMSBody
  },
  decisions: {                              // HITL only
    approve(s), raise(s, amt), lower(s, amt), revert(), handoff(s)
  }
}
```

### Key functions

- `selectCustomer(id)` — swaps profile, conversation, copilot; toggles `.panel-weighted` on body
- `renderCustomerList()` — renders all 6 cards
- `renderProfile(s)`, `renderConversation(s)`, `renderCopilot(s)` — branch on scenario type
- `renderChips(chips)` — sets the suggestion rail, stashes `window._chipBank`
- `handleChip(i)` — clicks a chip, routes to `runDecision` → `runScript` (Jordan) or `decisions.X` (Rachel)
- `runScript(action)` — Jordan's scripted state machine
- `runDecision(action, arg)` — Rachel's approve/raise/lower/revert/handoff model
- `pushAIMsg(text, opts)` — streaming AI message with feedback row; `opts.draft` adds Use button; `opts.extra` appends action/product card
- `pushAgentMsg(text)` — user-side chat bubble (right-aligned, gray fill)
- `sideEffectSendOutbound(channel)` / `sideEffectSendOutboundSMS()` / `sideEffectApproveRun()` — post-decision effects on the customer timeline
- `onUse(btn, action)` / `onCopy(btn)` / `onThumb(btn, dir)` / `onRegen(btn)` — feedback row handlers
- `toggleList()`, `toggleFocus()` — list collapse, copilot expand
- `togglePop(e, n)` — inline citation popovers

### Two new v9 component types

- **Draft rendering:** body IS the AI message (pre-wrap), Use button + feedback icons inline below — no outer container
- **Action card (`.action-card`):** solid-border block with uppercase label, numbered step list, primary `Approve & run` + secondary `Edit steps` buttons

### Feedback row (every streaming AI message)

Rendered by `renderMessageActions(isDraft, useAction)`:
- Use (green pill, drafts only)
- Regenerate (↻ icon)
- Copy (📋 icon)
- Thumbs up (👍, toggleable, green when active)
- Thumbs down (👎, toggleable, red when active)

---

## 8. Version history

| Version | Date | Theme | Key changes |
|---------|------|-------|-------------|
| v1–v4 | Apr 1 | Early iterations | Pre-Apr 17 review; various task-card explorations |
| v5 | Apr 1 | Baseline | Tabbed Task Details / Team Assist panel, purple Team Assist chrome, modals |
| v6 | Apr 17 PM | Apr 17 direction | Expanded customer list; Jordan scenario added; panel-not-tabbed; task card still in timeline |
| v7 | Apr 21 AM | Everything-in-the-copilot | **Killed task card.** Decisions in copilot chat. Assist chips in timeline. No modals. Plain English. Focus mode. |
| v8 | Apr 21 PM | Polish | Facts as prose bullets. Panel-weighted default. Focus keeps profile. Chronological timeline. Toned-down rec. "SENT WITH TEAM ASSIST" badge added then removed. Purple chips removed. |
| v9 | Apr 21–22 | Hoka + two flows | Both customers → Hoka buyers. Rachel keeps HITL (Hoka Race-Day Pro Pack). Jordan gets Team Assist scripted flow (catch-up → sentiment → policy → draft → warmer → use → process return → approve & run → recommend → SMS). Full-height copilot, narrow bottom bar. Draft-card / action-card / product-list components. No credit card refs. Iterated 5× post-ship: chat-style drafts (no greeting/signoff), streaming draft UX with inline Use + feedback icons, flex-column AI messages (fix side-by-side bug), right-aligned activity events. |

### v9 post-ship iteration log

1. **Jordan docx fix:** added Feb 8 prior chat, changed channel to chat, added product-consultation + SMS beat
2. **Chat-style drafts:** removed "Hi Jordan" greeting and "— Joseph" signoff from Jordan's drafts (kept on SMS per convention)
3. **Streaming drafts + feedback icons:** drafts render AS the AI message (no preface, no container); Use button + regenerate/copy/thumbs-up/thumbs-down icons on every AI reply
4. **Layout stack fix:** `.cm.ai { flex-direction: column }` so message body + feedback row stack vertically (was splitting into 2 columns)
5. **Right-aligned activity events:** new `.tl-activity` class for outbound-side acknowledgements (Lisa approved / Gladly AI issued refund / etc.); kept `.tl-event` for centered date dividers and routing events

---

## 9. Deployment workflow

### Standard edit → live cycle

```bash
# 1. Edit the source file
/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/hitl-prototypes/HITL-Task-Prototype-v9.html

# 2. Copy to repo
cp "/Users/…/hitl-prototypes/HITL-Task-Prototype-v9.html" \
   /Users/steve.westgladly.com/projects/gcl-hitl-prototypes/

# 3. Commit + push
cd /Users/steve.westgladly.com/projects/gcl-hitl-prototypes
git add HITL-Task-Prototype-v9.html
git commit -m "v9: <change>"
git push

# 4. Manual deploy (Git auto-deploy is not firing — open issue)
vercel deploy --prod --yes

# 5. Verify with browser UA (Vercel bot-mitigation blocks curl otherwise)
curl -sA "Mozilla/5.0" https://gcl-hitl-prototypes.vercel.app/HITL-Task-Prototype-v9.html | grep -c '<new string>'
```

### Versioning policy

- **Never edit a shipped version** (v1–v8 frozen for the deck)
- New iterations go into a new `HITL-Task-Prototype-vN.html`
- `vercel.json` `destination` points `/` at the current canonical version

### Notes on Vercel

- Production alias: `gcl-hitl-prototypes.vercel.app`
- Bot mitigation ("Security Checkpoint") may return 403 to `curl` without a real User-Agent. Use `curl -A "Mozilla/5.0"` or just open in a browser.
- Deploy Protection is off at the project level; site is publicly accessible.

---

## 10. Source-of-truth references

### v9 demo script (authoritative for scenario copy)

`/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/demo-drafts/GCL_Live_Service_Demo_-_v9.docx`

- **Part A:** Jordan's Team Assist flow — catch me up, sentiment, approve check, draft + refine, process return, product consultation + SMS, thumbs feedback
- **Part B (implicit):** Rachel's HITL flow — AI asks Lisa, bumps credit, approves, AI executes

Extract via: `unzip -p <file> word/document.xml | sed 's/<[^>]*>//g'`

### Feedback doc

`/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/hitl-prototypes/HITL Feedback.md`

- **Round 1 (Apr 21 AM):** Joseph's "flip the chair" framing, kill task card, everything in copilot, no modals, plain English
- **Round 2 (Apr 21 PM, onsite):** navigation/admin nav decisions, pricing, naming (all out of prototype scope except for UI polish on HITL)

### Original research

`/Users/steve.westgladly.com/projects/Gladly Team/GCL Keynote/hitl-prototypes/HITL-Tasks-Analysis-Apr2026.md`

600-line foundation document. Customer quotes from Ulta, Aceable, Shields, StockX. Gong call analysis. 24-month Slack SWOT. Rachel + Jordan scenarios derived from Ulta's explicit HITL walkthrough request.

### Figma references

- SC-Template 3.4 file: `wZBpIXbq9U21IVxGZG7GNd` — Gladly agent desktop chrome (nav, customer list, profile, conversation, bottom bar, task panel)
- Gladly Team AI Assist file: `2ImzZQNQ2yy6fsZ3Br2trz` — Team Assist copilot panel (Ben Long scenario informed v6's panel structure)

---

## 11. Open issues and flags

1. **Vercel Git auto-deploy not firing.** `git push` to `main` doesn't trigger a new build; manual `vercel --prod --yes` is required each time. Integration shows "Connected" in the dashboard. Not yet debugged.
2. **SMS greeting/signoff.** Jordan's recovery-recommendation SMS opens with "Hey Jordan" and signs off "— Joseph". Flagged to Steve as potentially inconsistent with chat-style drafts; SMS convention was the reason for keeping. Awaiting confirmation.
3. **Opening AI message in copilot has no feedback icons.** Intentional — it's structural (in `#ao-text`), not part of the stream. If icons are wanted there too, it's a small addition.
4. **Dead code:** `renderDraftCard()` is no longer called (drafts stream inline now). `.draft-card` CSS also unused. Harmless but could be cleaned up on next major edit.
5. **Regenerate button** is a toast-only stub on drafts — no actual regeneration. Could wire it to re-run the current beat if we want more fidelity.

---

## 12. Naming decisions (still in flight at the product level, but locked for demo)

- Prototype uses **"Team Assist"** throughout
- Joseph flagged `Gladly Assist` / plain `Assist` as alternatives; not resolved
- `Concierge` considered for the HITL-manager role, dropped
- No "task" language in the UI — replaced with "Needs input" in list tags and plain-English in messages

---

## 13. Demo walkthrough (what to click on stage, in order)

### Jordan (Team Assist, ~90 seconds)

1. Land on Jordan — conversation visible, copilot shows handoff opening + 3 chips
2. Click `Catch me up on Jordan`
3. Click `What's his sentiment?` *(optional — can skip for time)*
4. Click `Can I approve this return?` — optionally click inline `⁽¹⁾` to show citation popover
5. Click `Draft a response` — procedural draft streams in with **Use** button + feedback icons
6. Click `Make it warmer` — warmer draft replaces (or adds; verify live behavior)
7. Click inline **Use** button on the warmer draft — Joseph's chat message posts to timeline; Jordan replies with thanks ~1.5s later
8. Click `Process the return` — action card with 3 steps
9. Click inline `Approve & run` — card fills with ✅, 3 right-aligned activity events append
10. Click `Recommend something for his recovery` — inline product list appears
11. Click `Draft an SMS` — SMS draft with **Use** button
12. Click inline **Use** — outbound SMS posts to timeline

### Rachel (HITL, ~30 seconds)

13. Click **Rachel Thompson** in the customer list — layout flips to panel-weighted (copilot 440)
14. Click `Bump credit to $50` — rec card rewrites with `Updated` pill; re-ask chips appear
15. Click `Yes, go ahead` — AI confirms in copilot; 4 right-aligned activity events append; AI's customer-facing chat reply lands

Total demo time target: 2–5 minutes.

---

## 14. Stakeholder map

- **Steve West** (Director of Revenue Enablement) — owns prototype, drives feedback loops
- **Joseph Ansanelli** (CEO) — "flip the chair" direction, kill-the-task-card call, deep UX opinions
- **Austin Reece** — coordinating GCL demo arc, voiceover
- **Matt Baker** (Head of Product) — Team Assist + HITL packaging; Tasks strategy
- **Ellen Laux** — UI/UX design direction
- **Christina Lingga** — designing interface iterations in Figma alongside the prototype
- **Greg's team** — building the actual Team Assist implementation

Prototype's role: **illustrative demo, not production**. Design can diverge from the final product as long as the direction lands on stage.
