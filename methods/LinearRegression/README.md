## Linear Regression on prostate cancer data

Linear regression is a very simple model, but for prediction purposes, they can sometimes excel other non-linear models, especially when there is only small training data, low signal-to-noise ratio, or sparse data.  

**Prostate cancer data**  
The data are from The Elements of Statistical Learning (ESL, [link](https://web.stanford.edu/~hastie/ElemStatLearn/datasets/prostate.data)) and originally
from the study of Stamey et al. (1989).  
You can find the data in [data/prostate.csv](../../data/prostate.csv) in this repository.

**Response variable:**
- Level of prostate-specific antigen (lpsa)

**Predictors:**
- lcavol (log cancer volume)
- lweight (log prostate weight)
- age
- lbph (log of the amount of benign prostate hyperplasia)
- svi (seminal vesicle invasion)
- lcp (log of capsular penetration)
- gleason (Gleason score)
- pgg45 (percent of Gleason scores 4 or 5)  
  
I fitted three linear models with the data.  
- First one is a "naive" linear regression, which normalizes all the predictors and fit the model. This is exactly what the authors did in ESL.
- Second one is a linear regression with additional categorical variables. Predictors 'age', 'svi', and 'gleason' are discrete values, so if we introduce categorical variables for those predictors, the model may show better performance.
- Third one is the same model as the second one with different train/test data.  
  
**Additional Categorical Variables**  
| variable name | values | count |
| -- | -- | -- |
| age_lo | 55 or younger | 10 |
| age_mid | 55 ~ 65 (including) | 44 |
| age_hi | older than 65 | 43 |
| |
| gleason_6 | 6 | 35 |
| gleason_7 | 7 | 56 |  

Variables for 'gleason' value 8 and 9 are not introduced, since they will be reflected in the intercept.
For 'svi', I didn't introduce new variable, but left it un-normalized to consider it categorical directly.

### Result
Below is the mean squared error (MSE) results for each model.  
Note that  
1) a base model is just the average of the traing set, and  
2) the train/test data split is exactly the same as in ESL for the upper result, and different split for the lower result.

| Model | MSE | MSE reduced |
| ----- | --- | ----------- |
| Base Model | 1.0567 | - |
| Naive Linear Model | 0.5213 | 50.67% |
| Categorical Linear Model | 0.4692 | 55.60% |
| |
| Base Model with different split | 1.7033 | - |
| Naive Linear Model with different split | 0.4834 | 71.62% |
| Categorical Linear Model with different split | 0.4331 | 74.58% |
