+++
title = 'Who Signs for the Machine?'
date = 2026-09-19
draft = false
+++

*On tokenomics, cost per successful (and correct) outcome, and the responsibility gap*

A couple of posts back I told you about the afternoon an AI agent swapped an embedding model on one of my side projects, deployed, and took the site down. I used it to make a point about discipline versus context. There's a second point hiding in that story, and it has been bugging me ever since.

By every measure the agent had, that afternoon was a success. The change was made. The deploy went green. The turn ended with a cheerful summary of the work completed. If I had been looking at a dashboard of the session, it would have shown me tokens in, tokens out, and a bill that was, honestly, pretty reasonable. Nothing on that dashboard knew the site was down. A human found that out, later, the way humans usually do.

That gap, between "it finished" and "it was right," is the whole subject of this post. And underneath it is a harder question I've been circling for most of a year: when the machine finishes something and it turns out to be wrong, whose name is on it?

## You don't pay for the truck

There's an old rule in cattle country: you don't pay for the truck, you pay for what it is delivering. Nobody at the sale barn ever bought a truck-hour. They bought cattle, delivered healthy, and everything the hauler spent to get them there (the diesel, the driver, the hours) was a cost he ate against that one transaction where the cost of delivery is absorbed into the payload invoice at the end.

Back in July I ran a bake-off of open-weight models on rented GPUs for one of my side projects and instrumented the whole thing down to the pod launch (the ops lessons and the GPU-level taxes I hit deserve their own post). The headline that stuck with me: the cost of a correct outcome spread 47x across a fleet whose hourly rates spread barely 4x. The cheapest cards per hour were among the most expensive per correct answer. One model was slow *and* wrong, the worst of every axis at the lowest hourly rate. If I had costed that fleet from spec sheets, I'd have gotten the ranking wrong at both ends.

Hours are the truck. Tokens are the diesel. And right now the whole industry is, quite reasonably, building itself a very good fuel account.

## Tokenomics is the fuel account

I want to be careful here, because I work in FinOps, and I think the tokenomics conversation happening right now is good and overdue. Before you can optimize anything you have to see it, and AI spend today is scattered across models, providers, gateways, and tools in a way that makes the cloud spend of ten years ago look tidy. Counting tokens, normalizing them across vendors, and mapping them to teams, users, and products is the visibility layer. The FinOps framework calls that phase Inform, and nobody gets to skip it. I've watched too many organizations try to skip it with cloud, and the bill always found them.

So this isn't "tokens are the wrong metric." Tokens are the right metric for what tokens measure. The organizations doing tokenomics well already know this, which is why the smart ones are asking what comes next: how do you tie the spend to outcomes, and how do you know whether it was worth it?

That's the question I want to give a vocabulary to, because I think we're about two words short of being able to answer it.

## Two words: successful, and correct

Here's the distinction the deploy story forced on me.

An outcome is **successful** when the thing the objective asked for actually happened. The pull request merged. The email went out. The record got updated. The deploy went green. Success is judged at the moment the execution lands, against the definition you wrote down going in.

An outcome is **correct** when it turns out to have been right. The merged PR didn't get reverted. The email said the true thing to the right person. The record is what the customer actually owes. The deploy didn't take the site down. Correctness is judged later, by the world, and it has a clock on it: you don't know a change was correct on the day it merged, you know it two weeks later when nobody had to fix it.

I've been saying "cost per correct outcome" for a while now, and lately I've heard more people say "cost per successful outcome." I've come around to believing we need both, and that they are not competing metrics. They're two columns on the same ledger.

**Cost per successful outcome (CPSO)** is total cost divided by the outcomes that met the definition. It tells you whether the machine is finishing.

**Cost per correct outcome (CPCO)** is total cost divided by the outcomes that met the definition *and held up*. It tells you whether the machine is finishing right.

The gap between them is where the money goes. A system with a great CPSO and a bad CPCO is producing confident garbage at scale, and your dashboard will call it productive. I saw this in the bake-off in miniature: below a certain capability threshold, models "succeed" at structured-output tasks by spraying plausible values into every field. Their success rate looks fine. Their correctness rate, once you check the values against reality, is a catastrophe. Any metric that counts completions rewards this. Only a metric that checks the cargo catches it.

## The contract comes first

Here's the part I skipped for the better part of a year, and it's the part that makes the rest computable.

You cannot measure success without a definition of success, and you cannot measure correctness without a test for it. Neither of those comes from the machine. They come from whoever owns the objective, written down before the work starts. I've started calling this the **contract**, and it has three parts:

1. **The objective.** What we're trying to accomplish, in plain language. "Reduce the on-call load from this class of alert."
2. **The outcomes that would count as success.** Not one, usually. An objective has a handful of shapes success can take (a fix merged, a runbook written, an alert retired), and each needs a definition concrete enough that a machine or a person can say yes or no to it.
3. **The correctness test.** How we'll know, later, that the outcome was right, and how long we wait before we believe it. "The alert didn't fire for the same cause within thirty days" is a correctness test. "The PR merged" is not.

If this sounds like the thing I told you in the buffalo wings post (don't say "kill the chicken," say what the meal is supposed to be), it's because it is. The contract is the outcome definition, promoted from a prompt to a document that outlives the session, with a scoreboard attached.

## The five things you have to write down

Once the contract exists, I think there are exactly five quantities that matter, and everything else people want to know is arithmetic on them.

**Total cost.** Cumulative, over the life of the journey toward the objective. Not per call. The tokens, yes, and the GPU hours behind them, but also the retries, the review minutes the human spent, the CI runs, and the day-two cleanup when a "successful" change turned out to be wrong. A metric that stops counting when the turn ends is lying to you about what the outcome cost. The 1024 bug cost tokens to create and a lot more than tokens to find.

**Correctness.** Measured against the contract's test, after the fact, with the clock respected. If you can't measure it, say so out loud, because your CPCO now has an error bar the size of the metric.

**Successful outcomes.** How many outcomes met the definition. This is the count CPSO divides by.

**Value of a successful outcome.** What it's worth when it's right. Sometimes that's dollars (a closed ticket has a loaded cost, a retired alert has an on-call cost). Sometimes it's a proxy you agree on in the contract. It doesn't have to be precise. It has to be written down, because the next quantity is measured in the same units.

**Risk of being wrong.** What it costs when the outcome is incorrect, times how likely that is. A wrong comment on a pull request costs someone thirty seconds. A wrong email to a customer costs a relationship. A wrong change to a billing record costs more than the quarter's whole token budget. Same execution shape, wildly different risk, and no token count will ever tell them apart.

Those five are the first principles. CPSO and CPCO fall out of the first three. ROI falls out of all five. And the fifth one, risk, is the one that decides whether the machine gets to act alone.

## Execution, delegation, and the human on the other end

Two more words.

An **execution** is a thing that happened to the world on the way to an objective. A PR raised. An email sent. A ticket closed. A row updated. Executions are the atoms; outcomes are made of them.

A **delegation** is the record of who handed that execution off, which is to say, who is accountable for its result. This is the piece I had been missing myself, and I don't see many tools carrying it. Every gateway can tell you which API key made the call. Almost nothing I've used can tell you which *person* is answerable for what the call did.

And there has to be a person. A machine cannot be accountable. It doesn't have a mortgage, a reputation, a boss, or a Saturday it would rather have spent doing something else. When the execution turns out wrong, the correction has to land on someone who can learn from it, absorb the cost, and decide differently next time. That's not a limitation of current models. It's what accountability means.

So every execution carries a delegation, and every delegation carries a name. That's the data model. It's not complicated, and I think it's the most important schema decision anybody building agent infrastructure will make this year.

## When the machine gets to act alone

Here's what the five quantities buy you once the names are attached.

Every agent harness I've used decides when to stop and ask a human by vibe. Some ask before every write. Some ask before nothing. Neither is a policy; both are defaults. The contract gives you an actual rule:

```
act autonomously when
  (value of a correct outcome × probability it's correct)
    is greater than
  (cost of being wrong × probability it's wrong) + cost of asking
```

The probability terms aren't guesses. They're the machine's measured correctness rate on this shape of execution, under this contract, which is exactly what CPCO's denominator has been counting all along. The value and the risk are in the contract. The cost of asking is the human's time, which you also know.

Read that rule and a few things fall out. A low-stakes execution with a good track record (reformatting a doc, answering a rules question, opening a draft PR) clears the bar and the machine should just go. A high-stakes execution with no track record (sending the email, changing the record, touching production) does not, and the machine pulls the human in, not because someone configured a checkbox but because the numbers said so. And, the part I like most: the machine earns autonomy the same way a new engineer does. Its correctness history is the trust. As measured correctness goes up and CPCO comes down, the same rule lets it do more on its own, one execution shape at a time, with a human's name on every step of the way.

That is how I already run a team. I delegate. I don't watch every keystroke. I'm accountable anyway. And people earn the right to more autonomy by their track record, not by my mood. The human in the loop is a steering mechanism, not the failure sink, and the rule above is what makes the difference computable.

## The FinOps view

For a business, the question underneath all of this is blunt: did every dollar I put into the machine come back multiplied, and at what rate?

The five quantities are the inputs. Value of the successful outcomes, minus total cost, over total cost. Tokenomics supplies one line of the cost (the fuel bill), and it's an important line. The contract supplies the rest: what success was, whether it was correct, what it was worth, and what it would have cost to get wrong.

If you've done FinOps for cloud, this is unit economics with a twist. We learned to stop reporting cloud spend as a total and start reporting it per customer, per transaction, per whatever unit the business actually sells. The twist with agents is that the unit has to be a *correct* one, and correctness has a clock on it, so the report has to wait for the world to weigh in before it's allowed to declare victory. A cost report that closes the books when the tokens stop is a tachometer on the wall. Busy, always busy, and no idea what came off the trailer.

## The responsibility gap

Now the deeper part, the one I think outlasts FinOps.

I wrote a longer piece on this recently, [The Responsibility Gap in Enterprise AI](https://k5cv.com/posts/ai-ml/the-responsibility-gap-in-enterprise-ai/), so I'll only summarize the frame here. If the machine makes the change but a human inherits every failure that follows, we haven't transferred responsibility. We've moved execution and left accountability and risk exactly where they were. Most systems today automate the action and externalize the consequence: the agent finishes when the tool call succeeds, and if production breaks later, the work moves back to a person. We call that autonomy. It's closer to automated execution with human-owned risk.

The way through, I argued there, is to be precise about the word. A machine cannot be *accountable*. It can't accept blame, exercise judgment as a legal person, or answer to a customer. What it can carry is *operational responsibility*: staying attached to the change after it lands, watching the agreed signals for the agreed period, containing or reversing within its authority, escalating what it can't resolve, and keeping the lesson. Accountability stays with a person. Operational responsibility can and should move to the machine, and the more of it the machine carries, the more autonomy it has earned.

So you don't close the gap by making the machine accountable. It can't be. And you don't close it by pretending a human controlled every step, because the whole point of delegation is that they didn't. You close it the way we've always closed it in organizations: with a name on every handoff, a definition of done written before the work starts, and a scoreboard that reports correctness and not just completion, rolled back up to the person who delegated. Responsibility doesn't have to mean *control*. It has to be *traceable*, and it has to be *accepted*.

I lead a team of engineers. I can't tell you what each of them typed yesterday. I can tell you what they were asked to accomplish, what would count as done, how it turned out, and that the result is mine to answer for. Nobody thinks that arrangement is a gap. It's called management, and it works because the ledger is honest.

Working side by side with machines, the way I believe we're about to, means the same shape. Every objective gets a contract. Every execution gets a delegation. Every delegation gets a name. And correctness gets measured after the fact, on a clock, and lands on that name, so the person learns, the harness learns, and the machine's next execution is bounded by what the last one actually turned out to be.

That's not a constraint on the future. It's the thing that makes the future safe enough to delegate to.

## Where I've landed, for now

I don't have this fully worked out. The value term is hard to write down honestly, the correctness clock is different for every kind of work, and I haven't yet seen a tool that carries the delegation all the way from the person to the execution and back. I'm building pieces of it for myself, and I'd genuinely like your help with the rest. If you're working on any corner of this, or you think I've drawn a boundary in the wrong place, I want to hear it. We're in a rare moment: every one of these ideas gets to drive us toward new knowledge, new experience, and eventually outcomes nobody has seen yet, as we take apart a new (but also not new) set of problems. Reply wherever this post found you, or find me on X (@cliff_colvin) or GitHub (cliffcolvin). I'd rather work through it with company than alone.

But the shape I'm confident in. Tokens tell you what the machine ate. Success tells you what it finished. Correctness tells you what it got right. Value and risk tell you whether it should have been allowed to try. And a name tells you who signs for it.

Two posts ago I said the machine had learned to take notes. It has. What it can't do is sign.

Hours are what you rent. Tokens are what you burn. Outcomes are what you bought. Somebody signs for every one of them, and it's never the machine.
