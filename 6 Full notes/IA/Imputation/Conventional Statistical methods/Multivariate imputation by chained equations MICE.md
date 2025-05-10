
- It involves filling in the missing values multiple times by creating multiple imputed datasets
- It operates under the assumption that the missing data are [[Missing at random MAR]]
- We assume that the multivariate distribution $p(X \mid \theta)$ of X is completely specified by $\theta$ a vector of unknown parameters
- Is a [[Gibbs sampler]] that estimates the posterior distribution of $\theta$ by sampling iteratively from conditional distributions $p(X \mid X_{-1}, \theta_1),\ \dots,\ p(X \mid X_{-k}, \theta_k),\ \dots,\ p(X \mid X_{-d}, \theta_d)$ where $X_{-k} = (X_1, \dots, X_{k-1}, X_{k+1}, \dots, X_d)$  denotes the collection of $d - 1$ variables in X except $X_{k}$ and the parameters $\theta_{1}, ..., \theta_{d}$ are specific to the corresponding conditionals densities.
- Starting from a simple draw from observed marginal distributions, the Gibbs sampler successively draws from observed marginal distributions, the Gibbs sampler successively draws

$$
\hat{\theta}_1^{(t)} \sim p(\theta_1 \mid X_1^{\text{obs}}, X_2^{(t-1)}, \ldots, X_d^{(t-1)})
$$

$$
\hat{X}_1^{(t)} \sim p(X_1 \mid X_1^{\text{obs}}, X_2^{(t-1)}, \ldots, X_d^{(t-1)}, \hat{\theta}_1^{(t)})
$$

$$
\vdots
$$

$$
\hat{\theta}_d^{(t)} \sim p(\theta_d \mid X_d^{\text{obs}}, X_1^{(t)}, \ldots, X_{d-1}^{(t)})
$$

$$
\hat{X}_d^{(t)} \sim p(X_d \mid X_d^{\text{obs}}, X_1^{(t)}, \ldots, X_{d-1}^{(t)}, \hat{\theta}_d^{(t)})
$$

where $X_k^{\text{obs}}$ and $\hat{X}_k^{(t)}$ stand for the observed and imputed data for the $k$th variable at iteration $t$, and  $X_k^{(t)} = (X_k^{\text{obs}}, \hat{X}_k^{(t)})$  
- The convergence of this algorithm is typical fast