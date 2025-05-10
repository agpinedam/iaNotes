
- Using generative adversarial nets GAN
- Consist of two main components :
	-  A generator G that imputes the missing data conditioned on the observed data and outputs a completed vector
	- A discriminator D that takes the output of G and attempts to identify which parts of the data are imputed
- To ensure that G produces a unique distribution, the authors introduced a hint vector that is correlated to the missing pattern to D
	![[GAIN.png]]


### 1. **Input Components**

- **$X^M$**: The data matrix with missing values (gray squares). Zeroes or placeholders are used for missing entries.
- M The binary **mask matrix**, where:
    - $M_{ij}=1$ means the data is **observed**.
    - $M_ij = 0$ means the data is **missing**.
- R: Random noise used to fill in the missing spots initially — serves as a placeholder.

### 2. **Generator**

- Takes three inputs: $X^M, M,$ and $R$
- Its job is to **guess (impute)** the missing values in $X^M$
- Outputs:  
    $\hat{X}$ — a completed version of the data matrix where:
    - Known values are preserved
    - Missing values are replaced with **generated values** $\tilde{x}$ (shown in blue)
        
### 3. **Hint Mechanism**

- A unique idea in GAIN to help the Discriminator learn:
- A **hint matrix** $H$ is built by **partially revealing** the mask $M$
- For some positions, the Discriminator is **told whether a value was observed or imputed**
- This helps the Discriminator focus on **only parts of the matrix**, improving training

### 4. **Discriminator**

- Takes $\hat{X}$ and hint matrix $H$ as inputs
- Its job is to **predict the mask** $\hat{M}$: which values were originally missing?
    - Outputs a matrix of probabilities $p_{ij}$ (in blue), indicating how likely it thinks a value was imputed
- The **Generator** is trained to **fool the Discriminator**, so it makes very realistic imputations

### 5. **Final Output**

- A final imputed matrix can be built using the Generator’s output, selecting the imputed values only for the missing entries.

### **Summary of GAIN Flow**

| Step | Component        | Role                                         |
| ---- | ---------------- | -------------------------------------------- |
| 1    | $X^M,M,R$        | Input data, mask, and noise                  |
| 2    | Generator        | Fills in missing values to produce $\hat{X}$ |
| 3    | Hint transformer | Partially reveals $M →$ produces $H$         |
| 4    | Discriminator    | Tries to guess which values were imputed     |
| 5    | Output           | Final predictions and learned imputations    |

---

### Why does this work?

Because the Generator and Discriminator play a **game**:

- The Generator tries to make imputed values **look real**
- The Discriminator tries to detect **which are fake**  
    Over time, the Generator learns to produce very realistic guesses — making this a powerful method for missing data imputation.
