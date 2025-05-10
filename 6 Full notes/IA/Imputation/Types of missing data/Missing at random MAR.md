- Probability of a data point being missing is related to **observed data**, but **not related to the value of the missing data itself**, once the observed data is taken into account.

###  Example:

Let’s say you’re collecting data on income and age, and people with higher income are less likely to report their income — but you still have their age. If the probability of missing income depends on age (which you observed), but not on the actual missing income value, then the data is MAR.
###  Key idea:

If data is **MAR**, it’s possible to handle the missingness properly using statistical methods like **multiple imputation** or **maximum likelihood**, because we can "explain" the missingness using the available data.