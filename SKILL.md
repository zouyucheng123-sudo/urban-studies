---
name: social-network-coevolution-rsiena
description: Use this skill to maintain, audit, document, and extend an RSiena social network coevolution workflow for Chinese city networks, including official investment-attraction visits, capital-flow matrices, data cleaning, robustness checks, visualization, and grant or benefit application narratives.
metadata:
  short-description: Maintain RSiena city network coevolution workflows
---

# Social Network Coevolution RSiena

Use this skill when working on the user's social-network coevolution project: official investment-attraction networks, capital-flow networks, city-level covariates, RSiena SAOM models, robustness scripts, visualization, and application materials explaining the project's open-source maintenance value.

## Core project frame

The project studies how inter-city official investment-attraction ties and capital-flow ties coevolve. Existing scripts use RSiena with 41-city directed yearly matrices, construct actor and dyadic covariates, run SAOM models, check convergence, and export paper-ready coefficient tables.

For the project identity and benefit-application narrative, read `references/project-profile.md`.

For the executable maintenance workflow and code checklist, read `references/rsiena-workflow.md`.

## Default workflow

1. Inventory the target scripts and data paths.
   - Identify the network pair and direction: official visits -> capital flow, capital flow -> official visits, city alliance -> capital flow, etc.
   - Identify the capital type: total, private, foreign, state-owned, or robustness windows.
   - Record years, node count, matrix dimensions, and expected input folders before editing.

2. Clean and standardize data loading.
   - Replace repeated `p0`, `p1`, `c0`, `c1` blocks with loop-based loaders when the user permits refactoring.
   - Keep direction explicit: raw capital `i -> j`, reversed capital `j -> i`, in-degree as attractiveness, out-degree as sending capacity.
   - Validate that all matrices are square, same node order, same dimensions, and binary when passed to `sienaNet` or `varDyadCovar`.

3. Build RSiena objects deliberately.
   - Use `sienaNet()` for endogenous networks.
   - Use `coDyadCovar()` for time-invariant dyadic covariates such as adjacency and province relation.
   - Use `varCovar()` for time-varying actor covariates such as population, FDI, fiscal revenue, patents, and GDP.
   - Use `varDyadCovar()` for time-varying dyadic covariates such as reversed capital flow.

4. Specify effects with hypotheses attached.
   - Baseline network effects: `density`, `inPop`, `reciprocity`.
   - Dyadic controls: adjacency and province `X`.
   - Coevolution mechanism: `X` with reversed capital flow.
   - Capital centrality mechanisms: `altX` for capital in-degree and out-degree.
   - Actor controls: `altX` and `egoXaltX` for city covariates.

5. Run and verify.
   - Set a reproducible seed in `sienaAlgorithmCreate()`.
   - Check `ans$tconv.max`; target below 0.25 before treating estimates as stable.
   - If convergence is not reached, continue with `prevAns=ans` and document each iteration.
   - Export coefficient, standard error, t-ratio, significance stars, and convergence notes.

6. Visualize and explain.
   - Produce density-over-time tables or plots for each network before interpreting SAOM results.
   - For model outputs, separate substantive effects from controls and always report network direction.
   - Convert results into thesis-ready Chinese prose only after convergence and sign checks pass.

7. Before GitHub upload or public release.
   - Remove absolute private data paths or move them to a config template.
   - Do not upload proprietary or sensitive raw data.
   - Include reproducible sample inputs or schema descriptions if data cannot be shared.
   - Add a maintenance note explaining which scripts are production, exploratory, and robustness-only.

## Response style

When helping with this project, be concrete and workflow-oriented. Prefer checklists, exact filenames, exact RSiena objects, and specific maintenance actions over broad statements. When drafting an application, explicitly answer:

- who the maintainer is
- what repository or workflow is maintained
- why the project matters
- how the requested benefit will be used in real maintenance work
