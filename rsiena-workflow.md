# RSiena Workflow Reference

Use this reference when editing or reviewing the user's R scripts.

## Current script pattern

The main script `0-1-R-1-缩减招商引资-总资本.R` follows this pipeline:

1. Load `RSiena`.
2. Read official investment-attraction yearly binary matrices for 2010-2022.
3. Stack them as `offic <- array(..., dim = c(41, 41, 13))`.
4. Convert to endogenous network: `official <- sienaNet(offic)`.
5. Read capital-flow yearly binary matrices, usually 2010-2021.
6. Build `capital_bin <- (capital_arr > 0) * 1L`.
7. Reverse capital direction into `capital_rev_bin` and create `capital_rev <- varDyadCovar(capital_rev_bin)`.
8. Compute capital in-degree and out-degree using `colSums` and `rowSums`, then wrap with `varCovar()`.
9. Read time-invariant dyadic controls through `coDyadCovar()`.
10. Read actor time-varying controls through `varCovar()`.
11. Create RSiena data with `sienaDataCreate()`.
12. Add effects with `includeEffects()`.
13. Run `siena07()`, continue with `prevAns` if needed, and check `ans$tconv.max`.
14. Export estimate, standard error, t-ratio, and significance table.

The sibling scripts repeat the same structure for private, foreign, and state-owned capital. Robustness scripts repeat the same logic for merged time windows.

## Pre-edit audit checklist

Before changing model code, verify:

- Which script is target: total, private, foreign, state-owned, or robustness.
- Whether official network is endogenous and capital flow is dyadic covariate, or the reverse.
- Whether the capital matrix direction is raw `i -> j` or reversed to match the hypothesis.
- Whether official years and capital years have the same number of waves; RSiena covariates generally need wave alignment with the modeled network.
- Whether comments and output filenames match the capital type and year range.
- Whether all `simplify2array(list(...))` calls have no trailing comma.

## Data validation checklist

For each matrix family:

- dimensions are `41 x 41`
- all annual matrices use identical city order
- values are numeric
- binary matrices contain only 0 and 1 after conversion
- diagonal policy is explicit: retained, zeroed, or ignored in density calculation
- number of waves matches `years_*`
- no missing file silently truncates the time range

Suggested R helper shape:

```r
stopifnot(all(dim(M) == c(41, 41)))
stopifnot(all(M %in% c(0, 1)))
```

## Model specification map

Use this map when explaining effects.

| Code | Meaning in this project |
| --- | --- |
| `density` | baseline tendency to form official ties |
| `inPop` | popularity effect: already-attractive cities attract more ties |
| `reciprocity` | reciprocal official visit or cooperation tendency |
| `X` with `adjacency` | geographically adjacent cities are more likely to tie |
| `X` with `province` | province-related dyadic control |
| `X` with `capital_rev` | prior or concurrent capital direction predicts official investment-attraction ties |
| `altX` with `capitalIn` | capital-receiving cities are more likely to become official visit targets |
| `altX` with `capitalOut` | capital-sending capacity as alter attractiveness, if specified that way |
| `altX` actor controls | cities with higher covariate values attract more ties |
| `egoXaltX` actor controls | similarity or interaction pattern between sender and receiver covariates |

Always describe the direction in prose. Do not say "capital matters" without saying whether it is capital inflow, outflow, or reversed dyadic flow.

## Output quality checklist

Before treating a model as usable:

- `ans$tconv.max` is below 0.25 or the report explicitly says it is not converged.
- Standard errors are non-missing and positive.
- `Estimate / SE` is used consistently for t-ratio.
- Significance stars are based on absolute t-ratio: 2.58, 1.96, 1.64.
- Export filenames contain capital type and date or model label.
- The table preserves original RSiena effect names plus a human-readable label when possible.

## Refactoring guidance

Prefer local, conservative refactors:

- extract `read_matrix_series(base_dir, prefix, years)` only after confirming all file naming conventions
- extract `network_density(A3)` because it is already reusable
- extract `format_siena_table(ans)` for all model variants
- keep effect specification close to hypotheses so thesis interpretation remains easy to audit
- avoid changing model effects and data-loading refactors in the same edit unless requested

## Public-release checklist

Before uploading to GitHub:

- replace absolute local paths with a config file, environment variables, or documented placeholders
- remove raw confidential data
- include sample matrix schemas or synthetic example data
- add a clear note that full empirical data may be restricted
- document required R packages, especially `RSiena`
- document how to run baseline, capital-type variants, and robustness variants separately
