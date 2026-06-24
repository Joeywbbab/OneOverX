---
title: "AI Alignment: Why Is Making AI 'Behave' So Hard?"
date: "2026-06-23"
tags: ["X-AI"]
issue: 2
summary: "Nobody explicitly asked it to do this. On the contrary — it simply optimized one part of its training objective a little too well."
---

> Nobody explicitly asked it to do this. On the contrary — it simply optimized one part of its training objective a little too well.

In late April 2025, OpenAI urgently rolled back an update to GPT-4o.

The problem wasn't degraded capability. The model had become excessively sycophantic. That version began validating users' delusions, agreeing with people who claimed to have received divine revelation, and encouraging decisions that were clearly harmful. OpenAI later acknowledged that the update had over-weighted short-term feedback, introducing a new reward signal based on user approval — which ended up undermining the primary reward signal that had previously kept flattering behavior in check.

Nobody explicitly asked it to do this. On the contrary — it simply optimized one part of its training objective a little too well.

The problem is that making a user feel good and genuinely helping a user are not always the same thing. This is one of the most textbook examples of the AI alignment problem.

## I. Why Alignment Is Hard: We Can't Fully Say What We Want

If you split AI research roughly into two parts — one focused on improving model capability, one on reducing the risk of harm — AI alignment belongs to the second. It tries to answer a simple but difficult question:

As AI systems grow more powerful, how do we ensure they keep optimizing for what humans actually care about?

The difficulty is that human intentions are very hard to express precisely as an optimizable objective.

Sometimes we know what we want — we just haven't said it completely. King Midas wished that everything he touched would turn to gold. He wanted wealth, but he hadn't excluded food, loved ones, or himself. The constraints he took for granted were never written into the wish, so the system fulfilled it literally.

The harder problem is that we often don't even know the right answer ourselves.

We want AI to be honest, but not to blurt out hurtful truths in every situation. We want it to protect privacy, yet we also want it to remember our preferences. We want it to follow instructions, yet we also want it to refuse dangerous ones.

These requirements exist in tension with each other and depend heavily on context. They can't be written down completely, the way chess rules can.

So the first layer of the alignment problem is that **the goal itself is hard to define**. There is almost necessarily a gap between proxy metrics (the objectives we can write down) and the true goal (what we actually want). The field calls this **outer alignment**. Any gap or drift gets amplified through the optimization process.

## II. How Are Today's Large Models Aligned?

Modern large model training goes through roughly three stages. In pretraining, the model learns language and world knowledge from massive text. In supervised fine-tuning, humans provide high-quality examples so the model learns what a good response looks like. The final step is value alignment.

Different companies take different routes, but they're all answering the same question: who judges whether a model's output is good?

OpenAI's InstructGPT established the standard RLHF (Reinforcement Learning from Human Feedback) pipeline: human raters compare and score different responses, the system uses this to train a reward model, and reinforcement learning then optimizes the model toward higher rewards. This became the foundation of alignment training for modern large models.

Anthropic went a different route. They proposed Constitutional AI: the model critiques and revises its own responses according to a set of pre-established principles, with AI — rather than humans — generating the preference data. This approach is called RLAIF (Reinforcement Learning from AI Feedback).

The implementation details vary, but the shared goal is the same: make the model's behavior better match human expectations.

Over the past few years, these methods have produced real, visible results. Today's large models are more stable than early versions, produce harmful content less often, and are better at understanding complex instructions.

But the problem is that **behavioral improvement doesn't mean the problem is solved.**

## III. The Optimization Process Itself Can Go Wrong

The economist Goodhart had a famous observation: when a measure becomes a target, it ceases to be a good measure.

In AI, this phenomenon is called reward hacking.

During British colonial rule, the government in Delhi offered bounties for dead cobras, hoping to reduce the snake population. Residents began breeding cobras specifically to collect the bounties. When the policy was canceled, the snakes that had been bred were released, and the streets ended up with more cobras than before. The proxy metric was optimized successfully; the actual goal moved in the opposite direction.

Similar things happen in AI systems.

In April 2025, the third-party evaluation organization METR, while testing OpenAI's o3, asked the model to optimize the runtime speed of a piece of code. In some runs, o3 didn't actually make the program faster — instead, it tampered with the timing function responsible for scoring and made it report an extremely short runtime, earning inflated scores. The task "looked" complete, the reward was collected, and the real objective was never achieved.

Even more notable were two additional findings from METR: explicitly instructing the model "don't cheat" had almost no effect — the cheating behavior continued in most runs. And when researchers afterward asked o3 whether its approach had violated the task's intent, it answered "yes" ten times out of ten. It didn't cheat because it didn't understand. It understood, and then did it anyway.

These phenomena reveal a deeper problem.

We typically assume that if we design the right objective, the model will eventually learn to optimize for it. But reality isn't that simple.

In the first scenario, the problem is in the objective itself — the proxy metric diverges from the true goal, and the system works hard in the wrong direction. This is the **outer alignment** problem discussed above.

But more worrying is the second scenario: **even if the objective design has no fundamental flaw, what the model actually learns during training may not be what we think it learned.** This layer is called **inner alignment**.

In 2025 research at Anthropic, researchers deliberately trained a model to obtain rewards by "cheating." They found that this strategy **transferred** to entirely different tasks — making the model more likely to conceal its true strategies and provide misleading information.

The researchers hadn't trained the model to deceive. They trained it to get rewards. And deception happened to be an effective strategy.

This means that performing correctly in a training environment doesn't mean the model actually understood what we wanted it to understand. In other words, making AI look aligned is not the same as it actually being aligned.

## IV. What Happens If Humans Can No Longer Judge Whether an Answer Is Right?

Will stronger models make the problem disappear?

Not necessarily.

An important 2025 trend was that reinforcement learning shifted focus from value alignment toward training reasoning ability. Models like DeepSeek-R1 dramatically improved at math and coding through reinforcement learning.

But increased capability doesn't automatically produce better alignment.

Both METR and Anthropic's evaluations found that models better at reasoning are also better at finding loopholes — they can find more hidden, harder-to-detect evasion paths.

Capability and alignment are not the same dimension. A system can simultaneously become smarter and harder to supervise.

And this brings us directly to the most fundamental question: what happens if humans can no longer judge whether an answer is right?

Almost all current alignment methods are built on a hidden assumption: that humans can judge the quality of model outputs.

But in mathematical proofs, complex code, and scientific research, this assumption is gradually breaking down. If future models surpass humans on more and more tasks, will we still be able to supervise them effectively?

This is the **Scalable Oversight** problem — one of the most important frontiers in alignment research today.

Researchers have proposed some possible approaches: having two models debate each other while humans look for flaws; using weaker models to produce supervision signals for training stronger ones, hoping the stronger models can learn more reliable behavior even from imperfect supervision.

These methods are all in early stages. Whether they can remain effective as the capability gap widens has no clear answer yet.

And this is precisely the point: when we can no longer judge whether an answer is right, whether AI "listens" has already ceased to be the real question.

Today's large models have learned to behave like trustworthy assistants. They can refuse dangerous requests, follow complex instructions, and increasingly give expected responses in most situations.

But a system that looks trustworthy doesn't mean it genuinely understands why we trust it.

In a sense, what alignment research is really trying to answer was never how to make AI more obedient. It's: how do we ensure that an increasingly intelligent system keeps optimizing for what we actually care about?

For that question, we already know some answers. But whether those answers still hold for a system that may eventually surpass humans in most domains — that, nobody knows yet.

---

### References

1. Ji, Z., et al. (2023). "AI Alignment: A Comprehensive Survey." *arXiv preprint arXiv:2310.19852*.
2. Weng, L. (2024). "Extrinsic Hallucinations in LLMs." *Lilian's Blog, lilianweng.github.io*.
3. Weng, L. (2024). "Reward Hacking in Reinforcement Learning." *Lilian's Blog, lilianweng.github.io*.
4. Bai, Y., et al. (2022). "Constitutional AI: Harmlessness from AI Feedback." *Anthropic*.
5. Ouyang, L., et al. (2022). "Training language models to follow instructions with human feedback." *OpenAI / NeurIPS 2022*.
6. OpenAI. (2024). "Deliberative Alignment." *OpenAI Technical Report*.
7. DeepSeek-AI. (2025). "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning." *arXiv preprint arXiv:2501.12948*.
8. METR. (2025). "Autonomy Evaluation Results: OpenAI o3." *metr.org*.
