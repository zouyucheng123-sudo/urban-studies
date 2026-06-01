# Project Profile and Application Narrative

Use this reference when drafting GitHub, OpenAI, or developer-benefit applications for the project.

## Four required points

### Who you are

The maintainer is `zouyucheng123`, a researcher maintaining a reproducible computational social-science workflow for city-level social network coevolution. The work combines R, RSiena, matrix data cleaning, city covariates, robustness checks, and thesis-ready result reporting.

Suggested phrasing:

> I maintain an R/RSiena workflow for studying the coevolution of Chinese inter-city official investment-attraction networks and capital-flow networks. My work is not a one-off script: it is a thesis and research pipeline that turns yearly city-pair matrices, dyadic controls, and actor covariates into auditable SAOM estimates, convergence diagnostics, robustness tests, and visualization-ready outputs.

### What you maintain

The maintained workflow includes:

- yearly directed 41 x 41 city matrices for official investment-attraction ties from 2010 to 2022
- yearly directed 41 x 41 capital-flow matrices by capital type: total, private, foreign, and state-owned
- city-level time-varying covariates: population, FDI, fiscal revenue, patent grants, and GDP
- dyadic controls: geographic adjacency and province relation
- RSiena model scripts for coevolution mechanisms, capital centrality effects, and actor controls
- robustness scripts using 2-year, 3-year, and 4-year merged windows
- output steps for convergence checks, density summaries, significance-star tables, and thesis-ready interpretation text

Suggested phrasing:

> I maintain scripts that convert raw city-pair matrices into RSiena-compatible network arrays, construct dyadic and actor covariates, estimate stochastic actor-oriented models, and export model tables used in academic writing. The repository covers the full path from data validation to result interpretation, including robustness checks over alternative time windows.

### Why the project matters

The project matters because it makes a difficult social-science workflow more reproducible. RSiena coevolution models are sensitive to node order, matrix dimensions, network direction, missing years, and convergence diagnostics. Without a maintained workflow, a researcher can easily produce results that are hard to audit or impossible to reproduce.

Suggested phrasing:

> This project matters because inter-city economic coordination is often discussed qualitatively, while the underlying network evolution is hard to audit. The workflow makes the empirical chain explicit: how official visits, capital flows, geographic structure, city attributes, and robustness windows enter the model. That helps other researchers inspect assumptions, reproduce estimates, and adapt the pipeline to related regional network studies.

### How the benefit will be used

The requested benefit should be tied to concrete maintenance work, not generic productivity.

Suggested phrasing:

> I plan to use the benefit to maintain the project in four practical ways. First, I will refactor repeated R loading blocks into tested functions while preserving model equivalence. Second, I will add validation scripts that check matrix dimensions, binary encoding, node-order consistency, year coverage, and RSiena convergence thresholds before results are exported. Third, I will generate clearer documentation for each model variant, including capital direction, hypotheses, and robustness-window differences. Fourth, I will improve visualization and reporting so density trends, model estimates, and convergence diagnostics can be reviewed before thesis writing or public release.

## Concrete maintenance workflow for benefit usage

Use this table when the application asks for a specific plan.

| Maintenance area | Concrete use | Output |
| --- | --- | --- |
| Data cleaning | Check every yearly matrix for 41 x 41 shape, no diagonal artifacts, binary values, same city order | validation report |
| Code refactor | Replace repeated annual file reads with parameterized loaders for capital type and year range | cleaner R modules |
| Model audit | Verify `sienaDataCreate()` inputs, effect names, network direction, and `ans$tconv.max < 0.25` | model audit checklist |
| Robustness | Compare 2-year, 3-year, and 4-year merged-window scripts against the baseline | robustness summary |
| Visualization | Produce density trends, edge-count trends, and model coefficient tables | figures and thesis tables |
| Documentation | Explain who maintains the workflow, what each script estimates, and how to reproduce safe outputs | README or docs updates |

## Short application answer

I am `zouyucheng123`, the maintainer of an R/RSiena social-network coevolution workflow for studying Chinese inter-city official investment-attraction ties and capital-flow networks. I maintain code that cleans yearly 41-city matrices, builds RSiena network and covariate objects, estimates SAOM models, checks convergence, runs robustness windows, and exports thesis-ready tables and visual summaries.

The project is important because coevolution modeling is fragile: a small mistake in node order, matrix direction, year alignment, or convergence handling can change the substantive interpretation. By maintaining the workflow publicly, I can make the empirical pipeline more transparent for regional economics, urban governance, and computational social-science researchers who need reproducible network-evolution evidence.

I will use the benefit for concrete maintenance: refactoring duplicated R scripts, adding matrix and convergence validators, documenting each model variant, producing visual diagnostics, and preparing reproducible examples that do not expose private raw data. The goal is to turn the current thesis code into a maintainable research workflow that other scholars can inspect, reuse, and adapt.
