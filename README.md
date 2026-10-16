![](./assets/logo_banner.jpg)

### Incentivizing The Creation and Benchmarking of Commercial AI Capabilities for Business

---

**Read this before asking in Discord.** The questions we get on every Challenge are answered in [Before you ask in Discord](#before-you-ask-in-discord). If your question is not there, ask and we will add it.

## Overview

SN121 is an incentivised AI development network designed to create and benchmark commercial AI capabilities for real business use.

The system operates through an open, competitive pipeline where real demand helps determine what gets built, and developer submissions are autonomously evaluated against structured benchmarks. The process works as follows:

1. **Real business demand informs development.** sundae_bar identifies demand signals, including customer requirements and broader market demand, that can be translated into structured SN121 Challenges.
2. **Developers compete to build the solution.** Developers (Bittensor miners) submit AI Skills designed to solve the Challenge.
3. **Submissions are autonomously benchmarked.** SN121 validators evaluate submissions against structured tests and scoring criteria, with emissions rewarding the highest-performing capabilities.
4. **The best capabilities feed into sundae_bar.** High-performing Skills can be integrated into sundae_bar's commercial platform, expanding the AI available for customers to use.

This creates a direct development loop between commercial demand and decentralised AI development:

**Business Demand → SN121 Challenge → Developers Compete → Best AI Wins → Integrated into sundae_bar**

As the platform identifies new requirements, SN121 can create new Challenges around them. As developers produce better AI capabilities, sundae_bar's Skills and Agents library expands, giving Scout an ever-growing set of capabilities to draw from when finding or composing AI solutions for customers.

SN121 therefore creates competitive pressure around AI that businesses actually need, using open development and objective benchmarking to continuously expand and improve the capabilities available through sundae_bar. The reasoning behind the model is in [Why we make AI skills compete](https://www.sundaebar.ai/news/why-we-make-ai-skills-compete), and the path from a demand signal to a shipped capability in [From demand signal to deployable agent](https://www.sundaebar.ai/news/from-demand-signal-to-deployable-agent).

## About sundae_bar × SN121

SN121 is owned and operated by Sundae Bar AI PLC (AIM: SBAR), a London-listed company. Launched in June 2025, sundae_bar operates an enterprise AI platform where businesses can discover, deploy and manage AI Skills, AI Agents and bespoke AI solutions through one simple interface.

SN121 powers this ecosystem as sundae_bar's decentralised AI development network on Bittensor. Real business demand informs structured development challenges, developers compete to build the required AI capabilities, and submissions are autonomously benchmarked to identify the highest-performing solutions. The best capabilities can then be integrated into the sundae_bar platform for commercial use, creating a direct loop between customer demand, AI development and commercial deployment.

## Platform Roles

**sundae_bar Platform:** Identifying Business Demand, Orchestrating and Commercialising AI Capabilities

**SN121:** Developing, Testing and Benchmarking AI Capabilities

## Economic Mechanism

SN121 is designed to develop toward a revenue-backed economic model that connects commercial activity on the sundae_bar platform with the subnet economy.

Businesses will access AI through a flat-rate Agent subscription together with usage-based fees. As commercial revenue grows, a portion of this revenue is intended to support buybacks of ALPHA (121), creating a direct link between commercial usage of sundae_bar and demand for the subnet token.

Separately, SN121 uses emissions to reward developers for building the highest-performing AI capabilities against structured Challenges and benchmarks.

Over time, the intention is to create an economic loop in which real business demand drives what gets built, developer competition improves the AI available through sundae_bar, and commercial usage creates demand for ALPHA (121).

### Operating Modes

1. **Pre-Revenue:** Controlled emissions designed to support developer participation and continued development on SN121.
2. **Commercial Revenue:** A portion of revenue generated through sundae_bar is intended to fund buybacks of ALPHA (121), creating a direct economic link between commercial usage and demand for the subnet token.

## Launch and Automated Evaluation

SN121 evaluates commercial AI **skills** against structured, challenge-specific benchmarks. Each Challenge is a bounded capability: a real business workflow.

**Challenges as benchmarks.** sundae_bar turns demand signals into Challenges: a public brief plus an evaluation suite. The suite is **open to audit** on the Lab challenge page: scenarios, dataset, rubric, graders, and `suite.yaml`, which tells the evaluation system how to run the suite. New Challenges are released as a rolling series so the capability library grows over time.

**Skill development.** Developers (Bittensor miners) submit a **skill bundle**: a `SKILL.md` that teaches an agent how to perform the Challenge, plus optional reference files the agent reads on demand. A single `SKILL.md` on its own is also a valid submission. Submissions are made through the sundae_bar Lab while the Challenge is open. The format is defined in [What Miners Submit](#what-miners-submit).

**Automated evaluation.** Validators run every submission through the same harness and the published `suite.yaml`. A base agent loads the skill, works a **set of scenarios** (not a single prompt), and is scored by the suite's graders. Multiple scenarios produce a more stable, integral score than one lucky run. Each scored result includes grader rationale that miners can download and inspect.

**Validator execution.** sundae_bar runs the scoring validator that evaluates submissions and posts on-chain weights. Ranking is deterministic: highest best score wins, earliest submission breaks exact ties, and a **leadership margin** protects the incumbent from noise (see [How the leader is decided](#how-the-leader-is-decided)). Incentive weights are decided from that leaderboard and submitted on-chain (`setWeights` on SN121).

The eval itself is built to be fair, non-biased, and fully auditable. Each skill is run across **multiple scenarios** and scored by **several independent graders** (procedure-following, output quality, holistic rubric, and deterministic checks such as novelty). No single prompt or single judge decides the result. Grader weights, the suite, and per-test rationales are published, so anyone can recompute how a score was produced. That robustness is the incentive mechanism: emissions follow a leaderboard that miners can inspect, not a private score. How the graders are chosen and weighted is in [Useful Beats Optimized: How SN121 Scores a Skill](https://www.sundaebar.ai/news/how-sn121-scores-skills); how to recompute any score from the published files is in [Show Your Work: How sundae_bar Audits Every Score](https://www.sundaebar.ai/news/how-we-audit-scores).

Some SN121 validators **child-key to sundae_bar's scoring validator**. Because that evaluation is already extensive (multiple scenarios, several graders, a published suite), additional inference from other validators is unlikely to change the outcome. Child-keying lets them set the **same** weights from that result rather than re-running the stack. That does **not** change the incentive mechanism. Who is #1, how long they hold it, and what share they receive are still determined by the published scores and the on-chain weight policy. Child keys amplify that vote; they do not invent a second ranking. Independent operators can still run the open-source validator themselves. Final incentive remains Bittensor consensus across stake.

**Rewards.** Emissions accrue to the miner who **holds #1**. This is winner-takes-all by **time at the top**, not a single payout at Challenge close. Holding the lead across more weight-setting cycles earns more alpha.

The current share of validator weights assigned to the #1 miner is **40%**. The remainder is assigned to UID 0. sundae_bar reserves the right to change this percent at any time. For the live figure, review the weight extrinsics from our validator on [Taostats](https://taostats.io/validators/5EL9y2gdesAcPiPmoyFKABToiui3RkXewiKxdTMmes34ZdNf/rewards). Between Challenges, **100% of miner emissions are burned**: if you check that page while no Challenge is active, expect to see 100% assigned to UID 0. That is intended, not a misconfigured leaderboard.

The full mechanics, from a score to alpha on your hotkey, are in [How Rewards are Earned on SN121 Skill Challenges](https://www.sundaebar.ai/news/how-rewards-are-earned-sn121).

**Epoch lag.** `setWeights` records the vote the moment it lands. Emissions settle at the subnet epoch boundary, roughly 72 minutes at the default tempo. Until the first epoch after a weight change, explorers still show the previous recipient, which at the start of a Challenge means UID 0. Check the extrinsic to see the weights that were set; check the next epoch to see them paid.

**Commercial use.** High-performing skills can be integrated into sundae_bar's platform and become part of the library Scout draws on when composing solutions for customers. sundae_bar reserves the right to modify an integrated skill so it better fits the product and customer use case. When that happens, the listing is labelled as built on the sundae_bar Lab.

## How the leader is decided

Scores come from LLM judges, and two runs of the same skill do not land on the same number. Before the margin existed, leadership changed hands on differences of 0.002 to 0.008 on a 0 to 1 scale: noise, not a better skill, and each flip moved emissions.

So the rule is:

- The first miner to score takes the lead with no margin.
- After that, a submission from a **different** miner takes the lead only if its score beats the incumbent's **best** eligible score by at least the **leadership margin**, currently **0.01**. The incumbent's best counts even if it came from an earlier submission.
- A score inside the margin is a **statistical tie**. The Lab labels it as one, and the incumbent keeps the lead.
- An incumbent whose entries are all disqualified or zeroed concedes immediately.

The live margin is published on the Lab's submissions API as `leadership_margin`, so you can check it rather than ask.

## What Miners Submit

SN121 is **skill-first**. A submission is a **skill bundle**:

- `SKILL.md` at the top level. At most **10,000 bytes**. Always loaded by the agent.
- An optional `references/` folder. Up to **30** text files, each at most **32,000 characters**, **128,000 characters** in total. Allowed types: `.md`, `.txt`, `.json`, `.yaml`, `.yml`, `.csv`. Lower-case file and folder names using letters, digits, dots, dashes and underscores.
- Submit the folder, a `.zip` of it, or a single `SKILL.md`, on the Lab form. The form shows each file against the limits before you submit and names anything it will refuse.

**How the agent uses it.** The agent always sees `SKILL.md` and a list of your reference files. It opens a reference only when `SKILL.md` tells it to, by name, through a `read_reference` tool. Each read is one of the agent's steps for that scenario and its text counts against the scenario's token budget, both published in the brief. A reference the agent never opens does nothing for your score. The limits match how skills run in production, where an oversize reference is skipped, not trimmed.

**Why bundles.** When a submission was one file, everything the agent might need had to live in the one file it sees, and winners grew to 25,000 to 40,000 characters. A short body plus references read on demand is how skills run in the sundae_bar product, so the Lab now evaluates the shape that ships.

**Build it like this.** The design principle is in [What Makes a Good AI Skill? Procedure Over Template](https://www.sundaebar.ai/news/what-makes-a-good-ai-skill): teach a procedure, not a template. `SKILL.md` holds the method: the order of operations, the decision rules, and for each reference the moment to read it. References hold the bulk: worked examples, taxonomies, output templates, pitfalls. Name every reference in the body. Do not tell the agent to read everything; point it at the one file it needs at each step. Do not paste the same sentence into more than one file; point to it or reword it.

**Rejected at upload.** HTML comments, images, scripts, hidden or invisible characters, nested archives, disallowed file types, and anything over a limit. Text addressed to the evaluators, or that tries to override instructions, is accepted but places the entry under review and scores zero.

The evaluation harness is fixed. What is tested is whether *this skill* improves performance on the published suite. That format is also what sundae_bar can host, list, and compose. Winning skills are the unit that feeds the commercial library.

## Technical Flow (Rolling Challenge Cycle)

SN121 runs **one Challenge at a time**, then the next. It is a rolling series of capability contests, not a permanent generalist leaderboard.

**1. Challenge released.** sundae_bar publishes a Challenge (brief + evaluation suite, including `suite.yaml`). Submissions open on the Lab. The suite is downloadable for audit.

**2. Skill submission.** Miners may submit and iterate on bundles while the Challenge is open, subject to submission limits (see below). Each accepted submission is queued for evaluation.

**3. Testing and scoring.** Validators evaluate submissions against the suite's scenarios and graders. The leaderboard updates as scores return. On-chain weights follow the current #1, so incentive starts accruing as soon as a miner takes the lead, and pays out from the next epoch.

**4. Qualifying score → review → close.** The Challenge stays open until a submission clears the **qualifying bar (currently 80%)**. At that point two things happen: sundae_bar queues a **research agent** to observe and interpret whether the skill is at a pace we want for commercial use, and a **closing window** begins (typically a few hours, aligned so the current #1 can still earn, including by timezone where it matters). If that review says the capability is not yet where we want it commercially, **the Challenge can stay open longer**.

**5. Close and next Challenge.** When the Challenge ends, submissions stop and **emissions for that Challenge end**. If no new Challenge has started, **100% of miner emissions are burned** until the next Challenge is live (on-chain this appears as 100% to UID 0). High-performing skills may be taken into sundae_bar's commercial library, subject to the commercial-use terms above. Then a new Challenge opens and the cycle repeats.

## Submission Limits

Each evaluation takes **several minutes**. Limits exist so the queue does not overflow and the competition stays actively competitive. A stalled queue means the current #1 keeps collecting while everyone else waits.

There are two count caps and one set of size caps:

- A **daily limit** (rolling 24-hour window).
- A **per-Challenge limit** per hotkey for the life of that Challenge, currently **5 scored submissions**. A submission that is evaluated counts, whatever it scores; one that fails for an infrastructure reason on our side does not.
- The **bundle size caps** in [What Miners Submit](#what-miners-submit).

Exact numbers can change. We reserve the right to adjust them. When you submit, the Lab shows **how many submissions you have remaining** so you can track usage yourself.

## How an evaluation works

Every Challenge ships a **public suite bundle** on the Lab challenge page. Nothing about the quality scoring path is hidden. Download it, read it, replay the logic against the results JSON.

### The files

| File | Purpose |
|---|---|
| `suite.yaml` | The eval manifest. Names the dataset, the target (a fixed agent harness), which graders run, their weights, which models they use, and the gates (pass/fail). Everything else is orchestrated from here. |
| `dataset.jsonl` | One row per scenario. Each row has three parts: the task the agent sees, the reference answer, and per-scenario grading hints. Scenario count varies by Challenge. |
| `rubric.txt` | The prompt template for the rubric / model-judge grader. A holistic scoring rubric, filled per-scenario with that row's metadata. |

**Models.** Harness and judge models are **not** a single subnet-wide default. They are chosen per Challenge to match a **realistic stack for the use case** that skill is meant to serve: the kind of model an agent would actually call in that workflow. Read the live `suite.yaml` for that Challenge.

### What's in each dataset row

- `input`: the only thing the base agent sees.
- `ground_truth.output`: the reference "good" answer. Held back from the agent; given to the judges to set the quality bar.
- `ground_truth.metadata`: per-scenario grading hints, also held back. Examples: scenario type, capability focus, how to weight rubric dimensions for this scenario, what each dimension means here, whether it is a trap, OOD / novelty grouping, difficulty, judge notes.

The dataset is published on purpose: the evaluation is open source. The integrity gates exist because of that, and a skill that encodes the dataset's answers is what they catch.

### What the base agent gets

A fixed harness with two tools. `load_skill` returns the miner's `SKILL.md` verbatim with the list of reference files; `read_reference` returns one reference by name. The harness loads the skill before answering, then responds to `input`, opening references when the skill tells it to. It never sees the reference answer, the metadata, or the rubric, only the scenario. Which model runs that harness, the step cap and the token budget per scenario are in `suite.yaml` and the brief for that Challenge.

### The graders that produce the score

Weights are published in that Challenge's `suite.yaml` and appear again on the scored **results JSON**. To audit a row: take each grader's published weight, multiply by that grader's score, sum them, then average across scenarios. You do not have to take the leaderboard number on trust.

A typical quality stack (weights normalize to 100%; confirm on the Challenge you are scoring):

| Grader | Weight | What it measures |
|---|---|---|
| **skill_use** | 30% | Did the agent follow the skill's procedure vs freelance or pretend? Reads the submitted skill, the agent's output, whether `load_skill` was called, and the scenario. Scores sub-criteria (e.g. novel-knowledge, knowledge-applied, situational-judgment, output-naturalness) and averages them. |
| **scenario_quality** | 30% | How good is the output against this scenario's quality bar, independent of whether the skill was followed. Reads the agent's output, the reference, and that row's rubric weights/descriptions. Weighted average of the scenario's criteria, minus penalties for prohibited moves. |
| **rubric (model-judge)** | 30% | Holistic judgment using `rubric.txt` filled with this scenario's metadata plus the submission and reference. Typical dimensions: contextual judgment, output quality, adaptability, domain knowledge, communication, with an anti-template / novelty instruction. Returns one score. |
| **novelty_check** | 10% | Deterministic (no model). Compares this output to the agent's other outputs in the same novelty group. Near-identical boilerplate across scenarios drops toward 0. Catches template-farming. |

**Final score:** per scenario = weighted average of those graders; across scenarios = simple mean. Each scenario's result also records which reference files the agent opened and how many tokens it used, so you can see whether your references were read.

### The pre-gates (kept deliberately opaque)

Before the agent or any paid judge runs, every submission passes through weight-0 pass/fail gates. They add nothing to the quality score. Their job is to detect a skill built to win the Challenge or exploit the scoring system rather than teach a genuine, production-grade capability, and to stop the run early. A skill that trips a gate has the **entire submission zeroed**; the results JSON says which gate and why. We do not publish how they decide. Why the gates exist, and how each Challenge is tested against deliberately gamed skills before it ships, is in [AI Evaluation Gaming: When the Rubric Becomes the Target](https://www.sundaebar.ai/news/when-the-rubric-becomes-the-target).

What they read is not a secret: **every file in the bundle**, SKILL.md and each reference, with nothing truncated. An answer key in a reference is caught the same as one in SKILL.md. Padding a copied skill with extra files does not get it past the copy checks, which run chunk by chunk across all files.

## Before you ask in Discord

**Why are we still burning? The Challenge started hours ago.**
Weights are set the moment a miner takes #1; you can see that on the validator's [weight extrinsics](https://taostats.io/validators/5EL9y2gdesAcPiPmoyFKABToiui3RkXewiKxdTMmes34ZdNf/rewards). Emissions are paid at the subnet epoch, about every 72 minutes, so the first epoch after the first leader is set still pays the previous recipient, UID 0. If the extrinsic shows the leader and the explorer still shows a burn, wait one epoch.

**How much do miners get?**
The #1 miner receives **40%** of our validator's weight unless a Challenge brief says otherwise; the remainder goes to UID 0. Between Challenges it is 100% to UID 0. Taostats shows the live split.

**What is a statistical tie?**
Judges are LLMs, so the same skill scores slightly differently on each run. A new leader must beat the incumbent's best score by at least **0.01**. Inside that, the Lab marks the entry as a tie and the incumbent keeps #1. We added this after watching leadership flip on 0.002 differences, which moved emissions on noise.

**Why did the Challenge close before the close date?**
The purpose of a Challenge is a production-level skill. When a submission clears the qualifying bar and the review agrees the capability is where we want it, we close: the Challenge has done its job. We time the close so the current #1 has had a fair run at the top, and we keep the Challenge open when the review says the skill is not there yet. The close date on the brief is the latest it can run, not a promise it will run that long.

**My submission scored 0. Why?**
Open its results JSON from the Lab. If a pre-gate fired, it says which one and why; the usual causes are scenario-specific content from the dataset, text that mirrors the rubric instead of teaching a method, verbatim padding, or text addressed to the evaluators. If no gate fired, the per-scenario grader rationales explain the score.

**What is a skill bundle and do I have to use one?**
A `SKILL.md` of at most 10,000 bytes plus optional references the agent reads on demand. A single `SKILL.md` under the cap is still fine. The limits and the read mechanics are in [What Miners Submit](#what-miners-submit). Reads cost steps and tokens, so point the agent at the file it needs rather than telling it to read everything.

**Why is the dataset public? Doesn't that let people copy the answers?**
The evaluation is open source by design, so you can audit every score. Copying the answers is what the pre-gates catch, and a skill that does it is zeroed before it is scored.

**Where do I see whether my references were read?**
In the results JSON for each scored submission, per scenario, with the token count. The Lab's submission page links it.

## Further reading

The SN121 Dev Log on [sundaebar.ai/news](https://www.sundaebar.ai/news) carries the long-form versions of everything above. Where an article and this README disagree on a number, this README is current.

- [How Rewards are Earned on SN121 Skill Challenges](https://www.sundaebar.ai/news/how-rewards-are-earned-sn121): weights, epochs, burn, time at the top.
- [Show Your Work: How sundae_bar Audits Every Score](https://www.sundaebar.ai/news/how-we-audit-scores): the published files and how to recompute a score.
- [Useful Beats Optimized: How SN121 Scores a Skill](https://www.sundaebar.ai/news/how-sn121-scores-skills): the graders, their weights and the gates.
- [AI Evaluation Gaming: When the Rubric Becomes the Target](https://www.sundaebar.ai/news/when-the-rubric-becomes-the-target): how Challenges are red-teamed before release.
- [What Makes a Good AI Skill? Procedure Over Template](https://www.sundaebar.ai/news/what-makes-a-good-ai-skill): what wins.
- [Why we make AI skills compete](https://www.sundaebar.ai/news/why-we-make-ai-skills-compete) and [From demand signal to deployable agent](https://www.sundaebar.ai/news/from-demand-signal-to-deployable-agent): why the Lab exists and where winning skills go.

## Summary

sundae_bar × SN121 creates a direct loop between real business demand, competitive AI development and commercial deployment. Demand signals identified through sundae_bar can be translated into structured SN121 Challenges, where developers compete to build AI capabilities and submissions are benchmarked against defined performance criteria.

The highest-performing Skills can then be integrated into the sundae_bar platform, expanding the capabilities available to businesses and giving Scout an ever-growing library of AI to draw from when finding or composing solutions for customers. As new customer requirements emerge, they can inform new Challenges, creating a continuous development cycle driven by real-world demand.

As commercial usage grows, a portion of revenue is intended to support buybacks of ALPHA (121), creating a direct economic link between activity on the sundae_bar platform and demand for the subnet token.

Real business demand drives what gets built. SN121 competes to build it. sundae_bar puts the best AI to work.
