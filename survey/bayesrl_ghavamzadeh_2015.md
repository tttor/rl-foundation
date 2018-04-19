# Bayesian Reinforcement Learning: A Survey
* Foundations and TrendsR ? in Machine Learning
* Vol. 8, No. 5-6 (2015) 359–483
* M. Ghavamzadeh, S. Mannor, J. Pineau, and A. Tamar
* DOI: 10.1561/2200000049

## abstract
* Bayesian methods
  * for incorporating prior information into inference algorithms.
* incentives for incorporating Bayesian reasoning in RL are:
  * provides an elegant approach to action-selection (explo- ration/exploitation)
    as a function of the uncertainty in learning; and
  * provides a machinery to incorporate prior knowledge into the algorithms
  * implicitly facilitates regularization
    * The role of the prior is therefore to
      soften the effect of sampling a finite dataset, effectively leading to regularization.
  * the principled Bayesian approach for handling parameter uncertainty

## 1: intro
* rl vs supervised learning (sl):
  * sl:
    * deal with independently and iden- tically distributed (i.i.d.) samples from the domain
    * data are given, no policy for collecting data, but cf active learning
  * rl:
    * learns from the samples that are collected from the trajectories generated by
      its sequential interaction with the system.
    * different policies naturally yield different distributions of sampled trajectories,
      and thus, impacting what can be learned from the data.
* Bayesian reinforcement learning (BRL)
  * is an approach to RL that leverages methods from Bayesian inference to
    incorporate information into the learning process.
  * assumes that
    * the designer of the system can express prior information about
      the problem in a probabilistic distri- bution, and
    * new information can be incorporated using standard rules of Bayesian inference.
  * for model-based:
  * The information can be encoded and updated using a parametric representation
    * of the system dynamics, in the case of model-based RL, or
    * of the solution space, in the case of model-free RL
* challenges arise in applying Bayesian to RL paradigm.
  * there is the challenge of selecting the correct representation for
    expressing prior information in any given domain.
  * defining the decision-making process over the information state is
    typically computationally more demanding than
    directly considering the natural state representation

## 5: model-free bayesian reinforcement learning
* model-free RL methods are
  * those that do not explicitly learn a model of the system and
  * only use sample trajectories obtained by direct interaction with the system.

### 5.1 Value Function Algorithms
* to employ the Bayesian methodology to infer a posterior distribution over
  value functions, conditioned on the state-reward trajectory observed while running a MDP.
  * eg: Gaussian process temporal difference (GPTD) learning, GPSARSA.

#### 5.1.1 Gaussian Process Temporal Difference Learning
* is a GP-based framework that uses linear statistical models (see §2.5.2) to relate,
  in a probabilistic way, the underlying hidden value function with the observed rewards,
  for a MDP controlled by some fixed policy µ.
* Parametric Monte-Carlo GPTD Learning:
* Non-parametric Monte-Carlo GPTD Learning
* Sparse Non-parametric Monte-Carlo GPTD Learning:

#### 5.1.2 Connections with Other TD Methods
* the stochastic GPTD model is equivalent to GP regression on MC samples of
  the discounted return

#### 5.1.3 Policy Improvement with GPSARSA SARSA

### 5.2 Bayesian Policy Gradient

#### 5.2.1 Bayesian Quadrature
* is a Bayesian method for evaluating an integral using samples of its integrand

#### 5.2.2 Bayesian Policy Gradient Algorithms
* use Bayesian quadrature (BQ) to estimate the gradient of the expected return
  with respect to the policy parameters (Eq.

### 5.3 Bayesian Actor-Critic
* to apply the Bayesian quadrature (BQ) machinery described in §5.2.1 to
  the policy gradient expression given by Eq. 5.29 in order to
  reduce the variance in the gradient estimation procedure

## 8: outlook
* Bayesian reinforcement learning (BRL) frameworks for leveraging
  an explicit representation of prior information either
  * over the model parameters (model-based BRL) or
  * over the solution (model-free BRL).
* limitation 1:
  the need to provide a prior.
  * A prior serves as a mean to regularize the model selection problem.
  * the problem of specifying a prior is addressed by any RL algorithm that
    is supposed to work for large-scale problems
  * promising:
    * concerns devising priors based on observed data,
      as per the empirical Bayes approach
    * model mis-specification and
      how to quantify the performance degradation that
      may arise from not knowing the model precisely
* limitation 2:
  scaling BRL is a major issue
  * currently no solution (neither frequentist nor Bayesian) to
    the exploration-exploitation dilemma in large-scale MDPs.
    * scaling up BRL, in which exploration-exploitation is naturally handled,
      may help us overcome this barrier
    * BRL may be easier to scale since it allows us, in some sense, to
      embed domain knowledge into a problem.
* limitation 3:
  BRL framework we presented assumes that the model is specified correctly
  * Bayesian approach can naturally handle model selection and misspecification by
    not committing to a single model and
    rather sustaining a posterior over the possible models.
* limitation 4:
  the complexity of implementing the majority of BRL methods.
  * Thompson sampling style algorithms can pave the way to efficient algorithms
    in terms of both sample complexity and computa- tional complexity 