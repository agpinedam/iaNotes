- Method for obtaining maximum likelihood estimates when data are missing 
- It's an iterative procedure in which it uses other variables to impute a value **(Expectation)**
- Then checks whether that is the value most likely **(Maximization)**
- Is generally better than mean/median imputation since it preserves the relationship with other variables
- Steps :
	-  Expectation step (E-step) : uses the current estimate of parameter to impute (expectation of) missing data
	- Te maximization step (M-step) : uses the updated data from the E-Step to find a maximum likelihood estimate of the parameter
	- The  iterative process continues until there is convergence in the parameter estimates

**Code example:**
```python
import numpy as np
import pandas as pd
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

# Create a sample dataset with missing values
data = pd.DataFrame({
    'Age': [25, 27, np.nan, 35, 40, np.nan, 50],
    'Salary': [50000, 52000, 51000, np.nan, 58000, 60000, 62000]
})

print("Original data with missing values:")
print(data)

# Instantiate the IterativeImputer (default estimator is BayesianRidge)
imputer = IterativeImputer(max_iter=10, random_state=0)
data_imputed = imputer.fit_transform(data)

# Convert back to DataFrame for better display
data_imputed_df = pd.DataFrame(data_imputed, columns=data.columns)

print("\nData after EM-like imputation:")
print(data_imputed_df.round(2))
```

