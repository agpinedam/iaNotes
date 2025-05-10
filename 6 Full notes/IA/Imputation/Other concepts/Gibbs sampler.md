
> Permite explorar una distribución complicada sin conocerla completamente, pero sí conociendo **sus partes condicionales**.

The **Gibbs Sampler** is a [[Markov Chain Monte Carlo]] (MCMC)** algorithm used to **generate samples from a multivariate probability distribMarkov Chain Monte Carloution** when direct sampling is difficult.
P
Rather than sampling all variables at once from the full joint distribution, Gibbs sampling:

- Breaks the problem into **conditional distributions**, each involving only **one variable at a time**.
    
- **Iteratively samples** each variable from its **conditional distribution**, given the current values of all other variables.
    

Over time, this process produces samples that approximate the **true joint distribution**.
###  **How it works (simple explanation):**

Suppose you have a joint distribution over variables $X=(X_1,X_2,...,Xd)$.

1. **Initialize** all variables:  
    ${X_1}^{(0)},{X_2}^{(0)},...,{X_d}^{(0)}$
    
2. For each iteration t=1,2,...t = 1, 2, ..., update each variable in sequence:
    
    $\begin{align*} X_1^{(t)} &\sim p(X_1 \mid X_2^{(t-1)}, X_3^{(t-1)}, ..., X_d^{(t-1)}) \\ X_2^{(t)} &\sim p(X_2 \mid X_1^{(t)}, X_3^{(t-1)}, ..., X_d^{(t-1)}) \\ &\vdots \\ X_d^{(t)} &\sim p(X_d \mid X_1^{(t)}, X_2^{(t)}, ..., X_{d-1}^{(t)}) \end{align*}$
    
    
3. Repeat the process until the samples converge to the **stationary distribution**, which is the **target joint distribution** $p(X_1,...,X_d)$.
    

### **Why use Gibbs Sampling?**

- It’s useful when you can’t sample directly from a complex joint distribution, but **you can sample from the conditionals**.
    
- Especially helpful in **Bayesian statistics**, where posterior distributions are often complex.
## Example

Let’s say you have two related random variables: **height (X)** and **weight (Y)**.

- You know how to randomly choose a height **if you know the weight**.
    
- And you know how to randomly choose a weight **if you know the height**.
    
- But it’s hard to choose both together directly.
    

So you:

1. Start with any weight.
    
2. Use that to pick a height.
    
3. Use the new height to pick a new weight.
    
4. Repeat this process.
    

After enough repetitions, the **height–weight pairs** you’ve created act like real examples from your population.

##  Example in Code 

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters of the true joint distribution
mu_x = 0       # Mean of X
mu_y = 0       # Mean of Y
rho = 0.8      # Correlation between X and Y
sigma_x = 1    # Standard deviation of X
sigma_y = 1    # Standard deviation of Y

# Conditional distribution: X | Y
def sample_x_given_y(y):
    mean = mu_x + rho * (sigma_x / sigma_y) * (y - mu_y)
    std = np.sqrt(1 - rho ** 2) * sigma_x
    return np.random.normal(mean, std)

# Conditional distribution: Y | X
def sample_y_given_x(x):
    mean = mu_y + rho * (sigma_y / sigma_x) * (x - mu_x)
    std = np.sqrt(1 - rho ** 2) * sigma_y
    return np.random.normal(mean, std)

# Gibbs sampler settings
n_samples = 5000
samples = np.zeros((n_samples, 2))  # To store (X, Y) samples

# Initial values
x = 0
y = 0

# Run the Gibbs sampler
for i in range(n_samples):
    x = sample_x_given_y(y)   # Sample new X based on current Y
    y = sample_y_given_x(x)   # Sample new Y based on new X
    samples[i] = [x, y]       # Save the sample

# Plot the result
plt.figure(figsize=(6, 6))
plt.scatter(samples[:, 0], samples[:, 1], alpha=0.3, s=5)
plt.title("Gibbs Sampling from a Bivariate Normal Distribution")
plt.xlabel("X")
plt.ylabel("Y")
plt.axis("equal")
plt.grid(True)
plt.show()

```

![[GibbsSample.png]]