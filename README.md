# Urban Studies: Social Network Coevolution Workflow

This repository maintains an R/RSiena workflow for studying the coevolution of Chinese inter-city official investment-attraction networks and capital-flow networks.

The project converts yearly city-pair matrices into RSiena-compatible network objects, adds dyadic and actor covariates, estimates stochastic actor-oriented models, checks convergence, runs robustness tests, and exports thesis-ready tables and visualization inputs.

## Maintainer

Maintained by `zouyucheng123`.

I use this repository to organize and improve a computational social-science workflow for urban studies, regional economic coordination, and inter-city network evolution.

## What This Project Maintains

This project focuses on the full workflow from raw matrix data to interpretable model results:

- data cleaning for yearly directed city-pair matrices
- official investment-attraction network construction
- capital-flow network construction by capital type
- actor covariates such as population, FDI, fiscal revenue, patents, and GDP
- dyadic covariates such as geographic adjacency and province relation
- RSiena SAOM model specification
- convergence diagnostics using `ans$tconv.max`
- robustness checks using alternative time-window aggregation
- result tables and visualization-ready summaries

## Research Workflow

The current workflow is organized around the following steps:

1. Read yearly 41 x 41 directed matrices for city networks.
2. Convert official investment-attraction ties into RSiena endogenous networks.
3. Convert capital-flow matrices into binary dyadic covariates.
4. Construct reversed capital-flow variables when the hypothesis requires direction alignment.
5. Compute capital in-degree and out-degree as city-level covariates.
6. Add city-level controls and dyadic controls.
7. Estimate stochastic actor-oriented models with RSiena.
8. Check model convergence before interpreting results.
9. Export coefficient tables with estimates, standard errors, t-ratios, and significance markers.
10. Compare baseline models with robustness-window models.

## Why This Matters

Social network coevolution models are difficult to reproduce because results depend on matrix direction, node order, yearly alignment, covariate construction, and convergence diagnostics.

This repository makes those steps explicit. It helps researchers audit how official visits, capital flows, geographic structure, and city attributes enter the model. The goal is to make an empirical urban-studies workflow easier to inspect, reuse, and improve.

## Repository Structure

```text
skills/
  social-network-coevolution-rsiena/
    SKILL.md
    agents/
      openai.yaml
    references/
      project-profile.md
      rsiena-workflow.md
