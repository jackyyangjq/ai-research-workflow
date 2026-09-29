# Before you trust a number

Checks for errors that produce no error message. Run them before a result goes into a draft, a figure or a slide.

## Data

- [ ] Types are wide enough before any arithmetic on IDs or counts. Small integer types overflow without warning.
- [ ] Units and signs match the data documentation. Some sources store costs and outflows as negative numbers.
- [ ] Each variable's coverage over time is plotted, and no gap sits on top of the event under study.
- [ ] Row counts are checked after every merge and filter.

## Estimation

- [ ] The main estimate is reproduced by a second, independent implementation.
- [ ] Weights, fixed effects and clustering are applied in every step, not only the last one.
- [ ] The design has been tested against the obvious confound: what else changed at the same time?

## Outputs

- [ ] Every number in the draft comes from the results file, and a script writes each one.
- [ ] Generated files (Word, PDF, figures) have been opened and inspected. A build log that says "success" is not a check.

## Process

- [ ] A session other than the one that wrote the code has checked the result.
- [ ] Agents that search files are given narrow folder paths, and leftover processes are cleared after long jobs.
