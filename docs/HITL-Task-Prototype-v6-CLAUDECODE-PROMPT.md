# Claude Code Kickoff Prompt — HITL Task Prototype v6

**Owner:** Steve West (Director, Revenue Enablement)
**Purpose:** Build the next iteration of the task-centric HITL prototype for the GCL'26 keynote
**Working folder:** `/Gladly Team/GCL Keynote/hitl-prototypes/`
**Baseline to evolve:** `HITL-Task-Prototype-v5.html` (task-centric — NOT the GCL side-demo)
**Target output:** `HITL-Task-Prototype-v6.html` (single, self-contained HTML)

---

## 1. Paste this whole prompt into Claude Code

> You are helping me build **v6 of the HITL Task Prototype** for Gladly's GCL'26 keynote. This is a clickable HTML demo that will run live on stage and drop into a slide deck.
>
> **Start by reading these files in order** so you have full context:
>
> 1. `HITL-Task-Prototype-v5.html` — the current baseline. Study the task card, tabbed right panel (Task Details / Team Assist), Review Decision buttons, modals, and resolve() flow. This is the functional foundation.
> 2. `HITL-Tasks-Analysis-Apr2026.md` — the 600-line research foundation explaining WHY tasks are the right model for HITL (customer pain points, Ulta's 1.27M tasks, Aceable's Tier-2 pattern, Matt Baker's Tasks-as-conversations thesis, the cancel-order scenario).
> 3. `../GCL Keynote Demo (Team Assist) - 2026_04_17 09_00 PDT - Notes by Gemini.md` — the **latest** meeting transcript. Read lines 34-73 (ALIGNED decisions + next steps) and lines 728-1000 (the HITL prototype critique). This is the direction we're building to.
>
> Then read the Figma design via MCP:
>
> - File: `wZBpIXbq9U21IVxGZG7GNd` (SC-Template 3.4)
> - Root node: `3577-207009` ("Tasks Open" — the canonical Gladly agent desktop with a Task panel active)
> - Sub-nodes worth pulling individually: `3577-207011` (Customer List, 80px strip), `3577-207015` (Right Panel / Task Panel variant), `3577-207014` (Conversation Panel), `3577-207016` (Navigation Bar), `3577-207017` (bottom-bar)
> - Use `get_design_context` (fileKey + nodeId) with `clientFrameworks: html`. If the response is too large, use `get_metadata` first and then call `get_design_context` on sublayers.
> - Use `get_screenshot` on each node to pin down the visual.
>
> **Do not install Tailwind.** This prototype must be a single self-contained HTML file with embedded `<style>` and `<script>` blocks, matching the v5 pattern.

---

## 2. Why we're doing v6 — the direction change from Apr 17

On Apr 17, Joseph Ansanelli, Austin Reece, Matt Baker, Ellen Laux, Christina Lingga and I reviewed v5. Joseph's core critique was that the v5 prototype created a **separate list/inbox for HITL tasks**, and that is the wrong mental model. The agreed direction is:

**Use the existing Gladly Teams UI. Do not invent a new management interface.**

Concretely:

- **Customers route to the human via the standard customer list on the left** (the 80px strip with circular avatars). The routing engine prioritizes the most important customer at the top — same as today. When the routed "customer" is actually an AI-requested approval/action, the human clicks the avatar, sees the customer profile + conversation timeline + task card in the right panel, decides, and moves on.
- **Same UX as Team Assist chat.** The right-panel pattern we already have (AI presenting context + asking the human to approve/deny/modify/give feedback) IS the HITL UX. Don't build a parallel one.
- **The AI asks the human a question about a customer.** Framing: "Can you help me with this customer? Here's what's going on. Approve / deny / give me other feedback."
- **Routing model = routing model.** Multi-customer handling works the same way chat works today (min/max customers per agent, routing engine behind). You can be in a chat AND handling approvals at the same time — that's a feature, not a conflict. This was the reconciliation Joseph made to my concern about mixing decisions with conversations.
- **Drop the purple Team Assist branding.** Use standard Gladly UI colors — green-400 (#009B00) primary, Inter typography, existing tokens. Experiment with removing the "Team Assist" header and the "Beta" label (Ellen's action item: update panel color from purple back to the standard Gladly UI color scheme).
- **Inline citations, not bibliographies.** When AI cites sources (e.g., policy articles), render as inline `(1) (2) (3)` superscripts like Gemini does. No bottom-of-panel "Sources" block.
- **Continuous suggestions.** Team Assist should surface suggested next actions throughout the workflow, not just at one moment.
- **Integrate actions (Vibe Service).** The demo should show "process this return for me → AI generates the shipping label → drop into email to customer." That exchange — human asks, AI acts via API, human approves the result — is the point.

The demo flow we landed on (Austin + Joseph):

1. **Team Assist demo** (already built — agent using AI copilot mid-conversation)
2. **"Coming soon: actions within Team Assist"** (tee-up)
3. **HITL / "AI manager" prototype** — show what it looks like when a customer comes in but the human only receives an action/request surface, decides, and hands back to AI

**v6 is #3.**

---

## 3. Keep from v5, change in v6

### Keep (these work)

- The **task card in the conversation timeline** with labeled rows (Action / Item / Status / Handoff reason). Matt has said tasks should behave like conversations; this pattern reinforces that.
- The **right-panel Review Decision block** with Approve / Modify & Approve / Reject buttons and keyboard shortcuts (⌘+Enter, ⌘+M, ⌘+R).
- The three **modal flows** (approve / modify / reject) with confirmation text and optional/required notes.
- The `resolve()` state transitions — task card dot changes color, "Closed Task" label appears, conversation timeline appends an AI response and a resolved state in the right panel.
- The **Summary** structure (Inquiry / Steps taken / Handoff reason / Recommended action). Keep this structure but restyle to match Gladly tokens and add inline citations.
- **Cancel-order scenario with Rachel Thompson** ($847 Dyson V15, VIP, apartment restriction). This is the right story.

### Change (these are the Apr 17 deltas)

1. **Replace left-panel composition.** The leftmost column should be the 80px Gladly customer list strip (circular 40px avatars stacked vertically, 8px notification dots, "Task" state rendered as a navy `#0F203C` avatar with a clipboard-with-checkmark icon — see Figma node `3577-207011`). Next to it: the 360px customer profile panel (Julie-Chang-style: avatar + name, Customer since, Lifetime Value, Link to customer suggestion, Contact block with address / email / phone / social handles, Orders block with order cards). Keep Rachel Thompson as the profiled customer but restyle using the Figma pattern.
2. **Kill the purple Team Assist tab.** The right panel should match the Figma Task panel (node `3577-207015`, variant "Task Panel"):
   - Left-edge vertical tab stack: green filled Task icon tab (active), white outlined Answer icon tab
   - Header row in `#F1F1F1`: a green "●" dot, "Task For **[Assignee]**" with dropdown chevron, "Due [date] at [time]" in bold, "Close" primary-outlined pill button, overflow dots
   - Body stays white, Inter 13/1.62 black text
   - Comments use the 32px Julie avatar + bold name + regular copy pattern
   - Comment input: 32px tall, green 1px border, 4px radius, placeholder "Comment on this task"
3. **Ask AI / Team Assist becomes a context-aware drawer or secondary tab without the purple chrome.** Keep the chat functionality but style it the same as the rest of the panel. The "AI" avatar stays but uses the standard navy `#0F203C` icon-avatar pattern, not purple.
4. **Citations inline.** Rewrite the Summary block so claims like "Order value exceeds $500 auto-approve threshold" render as `...exceeds the $500 auto-approve threshold (1)` with `(1)` as a clickable inline reference that opens a small popover or scrolls to the source. No separate bibliography.
5. **Bottom bar** follows Figma: "Assigned to VIP Response Team — [Agent Name]" on the left with a small avatar, a green `+` icon button, the reply input, a "Topic" dropdown pill, a green `Close & Next` primary button on the right.
6. **Navigation bar** follows Figma node `3577-207016`: hamburger + Home link left, "+Gladly" logo centered in green, right side = message / history / "Next" pill / search / notification bell (with red badge) / user avatar.
7. **Customer-list routing state.** When the prototype loads, the 2nd avatar in the left strip is active (green background `#009B00`) representing Rachel Thompson's routed approval. Clicking a different avatar should swap the customer profile + conversation + task on the right — even if we only wire one real customer, show 2 or 3 other avatars with task-state chrome (navy + clipboard icon) so the "customers are routed into your list, not a separate inbox" story reads at a glance.
8. **Add a suggestion rail.** Somewhere in the right panel (below the summary, above Review Decision), expose 2–3 inline suggestion chips the human can tap, e.g. "Check return policy for VIPs", "See Rachel's order history", "Ask Team Assist: what's my discretion here?". These should feel like a natural part of the panel, not a purple sidecar.

### Add (new for v6 per the transcript)

- **Actions / Vibe Service moment.** After Approve, show a moment in the conversation timeline where the AI "takes action": e.g., a small timeline event card "Gladly AI processed cancellation via Commerce Cloud API — just now" with a green checkmark and a link to "View API call detail" (this can be non-functional; just read-only). Then the AI's chat reply to Rachel follows. This is what Joseph meant by "connect Team Assist to actions — process this return, generate the shipping label, drop it in the email."
- **Catch Me Up panel (optional stretch).** If bandwidth allows, add a "Catch Me Up" collapsed section at the top of the right panel that expands to a 2–3 sentence historical context summary (Jordan-style: "Rachel is a VIP customer since 2022 with $12.4K lifetime value and a clean history — this is her first cancellation in nearly 4 years"). Joseph wants this focused on historical context and purchase patterns, not a restatement of the current inquiry.
- **Feedback on AI.** Inline 👍 / 👎 thumbs on the AI's recommendation (visible in the Summary block and in any AI message in the timeline). Clicking should visually confirm (filled thumb) without opening a modal.

---

## 4. Design tokens to use (pulled from Figma SC-Template 3.4)

```css
/* Colors */
--green-400: #009B00;   /* primary */
--green-300: #64B964;   /* accent */
--red-400:   #D50E0E;   /* destructive */
--black:     #000000;
--white:     #FFFFFF;
--dark-gray-2: #4D4E4E;
--navy:      #0F203C;   /* icon-avatar bg (Task state, etc.) */
--gray-100:  #F6F6F6;
--gray-200:  #F1F1F1;   /* Task header bg */
--gray-300:  #E3E3E3;
--gray-400:  #CECECE;
--gray-500:  #B3B3B3;
--gray-600:  #919191;
--gray-700:  #767676;

/* Typography (Inter) */
--h2:   700 20px/1.0 "Inter";
--h3:   700 16px/1.0 "Inter";
--copy: 400 13px/1.62 "Inter";
--copy-bold: 700 13px/1.62 "Inter";
--button: 500 13px/1.0 "Inter";
--button-copy: 500 12px/1.0 "Inter";
--copy-small: 400 10px/1.62 "Inter";

/* Shape */
--radius-sm: 4px;    /* cards, inputs */
--radius-md: 8px;    /* containers */
--radius-pill: 20px; /* buttons */
--radius-avatar: 100px;

/* Shadows */
--shadow-sm: 0 2px 8px rgba(0,0,0,0.08);
--shadow-md: 0 4px 12px rgba(0,0,0,0.08);
--shadow-soft: 5px 5px 25px rgba(0,0,0,0.15);
```

**Do not use purple.** `#8C69F0 / #6B45D9 / #F3EFFE` were v5 Team Assist colors — explicitly remove per Ellen's action item.

---

## 5. Acceptance criteria for v6

The demo is done when:

1. Layout matches Figma node `3577-207009` at 1440×900: `nav (56) + [customer-list (80) | profile (360) | conversation (~613) | right-panel (387)] + bottom-bar (48)`.
2. No purple anywhere. All AI/task chrome reads as native Gladly green/navy/gray.
3. The left 80px strip shows 5–6 stacked customer avatars, with Rachel's (active, green background) second in the stack and at least one other showing the Task state (navy avatar + clipboard-check icon). Clicking any avatar is visibly interactive (cursor pointer + hover state) even if only Rachel has full content wired.
4. Clicking Rachel opens the current v5 content in the new chrome: customer profile populated, conversation with the task card in the middle, right panel showing Task For Tier 2 Support / Summary / suggestion chips / Review Decision buttons.
5. Inline citations render as superscript-style `(1)` after the sourced claim and open a small popover with the source title + link on click.
6. Approve flow writes the AI "took action" line in the timeline before the AI's reply to Rachel. Reject and Modify flows still work as in v5.
7. Keyboard shortcuts preserved: ⌘+Enter approve, ⌘+M modify, ⌘+R reject, Esc closes modal.
8. One copy pass — all text sounds like Gladly. No "self-checkout," no "co-pilot," no "Beta" label. The header on the right panel is just "Task For Tier 2 Support" with a chevron — no "Team Assist" wordmark.
9. The file renders cleanly in Chrome and Safari at 1440 viewport. No console errors.

---

## 6. Working notes for Claude Code

- **Iterate in place.** Write v6 as a brand-new file `HITL-Task-Prototype-v6.html` alongside v5. Do not edit v5 — I keep versions for the deck.
- **Pull Figma assets as you go.** For each region (customer list, profile panel, right panel, nav, bottom bar), call `get_design_context` on the matching sub-node, adapt the layout/spacing/typography, and inline the SVG icons directly rather than linking out to `figma.com/api/mcp/asset/...` URLs (those expire in 7 days). Use simple inline SVG that matches the shapes from the Figma screenshots.
- **Self-contained, no network dependencies.** Fonts can fall back to system: `-apple-system, BlinkMacSystemFont, 'Inter', 'Helvetica Neue', Arial, sans-serif`.
- **Check your work against the screenshots.** After each major section is built, compare visually against `get_screenshot` of the corresponding Figma node. Fix obvious mismatches before moving on.
- **Keep Joseph's principles visible in comments at the top of the file** so the next iteration doesn't regress:
  ```html
  <!--
    HITL Task Prototype v6 — Apr 17 direction
    - No separate HITL inbox. Customers route into the standard 80px list.
    - Right panel = standard Gladly Task panel, no purple, no "Beta".
    - AI asks the human about a customer. Approve / modify / reject / feedback.
    - Actions/Vibe Service moment appended to timeline on approve.
    - Inline citations, not bibliography. Continuous suggestions.
  -->
  ```
- **Ask me before adding scope.** If Figma has a pattern you want to use that isn't covered in section 3 above, propose it in a one-line summary rather than just adding it.

---

## 7. Reference files (absolute paths in Cowork, same relative paths in Claude Code)

- Baseline prototype: `HITL-Task-Prototype-v5.html`
- Analysis: `HITL-Tasks-Analysis-Apr2026.md`
- Transcript: `../GCL Keynote Demo (Team Assist) - 2026_04_17 09_00 PDT - Notes by Gemini.md`
- Earlier iterations for reference: `HITL-Task-Prototype-v1.html` through `v4.html`
- Figma file: https://www.figma.com/design/wZBpIXbq9U21IVxGZG7GNd/SC-Template-3.4?node-id=3577-207009

---

## 8. First commands I expect Claude Code to run

```
Read HITL-Task-Prototype-v5.html
Read HITL-Tasks-Analysis-Apr2026.md
Read "../GCL Keynote Demo (Team Assist) - 2026_04_17 09_00 PDT - Notes by Gemini.md" (focus on lines 34-73 and 728-1000)
mcp figma get_metadata  fileKey=wZBpIXbq9U21IVxGZG7GNd  nodeId=3577-207009
mcp figma get_screenshot fileKey=wZBpIXbq9U21IVxGZG7GNd  nodeId=3577-207009
mcp figma get_design_context fileKey=wZBpIXbq9U21IVxGZG7GNd  nodeId=3577-207011   # customer list
mcp figma get_design_context fileKey=wZBpIXbq9U21IVxGZG7GNd  nodeId=3577-207015   # right panel
mcp figma get_design_context fileKey=wZBpIXbq9U21IVxGZG7GNd  nodeId=3577-207014   # conversation
```

Then propose a 3-bullet plan for v6 and wait for my approval before writing the file.
