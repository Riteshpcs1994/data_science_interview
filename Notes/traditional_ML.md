## 1. Why MSE penalizes large errors more than MAE because the error is squared?
MSE penalizes large errors more than MAE because the error is squared, causing large deviations to grow quadratically rather than linearly.

## 2. Why Normalize or Standardize?

- It can make the learning process faster.
- It ensures that no single feature dominates the others.
Scale Features Based on Data Distribution:

- For normal distributions: StandardScaler
- For non-normal distributions: MinMaxScaler

## 3. When data is skewed, which impution we should use and why?

- For right-skewed data, median imputation is preferred because the mean is pulled by extreme values and would overestimate missing observations. The median is robust to skewness and preserves the central tendency of the distribution

- In left-skewed distributions, where mean < median < mode, the mean is affected by extreme low values. Median imputation is preferred because it is robust to skewness and better represents the central tendency.

- Mental shortcut
    - Skewed → median
    - Symmetric → mean OK
    - Mode → categorical only


