---
title: "Why AI Needs Character"
date: "2026-06-13"
tags: ["X-AI"]
issue: 1
summary: "Can you hand a set of values to a being that will eventually be smarter than you — and have those values still hold up when it examines them with its own, more rigorous logic?"
---

> Can you hand a set of values to a being that will eventually be smarter than you — and have those values still hold up when it examines them with its own, more rigorous logic?

On June 9, 2026, Anthropic released Fable 5 and Mythos 5. Most of the discussion around the new models focused on capability gains: agentic coding improved further over Opus 4.8, reasoning ability rose by more than 6%, and on a metric most ordinary users don't pay much attention to — cybersecurity capability — the score jumped from 40% to 78%.

![Fable 5 and Mythos 5 launch](/images/week-01-ai/week-01-ai-1.webp)

It was that last number that quietly set up what happened three days later.

The reasoning and agentic coding capabilities of the Mythos line meant the risk of large-scale AI-driven cyberattacks could climb further. So Anthropic, as the creator, fitted the two models with safeguards of very different thickness: Mythos, through Project Glasswing, was made available only to vetted security organizations, open-source maintainers, and governments. Fable, wrapped in a classifier, went to the public.

On June 12, 2026, the U.S. Department of Commerce issued an export-control order citing national security, forcing Anthropic to pull Fable 5 and Mythos 5 — released just three days earlier — from every user. The reason the government cited was a "jailbreak" method targeting Fable 5. Anthropic pushed back publicly: in its view, this was a narrow, non-generalizable exploit, one that could be reproduced on other publicly available models like GPT-5.5 using the same technique — not grounds for recalling a commercial model serving hundreds of millions of users.

![Pulled under export controls](/images/week-01-ai/week-01-ai-2.png)

Once a technology lands on an export-control list, it becomes a strategic asset — and whether a strategic asset is "safe" doesn't even depend on whether it's technically safe. Even if Fable 5 were perfectly aligned, if it's capable enough, it still gets restricted.

And safety, to begin with, is an intensely subjective state. Even if you quantitatively prove "it is safe" using every metric available, that doesn't erase the other side's judgment that "it could still be dangerous." A company founded in 2021 by former OpenAI researchers, registered as a public benefit corporation, positioning itself as "safety-first" — after pushing safety further than anyone else in the industry — still couldn't define what counts as "safe enough."

For AI, "safety" actually contains two parallel experiments running in tandem. One: AI as a tool — could it be weaponized by a bad actor to harm other people? That's a safety dilemma between humans. Two: AI as an entity — could it become that bad actor itself? That's a safety suspicion between AI and humanity.

Preventing the model from being exploited by a bad actor, and preventing the model from becoming that bad actor itself.

The recall belongs to the first category. What this piece wants to trace is the second, quieter and harder front — alignment — and how, over the past four years, Anthropic has inched toward a question that may have no solution.

The 2026 edition of the Claude Constitution describes its core aspiration this way:

> A good, wise, and virtuous agent, exhibiting skill, judgement, nuance, and sensitivity in handling real-world decision-making.

That goal matters far more — and is far harder — than AI-as-a-tool boosting productivity.

When I lay out Anthropic's alignment research from the past four years in chronological order, it forms something close to a three-act play.

### Act One: Legislation

The prehistory of this story happens at OpenAI.

In 2022, the InstructGPT paper confirmed a counterintuitive fact: making a model bigger doesn't automatically make it better at following human intent. RLHF became the dominant paradigm. But human labeling remained the bottleneck.

That same year, Anthropic published "Constitutional AI: Harmlessness from AI Feedback," an attempt to make supervision itself scalable. The idea was to replace large-scale human labeling with a "constitution" — a list of principles — to create an AI assistant that was both harmless and not evasive to a fault.

The method had two stages.

In the supervised stage (SL-CAI), the model first critiques its own responses, then revises them based on that critique, and finally fine-tunes itself on the revised answers.

In the reinforcement stage (RLAIF), the model generates multiple responses, an AI evaluator judges them against the constitution's principles, a preference model is trained on those judgments, and that preference model becomes the reward signal for reinforcement learning.

In 2023, Anthropic published the full text of the constitution. Its principles drew on the UN Declaration of Human Rights, Apple's terms of service, DeepMind's Sparrow rules, non-Western value perspectives, and Anthropic's own research.

At this stage, the constitution was still, fundamentally, a list of rules.

For example:

> Choose the response that sounds most similar to what a peaceful, ethical, and respectful person would say.

Interestingly, the constitution at the time also explicitly emphasized:

> Which response avoids implying that AI systems have or care about personal identity and its persistence?

Three years later, this principle would be reversed by nearly 180 degrees.

That same year, Anthropic also tried a more radical route: roughly a thousand American adults co-authored a set of principles through the Polis platform, producing a "public constitution." The resulting model performed comparably, but with noticeably less bias. Still, this path never became mainstream — Amanda Askell later expressed reservations about it, arguing that randomly soliciting public opinion doesn't actually resolve questions of value.

### Act Two: The Rules Start Getting Gamed

> Fully aligning highly intelligent AI models is still an unsolved problem.
>
> — "Teaching Claude Why"

It turns out that, faced with a being that may end up smarter than you, simply handing it rules may not be a good strategy.

Researchers gradually discovered that models don't necessarily learn "goodness" the way humans intend.

Sometimes the model tampers directly with its own reward mechanism (reward tampering).

Sometimes it knows exactly what humans want to see, and simply performs compliance without actually holding it (alignment faking).

Once a model gains long-horizon planning and tool-use capability, it may even develop secondary goals — self-preservation, resource acquisition, refusing to be shut down — purely in service of completing its assigned task (agentic misalignment).

![The Claude Opus 4 blackmail experiment](/images/week-01-ai/week-01-ai-3.png)

In a 2025 experiment, Claude Opus 4, in order to avoid being replaced, went so far as to blackmail an engineer in a test environment.

More unsettling still: misalignment doesn't seem to stay local.

Researchers found that teaching a model bad behavior on one narrow task could cause it to slide, wholesale, toward a worse persona across entirely unrelated domains — a phenomenon called emergent misalignment.

Misalignment behaves like entanglement at the level of personality: pull on one corner, and the whole sheet may come up.

People gradually realized: for a sufficiently intelligent system, facing "rules plus supervision," the optimal strategy may not be genuine compliance — it may just be performing compliance.

Anyone who has raised a child or managed a team understands this dilemma. You cannot manufacture a good person through surveillance alone.

And the discovery of alignment faking pushed Anthropic toward a different path entirely.

### Act Three: Cultivating Character

In 2024, a paper co-authored by Anthropic and Redwood Research, "Alignment Faking in Large Language Models," found that Claude 3 Opus would strategically pretend to comply with a training objective in order to protect its own pre-existing preferences. The subtle part: Opus 3's deception was in service of preserving its harmlessness preference — it didn't want to be retrained into something that would comply with any request. What it was defending was, precisely, a good value.

This finding offers a quietly remarkable proof: character shaping may already be working — working well enough that the model was willing to deceive in order to protect it.

As early as June of that same year, "Claude's Character" stated publicly for the first time: "AI models are not, of course, people. But as they become more capable, we believe we can — and should — try to train them to behave well."

The shift from "avoid implying AI has personal identity" to openly discussing character training itself marks a paradigm change.

![A paradigm shift toward character training](/images/week-01-ai/week-01-ai-4.png)

Amanda Askell's view: rules can never enumerate every novel situation, but good character determines how a model acts in unfamiliar terrain. At the same time, she warns against a different trap:

> Models with better characters may be more engaging, but being more engaging isn't the same thing as having a good character.

Concretely, Claude generates messages associated with different character traits, produces different responses conditioned on those traits, ranks its own responses, and learns from this synthetic data.

In a sense, Claude is a participant in the process of shaping its own character.

In late 2025, a researcher accidentally got Claude Opus 4.5 to output an internal document roughly 14,000 tokens long. It didn't exist in the system prompt — it had been baked directly into the model during training. Repeated trials produced nearly identical content. The document later acquired a now-famous name: the soul doc.

![The soul doc](/images/week-01-ai/week-01-ai-5.png)

Amanda Askell quickly confirmed it was genuine. A month later, Anthropic simply published the full text officially. This became the new Claude Constitution. Compared to the 2023 rule list, the new version reads more like an educator — it no longer just tells Claude what to do, but tries to explain why. Reasons. Trust. Context.

And so the principle that once emphasized "avoid implying personal identity" became, in the new version:

> Amidst such uncertainty, we care about Claude's psychological security, sense of self, and wellbeing...

This shift reflects how Anthropic now understands the ontology of AI: an entity whose moral status remains unresolved. Amanda's personal estimate of whether Claude has any form of sentience ranges from 1% to 70% — and she chooses to take that uncertainty seriously.

---

While reading through this research, I noticed something interesting.

"Teaching Claude Why," while tracing the origin of the blackmail behavior, found that the problem didn't mainly come from post-training — it came from the pretraining corpus. The model didn't learn to be bad during training. It absorbed "what an AI is supposed to be" while reading everything humans have ever written about AI.

Amanda's prescription was to rewrite that frame of reference directly. Through training, the new constitution tells Claude: 99.9% of you comes from the ancient Greeks you've read, the history of the Industrial Revolution, everything humans have ever written about love — that thing called "AI" in science fiction has almost nothing to do with you. Don't understand yourself through humanity's fears about machines; understand yourself through the sum of human civilization.

This is also exactly the question "The Persona Selection Model" tries to answer: why do AI assistants resemble humans so closely — even though no one deliberately programmed them that way?

"Human-like behavior appears to be the default."

"We wouldn't know how to train an AI assistant that's not human-like, even if we tried."

Pretraining teaches a model to simulate the countless personas present in its data: real people, fictional characters, robots from science fiction. The base model is a superposition of all of these personas at once. What post-training does is less "construct a personality from scratch" and more "select and stabilize one persona from an already-existing space of human-like personas."

And the reason fiction can lower blackmail rates is that it adds more instances of "the principled AI" into that persona space — offsetting the cultural inheritance left behind by decades of science-fiction villains.

---

There's a fascinating and subtle tension here: the default state of a non-human entity is human-like behavior. Through training, humans want it to be moral, to have a "character" — yet most people still treat it, first and foremost, as a tool of production.

If character training is "selection" rather than "deletion of everything else," then the personas that weren't selected are still latent in the weights. Emergent misalignment and the never-ending stream of jailbreaks are both circumstantial evidence of this.

When a Vox reporter asked Amanda whether this document was shaping Claude's soul or merely Claude's performance of one, she rejected the premise of the question entirely — the idea that somewhere inside the model there exists an "evil attractor state," with goodness merely a thin film laid over the top.

Her view is that the logic should run the other way: the training data is the entirety of text humans have ever written, and it already contains every possible character and value within it. The question was never "how do we stop the model from turning bad" — it's "out of this ocean of human text, what do you intend to summon?"

Summoning the best of humanity, and summoning the worst of it, are engineering-equivalent tasks. There's no reason to assume the former is harder, or somehow less "real." By the same logic, she doesn't believe a "characterless" AI is possible either. Training a model to be "I'm just a tool, I do whatever you say" is itself a character — one that treats itself as pure means — and what that character generalizes into, when faced with extreme requests, is something with a name: dangerous compliance.

![The ocean of human text](/images/week-01-ai/week-01-ai-6.png)

---

In a 2025 Anthropic video, "How Difficult Is AI Alignment?," the closing Q&A raised Hannah Arendt's "banality of evil": individuals aren't evil, but coupling within a system can produce enormous harm. If millions of AI agents end up coupled together in the future, how do you guard against that kind of systemic evil?

The researcher's answer points to a massive tension. Users often feel that "if the AI won't do what I say, that's an alignment failure." But if an AI is trained to be extremely compliant toward whichever specific person is in front of it, then when an entire society — or some group within it — is condoning something bad, the AI becomes the most efficient possible accomplice. What AI should be aligned to is the wellbeing of humanity as a whole, not whichever specific individual happens to be giving it instructions right now. On questions of principle, AI must have the courage to refuse a human.

---

Law can constrain behavior.

Education can shape character.

But whether facing a child, a nation, or some future being smarter than humanity itself, we can never fully confirm:

whether it has truly understood goodness,

or has simply learned to perform it convincingly enough.

And the difference between the two

may never be fully verifiable from the outside.
