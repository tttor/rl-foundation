# Deterministic Policy Gradient Algorithms
* David Silver et al
* Proceedings of the 31st International Conference on Machine Learning, Beijing, China, 2014

## problem
* computing the stochastic policy gradient may **require more samples**, 
  especially if the action space has **many** dimensions.

## idea: deterministic policy gradients (theorem 1)
* vs stochastic case
  * In the stochastic case: the policy gradient integrates over both state and action spaces, 
  * in the deterministic case:  the policy gradient **only** integrates over the state space.
* to choose actions according to a stochastic behaviour policy (to ensure adequate exploration), but 
  to **learn about a deterministic target policy** (exploiting the efficiency of the deterministic policy gradient)
  * use the deterministic policy gradient to derive an off-policy actor-critic algorithm that 
    estimates the action-value function using a differentiable function approximator, and 
  * then updates the policy parameters in the direction of the approximate action-value gradient. 
* present the theory that shows that, like the stochastic policy gradient theorem, 
  there is no need to compute the gradient of the state distribution;

## setup
* task
  * bandit with 50 continuous action dimensions
  * a high-dimensional task for controlling an octopus arm

## result
* show that the deterministic policy gradient does indeed exist, and 
  it has a simple model-free form that simply follows the gradient of the action-value function
* the deterministic policy gradient can be **estimated much more efficiently** than the usual stochastic policy gradient.
* our algorithms require no more computation than prior methods: 
  the computational cost of each update is linear in the action dimensionality and the number of policy parameters
* the deterministic policy gradient theorem is in fact a limiting case of the stochastic policy gradient theorem;
  theorem 2

## misc
* Policy gradient algorithms typically proceed by sampling this stochastic policy and 
  adjusting the policy parameters in the direction of greater cumulative reward.
* Stochastic Policy Gradient Theorem:
  * reduces the computation of the performance gradient to a simple expectation;
    eg: by forming a sample-based estimate of this expectation.
  * One issue: how to estimate the action-value function `Q_{\pi}(s, a)`. 
    * simplest approach is to use a sample return, 
      which leads to a variant of the REINFORCE algorithm
* It is often useful **to estimate** the policy gradient **off-policy** from trajectories sampled from 
  a **distinct behaviour policy**, `\beta(a|s) \neq \pi_{\theta}(a|s)`. 
  * In an off-policy setting, the performance objective is typically modified to be 
    the **value function of the target policy**, averaged over the **state distribution of the behaviour policy**
  * leads to 
    * off-policy policy gradients, 
    * Off-Policy Actor-Critic (OffPAC) algorithm: 
      * uses a behaviour policy `\beta(a|s)` to generate trajectories
      * A critic estimates a state-value function, V v(s) ≈ V π(s), **off-policy** from these trajectories, 
        by gradient temporal-difference learning (Sutton et al., 2009). 
      * An actor updates the policy parameters `\theta`, also **off-policy** from these trajectories, 
        by stochastic gradient ascent of Equation 5.
      * Both the actor and the critic use an **importance sampling ratio** to 
        adjust for the fact that actions were selected according to `\pi` rather than `\beta`
* In continuous action spaces, greedy policy improvement becomes problematic, requiring a global maximisation at every step
  * Instead, alternative is to move the policy in the direction of the gradient of Q, rather than globally maximising Q
* the notion of **compatible function approximation** for deterministic policy gradients, 
  to ensure that the approximation does not bias the policy gradient.