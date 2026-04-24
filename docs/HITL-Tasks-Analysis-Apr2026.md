# HITL × Tasks: Exploration & Analysis
## From Gladly Tasks to Human-in-the-Loop AI — Research Foundation

**Author:** Steve West, Director of Revenue Enablement
**Date:** April 1, 2026
**Status:** Exploration / Pre-PRD
**Milestone Target:** Gladly Connect Live (May 2026) — Articulate problem + solutioning feat. prototypes for Team Assist and HITL

---

## Executive Summary

This document synthesizes research across Gladly Help Center documentation, customer feedback sessions (Aceable, Shields), 24 months of internal Slack conversation analysis, Gong call transcript analysis, and product team discussions to evaluate **Gladly Tasks as the foundation for Human-in-the-Loop (HITL) AI workflows**.

The thesis: rather than building HITL as an isolated new capability, Gladly should **revamp and enhance Tasks** — already a familiar work object — so that either a human or AI can route an approval, decision, or action to an agent. This approach piggybacks off existing adoption, addresses long-standing customer pain points, and creates a natural bridge between autonomous AI and human oversight.

**Key finding:** Tasks are heavily used (Ulta alone created 1.27M tasks in one year) but significantly underinvested. Customers are vocal about limitations and actively requesting the exact capabilities that a HITL-enabled Tasks upgrade would deliver. The sentiment is not "Tasks are bad" — it's "Tasks could be so much more." That's the ideal launchpad.

---

## Part 1: Current Tasks Feature Analysis

### What Tasks Are Today (Help Center)

Tasks are work objects in Gladly that allow agents and teams to collaborate and help each other resolve customer issues. They are created and managed within the Customer Profile.

**Core capabilities:**
- Assign yourself a reminder Task with a due date (e.g., send flowers to a customer)
- Assign Tasks to colleagues (e.g., ask shipping department to confirm delivery)
- Collaborate on a Task by commenting and @mentioning others
- Tasks appear in the Conversation Timeline and Customer Tasks card

**Task interface components:**
- (A) Comments and collaboration note area for posts, comments, and updates
- (B) Task Card in the Conversation Timeline
- (C) Consolidated list of open Tasks for a Customer
- (D) Notifications Center

**Task routing window:**
- Configurable via Settings → Agent Experience → Conversation Workflow → Tasks
- Controls how soon Tasks appear on the My Customers list relative to due date
- Default: 60 minutes (i.e., Tasks appear in routing 60 minutes before due)
- Requires Administrator role

**What Tasks cannot do today:**
- Cannot be searched or filtered like conversations
- Cannot have Topics applied
- Cannot trigger Rules on creation or answer application
- Cannot be prioritized relative to other channels (email, SMS, chat)
- No time-based automations (auto-escalate, auto-reassign)
- No bulk operations
- Answers (templates) don't run on Tasks
- No API to list all open tasks across an instance
- No outcome tracking or reporting on task results
- No association with inboxes for priority differentiation

---

## Part 2: Customer Feedback Deep Dive

### 2.1 Aceable (Montie Steele) — Heavy Task User

**Usage pattern:** Certificate updates, expiration date changes, out-of-policy refunds, certificate reporting, certificate generation. Two task-heavy teams: Tier 2 task team and fulfillment team. Tasks represent 60-70% of the fulfillment inbox.

**Critical pain points:**

> "The biggest pain point is the lack of ability to control task routing. Tasks default to routing behind emails, causing task backlogs of over 7 days in Tier 2."

- Tier 2 inbox: 42+ conversations with tasks overdue by 7+ days
- Fulfillment inbox: 119 items backed up
- No ability to prioritize task routing over communications like SMS
- Agents forced to manually cherry-pick tasks because automated routing fails

**Automation gaps:**

> "Answers don't run on tasks. I can't have an internal note template that is an answer that will apply in a task."

- Cannot trigger Rules on task creation or answer application
- Forced to maintain "clunky parallel workflow for automation" outside of task creation
- Need time-based automations similar to Zendesk (auto-escalate when overdue)

**The HITL connection:** Every Aceable task is fundamentally an escalation — "a customer waiting on a do" — where a higher-powered agent needs to approve or complete something. This is precisely the HITL pattern: AI identifies an action it can't take autonomously, routes it to a human with context, and the human makes the decision.

### 2.2 Shields (Jamielyn Arndt, Aaron Mcminn, Bailey Braatz)

**Usage pattern:** Tasks for orders, address updates (higher priority), and one-star review responses (lower priority). Mixed with emails in multi-channel inboxes.

**Pain points:**

> "We have tried to manage this by locking specific tasks to inboxes and setting SLAs at the inbox level, but the tasks still were not routing correctly." — Aaron Mcminn

- Desire for task-to-inbox association for priority differentiation
- Need ability to see all open tasks (currently only visible per customer profile)
- Leadership monitoring: want to see agent action history/timeline throughout the day

### 2.3 Ulta Beauty — Enterprise Scale

**Scale:** 1.27 million tasks created in the past year vs. 2.6 million conversations (from Matt Baker in #dev-gladly-team).

**Key insight from Slack (Tammy Bordeos, #ZC:ULTA Beauty):**

> "Task Management — Their agents have 203+ follow-ups each with no way to sort/prioritize in Gladly. Currently pulling data into Tableau → Excel to manage workload across teams. They need filtering and sorting capabilities within Gladly to function as one unit."

Ulta's tasks are primarily agents scheduling follow-ups for themselves — a workaround to keep conversations open without triggering customer surveys. This reveals Tasks being used as a state management tool, not just a collaboration tool.

### 2.4 StockX — Interdepartmental Workflows

**From Alex Tsibulya (#product-gladly-team):**

> "I was on a call with StockX about their use of tasks in interdepartmental workflows. They highlighted several issues: 1. Task search 2. Ability to report on task outcomes and their trends — they want to associate an outcome with a task. Currently they associate a task outcome topic with the conversation but since tasks aren't in conversations it makes reporting on task outcomes very difficult. 3. [Topics on tasks]"

StockX also experienced tasks not routing to agents at all, requiring escalation (Ricky Vidrio, #customer-stockx, March 2026). They asked whether task/email routing priority had changed — suggesting fragility in the current implementation.

### 2.5 Crate & Barrel — Email-to-Task Conversion

**From Julia Burnett (#ZC:Crate&Barrel):**

> "Melissa would like to convert all emails in B2B inboxes into Tasks. The workflow: email comes in → automatically close → create a Task. They believe this would help with threading issues from remailers."

This shows customers independently arriving at the idea of Tasks as a more flexible, internally-routable work object — exactly the HITL vision.

### 2.6 Integration Demand — External System Connectors

Multiple customers requesting Tasks ↔ external system integrations:
- **Abercrombie:** Five9 ↔ Gladly Tasks connector (Christian Eberle)
- **StockX:** Gladly Tasks ↔ ServiceNow integration (Reshma Bynum, #ama-product)
- **Genesco:** Tasks ↔ JIRA and/or ServiceNow (Christian Eberle)
- **Narvar:** Already built Tasks integration with Gladly (Ted Stetzel, #ama-product)
- **Tymely:** API to list all open tasks on an instance (support ticket GLADLY-37069)

---

## Part 3: Gong Call Transcript Analysis — Customer Conversations About Tasks

Analysis of Gong call transcripts from current customers and active prospects discussing Gladly Tasks as a feature. Calls span from Q1 2025 through Q1 2026 across sales demos, QBRs, roadmap reviews, onboarding sessions, and CSM syncs.

### 3.1 Enterprise Customers — Tasks as Critical Workflow Infrastructure

**Abercrombie & Fitch — 2026 Roadmap Review (Jan 12, 2026)**
Rachel from A&F highlighted Tasks as a **critical unit of work** for their organization, specifically for Tier 2 escalations. She expressed a need for better task functionality and explicitly connected Tasks to the HITL vision:

> "[Gladly is] driving conversations with human touchpoints for input or approval, aiming for close collaboration between AI and agents..."
> "One of the things that does jump to mind is being able to trigger tasks from AI workflows."

A&F also asked about topics for tasks — the same request surfacing in Slack from StockX. The Gladly rep acknowledged: "We don't currently have plans around investing there." This is a gap the HITL initiative would close.

**Ulta Beauty — Weekly Sync (Mar 2, 2026)**
Discussion centered on task creation and management at Ulta's scale. Key exchange:

> "At point of task creation... if we in future want to roll it out, we can also set a specific inbox just for these tasks, just for compliments and complaints."
> "We can apply automation rules to these tasks that are created... there's a lot of room for us to play with since the support for task creation and task management within Gladly is pretty robust."

Ulta is actively exploring task-based workflows for triage — transferring information gathered by AI to human agents via task creation. This is proto-HITL behavior: AI gathers context → creates a task → human reviews and acts.

**Ulta Beauty — Belk Onsite: CX Workflow Overview (Feb 10, 2026)**
During an onsite workflow review, a specific HITL-adjacent scenario was discussed:

> "If they're using it... it's a refund, they can collect that upfront and not have to go back and forth with somebody and it's moving over as a task into the system for the agent."
> "Is there a way to — once that task is created [above a certain dollar threshold]..."

This reveals the pattern: AI/system collects information → creates a task → task routes to an agent for approval based on business rules (dollar threshold). This is the exact HITL approval flow.

**Aceable — Gladly Asks Deep Dive (Jan 8, 2026)**
Key finding from Gong summary:

> "Task Functionality: Aceable is highly frustrated with the current task experience, specifically the inability to receive priority boosts and the limited triggers/conditions/actions available for tasks within rules."

Direct customer quote on what they need:

> "Yeah, I guess I wanted more task triggers to be like — when task is created, when task is solved, something like that — like just having more task triggers that could then run an automation than just task due date... and then conditions and actions."

This is a direct articulation of the Phase 1 prerequisite: Rules engine for Tasks.

**Fullscript — Multi-Brand Onsite (Apr 3, 2025)**
A Fullscript team member stated plainly:

> "There's just like some limitations for us to tasks that are pretty big pain points, like being able to report on them, search them and that kind of stuff."

Their asks centered on auto-creating/auto-assigning tasks — automation that would be foundational to AI-initiated task creation.

**Fullscript — QBR (Sep 11, 2025)**
Callan Levine (CSM) noted:

> "Two of the features within tasks — one of them was auto creating or auto assigning tasks..."

Fullscript's repeated requests across multiple calls signal that task automation is a retention-relevant issue for mid-market accounts, not just enterprise.

**Wine Enthusiast — Renewal Review (Jan 12, 2026)**
Callan asked directly about task usability:

> "Is some of the feedback from the team around like — tasks aren't the easiest to use? Or is it like escalation within tasks?"

The customer's response revealed that task users (warehouse team) view tasks as "another thing they have to monitor" — an adoption friction point that a cleaner, more powerful UX would address. Their task user count fluctuates as teams onboard and disengage.

**Pair Eyewear — Monthly Meeting (Jan 28, 2026)**
Callan noted:

> "Task cleanup — like task has been a big conversation for a lot of my customers and those have been a lot of items that have been pushed..."

This confirms Tasks is a recurring pain point across Callan's entire book of business, not isolated to one account.

### 3.2 Prospect Demos — How Tasks Are Positioned in Sales

Across prospect demo calls, Tasks is consistently positioned as a **key differentiator** for internal collaboration and escalation workflows:

**Obagi Cosmeceuticals — Reporting Demo (Jan 9, 2026)**

> "Internal Collaboration (Tasks): Gladly supports internal collaboration for workflows like refund approvals or new account onboarding via 'Tasks,' which are tracked on the conversation timeline, have assignable SLAs, and are reportable, without disrupting the customer experience."

Tasks is being sold as an approval workflow tool. The HITL upgrade would make this pitch true at a deeper level.

**BaubleBar — Demo Part 2 (Jan 29, 2026)**
Customer asked directly about task automation for escalations:

> "For escalations, we currently manually tag anything that needs like a manager escalation. Could you like auto-tag if something is requested from like gen [AI]?"
> "Meaning if a task was created by gen here... that for tracking and/or auto assign a task as a part of that workflow."

BaubleBar is independently describing the HITL pattern: AI creates a task, auto-assigns it, and tracks the outcome. This validates market demand even from prospects who haven't seen the capability.

**Mejuri — Agent-side Experience (Dec 9, 2025)**

> "Tasks can really be part of a workflow as well... if I assigned to the escalation inbox automatically, a task can be created on that profile."
> "This is in my opinion, a more sophisticated, more improved upon version of the snooze feature."

Tasks positioned as workflow automation primitives — exactly the framing needed for HITL.

**LuxyRide — Demo (Nov 24, 2025)**

> "Task Management & Escalations: Tasks can be created and assigned to specific agents or inboxes (e.g., for refund approvals or partner inquiries) with associated SLAs, allowing for parallel workflows and clear accountability."
> "Best practice would be a task because it is an SLA associated with [it]."

**Riot Games — Demo (Mar 23, 2026)**
Kevin (Gladly SE) explicitly demonstrated the task-as-approval pattern:

> "Task users only — where those task users have access to tasks. So if they maybe need to get approval from someone in a completely different part of the business who's not going through and responding to customers, you can confirm with them as a task user."
> "And that's the task functionality that Kevin showed [for when] a human agent who needs help but doesn't need to transfer yet."

This is almost a verbatim description of HITL: a human agent (or AI) needs help from another human, uses a task to route the request.

**Wonderbly — Demo (Mar 10, 2026)**

> "Is it possible to use Gladly for internal workflow automations as well — adding topics, automatically, creating tasks?"
> "Maybe it's a delivery delay, then we want to maybe add a task that's going to be due in two hours. We're going to select it to escalations..."

**Metropolis — Demo Part 2 (Jun 25, 2025)**
Customer described an explicit approval threshold scenario:

> "If it's over 40 dollars, if that's the rule that it requires an approval from some type of human, what I would like is to be able to generate or populate the reason... and the ability for a human to monitor multiple approvals."

This is the clearest Gong evidence of a prospect describing exactly the HITL approval UX we need to build.

### 3.3 Alo Yoga — Tasks + AI Integration Complexity

**Alo Yoga — SK Series (Feb 6, 2026)**
Alo Yoga's use case reveals a more complex task landscape — they are validating tasks across both Gladly and Sierra:

> "We will need to verify any kind of tasks from Gladly or Sierra. If it is a missing item, be it a Gladly or Sierra task, if there is a missing item task, we will need to say that... if there's already an open task about it."

This highlights that tasks exist in a multi-AI-vendor context. An upgraded Tasks system that can serve as the universal work object for any AI (Gladly or third-party) would be a competitive advantage.

### 3.4 MANSCAPED — Task-Oriented Routing

**MANSCAPED — Routing & Sidekick QA (Jun 24, 2025)**

> "MANSCAPED is considering task-oriented skills routing over regional specialties."

This is significant: a customer is actively choosing to organize their routing around task types rather than geographic regions. It validates that customers see tasks as a routing-worthy entity and want the same routing sophistication applied to tasks that exists for conversations.

### 3.5 Gong Analysis Summary

| Pattern | Frequency | Customer Evidence |
|---------|-----------|-------------------|
| **Tasks as escalation/approval workflow** | Very High | A&F, Ulta, Obagi, LuxyRide, Riot Games, Metropolis, BaubleBar |
| **Frustration with task automation limitations** | High | Aceable, Fullscript, Pair Eyewear, Wine Enthusiast |
| **Customers independently describing HITL pattern** | Medium-High | BaubleBar ("AI creates task"), Metropolis ("human approval threshold"), Ulta ("task creation from AI triage") |
| **Tasks as sales differentiator in demos** | Very High | Present in nearly every prospect demo reviewed |
| **Request for task search, reporting, topics** | High | A&F, StockX, Fullscript, Aceable |
| **Task routing parity with conversations** | Medium | MANSCAPED, Aceable, StockX |
| **Multi-vendor task landscape** | Emerging | Alo Yoga (Gladly + Sierra tasks) |

**The Gong data reinforces the Slack analysis and adds a critical dimension: prospects are being sold on Tasks as an approval and escalation workflow tool, but the current product can't fully deliver on that promise.** Upgrading Tasks for HITL doesn't just serve AI — it closes the gap between how Tasks are sold and how they actually perform.

---

## Part 4: 24-Month Slack SWOT Analysis — Gladly Tasks (Internal)

### Strengths

| Signal | Source | Evidence |
|--------|--------|----------|
| **High adoption at scale** | Matt Baker, #dev-gladly-team | Ulta: 1.27M tasks/year. Tasks are not a niche feature — they're core workflow. |
| **Understood mental model** | Multiple customers | Agents intuitively understand "assign a task to someone." No training gap. |
| **Cross-departmental bridge** | StockX, Aceable, Crate&Barrel | Tasks connect CX to fulfillment, Tier 2, B2B, QA — beyond just agent-to-agent. |
| **Existing licensing model** | Emilio Di Zazzo, #ZC:Wing | Task User license already exists as a distinct SKU — pricing and packaging groundwork done. |
| **Integration momentum** | Narvar, Five9, Tymely | Third parties are already building connectors to Tasks, validating the object's importance. |
| **Internal tooling exists** | Dirk Kessler, #product-gladly | "I have created an app platform app that can create Gladly tasks... could use something like that in a Guide to create tasks." |
| **Customer satisfaction with Gladly overall** | Revolve (Tammy Bordeos) | Customers who use Tasks heavily (Revolve: "she's really happy with us") aren't leaving — they're asking for more. |

### Weaknesses

| Signal | Source | Evidence |
|--------|--------|----------|
| **Routing parity gap** | Aceable (Montie Steele) | Tasks deprioritized behind emails/SMS. 7-day backlogs. No channel-level priority control. |
| **No searchability** | StockX, Aceable, Shields | Cannot find or filter tasks like conversations. Matt Baker confirmed: "If tasks are searchable, that would solve a lot of workflow problems." |
| **No topic association** | StockX (Alex Tsibulya) | Can't attach topics to tasks → no outcome reporting, no rule triggering, no trend analysis. |
| **No automation hooks** | Aceable (Montie Steele) | Rules don't fire on task creation. Answers don't apply. No time-based automations. |
| **No bulk operations** | MyHeritage (Shlomi), ai-hackathon | Hackathon team built a tool to close tasks in bulk because the platform can't. MyHeritage flagged as "must have." |
| **API limitations** | Tymely (GLADLY-37069) | Cannot list all open tasks via API. Only per-customer. Support recommended "Task Export reporting" as workaround. |
| **Historical underinvestment** | Matt Baker | "We made a decision a long time ago. We shipped it to focus away. We didn't put much additional on it." |

### Opportunities

| Signal | Source | Evidence |
|--------|--------|----------|
| **HITL as Tasks 2.0** | Steve West thesis | AI-generated tasks = natural extension. Same mental model, new initiator (AI instead of human). |
| **Functional parity with Conversations** | Matt Baker | "Squinting, it feels like tasks and conversation should just more or less be the exact same... Task is all internal workflow. Conversation is all public facing workflow." |
| **Task search on roadmap** | Steve West, #team-dab-leads | "Enhanced workspace — dark mode, task search, topics, etc." already listed alongside Team Assist and HITL. |
| **Enterprise expansion lever** | Ulta, StockX, Aceable | Largest accounts are the most vocal about Tasks. Fixing Tasks = retaining and expanding enterprise. |
| **Integration platform play** | Genesco, Abercrombie, StockX | Tasks ↔ JIRA/SNOW/Five9 makes Gladly the workflow hub, not just the CX tool. |
| **GCL demo moment** | Milestone | Showing "Tasks, but supercharged — now AI can create and route them too" is a tangible, demo-able story. |
| **Packaging with Team Assist** | Nidhi Nair DM | "Sounds like we are packaging Team Assist and human in the loop functionality together — which is smart." |

### Threats

| Signal | Source | Evidence |
|--------|--------|----------|
| **Churn risk from inaction** | Zenni Optical (Kristen Miller) | "We may not need to review Gladly tasks with QA because we plan to be off of Gladly in 2025." |
| **Workaround sprawl** | Ulta | Pulling task data into Tableau → Excel. Every workaround is a retention risk and a signal of unmet need. |
| **Competitive pressure** | Breeze Airways | CEO wants "Machine-First" 90% AI containment. If Gladly can't show AI-human handoff, competitors will. |
| **Internal pressure to rename/rebrand Tasks** | Steve West, Christina Lingga | Matt Baker "sort of liked the idea of task but not using tasks specifically" — risk of fragmenting the model by creating a parallel object. Mitigation: invest in making Tasks *so much better* that the upgrade speaks for itself. |
| **Product team bandwidth** | Historical pattern | Tasks have been deprioritized for years. Risk that HITL also gets scoped down. |

---

## Part 5: Capability ↔ Sentiment Alignment Matrix

| Customer Need | Current Tasks Capability | Sentiment | HITL Upgrade Required |
|---|---|---|---|
| Route work to the right human | Basic due-date routing window | 🔴 Frustrated — backlogs, no priority control | Full routing parity with conversations: channel priority, inbox association, SLA-aware routing |
| Search and find tasks | Not available | 🔴 Vocal demand from enterprise | Task search with conversation-like filters |
| Track outcomes and report | No topics, no outcome association | 🔴 StockX building workarounds | Topics on tasks, outcome fields, reporting integration |
| Automate task workflows | No rules, no answers, no time-based triggers | 🔴 Aceable maintaining parallel systems | Rules engine for tasks, answer support, time-based automations |
| AI creates a task for human review | Not possible natively | 🟡 Latent — customers haven't asked because they don't know it's possible | Guide/Workflow step that creates a task with AI context, routes to human |
| Human approves/rejects AI recommendation | Does not exist | 🟡 Ulta actively requesting HITL walkthrough | Approval UX within task: approve/reject/modify with context panel |
| Bulk manage tasks | Not available | 🔴 Hackathon team built workaround | Bulk select, reassign, close, prioritize |
| Integrate with external systems | Limited API, no webhook support for tasks | 🟡 Multiple integration requests | Full CRUD API, webhooks on task lifecycle events |

**The pattern:** Every red-sentiment item is a prerequisite for HITL. Fixing Tasks for humans automatically builds the infrastructure AI needs.

---

## Part 6: PRD Pathway — Tasks 2.0 as HITL Foundation

### Vision Statement

Tasks evolve from a simple reminder/collaboration tool into **Gladly's universal work routing object** — the mechanism by which any entity (human agent, AI, external system, or workflow) can route a decision, approval, or action to any other entity within Gladly. This positions HITL not as a bolt-on feature but as a natural capability that emerges from a more powerful Tasks system.

### Phased Approach

#### Phase 1: Tasks Foundation (Pre-GCL, 1-3 months post)
*Goal: Fix what's broken, earn trust, build the infrastructure HITL needs*

1. **Task Search & Filtering** — Make tasks searchable with filters matching conversations (by status, assignee, due date, inbox, customer). Already on the Enhanced Workspace roadmap.

2. **Topics on Tasks** — Allow topic association on tasks for outcome tracking and rule triggering. Directly addresses StockX and Aceable needs.

3. **Task Routing Parity** — Tasks route with the same priority controls as conversations. Inbox association, SLA-aware routing, priority boost capability. Fixes the #1 cross-customer pain point.

4. **Rules Engine for Tasks** — Rules fire on task creation, task assignment, answer application within tasks, and task completion. Enables automation without parallel systems.

5. **Answers in Tasks** — Templates/Answers are usable within Tasks. Removes the "clunky parallel workflow" Aceable described.

#### Phase 2: AI-Initiated Tasks (HITL Core, 3-6 months)
*Goal: Enable AI to create and route tasks to humans — the HITL primitive*

6. **AI Task Creation via Guides/Workflows** — A Workflow step or Guide action that creates a task with: AI-generated context summary, recommended action, confidence score, and relevant customer/conversation data pre-populated.

7. **Approval UX** — Within a task, an agent sees: what the AI recommends, why it recommends it, what information it used, and action buttons (Approve / Reject / Modify). This is the core HITL interaction.

8. **Task-to-Conversation Linking** — Tasks created from AI during a conversation maintain a live link back to the originating conversation. Agent can see full context without tab-switching.

9. **AI Feedback Loop** — When a human approves/rejects/modifies an AI recommendation via a task, that decision feeds back into the AI system for learning. Outcome data flows into reporting.

10. **Time-Based Escalation** — If a human doesn't act on an AI-generated task within a configurable window, the system escalates (reassign, notify manager, or allow AI to proceed with default action).

#### Phase 3: Universal Work Object (6-12 months)
*Goal: Tasks become the platform's internal routing backbone*

11. **External System Integration** — Full CRUD API + webhooks for task lifecycle events. Enables JIRA, ServiceNow, Five9, and custom integrations.

12. **Bulk Operations** — Bulk select, reassign, close, re-prioritize tasks.

13. **Task Templates** — Pre-configured task types (Approval, Review, Escalation, Follow-up) with structured fields, required actions, and routing rules.

14. **Bi-Directional AI** — AI can both create tasks for humans AND pick up tasks created by humans (e.g., "Research this customer's order history and summarize" → AI completes → human reviews).

15. **Reporting & Analytics** — Task volume, resolution time, approval rates, AI recommendation accuracy, human override patterns.

### What Must Be True for Phase 2 (HITL Core)

For the GCL demo scenario to work, these are the minimum requirements:

1. AI (via a Guide or Workflow) can programmatically create a Task
2. That Task routes to a specific agent or inbox with priority
3. The Task contains AI-generated context (what happened, what's recommended, why)
4. The agent can take an action (approve/reject/modify) that resolves the Task
5. The action outcome is captured and can trigger downstream behavior

**Dirk Kessler has already built an app platform app that creates Gladly Tasks** (#product-gladly, Aug 2025). This validates that the API surface exists — the work is in the UX and routing layer.

---

## Part 7: GCL Demo Scenario Design Considerations

### Recommended Scenario: Cancel Order with AI Confidence Threshold

This scenario was already surfaced by Ulta in their HITL review request (Christian Lathrop, #ZC:ULTA Beauty):

> "We want to walk through the flow for the Cancel Order Sidekick Action use case: 1. Customer initiates a cancel order request across one of the four channels — Chat, Email, Voice, or SMS/Text..."

**Flow:**
1. Customer requests order cancellation via chat
2. Gladly AI (via Guide) evaluates: order status, cancellation policy, customer history, order value
3. AI determines this requires human approval (e.g., order is high-value, partially shipped, or VIP customer)
4. AI creates a **Task** with: customer context, order details, recommended action ("Approve full cancellation + $25 credit"), confidence score, and reasoning
5. Task routes to Tier 2 inbox with appropriate priority
6. Agent opens Task, sees AI recommendation panel alongside customer profile
7. Agent approves with one click → AI executes cancellation and notifies customer
8. OR Agent modifies ("Approve cancellation, no credit") → AI executes modified action
9. OR Agent rejects ("Contact customer for more info") → AI creates follow-up

**Why this scenario works for GCL:**
- Cancel order is universally understood
- It naturally involves a decision point (approve/deny)
- It demonstrates AI + human working in concert, not AI replacing human
- It maps directly to how customers already use Tasks (Aceable's escalation pattern)
- Ulta has already asked for exactly this walkthrough

---

## Part 8: Prototyping Guidance

### Approach 1: HTML Prototypes via Claude Code (Recommended for Speed)

Claude Code can generate interactive HTML prototypes that demonstrate the HITL Task UX. This is the fastest path to something showable.

**What to build:**
- **Prototype A — Agent Task View:** An HTML mockup of the Gladly agent desktop showing a Task created by AI. Includes: AI context panel (recommendation, confidence, reasoning), action buttons (Approve/Reject/Modify), customer profile sidebar, conversation history link.
- **Prototype B — Task Creation Flow:** Shows the AI's perspective: evaluating a conversation, determining HITL is needed, creating a Task with pre-populated fields.
- **Prototype C — Manager Dashboard:** Shows task queue with AI-generated tasks, filtering by status, priority, AI confidence level.

**How to execute:**
1. Use Gladly's existing design system (colors, typography, component patterns) as reference — the Help Center screenshots and existing Gladly Team UI provide the visual language
2. Build as self-contained HTML files with embedded CSS/JS (no dependencies)
3. Make them interactive: clickable approve/reject buttons, expandable context panels, simulated routing
4. Claude Code can iterate rapidly — describe a change, get an updated prototype in seconds

**Deliverable format:** `.html` files that open in any browser. Can be screenshared, embedded in decks, or hosted for stakeholder review.

### Approach 2: Figma Prototypes via Figma MCP

Claude has access to the Figma MCP connector, which can:
- Read existing Gladly design files for component reuse
- Search the Gladly design system for tokens, components, and patterns
- Generate design context for building new screens

**Recommended workflow:**
1. Use `search_design_system` to pull Gladly's current component library
2. Use `get_design_context` on existing Task-related screens in Figma
3. Have Christina build in Figma using the design system, informed by the HTML prototypes as functional specs
4. HTML prototypes serve as the "what it does" reference; Figma becomes the "what it looks like" deliverable

### Approach 3: Hybrid (Best for GCL)

1. **Steve + Claude Code** → Build functional HTML prototypes this week to validate the UX flow and get alignment
2. **Christina in Figma** → Once flows are validated, Christina translates to pixel-perfect Figma prototypes using Gladly's design system
3. **GCL presentation** → Use the HTML prototypes for live demo; Figma screens for the deck

### Getting Started Immediately

To generate a first prototype in this session or the next:
1. Provide or describe the Gladly agent desktop layout (or point to a Figma file/screenshot)
2. Define the specific Task fields for the HITL approval UX
3. Claude Code will generate an interactive HTML prototype
4. Iterate: "make the confidence score more prominent," "add a conversation history sidebar," etc.

---

## Part 9: Key Stakeholder Quotes — Internal Alignment Evidence

**Matt Baker (Head of Product) on Tasks = Conversations:**
> "Squinting, it feels like tasks and conversation should just more or less be the exact same... Task should have topics on them. Task should — whatever almost a conversation can do, a task can do, except it's just the internal version of a conversation."

**Matt Baker on HITL model:**
> "Team assist, described as a self-checkout model for AI support — where agents could maybe help out when AI runs into a roadblock. Basically the idea of: should I do path A, path B, or do something different?"

**Matt Baker — Cross-Customer Distillation (DM with Steve West):**
> "Task routing and prioritization [was] the single biggest pain point across multiple customers. Both Aceable and Scheels have tier 2 or fulfillment teams that are days behind on tasks because there's no way to boost tasks or control their priority relative to other channels."

**Nidhi Nair on packaging:**
> "Sounds like we are packaging Team Assist and human in the loop functionality together — which is smart."

**Steve West on HITL = Tasks evolution (DM with Christina):**
> "Right now tasks are work one agent can't do and need a dedicated human to do. HITL is that but the AI can't do it initially."

**Christina Lingga on Matt's reaction:**
> "He sort of liked the idea of task but not using tasks specifically... which I am confused about."

*Note: This last quote is important context. Matt may envision HITL as a new object type that shares Task DNA but isn't literally "Tasks v2." The PRD should account for both paths — enhancing existing Tasks vs. creating a new "AI Work Item" that inherits Task capabilities. The argument for using Tasks directly: adoption friction is lower, licensing model exists, customers already understand the concept, and the infrastructure investment benefits both HITL and non-HITL use cases.*

---

## Part 10: Naming — It's Just Tasks

The central thesis of this analysis is that HITL doesn't need a new name, a new object, or a new brand. The answer already exists: **Tasks**.

Tasks are Gladly's routable, assignable, SLA-tracked work object. They live on the conversation timeline. Agents already know how to pick them up, act on them, and close them. The only thing that changes is *who can create them* and *what context they carry*. Today, a human creates a Task and routes it to another human. Tomorrow, an AI creates a Task and routes it to a human — or a human creates a Task and routes it to an AI. The object is the same. The workflow is the same. The muscle memory is the same.

This matters because every alternative name — Checkpoints, Approvals, AI Reviews, Gladly Loop — implicitly introduces a *separate concept* that fragments the model. Matt Baker's reaction ("sort of liked the idea of task but not using tasks specifically") is exactly the instinct this analysis argues against. Creating a new work object alongside Tasks doesn't simplify — it doubles the surface area agents need to learn, PMs need to spec, and engineers need to build. It also orphans the 1.27M tasks Ulta already creates per year and the task-based workflows every prospect is being sold on today.

**What changes about Tasks for HITL:**

The Task object gets richer, not renamed. Specifically:

- **Creator attribution** — Tasks display whether they were created by a human, an AI agent (via Guides), or an external system (via API). This is metadata on the Task, not a different object type.
- **AI context block** — When an AI creates a Task, it attaches structured context: the recommendation, confidence score, reasoning, and linked conversation. This renders as a card in the Task timeline, the same way comments render today.
- **Action outcomes** — Tasks gain discrete resolution states beyond "complete" (Approved, Modified, Rejected) so the AI can learn from the human decision and reporting can track approval patterns.
- **Bi-directional routing** — Tasks can route to AI agents, not just human agents. A human creates a Task ("Research this customer's order history") → AI picks it up → completes it → human reviews. Same object, new participants.

**How this maps to the product narrative:**

The feature set lives under **Team Assist** as a parent capability. Within Team Assist, the capability categories are:

- **Response Assist** — AI helps draft responses (existing)
- **Knowledge Check** — AI surfaces relevant knowledge (existing)
- **Task Assist** — AI creates, enriches, and acts on Tasks (new — this is the HITL capability)

The name "Task Assist" does the work without inventing vocabulary. It signals that Tasks got smarter, not that something new appeared. When a prospect asks "what's the human-in-the-loop story?" the answer is: "AI creates a Task, routes it to the right person, and that person approves, modifies, or rejects — all within the same Task workflow your agents already use."

**Why this framing wins at GCL:**

"We upgraded Tasks" is a better demo story than "We built a new thing." The audience already understands Tasks from their own Gladly instance or from the demo. Showing that AI can now *create* Tasks — with rich context, confidence scores, and structured outcomes — lands immediately. There's no conceptual overhead. The crowd sees a familiar object doing something new, which is more impressive and more credible than an unfamiliar object doing something unfamiliar.

**Addressing the Matt Baker concern directly:**

The risk in Matt's "not using tasks specifically" instinct is that it leads to building a parallel work object that competes with Tasks for agent attention, engineering investment, and product narrative. This analysis recommends the opposite: invest deeply in Tasks so they become the universal work object. If the Task UI looks and feels meaningfully better — richer context, smarter routing, AI-native metadata — the "not using tasks" concern dissolves because the upgraded Task *is* the new thing. It just has the right name already.

---

## Part 11: Recommended Next Steps

### This Week (Pre-Tomorrow's Session)
1. ✅ Complete this analysis (done)
2. Share with Christina for context before prototype work begins
3. Define the cancel-order HITL scenario in detail (fields, states, transitions)
4. Generate first HTML prototype of the Agent Task View with AI context panel

### Before GCL (May 2026)
5. Align with Matt Baker on whether HITL uses enhanced Tasks or a new object type (address the Christina/Matt quote)
6. Get Austin's input on technical feasibility for Phase 1 items
7. Complete 2-3 interactive prototypes covering the full HITL flow
8. Christina delivers Figma prototypes for GCL presentation
9. Draft the GCL demo script around the cancel-order scenario

### Post-GCL (1-3 Months)
10. Ship Task Search and Topics on Tasks (already on roadmap)
11. Ship Task Routing Parity (addresses the #1 customer pain point)
12. Begin Phase 2 engineering: AI Task Creation via Guides

---

## Appendix A: Data Sources

| Source | Type | Key Content |
|--------|------|-------------|
| Gladly Help Center — "What is a Task?" | Product documentation | Feature overview, interface components, notifications, mentions |
| Gladly Help Center — "Configure Task Routing Window" | Product documentation | Routing window configuration (Admin only) |
| Google Doc — Aceable customer feedback | Customer conversation transcript | Montie Steele: routing, automation, prioritization pain points |
| Google Doc — Shields customer feedback | Customer conversation transcript | Jamielyn Arndt, Aaron Mcminn: routing, visibility, SLA issues |
| Slack: #dev-gladly-team | Internal product discussion | Matt Baker: Ulta 1.27M tasks, Task-Conversation parity vision |
| Slack: #product-gladly-team | Internal product discussion | Alex Tsibulya: StockX interdepartmental task workflows |
| Slack: #product-gladly | Internal product discussion | Dirk Kessler: App platform app for task creation |
| Slack: #ZC:ULTA Beauty | Customer channel | Tammy Bordeos: 203+ follow-ups, no sort/prioritize; HITL review request |
| Slack: #ZC:Crate&Barrel | Customer channel | Julia Burnett: Email-to-Task conversion request |
| Slack: #customer-stockx | Customer channel | Ricky Vidrio: Task routing bugs, priority issues |
| Slack: #ZC:Aceable | Customer channel | Callan Levine: Task backlog recap, 60-70% fulfillment inbox |
| Slack: DM Steve West + Matt Baker | Internal alignment | Cross-customer themes distillation; HITL Gong analysis |
| Slack: DM Steve West + Nidhi Nair | Internal alignment | Team Assist + HITL packaging; naming framework |
| Slack: DM Steve West + Christina Lingga | Internal alignment | Matt Baker's reaction to Tasks-as-HITL concept |
| Slack: DM Steve West + Austin Reece | Internal alignment | Naming framework; Team Assist capability list |
| Slack: #farm-for-dissent | Internal review | Steve West: Team Assist PRD and HITL naming POV shared |
| Slack: #team-product-private | Internal coordination | Team Assist crit pre-read and demo org setup |
| Gong: Aceable — Gladly Asks Deep Dive | Customer call (Jan 8, 2026) | Task frustration, limited triggers/conditions/actions for tasks in rules |
| Gong: A&F — 2026 Roadmap Review | Customer call (Jan 12, 2026) | Tasks as critical work unit, need for AI-triggered tasks, topics on tasks |
| Gong: Ulta — Weekly Sync | Customer call (Mar 2, 2026) | Task creation/management at scale, automation rules for tasks, inbox routing |
| Gong: Ulta — Belk Onsite | Customer call (Feb 10, 2026) | Task creation from AI triage, dollar-threshold approval workflow |
| Gong: Fullscript — Multi-Brand Onsite | Customer call (Apr 3, 2025) | Task limitations: search, reporting, auto-assign |
| Gong: Fullscript — QBR | Customer call (Sep 11, 2025) | Auto-creating/auto-assigning tasks feature request |
| Gong: Wine Enthusiast — Renewal Review | Customer call (Jan 12, 2026) | Task usability concerns, fluctuating task user adoption |
| Gong: Pair Eyewear — Monthly Meeting | Customer call (Jan 28, 2026) | Task cleanup as recurring customer pain across book of business |
| Gong: BaubleBar — Demo Part 2 | Prospect call (Jan 29, 2026) | AI-created tasks for escalations, auto-tag from AI |
| Gong: Obagi — Reporting Demo | Prospect call (Jan 9, 2026) | Tasks for refund approvals and onboarding workflows |
| Gong: Mejuri — Agent-side Experience | Prospect call (Dec 9, 2025) | Tasks as workflow automation primitives |
| Gong: LuxyRide — Demo | Prospect call (Nov 24, 2025) | Tasks for refund approvals with SLAs |
| Gong: Riot Games — Demo | Prospect call (Mar 23, 2026) | Task users for cross-department approvals, HITL-adjacent demo |
| Gong: Metropolis — Demo Part 2 | Prospect call (Jun 25, 2025) | Explicit approval threshold scenario, human monitoring multiple approvals |
| Gong: Wonderbly — Demo | Prospect call (Mar 10, 2026) | Internal workflow automation via tasks |
| Gong: MANSCAPED — Routing & QA | Customer call (Jun 24, 2025) | Task-oriented skills routing preference |
| Gong: Alo Yoga — SK Series | Customer call (Feb 6, 2026) | Multi-vendor task landscape (Gladly + Sierra) |
| App Actions memory.md | Prior session context | Custom Actions, App Platform, Guides framework background |

## Appendix B: Aceable Shared Screenshots Context

The Aceable org screenshots shared in the Gladly team folder show Tasks operating in the live agent desktop context — demonstrating how agents currently see and interact with Tasks alongside conversations. These provide baseline UX reference for prototype design, showing the current Task card layout, comment threading, and how Tasks appear in the Conversation Timeline within a real customer profile.

---

*This document should be treated as a living research artifact. Updated as new customer data, product decisions, and prototype iterations emerge.*
