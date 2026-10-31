---
layout: post
title: "Measure every step your agents take, not just the final one"
date: 2026-10-31 07:30:00 -0600
description: "A new paper on prefix executability shows why final task success is a weak metric for tool-using agents and what TeamStation AI does about it."
tags: [agents, delivery, teamstation, cto, reliability, evaluation]
author: TeamStation AI
source_links:
  - http://arxiv.org/abs/2610.40444v1
---

A new paper from arXiv argues that we have been scoring tool-using agents the wrong way. The authors call their fix prefix executability. The idea is simple. When an agent runs a chain of tool calls, do not just ask whether the final answer was right. Ask whether every step along the way could actually run under the real tool schemas, state preconditions, and data dependencies. You can read the paper at http://arxiv.org/abs/2610.40444v1.

That sounds academic. It is not. If you buy agentic delivery, this is the metric that separates a demo from a system you can run on Monday.

## The problem with final success

Most agent benchmarks today ask one question. Did the task finish? If yes, score one. If no, score zero. That rubric treats a lucky recovery and a clean execution the same way. It also treats a failed first attempt the same as a brittle five-step dance that only works because the environment happened to be in a cooperative state.

Final success is a lagging indicator. It tells you what happened. It does not tell you how much runway you had, or which failure mode you were one unlucky input away from. If delivery is the thing you are paying for, that gap is not acceptable.

Prefix executability turns the lens around. For every predicted tool call sequence, you check each prefix. Prefix one. Prefix two. Prefix three. At every step, you ask whether the current call is admissible given the schema and the state the agent believes it is in. The protocol in the paper summarizes this with a few numbers. Prefix Executability Curves (PEC) chart the probability that a prefix of length k is executable. First-Error Depth (FED) tells you how deep the agent got before the first inadmissible call. Trajectory Executability Rate (TER) is a single rate across prefixes. Recovery Rate (RR) measures how often the agent repairs itself after an error.

That is a shift from "did it work" to "where did it almost fail, and did it know." For anyone running delivery, that distinction is everything.

## Why this matters for engineering squads

TeamStation AI builds agentic engineering squads for US CTOs and CIOs, backed by nearshore LATAM Managed Engineering Seats. We hear the same question from every buyer. Will it still work in week six, under real load, when something upstream changes.

Final success scoring cannot answer that. It cannot tell you whether an agent sneaks through a flaky prefix every time it runs. It cannot flag a trajectory that only works because the data store was warm. It cannot tell you which parts of a plan are robust and which are held together with wishful thinking.

Per-step evidence can. If you track prefix executability across a week of real tasks, you see where the squad is thin before the thin spot breaks. You see which tools your agents misuse at depth four and never at depth one. You see which plans fail at the same hop every time, which usually points at an unstated precondition that no one wrote down.

That is operational signal. It converts "the squad felt faster this sprint" into evidence you can defend in a quarterly review.

## Where this plugs into our stack

We treat delivery as something that must be measured, not promised. The agentic layer is one half of that. The other half is the human seat.

Axiom Cortex is our neuro psychometric evaluation for candidate engineers. It does the human equivalent of what prefix executability does for agents. Instead of grading on the final offer decision, it grades on the per-task signals that predict whether a candidate will perform under load, under ambiguity, and under pressure. You do not want to find out in month three that someone looks great on a resume and freezes on the fourth step of a real plan. You want to know before the seat is sold.

When you pair that candidate signal with per-step agent telemetry, you get a system where both sides of the delivery, the human seat and the agentic squad, carry falsifiable claims about how they will behave. If the squad drifts, the prefix curves show it. If a seated engineer drifts, the per-task signals show it. Nothing is left to the warm feeling at a retrospective.

## What a CTO or CIO should actually ask vendors

If you are evaluating an agent vendor this quarter, three questions follow from the paper.

Ask how they measure trajectory executability. If the only number they offer is a win rate on a benchmark suite, they are selling demos. Ask what their First-Error Depth looks like on your workflow, not theirs. Depth matters because real plans are long. Ask what their Recovery Rate is. An agent that fails and silently moves on is not safer than one that fails loudly, it is just quieter.

If you are evaluating a staffing vendor, ask the same thing of the humans. What is the per-task signal. What is the drift under load. What is the recovery behavior. If the answer is a reference call and a stack of logos, you are being sold a feeling.

## Why depth is the honest unit

One point from the paper is worth sitting with. The authors emphasize that final success collapses an entire plan into a single bit. Everything the agent did between step one and the terminal state becomes invisible. Depth, by contrast, is honest. It tells you how far the plan got, where it broke, and what shape the break had. In a long running engagement, depth is what you measure to catch regressions, because regressions almost never show up at the end. They show up in the middle, where no one is looking.

For a CIO defending an annual spend, that middle is where the real conversation happens. Did we deliver more. Did we deliver more reliably. Did the plans get longer and still finish. Prefix executability gives you a way to answer each question with evidence instead of a quarterly feeling.

## What TeamStation AI does about it

We run every agentic squad with per-step telemetry, and we run every candidate through Axiom Cortex before the seat is placed. The result for the buyer is predictable delivery that holds up when you look under the hood. If you want to see how prefix level evidence changes a quarterly plan, book a demo at https://teamstation.dev.
