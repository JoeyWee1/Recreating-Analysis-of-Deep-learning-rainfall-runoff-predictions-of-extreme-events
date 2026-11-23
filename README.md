# Recreating-Analysis-of-Deep-learning-rainfall-runoff-predictions-of-extreme-events

---

## RJMCMC Stationarity Analysis — Prior Specification

### Recommended Prior Values

For the LP3 parameters (mean μ, standard deviation σ, skewness γ of log-transformed flows), use **weakly informative priors** derived from physical constraints and regional hydrology literature rather than same-basin data (which causes double-counting and biases toward stationarity).

| Parameter | Prior | Justification |
|-----------|-------|---------------|
| Log-flow mean (μ) | N(μ_regional, large σ) or Uniform over physically plausible range | Uninformative; let the data dominate |
| Log-flow std (σ) | Half-Normal(0, 1) or Uniform(0, upper bound) | Must be positive; weakly constrained |
| Skewness (γ) | Beta shifted to (−0.5, 0.5), mean=0.10, std=0.122 | Martins & Stedinger (2000) "geophysical prior" |

The skewness prior is the most critical: unconstrained skewness leads to absurd estimates with short records. The Beta(6,9) prior shifted to (−0.5, 0.5) is the standard in hydrology and excludes physically implausible tail behavior while remaining data-dominated for record lengths typical of CAMELS/Caravan basins.

For **trend parameters** in the nonstationary model, use uninformative (flat/uniform) priors so the RJMCMC model comparison is not pre-biased toward either model.


### Literature

| Paper | Relevance |
|-------|-----------|
| Martins & Stedinger (2000). *Generalized maximum-likelihood GEV quantile estimators*. Water Resour. Res., 36(3), 737–744. | Introduced the "geophysical prior" for shape/skewness — the standard weakly informative prior in hydrology |
| Renard (2011). *A Bayesian hierarchical approach to regional frequency analysis*. Water Resour. Res. | Uses vague priors for all parameters; discusses why vague priors are needed for valid Bayesian model comparison |
| Gelman, A. *Weakly informative priors* (slides). Columbia Statistics. | Statistical foundation: data-derived priors bias model evidence; priors should be diffuse relative to the likelihood |
| Tholoana et al. (2022). *BLP3-SP: A Bayesian LP3 model with spatial priors*. | Uses cross-basin (not same-basin) data for priors — validates the alternative approach and implicitly warns against same-basin empirical Bayes |
| Faulkner et al. (2025). *Nonstationary Flood Frequency Analysis for Urban Watersheds*. Water, 18(5), 636. | Direct analogue: flat priors on location/scale/shape in nonstationary Bayesian LP3; trend parameters also receive uninformative priors |
| USACE/RMC. *Moving Beyond Bulletin 17C with Bayesian Flow Frequency Analysis* (2023). | Advocates weakly informative Bayesian LP3 as improvement over Bulletin 17C weighted-skew approach |
