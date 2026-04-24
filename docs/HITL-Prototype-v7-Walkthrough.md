# HITL Prototype v7 — Walkthrough

**File:** `HITL-Task-Prototype-v7.html`
**Live:** https://gcl-hitl-prototypes.vercel.app
**Repo:** github.com/stevewest-sketch/gcl-hitl-prototypes
**Direction:** Apr 21, 2026 feedback (Joseph, Steve, Greg, Christina)

---

## 1. What this prototype shows

The v7 prototype demonstrates **Human-in-the-Loop AI** inside the standard Gladly Team agent desktop. The premise is that Gladly AI can do most of what a customer needs — but when it hits an edge case (a policy exception, a high-value cancellation, something requiring judgment), it doesn't "surrender" the conversation to a human. Instead it **asks a human for input**, executes the human's decision, and keeps going.

Three moments use the same UX:

1. **AI asks the human for input.** AI has a recommendation, needs approval or modification before acting.
2. **AI assists the human when the human owns the conversation.** (Classic Team Assist — unchanged.)
3. **Human hands the conversation back to AI.** Or AI hands it back to the human.

v7's core design move is that **all three happen inside Team Assist (the right-hand copilot panel)**. There is no separate "task inbox," no "approval queue," no modal dialogs. The customer list on the left routes the customer to the human like any chat, the copilot on the right holds the conversation about what to do.

The demo wires two scenarios end-to-end: **Jordan Rivera** (return exception) and **Rachel Thompson** (VIP cancellation). Four other customers appear in the list as stubs to show the routing pattern but are not interactive.

---

## 2. Layout at 1440×900

```
┌─────────────────────────────────────────────────────────────────────────┐
│ Nav bar · +Gladly · channel toggles · search · bell · Lisa Green (56px) │
├────────┬─────────┬─────────────────────────────┬────────────────────────┤
│        │         │                             │                        │
│  Your  │ Profile │  Conversation timeline      │  Team Assist           │
│custom- │  panel  │  (customer ↔ Gladly AI)     │  (human ↔ AI)          │
│  ers   │         │                             │                        │
│        │         │                             │                        │
│ 260 px │ 320 px  │  flex                       │  380 px                │
│        │         │                             │                        │
├────────┴─────────┴─────────────────────────────┴────────────────────────┤
│ Assigned to VIP Response Team — Lisa Green  ·  Close & Next  (48px)     │
└─────────────────────────────────────────────────────────────────────────┘
```

The left column can collapse to 80 px. A **focus-copilot** toggle collapses the list and hides the profile so the copilot grows to ~640 px for when the agent wants to concentrate on the AI conversation.

---

## 3. Customer list — the routing surface

The list mixes **customers the AI needs input on** ("Needs input") and **regular chats**. AI-routed approvals aren't a separate inbox — they land in the same list the agent already lives in, prioritized by the routing engine.

Each card shows: a priority dot, the customer's avatar, a type pip (purple sparkle = AI wants input, gray speech bubble = chat), the name and timestamp, a two-line preview of what's happening, and a tag (`Needs input` or `Chat`) plus the channel.

### The six cards

| # | Customer | Type | Preview | Time | Channel | Wired |
|---|----------|------|---------|------|---------|-------|
| 1 | Sarah Kim | Chat | "Hey, where's my order? It's been a week…" | 1m | Chat | No |
| 2 | **Rachel Thompson** | **Needs input** | "Wants to cancel her Dyson V15 ($847) — can't use it due to apartment rules." | 1m | Chat | **Yes** |
| 3 | **Jordan Rivera** | **Needs input** | "Wants to return running shoes — 2 days past window. Torn ACL, can't train." | 3m | Email | **Yes** |
| 4 | Priya Shah | Needs input | "AI wants your call on a VIP exchange ($380 → $420)." | 6m | SMS | No |
| 5 | Marcus Klein | Chat | "Voice callback — follow-up on shipment." | 9m | Voice | No |
| 6 | Kira Fletcher | Chat | "Question on sizing — jackets run true to size?" | 14m | Chat | No |

Clicking a stub (Sarah, Priya, Marcus, Kira) fires a toast: *"…— this is a demo, only Rachel and Jordan are wired."* Clicking Rachel or Jordan swaps every panel on the page.

**Prototype default:** Jordan is selected on load (richer story).

---

## 4. Profile panel (middle-left)

Julie-Chang-style profile stack — avatar header, contact, preferences (if present), orders, conversation history.

### For Jordan

- **Header:** Jordan Rivera · JR avatar (olive green) · Customer since 2020 · Lifetime Value $4,240.00 · Link to customer (1 suggestion)
- **Contact:** 792 Evergreen Terrace, Austin, TX 78749 · jordan.rivera@gmail.com (Main) · (555) 123-0192 (SMS · Main) · Mobile
- **Preferences:** Favorite category *Running* · Sizing *Men's 10* · Brand preference *GCL Ultra · Nimbus*
- **4 orders** — highlighted: `GCL-55892 · GCL Ultra Marathon Shoes · Delivered · $189.00 · Ordered 03/18/2026`
- **Conversations:** Today *Return request (shoes)* · Feb 8 *Size swap — trail shoes* · Dec 21 *Gift card redemption*

### For Rachel

- **Header:** Rachel Thompson · RT avatar (blue) · Customer since 2022 · Lifetime Value $12,400.00 · Link to customer (1 suggestion)
- **Contact:** 2721 Addison Street, San Francisco, CA 94110 · rachel.thompson@email.com (Main) · (415) 555-0192 (SMS · Main) · Mobile
- **1 order** — `ORD-2026-84721 · Dyson V15 Detect · Processing · $847.00 · Ordered 03/28/2026`
- **Conversations:** Today *Cancel order request* · Mar 15 *Shipping address change* · Feb 2 *Product question — Dyson*

---

## 5. Conversation timeline — customer ↔ Gladly AI

This is the middle column. It shows **only events the customer would see in their inbox** — their own messages, AI's customer-facing replies, and system receipts. Nothing about "tasks," "approvals," or internal AI reasoning appears here. That's deliberate: the timeline mirrors the customer's reality.

When a decision happens in the copilot, a small **Assist chip** lands in the timeline as a compact history marker — the only internal breadcrumb the timeline carries.

### Jordan — initial state

**Header:** `Apr 21 · Return request · Waiting`

1. `Jordan Rivera sent an email — 5 min ago`
    > Hi, I need to return a pair of shoes — order #GCL-55892. I know I'm a few days past 30, but I'm hoping you can help given my situation.
    >
    > I've been training for a marathon for over a year. Last week I was diagnosed with a torn ACL — surgery and months of recovery. There's no way I'll be running for a long time.
    >
    > Shoes are unworn — just tried them on at home. Receipts and box included. Thanks.

2. `Gladly AI replied — 3 min ago` (outbound, navy AI avatar)
    > Hi Jordan — really sorry to hear about your injury. Let me check on this for you. I'll be back in just a moment.

*(nothing else until the human makes a decision in the copilot)*

### Rachel — initial state

**Header:** `Apr 21 · Cancellation request · Waiting`

1. `Rachel Thompson sent a chat — 2 min ago`
    > Hi, I need to cancel my order #ORD-2026-84721. I ordered the Dyson V15 Detect but I just found out my apartment building doesn't allow vacuum use after 9pm and I work late shifts. Can I get a full refund?

2. `Gladly AI replied — 1 min ago`
    > Hi Rachel — thanks for reaching out. Let me sort this out for you. I'll be back in just a moment.

### After the human approves (Jordan example)

Three items append to the timeline, in order:

3. `✓ Gladly AI issued a $189 refund and emailed a return label — just now · View API call`
    *(a one-line API receipt — proof the action happened via Commerce Cloud)*

4. `Gladly AI replied — just now` (outbound)
    > Hi Jordan — really sorry to hear about your injury. Good news: we're making this right. A full refund of $189 is on its way to your Visa ending 8204, and a prepaid UPS return label just landed in your inbox. We've also added a $25 credit to your account for when you're back. Wishing you a smooth recovery.

5. **Assist chip** (purple, clickable)
    > ⚡ **Lisa** approved a return exception for **$189** · just now
    >
    > *(with credit amount appended if the human modified: "…with a $50 credit")*

Clicking the Assist chip scrolls the copilot to the decision message and briefly highlights it.

### After handoff

5. **Assist chip** (gray)
    > ⚡ **Lisa** took over the conversation · just now

And the conversation header status flips to `Handed off to Lisa`.

---

## 6. Team Assist panel — AI ↔ human conversation

This is the right column. **The AI's ask for input, the human's response, and every clarification live here** — as chat messages, not as a task card or a modal.

Layout:
- 32 px left gutter with four icon-tabs: **Expand** (top), **Assist** (active, purple), **Answers**, **Library**
- Main body scroll: the AI's opening message at the top, then back-and-forth below
- Suggestion chip rail above the input
- Rounded pill "Chat with Gladly AI" input with send icon and attachment thumbnail

### The AI's opening message (visually one "turn," even though it's multi-block)

Three stacked blocks — **summary paragraph**, **facts block**, **recommendation card** — followed by a bold closing **ask**.

#### Jordan — opening message

**Summary**
> 👋 Hey Lisa — Jordan emailed about returning his running shoes (**order GCL-55892, $189**). He trained for a marathon for over a year and was just diagnosed with a torn ACL — surgery and a long recovery. Shoes are **unworn**, only tried on at home, and he's 2 days past our 30-day window.⁽¹⁾

**Facts block** (soft gray card)
| | |
|---|---|
| Order status | Delivered, unworn |
| Customer | Loyal since 2020, $4.2K lifetime, no prior exceptions |
| Window | 2 days past our 30-day window |
| Playbook | Covered under medical-hardship exceptions⁽¹⁾ |

**Recommendation card** (white with green heart badge "what I'd do")
- **Full refund + prepaid return label + $25 credit**
- $189 refund to Visa ···8204
- Prepaid UPS label emailed to Jordan · $25 thank-you credit

**Ask (bold)**
> Want me to go ahead, or would you like to tweak it?

#### Rachel — opening message

**Summary**
> 👋 Hey Lisa — Rachel's asking to cancel her **Dyson V15 ($847)**. She's a VIP since 2022, zero prior cancellations, clean 3% return rate. The order is still in processing, so cancelling is clean on our side.⁽¹⁾

**Facts block**
| | |
|---|---|
| Order status | Processing, not shipped |
| Customer | VIP, spent $12K+ with us since 2022 |
| Playbook | Our VIP playbook covers this⁽¹⁾ |
| Credit | Suggested $25 thank-you for $500–$1K orders⁽²⁾ |

**Recommendation card**
- **Cancel the order + $25 thank-you credit**
- $847 refund to Visa ···4821
- $25 loyalty credit on her account

**Ask**
> Want me to handle it, or would you like to tweak it?

### Citation popovers

The small `⁽¹⁾ ⁽²⁾` superscripts are clickable and open an inline popover with the source title, a one-sentence summary, and an "Open in Knowledge Base →" link. Sources are scenario-specific:

**Jordan**
1. **Medical Hardship Return Exception** — "When a customer gives a legitimate medical reason and the item is unworn, agents can approve a return outside the 30-day window. Default resolution is a full refund."
2. **Loyalty Tenure Guidelines** — "Customers with 3+ years and no prior exceptions generally qualify for good-faith resolutions. Jordan has been with us since 2020 with a clean record."

**Rachel**
1. **VIP Cancellation Playbook** — "Full refund for VIPs on orders still in processing, no questions asked. A $25–$50 thank-you credit is suggested for $500–$1K orders to encourage a return visit."
2. **Credit Guidelines** — "For orders $500–$1K, $25 is the default thank-you credit. For $1K+, the default is $50. Agents can adjust between $10–$75 without escalation."

---

## 7. The back-and-forth — how a decision happens

The human responds to the AI's ask either by clicking one of the four suggestion chips or by typing free text. Below is the exact dialogue for each path.

### 7.1 The four suggestion chips (under the input)

1. **Yes, go ahead** *(green, primary)*
2. **Bump credit to $50** *(white, secondary)*
3. **Lower credit to $10** *(white, secondary)*
4. **No, I'll take it** *(white, secondary)*

Clicking a chip:
- Appends the chip's text as an **agent message** in the copilot (gray bubble, right-aligned)
- Shows a **typing indicator** (3 dots) for ~700 ms
- Replaces with the AI's reply
- Clears the chip rail and re-renders chips appropriate to the next state

### 7.2 Path A — Yes, go ahead (direct approval)

Human clicks **Yes, go ahead** →

> **Lisa:** Yes, go ahead
>
> **Gladly AI:** *(Jordan)* Done — I've issued a $189 refund to Jordan's Visa ···8204 plus a $25 thank-you credit, and emailed the return label. Wishing him a smooth recovery.
>
> *(Rachel)* Done — cancellation processed, $847 refund on its way to Rachel's Visa ···4821, and a $25 credit on her account.

At the same moment, three things append to the **timeline** (see §5): API receipt, customer-facing AI reply, purple Assist chip. The copilot closes out — no further chips.

### 7.3 Path B — Modify, then approve (the "be generous" demo path)

Human clicks **Bump credit to $50** →

> **Lisa:** Bump credit to $50
>
> **Gladly AI:** *(Jordan)* Bumped it to a $50 credit. Want me to go with that?
>
> *(Rachel)* Bumped it to a $50 credit. Still within discretion. Go?

Simultaneously in the copilot:
- The **recommendation card** rewrites inline — title becomes "Full refund + prepaid return label + **$50 credit**," line 2 updates to "$50 thank-you credit," and a green **UPDATED** pill appears next to the title.
- The chip rail re-renders with three options:
    1. **Yes, go ahead** *(primary)*
    2. **Change my mind** *(secondary — reverts to $25 and restores the original four chips)*
    3. **No, I'll take it**

Human clicks **Yes, go ahead** → Gladly AI acts. The final "Done" message, the API receipt, the customer reply, and the Assist chip all reflect the modified amount. The Assist chip reads:

> ⚡ **Lisa** approved a return exception for **$189** **with a $50 credit** · just now

**Lower credit to $10** works identically in reverse.

### 7.4 Path C — No, I'll take it (handoff)

Human clicks **No, I'll take it** →

> **Lisa:** No, I'll take it
>
> **Gladly AI:** Got it — I'll stop responding to Jordan and hand the conversation to you.

Timeline gets a **gray Assist chip** — `⚡ Lisa took over the conversation · just now` — and the conversation header status updates to `Handed off to Lisa`. The human now owns the conversation; AI stays out.

### 7.5 Free-text input (for anyone who'd rather type)

The pill input at the bottom accepts natural language. The prototype parses a few patterns:

| If you type... | What happens |
|---|---|
| `yes`, `yep`, `go`, `go ahead`, `do it`, `approve` | Runs the approve flow (Path A) |
| `no`, `I'll take`, `take over`, `hand off` | Runs the handoff flow (Path C) |
| `bump to 50`, `raise to 40`, `$100 credit`, `lower to 5` | Detects the number, compares to current credit, runs raise/lower |
| `policy`, `why` | Short explanation: *"she/he fits our playbook — clean history, legitimate reason, within our discretion. The citations in the summary have the details."* |
| anything else | *"I'd still go with the recommendation as-is. Let me know — yes, no, or adjust the credit."* |

`Enter` sends; `Shift+Enter` adds a newline.

---

## 8. The Assist chip — persistent history in the timeline

Every decision that happens in the copilot leaves a **single compact chip** in the customer's conversation timeline:

- **Purple chip** for an approval: `⚡ Lisa approved a return exception for $189 · just now` *(optionally "with a $50 credit" if modified)*
- **Gray chip** for a handoff: `⚡ Lisa took over the conversation · just now`

Clicking the chip scrolls the copilot to the relevant message and briefly highlights it in purple. This is the feedback's "object that persists in the timeline for history" — a small breadcrumb so future agents (or the same agent, later) can see what happened without digging.

---

## 9. Focus mode — expanding Team Assist

The **expand** button is the topmost icon in the copilot's left gutter. One click:

- Customer list collapses to 80 px (avatars only)
- Profile panel collapses to 0 px (hidden)
- Conversation narrows to its min-width (~360 px)
- **Copilot grows to ~640 px**
- Agent chat bubbles can grow wider (420 px → 540 px)

Click again to restore. This supports Joseph's "the conversation can get bigger… maybe more important than the customer conversation" point from the Apr 21 review — the copilot is a first-class surface, not a sidebar.

---

## 10. The bottom bar (unchanged from standard Gladly)

- **Left:** Assigned to — *VIP Response Team — Lisa Green* (with a small inbox avatar)
- **Center:** New (+) button · reply input · Topic — *Return request* (Jordan) or *Cancellation request* (Rachel)
- **Right:** Green **Close & Next** split button

This anchors the demo in Gladly's current chrome. Nothing about the HITL flow changes the bottom bar.

---

## 11. What was removed from v6 (so v7 makes sense)

| v6 element | v7 treatment |
|---|---|
| Task card in the timeline with Approve / Handoff buttons | **Removed.** Decision moved to copilot. |
| Modal dialogs for Approve and Handoff | **Removed.** No modals anywhere. |
| "Review Decision" section in the copilot | **Removed.** The AI's message carries the decision ask. |
| Separate status strip (`● Awaiting your review · AI confidence 92%`) | **Absorbed** into the AI's opening message. |
| Green Vibe Service event card in timeline | **Simplified** to a one-line `✓ Gladly AI issued…` timeline event. |
| "Task for Tier 2 Support" labels, "Closed Task", `Needs approval — order value exceeds $500 auto-approve threshold` | **Removed.** The word "task" is no longer used in the UI. |
| Schema-style labels like `Customer tier — VIP · Lifetime $12.4K`, `Policy match — VIP cancellation within window` | **Rewritten plain English** — "VIP, spent $12K+ with us since 2022", "Our VIP playbook covers this". |
| Thumbs up/down on AI recommendation | **Removed** from the initial message. The chat conversation itself is the feedback loop. |
| `⌘+Enter` approve, `⌘+H` handoff shortcuts | **Removed** (no modals to trigger). Enter in the chat input sends the message; Esc closes any citation popover. |

---

## 12. Design principles in v7

1. **One UX for every AI ↔ human moment.** Asking for input, assisting during a conversation, and handing off all live in the same chat thread. No parallel surfaces.
2. **Timeline is for the customer.** If the customer can't see it, it doesn't belong in the timeline — except the single Assist chip that records a decision for history.
3. **Everything conversational.** No modals. No "Approve"/"Reject" formal labels. Suggestion chips offer the fast path; typing offers the flexible path; both produce the same outcome.
4. **Plain English.** No "task." No schema-style labels. If an agent can't read it out loud, rewrite it.
5. **Demo positive.** The default scripted path takes the human from the AI's $25 suggestion → **bump to $50** → approve. "Being generous" reads better than "denying."
6. **Scene-set with familiar AI.** Audience may not have used HITL systems, but many have seen Claude Code / cursor ask "approve this plan?" The tee-up in the deck can use that reference; the prototype speaks the same language.

---

## 13. Try it yourself — a guided 90-second walkthrough

1. Open https://gcl-hitl-prototypes.vercel.app — lands on **Jordan**.
2. Read the AI's opening in the copilot. Click the `⁽¹⁾` superscript after "30-day window" — a popover opens with the Medical Hardship Return Exception source.
3. Click **Bump credit to $50**. Watch the recommendation card rewrite inline with the green **UPDATED** pill; new chips appear.
4. Click **Yes, go ahead**.
5. In the conversation timeline (middle column), see three new items appear: the API receipt, AI's customer-facing reply with the updated $50 credit, and the purple **Assist chip**.
6. Click the Assist chip — the copilot scrolls and the AI's "Done" message briefly highlights.
7. Click the **expand** button (top of the copilot's left gutter). The customer list narrows, the profile hides, the copilot takes ~640 px. Click again to restore.
8. Click **Rachel Thompson** in the customer list — same pattern, different scenario (VIP cancellation, chat channel, $847 order).
9. For Rachel, type in the input: `bump to 100`. The AI bumps to $100, re-asks. Type `yes`. The approval processes with the $100 credit.

---

## 14. Non-goals (worth saying out loud)

- **Not a production UI.** Every interaction is scripted in-browser — no real API calls, no state persistence, no server.
- **Not pixel-perfect.** Chrome matches Gladly's SC-Template tokens and copilot Figma but isn't using the production component library.
- **No Claude Code tee-up in the HTML.** The audience reference to Claude Code's "approve this plan?" lives in the deck, not the prototype.
- **Two wired scenarios only.** Sarah, Priya, Marcus, Kira are stubs for the routing story.
- **No real Knowledge Base.** Citation popovers show inline copy; the "Open in Knowledge Base →" link is a placeholder.

---

## 15. File map

| File | Purpose |
|---|---|
| `HITL-Task-Prototype-v7.html` | The prototype (1,163 lines, self-contained HTML) |
| `HITL-Task-Prototype-v6.html` | Prior iteration — kept for reference and the deck |
| `HITL-Task-Prototype-v1–v5.html` | Earlier iterations |
| `HITL Feedback.md` | Apr 21 feedback round that drove v7 |
| `HITL-Prototype-v7-Walkthrough.md` | This document |
| `HITL-Tasks-Analysis-Apr2026.md` | Original research foundation (Dec 2025–Mar 2026) |
| `/Users/steve.westgladly.com/projects/gcl-hitl-prototypes/` | Clean public-facing folder; pushed to GitHub and deployed to Vercel |
