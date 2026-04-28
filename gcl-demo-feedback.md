# **Tab 1**

# **GCL Demo Feedback — April 24 Walkthrough**

Participants: Steve West, Matt Baker, Christina Lingga  
Use this to work through changes with Claude Code

---

## **1\. TEAM ASSIST — Flows, Actions & Panel Elements**

### **Panel Orientation & Flow Order**

- [ ] **Remove the action step from the first scenario** — Matt's point: don't do double actions; actions are the crux of the HITL end section. Keep them distinct.  
- [ ] **Proactive mode** — Demo should jump in with catch-me-up already triggered; make the transition from AI summary to proactive recommendation feel like an obvious segue.  
- [ ] **Pre-populated buttons** — Should load based on conversation context at the point in the flow where they appear.

### **HITL Plan Mode (Matt's main flow note)**

- [ ] **Adopt a "plan mode" pattern** (modeled after Claude Code plan mode):  
      - Step 1: Show the full plan upfront (e.g., "Cancel order \+ apply $25 credit") as a consolidated block  
      - Step 2: If user types a modification (e.g., "increase to $100"), collapse the old plan and show updated plan as new block with changed line highlighted  
      - Step 3: Confirm button should feel like "does this new plan look good?" not "approve again after already saying go"  
      - Goal: Iteration feels like refining a plan, not re-approving from scratch each time

### **Actions in the Flow**

- [ ] **Remove action step from Team Assist (first) scenario** — reduces duplication and lets HITL section own the action narrative  
- [ ] **Streamline audit events** — Currently too many raw audit lines. Options:  
      - Option A: Convert to a single feed item (e.g., "Joseph approved exception — \[summary of what ran\]")  
      - Option B: Remove entirely for demo purposes if design solution isn't ready in time  
- [ ] **"Process your return" button** — Should this trigger a plan view inline rather than just a button label? Consider: showing "here's what I'll run" before the button resolves.  
- [ ] **"Use" button on answer cards** — Sends directly to composer, skipping composer step. Confirm this is intentional per demo flow (Matt noted the step felt unnecessary).

### **HITL Experience — Broader Concerns (not blocking demo but flag for product)**

- [ ] **AI ownership not visually clear** — Customer should read as assigned to Gladly AI, not to Joseph. Add visual indicator like "AI agent waiting your input" or similar signal.  
- [ ] **Context overload** — Current HITL prompt is too dense. Goal: minimal context, deeply relevant, fast decision. Anything on screen that requires reading \= distraction.  
- [ ] **Consider: move HITL outside the Gladly app UI for demo** — Matt's suggestion: illustrate via text message or notification-style interface to sidestep "where does this live in the app" debate and emphasize it works anywhere.

---

## **2\. GLADLY UI — Workspace UX Updates & Bugs**

### **Contrast / Display**

- [ ] **Recommendation cards are too subtle** — Gray backgrounds wash out on projectors. Contrast adjustment isn't affecting the Team Assist chat panel — fix so contrast toggle hits everything including recommendation blocks.  
- [ ] **Austin's ask**: Colors should be quickly adjustable before GCL.

### **Left Panel / Customer Info**

- [ ] **Remove duplicate contact info** — Phone number, SMS, main, mobile, SMS preferred are all listed. Clean up: remove SMS label, remove "main," keep mobile only.  
- [ ] **Remove "Link to customer"** — Already linked; the UI element is redundant.  
- [ ] **Consider reordering**: Orders block may be more relevant than contact info at the top. Could allow reordering.  
- [ ] **Lifetime value placement** — Currently next to name; evaluate if that's the right location.

### **Header / Chrome**

- [ ] **Remove dark mode icon from header** — Per Matt; settings access should live under the user avatar/initials (e.g., under "J").  
- [ ] **Contrast toggle** — Keep as-is (Matt confirmed he realized it was a settings thing, not a persistent UI element).

### **Team Assist Panel — Visual / UX**

- [ ] **Three-tab structure** — Third tab only appears when customer has a task. Drop it from default view to reduce clutter.  
- [ ] **Icons** — Some icons are "wonky" per Matt; clean up icon set in the panel.  
- [ ] **Buttons vs. visual elements** — Be consistent: when is something tappable vs. display-only? (Example raised: "Process your return" looks tappable but behavior is unclear.)  
- [ ] **Plus button off-center** on the circle — minor but noted.  
- [ ] **Topic picker pushed far left** — Greg's implementation puts it next to assignment; should be repositioned closer to expected location per design.

### **Conversation Feed**

- [ ] **"Gladly AI transfer" bubble** — Matt noted the UX is nice but the text position (should be on right per Gladly convention for AI-generated items) looks off. Confirm alignment.  
- [ ] **Left rail shows "chat, chat, chat, chat"** — Every conversation labeled generically. Will be resolved when panel is minimizable — confirm that's scoped.

### **General / Layout**

- [ ] **Left side artifact elements** — Steve noted lingering elements from the Claude Code prototype. Remove anything not part of the agreed Gladly UI frame.  
- [ ] **Sentiment score format** — Currently shows something like \-0.6; confirm scale. Matt's suggestion: 0–5 or 0–10 are more recognizable. NPS is 0–10. Pick one and use it consistently.  
- [ ] **"Gladly AI" branding** — Matt noted it should read "Gladly AI" not "gladly" in lowercase or without qualifier. "Summary created automatically by Gladly AI" is the correct format.  
- [ ] **Command+zoom scaling** — Matt tested; confirmed it scales well at 1400×900 spec. No action needed.

---

## **3\. CONTENT — Messaging, Storyline & Customer Profile**

### **Demo Narrative / Storyline**

- [ ] **Story arc clarity** — Three acts need clear breaks:  
      1. "Here's Team Assist today" (existing capabilities)  
      2. "Here's where it's going" (future actions — framed as coming, no timeline commitment)  
      3. "Here's where the industry is headed" (HITL — exploratory vision, all within Team Assist)  
- [ ] **Don't make HITL feel like a separate product** — Joseph's direction: one unified surface. Matt agrees it shouldn't be framed as a new feature launch. It should feel like "Team Assist, evolved."  
- [ ] **Remove positioning that implies HITL \= Gladly Teams only** — Goal is standalone AI appeal. Visual and copy signals should reinforce that Gladly AI owns the customer, not the agent.

### **Response / Answer Copy**

- [ ] **"Make it warmer" button label** — Matt flagged this as good but raised a secondary issue with another message in the flow (couldn't recall which). Review all response/action copy in flow for anything that reads off.  
- [ ] **Citation display** — Current citation format (inline numbered sources) is too granular. Citations reflect whole-answer sourcing, not single-bullet sourcing. Options:  
      - Move to bottom of response (e.g., "Sources: 1, 2, 3") without inline labels  
      - Remove names from citations; numbers only  
      - Not a blocker, but needs to look intentional  
- [ ] **"I love" phrasing** — Matt flagged a response in the flow that used "I love" — locate and remove.

### **Customer Profile / Scenario**

- [ ] **Company: Retalè Outdoors** (confirmed by Steve, replacing previous company). Has outdoor/hiking products — product recommendation conversation still works.  
- [ ] **Customer: Jordan Rivera** (Team Assist scenario) / **Rachel** (HITL scenario) — Confirm all customer profile fields match the new company context.  
- [ ] **SMS recommendation in demo** — Remove or adjust any SMS messages that include links. Matt noted SMS doesn't support links; showing linked SMS recommendations won't reflect real behavior.  
- [ ] **Sentiment score in UI** — Currently a placeholder representation. Confirm value used is believable (see UI note above on scale).

---

## **Review Checkpoint**

- [ ] **Monday review with Matt \+ Christina** — Steve to implement the above; review together before next demo milestone  
- [ ] **Fine-tune pass after Monday** — Additional polish expected after group alignment

# **Tab 2**

Meeting Title: GCL Demo Walkthrough  
Date: Apr 24  
Meeting participants: Steve West, Matt Baker, Christina Lingga

Transcript:  
   
Me: Hey\!    
Them: How's it going?    
Me: Going all right? Long but very pretty week.    
Them: Yeah, I had imagine. I'll be home in, like, two minutes. I didn't realize it started at 120\. So I was out grabbing someone.    
Me: Yeah.    
Them: Like two blocks. Are you back in, back at home or you still in Barry?    
Me: Yeah. I got here last night.    
Them: Nice. How are the second. S?    
Me: What was that sorry?    
Them: How's the sessions with Jessa when I write?    
Me: Overall very good very productive to all be together.    
Them: Great.    
Me: Obviously a lot you're gonna see that we talk through a lot and prototype we put it all and then you could react and we can decide like what we want to push back on or decide we can move.    
Them: Yeah. Cool.    
Me: Forward.    
Them: Yeah.    
Me: So.    
Them: I mean. Yeah. My general, like, before I look at any of them, I just general senses, like, for the most part, I don't really have a strong opinion. For the demo. I think it just comes down to, like, you guys all line on, like, what time horizon things need to be delivered on for us to talk about them at GCL or. No.    
Me: Yeah.    
Them: Is it kind of like, it depends on the feature?    
Me: That part was covered for sure.    
Them: Okay. So what's our time horizon that we're, like, targeting?    
Me: I think what we got to actually was that the vibe service part is tied inherently to team assist so it's going to be it will appear to be part of like team assist evolving. So it doesn't necessarily force us into a timeline because now we can kind of be like is this exactly what we want to do so we're showing them something seems like an evolution or an enhancement to team assist and like that will exist versus like inventing something different and then being beholden to that for like the next three months if that makes sense.    
Them: Okay. Yeah. Okay. Okay. Got it. Okay.    
Me: Okay.    
Them: But, like. But, like, our. Our. Is it generally, like, things need to be delivered in the next three months? Is it things you need to be delivered in the next six months when we can't do stuff?    
Me: They didn't say three or six months I would say safely three but we can also make this call this week of like hey we want you to save this timeline if we go this direction. Because yeah like I don't know personally but like there wasn't like the the vibe of the room was not like I want to say that this is coming tomorrow like the vibe of the room is awesome.    
Them: Sorry. It's. It's not a. It's like a. I'm trying to get to as more of, like, a philosophical question because. Like. As I'm looking at the decos, I want to take a lens of, like, do I realistically think we will deliver on that in six months? If we're not going to do it in the next six months, do we want to show it?    
Me: Yeah.    
Them: Are we okay if the thing is more than six months out? Or is it three months is the time horizon that we're targeting? And. Yeah, so I guess based on, like, the way you've been answering, it makes me feel like. You all didn't exactly align on, like, a specific, like, hey, this is the horizon. We want all the demos to be focused on, which is fine.    
Me: What we did align on is part of what will be shown is basically what we have happening today and then everything else is being positioned as future like this is coming at some predetermined time that we can set. Like we didn't there was no expectation of when but like this is not something yet this.    
Them: Okay. Like, I'm hurting feedback before we even started, like, okay, I'm Google, which is like, hey. We got a lot of pushback from all our customers because we showed new stuff that we didn't ship over the last year. And so I thought at one point we talked about, like, oh, we only want to show things that were highly confident will ship in the next six months, for example. But then it felt like as we started talking. That we were going to change that and actually start. Showing features that may be more than six months or whatever the time, whatever that six months is, like, I'm using that as, like, a random date, not saying there's a hard line.    
Me: I still think we were living within that reality. Like we didn't go deep dive into that because what you'll see I don't think anything that we're showing is not possible within three to six months.    
Them: Okay. Okay. Give me two minutes. I can actually look at the screen.    
Me: All good. And Christina I made updates all day based on what was discussed so that we can be viewing the full concept and then backtrack with what we want to do.    
Them: Okay.    
Me: All right. Let me. Get those open.    
Them: So you combine this things I saw.    
Me: What do you mean combined?    
Them: Right? Like, you put the citation in there. On the contacts.    
Me: I did a lot of the things that were discussed like after we did our part Wednesday.    
Them: Okay.    
Me: Just so we had like the full view and now we can make decisions.    
Them: Yep.    
Me: So like a lot of the UI stuff too.    
Them: Oh, really? Okay.    
Me: Do you notice the bottom.    
Them: Oh, yeah. The box. Okay.    
Me: I was using the clot design portal today which was actually very cool I just ran out of UC very fast.    
Them: The world of AI.    
Me: Yep.    
Them: So funny. Welcome, Todd. Just, like, slowly freak out every day. About, like, how much are we spending in this token again?    
Me: Did you also see that quad did like a sneaky thing to turn cloud code off for only like the max plan.    
Them: They claim. I mean, it's probably a signal. But there's two. There's two things that I. I feel I've heard. Which is, like, one that, yes, I did see that. They claim that it was like a 2% AB test to just understand. I I think a lot of it, though, is just. I think they're just compute constrained. And so I think they're just like, listen, like, we're gonna have to start chopping something. But that's just my take on it.    
Me: Right. Right. Ready to roll? Okay. UI stuff I don't think is a big deal but I added it so Joseph obviously just at the end gave like making the team assist panel match more of the agent workspace panel so you'll see just generally like the composer being like our other composer and like having just like a place for the buttons to live and then also we have already talked about this ability to make this bigger. Other than that the other ask was that having it be proactive so not having him have to hit the catch me up button. Which I don't think is a big deal either and I think customers will have opinions on it anyway. So he just wanted to jump in and imagine like catch me up was already clicked and it's this obvious segue from what was in the AI summary into what is in this proactive response that has a clear recommendation of what to do. And then at this point having buttons which we already talked about as well pre-populate based on the context of what's happening. So in this flow wanting it to be like really obvious why you would look at answers like you gave me recommendation why are you giving me this? Context as to why to assure them double checking on the sentiment while they're saying like he feels frustrated up here like giving something a little more tangible here. And then at this point drafting a response and you'll notice some like simple UI things around like actual inputs. To shape them. So here's a draft at this point. He also wants to be able to like give a direction by typing so this one made sense like why would it tell you to make it warmer? And also we didn't want to have like conflict with buttons for use versus like predetermined things. So making it warmer can use. For the purposes of the demo it doesn't go into the composer. I just think that's an extra step that we don't really need to do here right now. So that's happened and at this point. This is where he says that's what it can do today quote unquote. Then it pivots to where we are going, what you're about to see was actually developed for the human in the loop portion, but since it pertained to actions we just put it in here so we could all react to it. So at this point it's like okay like show that team assist will be able to like help you do things or perform actions now. Okay and I know we said we wouldn't do this but again the human in the loop stuff was already going to do it so and it's all built into team assist future. So it can do this it can give you the steps of what it's going to do great approve it. It doesn't it's really simple it doesn't hold us to like any insane sort of like you know processes. And then at this point the recommendations anything product recommendation wise is also in this like future category. So suggest stuff for the injury that's like the situation that's happening. We can talk about whether it's as draft SMS or not but it's just to make this flow easier but showing that it can do multiple channels. Use done. Then in this so that's to say team assist is here now you saw what. It already has what it will have in this quote unquote future of like whatever that timeline is. Now we're going to show you one more thing where we believe where the industry is headed where we're headed. And this is like future. And it's positioned as like this. The very last thing being shown in a very future conceptualized idea. But all within team assist where team assist is now not just instructing the human on what to do but now giving the AI the ability to have the human help it with the decision. So same kind of scenario proactive prompt of what's going on with this customer, Rachel with the recommendation of what to do. This one's a little simpler but if you hit yes, go ahead it'll start the action that I showed but in this scenario to show that you could type it's like actually I want to increase. Credit to 100 and he wants to do something like that. Okay bunked it up great good to go. Yes. So same sort of experience here. One idea we had at the end that I'm just showing you now just so you have the full concept to react to was oh what if in this very future you don't just get the sort of approval action experience of human in the loop but you can actually as the human do more. So it gave you this end of things it would do actually I wanted to also send this SMS recap as well to the customer cool and you can add the step right in there. Predetermine whatever we think is possible. A proven run done. And that's what we discussed.    
Them: Overall, it looks really cool. I still don't think, like, to me personally, I don't feel like this gets me to, like, I can help. 10 customers at once.    
Me: Tot. Ally.    
Them: So without talking about joke. I'm super small thing. SMS doesn't support us, like, links. So this idea of, like. You're sending an SMS with recommendations and links like that just. It's not going to look like that. We can send it as is, but just calling that out. Yeah. I mean. Otherwise, it's fine.    
Me: Yeah, so my opinion on this is we prevented having to show. Like make a decision on where this thing is going in order to show it in this keynote. But rather we aligned on a vision that is totally exploratory. It's within the framing of like what customers are already seeing like they get to use team assist already it's not like oh I can't use it without this part. So whether this gets baked into the like team assist in the future if it's actually a viable idea it's not in any way impacting the actual vision for like the vibe surface altogether.    
Them: Yeah. I mean, I think the. I think the question in my mind is. Like, it goes back to this time horizon. Like, if we don't actually want to bake this into team assist, our customer is going to complain because they are expecting these type of workflows and actions to be in team assist. And, you know, Matt, in my mind. Like, team assist is. Team assist is like a finite cap in I dollars. So, like, we very quickly, like, in my opinion, almost like end of the month should not be focusing much at all on team assist. I guess we can sell it to customers, but, like. Honestly, adding actions, probably not that valuable. Until, unless customers are like, yeah, I'd pay for it, but I need these things. Like, I don't know if it's. Like, I just think very quickly we're going to hit a point where it's just not worth us. Spending more time there, and we should be focusing on things that are actually going to bring in AI dollars for broadly.    
Me: Yeah, so we did this and as I've been thinking about it. One thing I'm thinking is that we remove the action step from the first scenario like why do double actions? It also is like kind of the crux of the end part and then we're not like beholden to just that capability whether it's human or AI led or you know designed to execute with so I'd be down to remove that just because then Joseph can really like focus on the positioning of this one more thing in this future state that is where the industry is going type context.    
Them: And personally looking at it, it just doesn't feel any different. Like, I don't, like, I'm not like, I don't walk away from this being like, oh, this is actually much different. Like, honestly, just looking at this. It, I just, I'm like, cool. You just help did a second iteration and team. Like, I guess, like, I just don't see. It doesn't seem different.    
Me: Yeah no that's obviously what was sort of pushed on us that was the where the conversation went you saw kind of part one part two was more.    
Them: More my point, though, is just like, I think you demo it and, like, I just. I don't want him to think that this is going to come across as, like, a revolutionary thing when it looks the exact same of maybe what you just demoed. That's all. Like, hey, we added this team assist. We have people using it. Oh, by the way, we're going to have these, like, actions. And, like, that's coming and, oh, by the way, check out this really cool human loop. It looks the exact same as team assist. I don't care why you're even calling it different. So if I'm putting, like, my product marketer hat on, I'm like, why would I even get this a different name? This is all just team assist. And maybe that's fine. And maybe it's just like, hey, here's team assist and here's another iteration where you can execute actions.    
Me: Yeah that was honestly same page kind of my intention too so that we did not invent product for the sake of the keynote and then get stuck like I feel like now this gives us the space to really like do that product right and like make decisions for team assist that are actually impactful as we learn more from customers in early access you know like I don't think we're like you know holding ourselves to anything by doing this.    
Them: Like, I guess, like. Yeah, I agree. It comes down to. Like. To me, like, what are we just trying to walk away with? And I just worry going through both of those demos, I'm just going to walk away, be like, cool. They have a team assist. And if that's, if that's, like, what we're okay with, then fine. But if it's like, hey, I'm going to show you team assist. I'm going to take a new, like, slide break and we're going to say, oh, and, like, there's this other really cool thing we're really excited about. We bring this thing called human in the loop. And I come and show this demo. I'm just going to look at it as, like, a third party in the audience and be like, what was the difference? And maybe, and once again, maybe that is intentional. But I, I worry that, like, joseph wants it to, like, people to walk away and be like, oh, I want that feature. I feel like any feature comes across here. It just feels like part of team assist.    
Me: Yeah I don't know if it's. Like. I don't he I know he's looking at it as all team assist like this is what this thing is gonna do and he does have the opinion that we've also been thinking through which is like is the experience of working in the like in this workspace now going to be in this panel? So it's like more in the spirit of imagine a world where your agent is really just doing everything in here you know TBD on what everything is and that may include just prompting AI not just over the conversation. But yeah it's it's it's. I would say it's not like oh. Team assist has a feature is so powerful but rather like there's a shift happening in sort of how we work.    
Them: Yeah. I, I personally walk away from it. It was like team assist is powerful. It's not that there's another thing. One, now, maybe I'm doing the weeds and, like, I know that nuance speaker at all. I also think the other thing that. I worry about is once again, and it's why I don't think we should be. I think you need to be able to do human and loop in both places, but why I don't think there should be the entry point or, like, be the main thing. Is because. I think this only sells to Gladly team customers. The way that this is presented. And that makes me nervous. When our goal is like, we need to figure out how to go roast Standalone. So maybe that's more of a. We solve it after. But, yeah, if I'm, if I'm Express and I'm sitting there, I'm like, oh, that's kind of a really cool feature. But, like, too bad we're on zendesk. Still. It's like, no, the intent of human loop is really like you're using Gladly AI. Gladly got better, not your team got better. I don't think that comes across. And so maybe, like, the design experience here needs to be. Like the customer is not assigned to Joseph. The customer is still assigned to Gladly AI. Maybe, like, we need to visually make the ux look like, hey, AI is waiting your input. Or, like, you know, it's like your, your AI agent is waiting your response. So, like, maybe there are some visual indicators for us to, like, try to better demonstrate that.    
Me: Yeah.    
Them: But right now, to me, that definitely doesn't come across that way.    
Me: I think we could definitely do those Christina I think I saw you nodding yeah for sure agreed there's not like we have to go through with the fine tooth comb of like what's actually on the screen who these customers are what their info is what the conversation says it's decently but for like to that point exactly like we want to know that every element on the screen is meant to be there but yeah we wanted to make sure that sort of the big notes are we're all like aligned with we don't feel like they're going to mess up the work that we want to do. I think that that's kind of that was my intention I really did not want to get us in a place that was going to trap us and I thought this was going to be the like the most viable path to get something out there.    
Them: Yeah.    
Me: To make the presenter happy and also that we have.    
Them: Yeah. And then some of my other small things, like also on ux. I think the way I would imagine it. Like, have you played with, like, quad code plan? Mode before? So, like, to me, the way plan mode would work would be. Like, this recommendation is like, hey, I think we should cancel order and do 100\. It's. Like. I feel like we should almost view it as that. It's like, hey, here's a plan. And then it's like, oh, increase the credit to 100\. That next one should almost be like that. That plan is almost getting, like, consolidated before and expanded below every time you actually ask to, like, reiterate it. Does that make sense?    
Me: Just wanted to pull it up.    
Them: I'm not following you.    
Me: Yeah.    
Them: So, like. So on, restart it. Because the, the flow, if I remember, is. Like. On Jordan or Rachel and Looper, the regular. I mean, I, I either, like, we could do the design on both sides, but it was the human in the loop one, which was like recommended a 25\. Okay, so this. So, like, you know, it's like, approve it and I'll run. This is a plan above. Right. And it's like that recommendation, I think should be that view right here. It's not recommendation. It's like. Or maybe it does say recommendation, but it's like cancel order and I'm going to go do this. I'm going to do this and I'm going to apply $25. And then if you were to say you have the buttons of like, yes, go ahead. No, I'll take it. And then you have the box. Great. You say, oh, I want to go do $100. Okay. I think this, like, cancel order should get, like, collapsed. And then the message say, like, here's your new plan. And then it's this exact box again. But with the number on number three updated from 25 to 100\. Like. Like the way that, like, plan works on. And I'm just thinking of it from a club code. It's like you're iterating on that plan. And. And then I think it cuts down, though, like, yeah, go ahead. And it's like, oh, here's the plan. Like, that felt weird where you're like, oh, I want to do 100\. And it's like. It's like, oh, does that, like, do you want me to go ahead with it? And you're like, yeah, go ahead. And then it pulls up the plan, and you're like, oh, prove. It's like. It was like. Like if I'm just thinking of, like, clogged code, it's like, oh, here's your new plan. Does that look good to you now? It's like, no, I want you to tweak this. Here's your new plan. Does that look good to you? Not. I still need to. Like, that's where I think it would just get better.    
Me: Cool.    
Them: All right. I guess I didn't pay attention at all to this thing on the left.    
Me: Which part? Oh we can by the way sorry that's kind of like just from an original thing I actually meant to remove it and make it just our UI.    
Them: Okay. Okay. Okay. Okay. Which one? Just to make sure.    
Me: Like these things and like you know.    
Them: Yeah. Yeah. I'm in the middle of tweaking that, too. I think the. The human in the loop thing from, like, I don't know, Joseph at all and the way, like how he, like, how he preferred things. One thing that he mentioned that I thought was interesting. Why you wanted to go with this direction. Was he doesn't want a new surface. And the way we presented the other, like human loop, because we're all, like, on the same page, like, saying, this is not just Gladly teams. It could be like Gladly AI too. Like, if you have a simulation running in the background, whatever it is, right? He was like, why is this a new surface? Like, this is not how it's supposed to be. So that's where he is kind of like, we should just use the customer. I think if you have a good. Yeah. Yeah, I get it. But, like, my. What I was telling Steve is, like, my. And just so, like, you're aware of it as well. My view on it is, like, if you need to come to this whole view to make the decision, we've done a disservice. Like, we are not doing our job. And, like, Gladly needs to find a way. To be able to you to go click approve and run in something that looks just like an inbox item on Gmail. And, like, I can click in and yes, you can get to a view like this, and it has it populated, but, like, if you want to get to the world where, like, how you get somebody to become 10x more effective, I just don't believe it can be this now. Joseph likes this idea of, like, yeah, it's a single unified services. I get that. And I think it's like it will be in both. But I think to me, like, the holy moment would be. Like a demo where it's like, I'm on a view where it's just like a streaming thing of, like, oh, this, you know, AI agent X, you know, customers interacting with this agent. I need this help. You know, customer needs this agent. I need that help. Like, a view of that where it's like you're doing a bunch of them, you're probably like, yeah, provoke. That's fine. Like, no, actually, like, just pass that to an agent. Like, that's not. It's better for us to go handle that ourselves, like, whatever it is. And then finally, there's one like this where it's like, oh, like. That seems like it's going in a weird direction where it's like this context. But, like, the job of AI is to slim down context, and I come to this view, and I'm just, like, bombarded with context. Like, at that point, I might as well just stop and take the customer and respond and go do stuff. Is my view on this.    
Me: I agree on me I want to really think through that part still of just like the the orchestration of what has happened in the conversation to what is now preempted in this prompt. Let me get back to that because I agree like what I'm seeing now I agree it's it's overkill still everyone's on that page as well. Which I just have to refine it better.    
Them: What if. And I don't know if this is a GCL material because I don't know if Joseph's going to like that. What if we just completely. Take it out of Gladly? App? And, like, Illustrate it in, like, some sort of text message or something that's, like, outside of the app, so you're not like, we're not arguing where in the app it should be. You know, like chat GPT when you just run. And it'll take forever for them to, like, think about, they'll just send you a text message when it's done. Maybe it's something like that where, like, we don't get, like, it's the idea of. You know, it's just recommending you things, and you just click yes or no. And then it's like, okay, big picture instead of, like, where is this thing in the customer and team or whatever? I don't know. Something to think about. Yeah. Yeah, maybe. I just. Like that. That definitely could be a good option for us to go look into. Yeah, I just think that. I don't know. I just feel like if you're already doing all this to catch up on the entire conversation, reading all this stuff and, like, you're then, like, why not just respond and do the act? Like, I don't know. I just feel like you. We've lost the whole point of, like, what human and Luke is trying to achieve, in my opinion. So.    
Me: Totally agree on that. The experience that you're even whether it's here in the space that we think it should be I agree that has to be like this you don't have to take time to take in what needs to be done so that AI can work.    
Them: Yeah. Yeah, it's a bit of that. And then the other one, too, it's just. I'm really viewing this as, like, this can be a wedge to help us go standalone. And you're now telling me, like, I basically am actually implementing a whole new customer service platform. Like, that just feels off, too. Like, so now I'm bringing all this baggage. Like, what does topics mean in the world of, like, Gladly AI? Like, I don't care about topics. I don't care about, like, who's assigned. It's just the AI agent. I don't care maybe about the preferences and the contact. Like, none of that matters when I'm trying to make a decision. Now, Joseph's push, and maybe it's fair, would be. Hey, let's try to slim that down. Let's solve it in this view, which maybe that's the right approach. But I just feel like we're in. We're throwing so much, like, gladly team. Baggage, and I'd rather start from a, let's assume there's no baggage or build what we want. And we can pull it into the thing that has baggage, but I just worry. Like, it then becomes like, yeah, it's nice if you're a Gladly team and Gladly customer. But our goal is to go so glad they add, and I'm glad.    
Me: The room to do that in well one you weren't.    
Them: It's fine. It's fine. And I, like I said, I'm sharing this because I, Steve, I know I've said this to you, but I don't think I've said it to Christina, so I'm just trying to more bring where my mind is.    
Me: There.    
Them: As I've said, I'm totally fine with this for the demo. I don't really care about the demo. I think these are discussions we need to, like, just make sure we have time and space. I also think, as I was telling Austin, like, we don't have a PM on human in the loop. And as of right now, we're saying it's one of the biggest things that can help us grow as a business, and that worries me. And, like, I'm happy to go do it, if that's what we need. But I think we just need to be explicit, like, okay, who's driving actually him and Luke? Who's going to be with customers? And. Yeah, and I just don't think we've, like, said that explicitly. So I think Austin was going to think about it. I think we're talking maybe about it with some other managers on Monday as well. So. Yeah, it's just like where we want that. And like I said, it very well could be, like, the first iteration is in team assist view or just in the Gladly conversation view. And it's like, oh, cool. Like. And I just imagine the first complaint would be like, well, I'm already looking here. Like, why do you have a reply? Yeah, there's just so much stuff that. Just almost everything on this page is overwhelmingly. A distraction.    
Me: Part.    
Them: Or confusion. Right. It's like, why? Why can I go available for email and phone calls? What does that mean when I'm. And I think maybe Joseph has a perception that you should be able to do both of these. And I think that, like, this is a new persona in Gladly. I don't think it is like you'll be taking emails, and then occasionally you'll get one of the, like, I think it's a different mode of working. And maybe some companies can get it to be able to do both. But I just think to get it started, we really need it to be a unique. Anything.    
Me: Yeah I mean I hardline agree on why would we just go out very confidently saying that one person would manage a conversation and this activity in concert like they're two totally different things so. Yeah. Hopefully I took in as much to get us to a place that again is not trapping us but I could also very much improve the experience so it's like it's representing the idea that like minimal information but deeply contextual and all you need to make very very quick decisions whether it's for AI or yourself so that will be fixed. And anything that you're actually reading or being guided to will feel like the right thing to read.    
Them: Like, I personally have some feedback on something, like the specific words. Oh, the other one that. Like, I know Joseph wants it. We could do it in the demo. Think this citation one, two on that. Just that thing is, like, how ours is going to work for a long time.    
Me: Okay.    
Them: Like, our answers are too fine grained and it's not giving us a response back of, like, oh, this one bullet point. I use this answer to frame. It's like the whole answer is framed based on all of those answers content. If we don't get very specifics. So now maybe we just have them in there and, like, I don't. I'm not trying to say it's like a blocker. It could just be like, hey, we're just going to now switch it to, like, at the bottom of every response. There's like one, two, three, and there's no names. But. Yeah, that's just the other thing. Other small. And little thing. The current way that Greg implemented the. New topic picker. Is it gets pushed, like, all the way to the left. It's, like, next to the assignment, so it's on the other side of that plus button. Probably not a huge deal. Just calling it out if, like, we are making some design changes.    
Me: Yep.    
Them: Looking at this, that plus is off center on the circle. I think those are the main ones. There. I think there was, like, a term you use that in love in one of the responses. I forgot which one it was.    
Me: Like make warmer.    
Them: Yeah, I don't think, like, I love the turn make warmer, but then I think, like, click. I think it's this one. Click, like, I think you said you recommend this. I think you then said, what's his sentiment? Oh, this I didn't quite know does sentiment score go from, like, negative one to one. Is that right?    
Me: Check on that I just wanted the representation to be in here.    
Them: Okay. Yeah, I figured. Like, I. I mean, I think it just depends. And I think every company can kind of pick a different one. I feel a lot of people do, like, zero to five, but I could be totally wrong. Yes. And ps05 or 010\. Yeah, I think nps is zero to 10\. So I don't know. It just. I could see if it was like other sentiment went down 0.6 too from, like, you know, 4.3 to 3\. You know, whatever it is. But. And then I think when you click draft a response. Then I think you said make warmer. Fine. I thought it was like there was some random message.    
Me: Oh is it at the end? Here this.    
Them: Here's the plan. Yeah, sure. Just got through it again. I can't remember. It's fine. Okay.    
Me: Definitely make all those changes we can review Monday and see if we feel good about at least what that is obviously there will be fine tuning that needs to happen but yeah, I'll make sure that we're all lined on Monday with it.    
Them: My other. Maybe Christina, you have a thought on this in our, like, effort to streamline the view. I feel like we're doing the opposite. We're adding, like, a ton of audit events. I don't know if we just have, like, a design thought on. Is it. Is there just a feed item that's like, here's the action we ran. Joseph ran. Yeah. You know, it's like, that's fine. And, like. Or it's like joseph approved the exception. Like, what accept return exception? Like, what. What. Is that? I think it's like. Yeah, it feels like we're, like, missing, like. It feels like a lot of that stuff there is, like, missing something that it's, like, anchored to.    
Me: Yeah.    
Them: It's almost, to me, it's almost like begging that, like, that should be an item in the feed, which is like, hey, joseph approved this exception, and it's. Like this is the thing the exception was, like, you know, did these things. Yeah.    
Me: We can either do that or just completely skip it for the purposes of like this demo like I don't think that's gonna like there's a we could go either path I would like to see what it would look like in the design path because that'd be great but if we can't do that if we can't come together on something I would just opt to remove it completely like all these. Lines completely.    
Them: You know something very interesting. I show this to nina. Yeah. And she said. She said. This looks more modern than what we have, actually. I have that takeaway. This is, like, way more modern than what we have, but, like, in a good way. These, like, streamlined and, like, much more, like, tightened. The feet is, like, you know, got rounded things rather than. I don't know. It definitely feels a lot. Another small thing I think technically I should be glad the AI, not gladly. Summer is created automatically by Gladly AI, I think is what we. I could be wrong. I feel like we're also duplicating things on the left. I feel like I'm getting very nitpicky, but it's like being nitpicky. You have. You have the phone number, then you have SMS, then you have main, then you have mobile underneath, and you have SMS preferred, like you're duplicating a lot of the content there. Probably makes sense to just get rid of the SMS and honestly, just get rid of the mains. It just clears up visually, like, who gives a demo or for this, like, I'd probably get rid of the link to customer. They're already linked.    
Me: Yep.    
Them: There's no suggestion. Like, yeah, you've already. You've already linked the customer. To be honest. Like, we should discuss this is deckers. We should talk. I don't know what they have integrations for.    
Me: It's gonna be retalia outdoors now which has hookah products so we can keep the products conversation but it's for tally outdoors is the company.    
Them: But. All right, so it's retired doors. I would maybe just ask, like, maybe an implementation person. It's like another context here, but I do wonder if it, like, makes more sense. And it also is kind of weird. It's like you have some, like, customer sense lifetime value next to the name. And you have a preferences. And maybe it's fine. But, like, to me, it's like, maybe it makes more sense for our orders to actually be up and, like, we can. People can reorder them. So, like, does the contact information even matter to really see? Yeah. Like, obviously, we don't do the colors. It'd be kind of fun, though. That'd be a nice little project we could do.    
Me: Yeah, no this is iterating off of a clog code prototype so a lot of lingering weird lingering things stayed but I wanted to be in the exact frame that we all agree on. This was very helpful.    
Them: Yeah. One. One just FYI, I feel like normally, like, there's a lot of subtle gray in this. Normally that the. The projectors do a pretty job. Pretty bad job of, like, sharing this subtlety. So just an FYI. Like, I think Austin's asked you all to make sure that, like. Colors can be adjusted quickly. But, like, even you presenting here, like, I'm having a hard time seeing almost any of the subtle gray behind, like, the HOKA recovery slide, the bond eat, you know, it's. Like.    
Me: I got this built in but well we're gonna work on that we discussed.    
Them: Yeah.    
Me: Yeah.    
Them: The contrast doesn't seem to be changing, like, the. The team assist chat, though. It didn't look like to me. Not. Not the green. Sorry. The green's fine. When you were doing the contrast poll. The. The one I'm really looking at is these, like, the. The recommendation things here. Like, those see really subtle. Yeah. And, like, when you turn the contrast up, turn it back down. It's. It does, like, everything but the chat. It looked like. So just. Yeah.    
Me: We'll get that sorted that was brought brought up multiple times.    
Them: We struggle with it every year. It's like a rite of passage. Similarly on the left, you have, like, chat, chat, chat, chat. Yeah. Now I know you said you're redoing this thing anyways, but it's like everything's chats. You don't. Yeah. If you're getting rid of the thing at the top. Not short the arrow above that would do. By the your customers. I don't know if you.    
Me: It's going to be minimizable.    
Them: Like, just. Oh. Oh, got it. Got it. Got it.    
Me: Yeah.    
Them: It's going to show minimize. Right? Okay. I'm fixing the dot to be outside of the thing. Of the avatar. I guess none of these have used on it anymore in the team assist. Right? What? I was trying to see what these look like again. And what happens when you click use.    
Me: It sends right in. Which we said just to have the composer step in a very fast seemed like. Not necessary.    
Them: Another. Slight question comment would be like we have the three tabs we could probably drop the third. I think the third one only shows up when the customer has a task. Just like visual. Once again, visual clutter. Yeah, I'll clean that up. I think there are some icons too that are kind of wonky. I'll clean that up too. There's also a bit of the. Like when do you make it a button and when is it just visually there? You know, so like right here is a good example process your return should it just have. Like click it. Right. You know should should it almost just have that like this pre-populated it's like. Youe know sent breast to return now it's like should the plan be there?    
Me: Yeah. Yeah.    
Them: I guess like if we're trying to streamline. And cut out buttons. Like why have a button that says process return then when it's like you know it could be like hey send I can press return now like here's the plan I would go run or here's what I think you should do you can have a proven run where you can say you know chat so it's like. Kind of gives you the option. Because yeah, I'm just curious is the like all of a sudden there's this like gladly AI transfer the conversation to Joseph which I think the ux is kind of nice. But like what what is it like. Is that. I think it's supposed if if I remember correctly this is kind of like summary and I think the text is supposed to be on the right. Because anything that we do a thing is on all right so this one is. Not not quite the same.    
Me: This was assigned to this person.    
Them: Yeah yeah. Got it. Think otherwise like that's probably most of my feedback on the stuff I'm sure there's other things as I would play more with it.    
Me: Yeah.    
Them: But. I probably get rid of that I'd probably get rid of the dark mode icon in the header.    
Me: Let's get. Started.    
Them: No that was his that was his contrast boat oh that's hundreds more got it got it got it got it that's your settings page got it?    
Me: Yeah.    
Them: S not a bad idea to put the it's not a terrible idea there are a lot of apps that do it that way I just think again I'm trying to just like streamline the ux a bunch stuff from each thing. You could probably just put that opener if you want honestly under j. But. Yeah. I mean it looks awesome. Minus my good job Steve on how humans and the lubes are work but that's that battle.    
Me: Our. Part was very fast it went it was very seamless the days were spent mostly on the other two sections so you know the the strategy.    
Them: Yeah. I think yeah I think ours is the most polished one too and the story is the most kind of. Like you know like seamless and put together. Like ours has ours is like way ahead of the two of them.    
Me: Yeah.    
Them: So I mean I think we benefit from the fact that most of our stuff is already created to like you know this is all stuff Joseph has wanted to think about right it's like yeah hey I've been crafting this whole narrative here like I just want to extend it a little bit so I think that's nice one other thing that you should we should consider like does this command plus.    
Me: Exactly. What we said.    
Them: If you hit command plus on yours like how does it scale?    
Me: Oh.    
Them: Because one. I think we presented it at 1400 by 900\. I think.    
Me: Yeah there was an exact spec for it to be consistent.    
Them: Okay works pretty well okay I just wanted to make sure it like worked pretty well the only reason I was asking is I feel a lot of times yes we all design it to something and then we get there and it's like oh it's still a little too small hit like command plus. Or but it seemed like it was pretty well responsive which is great.    
Me: Yeah.    
Them: Yeah. Also Christina I had a one on Austin yesterday and one of the things him and I were discussing is just. Like how to better incorporate design as we're doing stuff. And one of the things that I share with him and so I'll just share both of you. Like. Where I. Where my mind is like a lot these days when it comes to software engineering is that. Design we should view as like very iterative and very cheap and nothing should be like sacred. And ultimately, like engineering should be really focused on like what are the APIs that power the things we're doing? And once we have those great like let's just go and let's go and do whatever we want. So if you ever feel like our designs like they might while they might look polished at times like feel free to like cut them up as much as you want. I'm happy to like we can definitely iterate fast on a lot of this nowadays. The design like updating how the ux looks is often very, very easy. Now obviously there'll be some times where it's like, oh, like the API doesn't support that. Maybe we need to discuss. But don't ever feel hesitations if you're like, oh, we're about to go live with team assist. It's pretty well set. Like if you want to make a drastic change, just make the drastic change. Don't feel any. And that's for both of you. If you guys have any feedback on like features that we're developing or building.    
Me: It wasn't as much us and our team assists either but like we did talk about a little bit before your chat with him but specifically with team assist too it's why I don't feel weird about having it be slightly different like it's like these things are minimal and barely people will barely. Talk it.    
Them: I think one of my, one of my biggest tasks or like what I want to do is to modernize. So, you know, I might go aggressive on it. Just, you know, just FYI in terms of like. You know, polishing it up. Like for example, the home screen is driving me bananas how like the. There's like this mountain of just like headlines like your customer is different than like the actual inbox and then there's the inbox name. Like those type of like stuff. I'm just going to do things. I'm going to just do stuff to it. And I can just do a PR on that stuff. Too. Yeah, those little things. I think it's just like at this point of the game, we need to be really polished like we're not a startup, you know, like we're like grown up. It needs to show that like those little things that are like people pay attention. Oh, totally. No. And. More my point, I think historically a lot of times we would get this like sunk cost fallacy because it's very expensive to like an engineer might be ahead of like we're a designer or PM could have been focus and like, well, I've already designed the API. I've already kind of designed the feature. We're just going to like make small tweaks based. It's like right now, especially when it comes to design in my opinion, it's like. We can make very radical changes very quickly. So that's like. Let's not feel that. Just because. Greg threw something together with quad code that, you know, team assist is looking great. Like doesn't mean we can't drastically change how that is. I think I'll have a, I have a PR out. I have to like just make sure it's still working. Okay. But for dark mode in the admin experience. Whoa, big deal. And then. Yeah, I think that's like the biggest thing this week. And then Greg's been making some improvements on. Greg's been making some improvements on team assist prompt. And then he's also working on conversation or task search.    
Me: Cool.    
Them: I think the thought right now is to just have it be like a unified search. Between conversations and tasks, and there'll be a filter where you could be like, oh, I want to target just conversations or I want to target just tasks. But I don't know where he landed on that. So if you have thoughts or opinions, feel free to drop in like dad's leads. You know, there are definitely some filters that don't make sense for tasks such as topics. So that's probably a question for us of like. Hey, like, what does that mean? If that just, what does that mean?    
Me: I can definitely start thinking about that once this prototype is done so.    
Them: Yeah. And then we have. We have the ability to favorite answers on the answers like the KB admin page I'll go out this week. And then we're working a lect shipped. It'll have like when the chat last timestamp. I think that was feedback Steve we heard from. One of the customers we met with last week. And. What's the other one? Oh, and then I think, I think it was visible shared this Steve where. He's like, oh, I really wish I could see, or maybe it was stock X, I don't know, or somebody shared this, but they're like, I really wish we could see. Like, filter answers by, like, you know, like which ones haven't been updated in over like 90 days. So I know tons to update.    
Me: Yeah. Yeah.    
Them: So I'm working on adding that onto the kb admin page where you'll be able to see, like, when a thing was last updated. And then, and then you, you can, we could add a filter on there, which is like, find me all that haven't been updated in 90 days or haven't been updated in 180 days or a year, you know, it can be predefined to start.    
Me: Once you have it like once that's released to I'm thinking we I can help put this together at some point maybe we do it end of next week it's like. The recap of our customer meeting so far and then the results of like what you've been able to push out.    
Them: Yeah. Yeah, that's a pretty good idea.    
Me: Yeah.    
Them: We have a bunch on Monday.    
Me: Yeah.    
Them: Right? Or some on Monday. I won't be able to be at the first one. I should be back by the second one. So the four Patriots one I won't be at. But I should be at. Yeah, I should be back by Decker's one.    
Me: Matt can you hi Christina.    
Them: Yes.    
Me: Cool.    
Them: And another thing is, I think we're gonna, I was gonna. I was going to open, thankfully, we don't have like seven this week, which is nice. I was going to open them up to other Gladly engineers. One thing Jared has been working on is trying to get more just engineers in front of customers to help continue to build up empathy. And, yeah, so he was looking for avenues when people are meeting with customers. So I figure it's a good one where we can like share out, you know, here the customers are meet with and you're welcome to join.    
Me: Because they tend to you know talk about things that aren't in our purview so why not more areas represented. Cool.    
Them: All right. Christina, you're out of the ones we have. And then. Oh, and then I won't be at the team meeting on Monday. I guess we can move it. If we want, I have a meeting with rent the runway. I'm just going to push it by half hour. I think I'm good. Anything you all need from me or any. That you guys want to talk about?    
Me: Appreciate all that feedback gonna be very very useful in getting this done fast and no glad to hear thanks for the update now we can get ahead all the summary stuff Monday.    
Them: Yeah.    
Me: So.    
Them: I need more tokens. Give me a sec. I really want to get out of this business, but I know I'm just like, wow, Matt is like holding on to the token skate. Well, Steve isn't in my orgs. I can't help him.    
Me: I'm in the other one and I have the tokens.    
Them: But. I'm just going to make you a premium seat because I feel like keep bumping you up. And we had one on assigned for some reason. Yes. Thank you. Okay, whatever.    
Me: Cool.    
Them: Else.    
Me: Thanks a lot.    
Them: All right. Yep. If you guys have anything else, just let me know. Thank you. See you.    
Me: All right see you guys. 

# **Tab 3**

### **GCL Demo Walkthrough Overview**

* Demo combines existing Team Assist capabilities with future AI actions functionality  
* Positioned as evolution of Team Assist rather than separate product  
* Timeline flexibility maintained \- no hard commitments to specific delivery dates  
* All future features framed as “coming at predetermined time we can set”

### **Current Team Assist Enhancements**

* UI updates to match agent workspace panel design  
* Proactive mode eliminates “catch me up” button requirement  
* Pre-populated action buttons based on conversation context  
* Clear recommendation reasoning with sentiment indicators (-0.6 sentiment score example)  
* Draft response capability with directional input (“make it warmer”)

### **Future AI Actions Capability**

* Team Assist evolves to perform actions, not just recommendations  
* Shows step-by-step action plans for approval  
* Multi-channel support (draft SMS demonstrations)  
* Human-in-the-loop workflow for AI decision assistance  
* Customer can modify AI recommendations (e.g., increase credit to $100 vs $25)

### **Design and Technical Feedback**

* Matt’s concerns about 10x productivity claims not being met  
* SMS doesn’t support links \- demo needs adjustment  
* Citation system too fine-grained for current answer structure  
* Plan mode iteration needed (similar to Claude’s approach)  
* Contrast issues for projector display  
* Remove audit events or consolidate into feed items  
* Streamline customer info panel (remove duplicated contact details)

### **Strategic Positioning Concerns**

* Risk of appearing Gladly Teams-specific rather than standalone AI  
* Need visual indicators showing AI agent ownership vs human assignment  
* Concern about overwhelming context defeating human-in-loop purpose  
* Consider text message interface outside Gladly app to avoid platform baggage  
* Product management ownership for human-in-loop needs clarification

### **Next Steps**

* Steve to implement design feedback by Monday review  
* Remove action step from first scenario to avoid duplication  
* Refine human-in-loop experience for minimal context, quick decisions  
* Austin discussing PM ownership with other managers Monday  
* Team meeting moved 30 minutes later due to Matt’s Rent the Runway conflict

---

Chat with meeting transcript: [https://notes.granola.ai/t/64e12755-f6cb-40bd-979c-78fee9fddf7f](https://notes.granola.ai/t/64e12755-f6cb-40bd-979c-78fee9fddf7f)

