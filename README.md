---
bibliography: bib.bib
format: gfm
title: Endogenous model shifts in algorithmic recourse
toc-title: Table of contents
---

Responsible Professor: Dr. Cynthia Liem Supervisor: Patrick Altmeyer

## Background and motivation

Algorithmic recourse is an approach towards not only explaining
black-box machine learning algorithms, but provide subjects who have
been adversely affected by such with a realistic set of actions they can
take in order to revise their outcome. The approach has been quickly
growing in popularity during recent years, perhaps because the
underlying tend to be methodologies tend to be intuitive and easy to
implement. This project aims to shed some light on what happens *after*
recourse is actually implemented. In particular, we want to investigate
if and how the resulting domain shifts lead to model shifts and compare
outcomes for different recourse generators.

The topic is also of great importance to society since automated
decision-making through black-box algorithm affects all of us -
inlcuding you! Suppose, for example, that upon graduation you apply for
a job at a large coorperation. Unfortunately, you soon receive an email
stating that you have not “met the short-listing criteria and no further
feedback can be provided”. Unbeknown to you, the company has used an
algorithm to decide who makes it onto the short list. The HR teams does
not fully understand the inner workings of the algorithm, so they
genuinely cannot provide you with feedback.

Algorithmic recourse aims to resolve these types of issues. But existing
work has paid little attention to the dynamics of recourse. The first
paper to consider the problem that algorithms are updated in response to
(exogenous) domain shifts was presented at NeurIPS in December 2021
(Upadhyay, Joshi, and Lakkaraju 2021). The authors propose a recourse
generator that is robust to “small (and not drastic)” shifts. But rather
than small shifts, we find that the actual implementation of recourse
can lead to potentially quite large domain shifts and consequently model
shifts. The animation below illustrates this: after a small share of
individuals moves across the decision boundary, the classifier is
updated in response. Evidently, the model shifts are quite significant
in this toy example. Below we refer to these types of shifts as
*endogenous* shifts.

We think that endogenous shifts deserve attention for various reasons:

1.  Our initial experimental results suggests that even generators that
    aim to produce realisitic counterfactuals can induce significant
    domain and model shifts.
2.  Model shifts in response to some individuals’ recourse may lead to
    undesired consequences (label switch) for other individuals.
3.  Individuals that have implemented recourse may end up forming their
    own distinct cluster in the feature domain. The original classifier
    could therefore be adapted to distinguish “recourse” indviduals in
    the target class from those that were always in the target class.

![](www/model_shifts.gif)

For a gentle introduction to the topic of algorithmic recourse you can
check out this
[primer](https://towardsdatascience.com/individual-recourse-for-black-box-models-5e9ed1e4b4cc)
written by Patrick as part of his PhD application. To familiarize
yourself further with the topic and
[CARLA](https://github.com/carla-recourse/CARLA) you should all read
this [paper](https://arxiv.org/pdf/2108.00783.pdf).

## Research Questions for the Sub-Projects

Collectively, students will discuss and agree on an answer to the
following question:

-   How can we quantify endogenous domain and model shifts?

Individually, each of the students will then choose one of the recourse
generators already implemented in
[CARLA](https://github.com/carla-recourse/CARLA) and run a simple
experiment (details below) to generate endogenous shifts and quantify
their magnitude. You will also each produce results for the baseline
generator
([Wachter](https://arxiv.org/ftp/arxiv/papers/1711/1711.00399.pdf)) and
benchmark the results from both generators.

You are free to choose any of the generators already implemented
[CARLA](https://github.com/carla-recourse/CARLA), but below are five
suggestions:

1.  [FACE](https://arxiv.org/pdf/1909.09369.pdf), (Poyiadzi et al. 2020)
2.  [REVISE](https://arxiv.org/pdf/1907.09615.pdf), (Joshi et al. 2019)
3.  [CEM](https://arxiv.org/pdf/1802.07623.pdf), (Dhurandhar et al.
    2018)
4.  [CEM-VAE](https://arxiv.org/pdf/1802.07623.pdf), (Dhurandhar et al.
    2018)
5.  [AR-LIME](https://arxiv.org/pdf/1809.06514.pdf), (Ustun, Spangher,
    and Liu 2019)

**Experiment**

The idea is that you replicate a variation of the following experiement:

1.  Train an algorithm ℳ for a binary classification task.
2.  Determine a target class. Using your chosen generator and the
    baseline generator
    ([Wachter](https://arxiv.org/ftp/arxiv/papers/1711/1711.00399.pdf))
    generate recourse for a share *μ* of randomly selected individuals
    in the other class to revise their label (i.e. move to the target
    class). Store some of the conventional benchmark measures readily
    implemented in CARLA (cost, success rate, …)
3.  Implement recourse for those indviduals and quantify the domain
    shift.
4.  Retrain ℳ and quantify the model shift.
5.  Repeat steps 1-4 for *K* rounds.

You are free to either follow this recipe exactly or tweak the various
parameters that determine the experiemntal design as you see fit. Make
sure that you end up running the exact same experiment though, in order
for the results to be comparable.

Use the results to answer the following questions with respect to your
chosen generator:

-   Does the magnitude of induced model shifts differ compared to the
    baseline generator?
-   If so, what factors might be playing a role here?
-   Based on your findings, what appear to be good ways to mitigate
    endogenous shifts?

While the individual part should really be done individually, do keep in
mind that you will end up comparing the results of your experiments and
you should therefore all generate the same, comparable output.

## Prerequisites

For this assignment, prior experience is Python is a requirement. A
basic understanding of gradient-based optimization is helpful, but not a
strict requirement.

## Planning of the research project

1.  kick-off meeting (Q3)
2.  research proposal presentations + collective evaluation requirements
    proposal (Q4 week 2)
3.  go/no-go presentations + collective benchmark available (Q4 week 4)
4.  deadline for receiving feedback on final draft (Q4 week 8)

## References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-dhurandhar2018explanations" class="csl-entry">

Dhurandhar, Amit, Pin-Yu Chen, Ronny Luss, Chun-Chen Tu, Paishun Ting,
Karthikeyan Shanmugam, and Payel Das. 2018. “Explanations Based on the
Missing: Towards Contrastive Explanations with Pertinent Negatives.”
*Advances in Neural Information Processing Systems* 31.

</div>

<div id="ref-joshi2019towards" class="csl-entry">

Joshi, Shalmali, Oluwasanmi Koyejo, Warut Vijitbenjaronk, Been Kim, and
Joydeep Ghosh. 2019. “Towards Realistic Individual Recourse and
Actionable Explanations in Black-Box Decision Making Systems.” *arXiv
Preprint arXiv:1907.09615*.

</div>

<div id="ref-poyiadzi2020face" class="csl-entry">

Poyiadzi, Rafael, Kacper Sokol, Raul Santos-Rodriguez, Tijl De Bie, and
Peter Flach. 2020. “FACE: Feasible and Actionable Counterfactual
Explanations.” In *Proceedings of the AAAI/ACM Conference on AI, Ethics,
and Society*, 344–50.

</div>

<div id="ref-upadhyay2021towards" class="csl-entry">

Upadhyay, Sohini, Shalmali Joshi, and Himabindu Lakkaraju. 2021.
“Towards Robust and Reliable Algorithmic Recourse.” *arXiv Preprint
arXiv:2102.13620*.

</div>

<div id="ref-ustun2019actionable" class="csl-entry">

Ustun, Berk, Alexander Spangher, and Yang Liu. 2019. “Actionable
Recourse in Linear Classification.” In *Proceedings of the Conference on
Fairness, Accountability, and Transparency*, 10–19.

</div>

</div>