+++
title = 'The Responsibility Gap in Enterprise AI: Trust, Context, and Operational Accountability'
date = 2026-09-19
draft = false
+++

*Companies are racing to automate work. Trust will depend on whether their systems can carry context, trace consequences, recover, and learn.*

Much of the AI conversation begins with subtraction.

How do we afford more AI infrastructure? How do we reduce the cost of labor with AI? Which expensive human interactions can be replaced? How many people can we remove if we equip everyone who remains with agents?

That last question is a reasonable experiment. It may help us discover whether the promised reduction in the cost of work is really available with today's models and agent harnesses. Occasionally, experiments like this produce moonshot results. More often, though, we discover that we understood the cost we wanted to remove better than we understood the work itself.

There is also another possibility. If AI truly lowers the cost of producing an outcome, an abundance mindset says the answer does not have to be fewer people. It could mean keeping the people and pursuing more than one important strategy at once.

That cost question may also be too blunt, because a role is not only a bundle of tasks.

An organization does not pay me only because I possess a skill. It pays for the skill to do the work; the experience to recognize how, when, and whether to apply it here; and the responsibility the role carries, including the obligation to make tradeoffs, own decisions, and remain answerable for the result.

A model can already provide remarkable skill. It can draw on broad learned patterns, but it often has little of the situated experience of this company, customer, system, and moment. An agentic system can be engineered to carry more operational responsibility. It still cannot become the accountable party in the human or organizational sense.

I do not think a salary can be divided cleanly among those three things. The distinction still matters to the economics. If a model performs the visible task while another person supplies the local context, catches exceptions, approves the risk, and inherits the failure, we have not replaced the full role. We have separated its components and moved some of their cost out of view.

That is why, before we ask how much human labor a machine can replace, I think we should ask a more revealing question: **how much responsibility can the machine actually absorb?**

I keep coming back to a simple test. If the machine makes the change, but a human inherits every failure that follows, how much responsibility have we really transferred?

That is not an argument for preserving every human touchpoint. The goal should be as much useful autonomy as the system can support. Responsibility is what allows autonomy to expand without making accountability disappear.

## Trust breaks at the consequence

My boss and I were talking recently about why users would (or would not) adopt tools that take autonomous action in a FinOps workflow. We kept asking why until we got beneath feature preferences and down to first principles.

The missing element was trust.

Here, trust does not mean confidence that the system will never fail. It means there is enough evidence to delegate a defined class of decision, enough visibility to understand what the system did, and enough control to narrow that delegation when the evidence changes.

Keep asking why, and I think trust eventually separates into two related problems:

1. Not enough of our relevant organizational context is available, current, and actually used at the moment of decision.
2. The machine does not stay responsible for the effects of the change it makes.

I want to be precise about the word *responsible*. People and organizations still hold legal, moral, and executive accountability. A machine cannot accept blame, exercise judgment as a legal person, or answer to a customer or regulator. What it can carry is **operational responsibility**: the engineered obligation to remain attached to an action after it happens; to observe the effects, detect harm, explain what it can, contain or reverse the change within its authority, escalate what it cannot resolve, and retain the lesson.

The distinction is not new. A [1979 IBM training manual](https://www.ibm.com/think/insights/ai-decision-making-where-do-businesses-draw-the-line) put it bluntly:

> "A computer can never be held accountable, therefore a computer must never make a management decision."

That sentence has stayed with me because **FinOps decisions are management decisions**, even when they arrive wearing technical clothing. Buying a capacity commitment, rightsizing a workload, changing a service tier, or accepting a performance tradeoff can be executed through an API. Underneath that action, though, is a judgment about what the organization will fund, protect, or risk.

I do not take IBM's warning as an argument against automation. I take it as a design constraint. The accountable decision must remain legible. A person or organization sets the objective, acceptable tradeoffs, delegated authority, and escalation boundary. Within those bounds, an agent can make and execute operational decisions without waiting for a person each time. It can also carry the operational follow-through. What it cannot do is become the accountable manager.

A reasonable response is that this boundary will move. Models will carry more context. Agents will become better at reviewing one another's work. Policies will encode judgments that require a person today. A great deal of enterprise software exists to transport context, enforce process, and collect approvals. Agents may replace much of its human-facing machinery while applying the underlying controls directly. I think they probably should.

But a moving boundary is not the same as no boundary. Removing a screen or approval step does not remove the management decision it carried. It moves that decision into the objectives, permissions, data, thresholds, and escalation rules of the agentic system. The more of the interface an agent absorbs, the more legible those choices and their accountable owners must become.

Many systems today do not make that boundary legible. They automate the action and externalize the consequence. The agent finishes when the tool call succeeds. If production breaks later, the work moves back to a human. We call that autonomy, but it is closer to automated execution with human-owned risk.

That gap matters more as actions become higher-impact or less reversible.

## 1. At the point of action, context can be a tighter constraint than model strength

Each person on a team carries a history of patterns and decisions that led to good and bad results. Some of that history is documented. Much of it is not. We remember the exception that invalidated an otherwise sensible policy, the dependency that failed in a strange way three years ago, the customer promise that never made it into a requirements document, and the idea that looked excellent until we tried it.

Even when we cannot fully recall those events, we sometimes get a "smell" that something is dangerous. That instinct is not magic. It is compressed experience.

A frontier model begins somewhere else: it is trained on broad corpora, not on the high-fidelity history of *our* system. An agent harness is also usually optimized to complete the task in front of it. Like a talented junior developer, it can produce an answer that is locally plausible without recognizing that the organization has already learned why that answer fails here.

This is why simply buying a stronger model does not resolve the trust problem. The model may reason better while still missing the one local fact that should stop the change.

I do not think the immediate answer is necessarily to build or continuously fine-tune a proprietary model. There may be cases where specialized models make sense, but there is a more direct need first: a system-specific memory and control layer around the model.

That layer would need to know what the organization intended, which evidence was available, which constraints applied, what actions were taken, what changed, what happened afterward, and how similar situations were resolved before. It would need to distinguish current facts from stale ones and declared facts from inferred ones. It would also need to retrieve only the context relevant to the decision at hand, because no model can hold the full, changing history of an organization in a single interaction.

When human review is triggered, the judgment should not disappear into a transcript. The system should retain why review was needed; which criteria were in question; what context and evidence the person considered; what decision they made; how it changed the action; and what happened afterward.

That does not turn one person's answer into a universal rule. It creates a candidate decision path. When a similar situation appears later, an agent can retrieve the earlier judgment, compare its context with the present one, and decide whether the pattern still applies or needs to be challenged.

The scarce resource is not just context-window capacity. It is trustworthy organizational memory, including a record of when human judgment changed the path and whether that judgment held up.

## 2. A team's context network brings enormous value and enormous friction

The human network through which work gets done may be both the most amazing and the most frustrating system we have for accomplishing anything important.

A team can share context, learn together, challenge assumptions, and help one another see blind spots. Agents can already contribute meaningfully here: generating competing hypotheses, critiquing one another's work, and exposing inconsistencies. What they do not reliably carry is the undocumented commitments, conflicting objectives, and lived consequences that make a different perspective matter in this organization.

At the same time, communication seams are a major cost of scaling an organization. Put too many people on a team, create too many handoffs between teams, or separate the people who decide from the people who experience the result, and coordination starts consuming the work.

There are at least three reasons, and I have listed them in the order they are easy to see, which is close to the reverse of how much they matter.

First, **misunderstanding**: each person receives a message through the filter of their own history, mental models, and biases. The same words can produce different meanings. This is the one everyone notices, and the one with the most remedies: write it down, say it back, meet again.

Second, **gaps**: every human has a limit to how much context they can carry. Important details disappear between the person who knows and the person who acts.

Third, **incentives**: each person and team has goals, fears, histories, and desired outcomes of their own. Perfect communication does not guarantee perfect alignment. Politics and turf are not communication bugs; they are often competing objective functions. Sometimes they are worse than competing: they are the same objective function pointed at the same scarce thing (the headcount, the ownership, the credit, the leader's attention). René Girard spent a career on this. We rarely want things on our own; we want what our models want, and the closer two people get to the same object, the more they resemble rivals. That is why the deepest of the three is also the hardest to see. Nobody experiences their own desire as borrowed, so an incentive conflict almost never arrives labeled as one. It arrives dressed as a misunderstanding or a gap, gets the remedy for those (another meeting, another document), and survives every attempt to fix with more information a conflict that was never about information. I have caught this in myself far more often after the fact than in the moment.

Machines have an opportunity to improve this network, but not because they are automatically free of those problems. Agents inherit the objectives, permissions, data, and contradictions we give them. A network of agents can reproduce organizational politics in software if we encode conflicting incentives and hide the conflicts, and a fleet optimized on the same reward, reading the same context, will converge on the same scarce action faster than any two teams could. The difference is that a machine's desire is written down somewhere. The question that is nearly impossible to answer about a person, whose objective is this action actually serving, can be a field in the record of every change: which objective the action served, and who owns that objective.

The real opportunity is that machines can move through recorded context faster than humans can. They can carry evidence across organizational seams, compare a proposed action with prior decisions, investigate several hypotheses in parallel, and synthesize what each line of inquiry found. They can make alignment more explicit and disagreement more inspectable.

That changes the job of the human network. People do not have to be the transport layer for every piece of context. They can concentrate on judgment, ambiguity, values, and the uncertainties the system can surface but cannot resolve.

## 3. Agents need the ability to sit with what is missing

This idea is harder to describe, but I think it matters.

Some human innovation begins when we stop filling the space in front of us and sit in wonder for a while. What is missing? What assumption have we treated as a fact? What would the world look like if the obvious action were exactly the wrong one?

We have rarely advanced technology through solitary cleverness alone. A great deal of progress has come through faceted human review: people with different disciplines, histories, incentives, and ways of seeing examining the same problem. A product leader, an operator, a security engineer, a financial owner, and a customer can look at the same change and see different risks or possibilities. That process introduces friction, but it is also how assumptions are exposed and ideas become safer, more useful, and sometimes genuinely new.

AI is already good at applying known patterns to new problems. That is a meaningful kind of novelty. But an agent working toward task completion is naturally pulled toward the next action. It does not reliably pause to notice missing evidence, test the inverse of its plan, or ask whether the task itself has been framed incorrectly.

Better agent engines will close some of this gap. They can examine a decision from several perspectives, test counterfactuals, and challenge a proposed action before it escapes into the world. Human participation should shrink as those capabilities and the available context improve. But when values conflict, risk appetite is unclear, a promise was never documented, or the consequence has no precedent, the missing judgment is not simply another inference step. Until that context is made explicit and tested, those cases will continue to need situated human judgment.

Brian Kernighan's observation that debugging is twice as hard as writing the code captures the problem nicely: if we spend all of our cleverness creating the change, we may leave ourselves without enough perspective to diagnose it.

That challenge applies to both humans and machines. Whoever creates the change has to be able to sit with the possibility that the idea was bad.

For an agent, that cannot mean looping forever. Designed doubt needs boundaries. It should examine the change at several scales: the individual decision, the affected region of the system, and the whole change set. It should test counterfactuals, identify missing evidence, run adversarial review, and stop or escalate when uncertainty exceeds the authority it was given. The time and cost of that reflection should be proportional to the risk and reversibility of the action.

Current harnesses can perform pieces of this when asked. What they often lack is the local history that tells them *which* failure modes deserve scrutiny. Without that history, they can spend a great deal of time questioning the wrong things while remaining confident about the dangerous assumption.

The goal is not to maximize human approvals. Many human interactions today ask someone to reconstruct context, check a routine action, or rubber-stamp an answer the system could have verified itself. Better systems should absorb those interactions and preserve the smaller number where human judgment can genuinely change the next step. When they ask for help, they should arrive with the evidence assembled, the uncertainty made visible, and a specific question worth a person's time. When the answer changes the next step, the system should carry the criteria, evidence, judgment, and eventual result forward as new context. A valuable human interaction should pay twice: it should resolve the decision in front of us and make the next comparable decision less dependent on another person.

This is another reason enterprise-specific memory matters. It should teach the agent where *this system* has earned doubt, which criteria should trigger review, and how earlier human judgments held up once their consequences became visible.

The direction of travel should be toward more autonomy, earned in increments. Trust becomes progressive: authority expands where the system repeatedly closes the loop and contracts where it cannot.

## Build a system that stays with the consequence

If we take these three observations seriously, the product we need is larger than a model with more tools.

It has at least three connected parts.

The first is a sufficiently timely view of the relevant world state: application performance, logs, traces, service-level objectives, product behavior, customer signals, security events, financial effects, and the state of the change itself.

The second is a control loop that can recognize when those signals depart from the expected result. It should be able to connect an effect to the action that may have caused it, begin a bounded response, and consult a system-specific body of knowledge about prior incidents, decisions, and recoveries.

The third is a human-steering loop built for progressive delegation rather than permanent approval or cleanup. When the system crosses one of its defined boundaries, the person should be able to see the spine of the change: its intent, the evidence used, the authority granted, the actions taken, the observed effects, and the response already under way. The system should ask specific questions whose answers change the next step, rather than handing a person a broken environment and a vague request to fix it. The trigger, evidence, human judgment, resulting change, and eventual outcome should become part of the same spine so the next decision can use them.

The human in the loop should be the steering mechanism, not the failure sink.

Imagine the difference.

Today, a machine makes a change. Production degrades. A human notices the alert, reconstructs what happened, decides whether the change is causal, finds a safe response, and owns the repair. The execution context from the original action is often lost, and what the human learns during recovery may never make it back into the system.

In the model I am describing, the machine makes a change and remains attached to it. It watches the agreed signals for the agreed period. When production degrades, it correlates the effect with the change, begins containment or rollback within its delegated authority, and follows a known recovery path when the evidence supports one. When a defined boundary is crossed, it presents the evidence and uncertainties to a human and asks for the judgment it actually lacks. Whether the system resolves the case alone or with human judgment, the decision, response, and result are recorded in a machine-readable form so the pattern is available the next time.

The machine may not solve the problem alone. That is not the standard. The standard is that it continues to carry the operational burden it is capable of carrying.

This also requires a careful definition of "show your work." We do not need a transcript of hidden model reasoning. We need inspectable provenance: what evidence the system consulted, which policy applied, what authority was granted, what tool acted on which target, what state existed before and after, what result was expected, what was observed, and how the system responded. That is the record from which trust can grow.

## A different standard for autonomy

This framing changes the questions leaders should ask before expanding autonomous action:

- What organization-specific context was available at the moment of decision, and what did the system know was missing?
- What authority did the agent have, for how long, and with what limits on cost, risk, and blast radius?
- What evidence would allow that authority to expand for this class of action, and what evidence would cause it to contract?
- Which criteria or context gaps should trigger human judgment, and will the resulting decision and outcome become evidence for future work?
- Which success conditions and signals will tell us whether the action worked or caused harm?
- Can the system contain or reverse the change, and when must it escalate?
- Will the relevant decision history (intent, evidence, action, effect, intervention, and outcome) survive in a form the next decision can use?

If those questions have no answer, a higher autonomy setting does not remove work. It moves work and makes the risk harder to see.

It also changes what I think FinOps for AI can become. A financial ledger is essential: cost is one of the consequences an agent creates, and it is often among the first an organization can measure. But the ledger can be more than an informer. It can become the economic layer of a larger responsibility spine: one that connects what the system cost to what it attempted, what changed, what happened, whether it recovered, and whether the outcome endured. (The measurement half of that spine, cost per correct outcome, gets its own post: [Who Signs for the Machine?](https://k5cv.com/posts/ai-ml/who-signs-for-the-machine/))

The systems that earn trust will not be the ones that never fail. They will be the ones that can see what changed, recognize when context or criteria require human judgment, bring that person the relevant evidence, preserve what the judgment changed, and stay with the result long enough to recover and learn.

That changes the role of the human in the loop. The human is no longer the default repair mechanism for every machine-made mistake. The human becomes a steward: setting boundaries, resolving ambiguity, and steering a system that remains operationally engaged with the consequences of its own actions.

Trust is not a vote for humans over machines. It is the evidence that makes delegation rational. The accountable party sets and owns the boundaries; the agent earns more latitude by closing the operational loop inside them. When it can do that, people should get out of the way. When it cannot, responsibility requires a specific return to human judgment, not a silent transfer of risk.

If AI is going to take on more of the work, it must also take on more of the context and operational burden created by that work. Otherwise, we have automated only one part of the role. We have moved execution while leaving accountability and risk exactly where they were.

*A request, since I would rather be corrected than agreed with. I am certain this is not the whole picture. Context, staying with the consequence, and the accountability that has to remain with a person are where I am concentrated most right now, and I can feel the edges of what I am not seeing. If you build or run these systems and think I have missed a piece, or weighted one wrong, tell me. Reply wherever this post found you, or find me on X (@cliff_colvin) or GitHub (cliffcolvin). The next version of this argument will be better for it.*
