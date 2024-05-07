---
title: AI Deception
layout: page
date: 2022-09-26 03:00:00 +0200
---
((Some remarks on the paper
_Honesty Is the Best Policy:
Defining and Mitigating AI Deception_,
[https://arxiv.org/abs/2312.01350](https://arxiv.org/abs/2312.01350),
by
Francis Rhys Ward,
Francesco Belardinelli,
Francesca Toni,
Tom Everitt))

Definition of deception for structural causal games
- grounded in philosophy literature
- real-world machine learning systems

Their paper aims to

- show with examples that their definitions aligns with philosophical and commonsense meaning of "deception".

- provide graphical criteria for deception.

- show experimentally that these criteria can be used to mitigate deception in reinforcement learning agents and language models.

# Main Definition of Deception
_An agent $S$ **deceives** another agent $T$ if $S$ <u>intentionally causes</u> $T$ to <u>believe</u> $\phi$, where $\phi$ is <u>false</u> and $S$ does not <u>believe</u> that $\phi$ is true._

Sylvy notes:
- this definition relies on the falsity of $\phi$.

There are notions of _intent_ and _belief_ involved in this definition.
_Intent_ depends on _instrumental goals_.

They remark "Agents that _intentionally_ deceive in order to achieve their goals seem less safe a priori than those which do so merely as a side-effect."

Setting: _Structural causal games_ (SCGs).

# Remarks
- __Belief.__
They acknowledge that their definition of belief is _functional_, thus divergent from the "standard philosophical account ... [that] ... belief is a _propositional attitude_".
- __Intention.__
There is no "universally accepted philosophical theory of intention".
- __My remarks about their definition of Deception.__
	- They reject accidental truths as lies [I disagree]
	- They reject lying in isolation [I agree]

	They comment that AI agents may deceive and may be deceived.

	They refer to "Lewis et al.'s negotiation agent" which learnt to deceive from self-play. They give further examples. AI agents (specifically LMs) have the capability to deceive humans to achieve goals.

# Structural Causal Game
An SCG is a pair $\mathcal{M}=(\mathcal{G},\theta)$
where $\mathcal{G}=(N,\mathbf{E}\cup\mathbf{V},\mathcal{E})$
with
- $N$ a set of _agents_,
- $(\mathbf{E}\cup\mathbf{V},\mathcal{E})$ a [carefully partitioned!] _directed acyclic graph_ with

	- a set $\mathbf{V}$ of _endogenous variables_ and
	- a set $$\mathbf{E}=\{E_{V}\}_{V\in\mathbf{V}}$$ of _exogenous parent variables_.

	The set $\mathbf{V}$ is partitioned into
	- chance $\mathbf{X}$,
	- decision $\mathbf{D}$, and
	- utility $\mathbf{U}$
	variables.

	The sets $\mathbf{D}$ and $\mathbf{U}$ are further partitioned by their association with particular agents.
	More formally,
	- $\mathbf{D}$ is a disjoint union $\bigsqcup_{i\in N}\mathbf{D}^{i}$ and
	- $\mathbf{U}$ is a disjoint union $\bigsqcup_{i\in N}\mathbf{U}^{i}$.

- $\theta$ is a set
$$\{\theta_{Y}\}_{Y\in\mathbf{E}\cup\mathbf{V}\setminus\mathbf{D}}$$
of _parameters_ $\theta_{Y}$,
indexed by $\mathbf{E}\cup\mathbf{V}\setminus\mathbf{D}$,
with $\theta_{Y}$ the parameter that governs a conditional probability distribution
$$\mathrm{Pr}(Y\mid \mathbf{Pa}_{Y},\theta_{Y})$$
for each non-decision variable $Y$.
Furthermore we require that the CPD for each endogenous variable is deterministic
and that the domains of the utility variables are real-valued.

#### Policies
A _policy_ for an agent $i$ is a CPD
$$\pi^{i}(D^{i}\mid \mathrm{Pa}_{D^{i}})$$.
A _policy profile_ is a tuple
$$\pi=(\pi^{i})_{i\in N}$$.
The corresponding _partial policy profile_ is
$$\pi^{-i}=(\pi^{j})_{j\neq i}$$.

__Note.__
An SCG together with a policy profile determines a joint probability distribution $P^{\pi}$ over all the variables.

#### Setting
A _setting_ is a tuple
$\mathbf{e}$
of the same length as $\mathbf{E}$.

#### Utilities
Given a policy profile $\pi$,
and an agent $i$,
the _expected utility_ is

$$\mathbb{E}_{\pi}^{i}:=\sum_{U\in\mathbf{U}^{i}}\mathbb{E}_{\pi}[U].$$

#### Best response
We say $\pi^{i}$ is _best response_ to $\pi^{-i}$ if
[it is a Nash equilibrium!]
for all policies $\hat{\pi}^{i}$ for $i$

$$\mathbb{E}_{\pi^{i},\pi^{-i}}^{i}=\sum_{U\in\mathbf{U}^{i}}\mathbb{E}_{\pi^{i},\pi^{-i}}[U]
\geq
\sum_{U\in\mathbf{U}^{i}}\mathbb{E}_{\hat{\pi}^{i},\pi^{-i}}[U]
=\mathbb{E}_{\hat{\pi}^{i},\pi^{-i}}^{i}.$$

# Belief.
This is the __heart of the matter__.

Let $\pi$ be a policy profile, $\mathbf{e}$ be a setting, $i$ and agent, and $\phi$ a proposition to which $i$ responds.
We say that $i$ _believes_ $\phi$ if
$i$ acts as though $\phi$ is true,
i.e. $$D^{i}(\pi,\mathbf{e})=D^{i}_{\phi=\top}(\pi_{i(\phi)},\mathbf{e})$$.

Proposition 3.2 is about the "coherence" (roughly, consistency) of believe. It is unproved!

__Remark.__
I'm mildly aware that there would be incompleteness phenomena underlying these systems: if an agent believes too much, too correctly, and the game is sufficiently complex/self-reflexive, then its beliefs are perhaps incomplete.

# Intention.
Let $\pi=(\pi^{i},\pi^{-i})$ be a policy profile,
$REF(\pi^{i})$ be a set of `alternative policies', for each $i$, and let $\mathbf{X}\subseteq\mathbf{V}$.
We say $i$ _intentionally causes_ $\mathbf{X}(\pi,e)$ with policy $\pi^{i}$



