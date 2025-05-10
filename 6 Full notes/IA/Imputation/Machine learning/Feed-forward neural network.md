
 - Estimate missing values by training a network to learn the complete variable (as an output) using the remaining complete variables a inputs
 - One constructs a feed-forward neural network using the subset that does not  contain any missing values $X^{\varnothing}$ 
 - Depending on the type of variable #categorical or #continuous , different type of error function is used during the training process
 - After each neural network is trained, unknown values are predicted using the corresponding model
 - Imputes values are obteined by averaging the missing data estimates by each model.

