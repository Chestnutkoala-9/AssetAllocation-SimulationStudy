# Asset Allocation Simulation Study

In this simulation study, I generated datasets for four different configurations to test the performance of eleven different asset allocation strategies, by calculating the out-of-sample average return and out-of-sample Sharpe ratio.

### Summary of Method:
- Equal weight: 1/d is invested in each risky asset
- Market Portfolio: only the factor asset is included in the portfolio
- Sample-based mean-variance: mean and covariance matrix of return of the d assets are calculated to get the allocation
- 1-Factor Model:
  1. First run an OLS with estimated factors with each individual asset: where x is the estimated factor, and y is the return of k-th risky asset.
  2. Given the coefficients, B will be formed by the coefficients. Given the residuals, we obstained a diagonal matrix D
  3. Calculate the variance of factor asset
  4. Plug in the formula for asset allocation
- Bayes-Stein: Shrink to minimum variance portfolio
- Ledoit-Wolf: Linear Shrinkage of the covariance matrix to an identical matrix
- Minimum-Variance
- Sample-based mean-variance with no shortsale constraints: Using the sample mean and variance, I utilized Scipy optimization tool to
calculate the optimal allocation under the optimization problem:
- Bayes-stein with no shortsale constraints: Replace the sample mean with the Bayes-stein estimator of mean for the optimization problem
- Ledoit-wolf with no shortsale constraints: Replace the sample covariance with the Ledoit-wolf shrinkage covariance matrix for the optimization problem
- Minimum Variance with sample-based mean-variance and no short sale constraints

### Data Configurations

| Configuration |       d       |       M       |    Normal    |      iid     |     Alpha    |      Effect     |
| ------------- | ------------- | ------------- |------------- |------------- |------------- |---------------- |
| 1             |      10       |      120      |     Yes      |     Yes      |      0       |     Baseline    | 
| 2             |      50       |      120      |     Yes      |     Yes      |      0       |  Number of Assets   | 
| 3             |      10       |      120      |     Yes      |     Yes      |    Uniform   |  Mispricing alpha   |
| 4             |      10       |      120      |     Yes      |    AR(1)     |      0       |  Intertemporal correlation   |


### Conclusion:
Real market incorporates all conditions in configurations 2,3, and 4, where the current return has correlations with past returns, individual assets will be influenced by the overall market condition, and we typically have a really large asset class. In this case, judging by the Sharpe
ratio, which takes into account both the returns and the risk taken to achieve those returns, Bayes-Stein and Ledoit Wolf methods perform well in practice and has advantages over the traditional mean-variance methods.

In addition, the no short-selling constraint may be useful in practice, especially for risk-averse investors and scenarios where short-selling is restricted. In general, mean-variance-based portfolios tend to have a better risk-adjusted performance compared to equal-weight or market portfolios. This is because mean-variance optimization considers the covariance between assets and aims to achieve the highest possible return for a given level of risk.

Overall, it is difficult to say which method will perform best in all situations, as performance depends on the specific market conditions and the preferences of the investor. We could use a combination of different methods and perform sensitivity analysis to assess the robustness of the
results to changes in the inputs and assumptions.


