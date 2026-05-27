---
title: Integration by Parts (IBP) and Kira / Fire tools
---
## What IBP means for Feynman integrals

In the context of Feynman integrals, integration-by-parts (IBP) identities are linear relations obtained from integrals of total derivatives in loop-momentum space within dimensional regularization. They relate integrals with different propagator powers and permit reduction of any integral in a family to a finite set of master integrals. Once masters are identified, one typically constructs differential equations for them and solves (often via an $\varepsilon$-form) to obtain analytic results.

Reference: material summarized from `recursos/IBP.pdf` (chapter on iterated integrals, section 6.1).

## Summary of the resources

- `recursos/IBP.pdf`: derivation of IBP identities, worked 1-loop example (two-point function), reduction strategy to master integrals and use of differential equations.
- `recursos/Kira2.pdf`, `recursos/Kira3.pdf`: examples and job formats for `kira` (topology definitions, job files, parallel options).
- `recursos/FIRE5.pdf`, `recursos/FIRE6.pdf`: workflows for `FIRE`, input formats and table outputs.

## Example: minimal `kira` job (orientative)

Create a job file describing topology, integrals and desired reductions (e.g. `kira_job.yaml`) and run:

```bash
kira --job kira_job.yaml --output kira_results.txt
```
## Minimal `fire` workflow (orientative)

1. Prepare input describing topology and propagators (e.g. `fire_input.m`).
2. Run reduction:

```bash
fire --input fire_input.m --reduce --output fire_reduction.tables
```

3. Read `fire_reduction.tables` to obtain expressions of integrals in terms of master integrals.

`FIRE` builds large linear systems (IBP identities) and resuelve para las reducciones; suele usarse con paralelización y almacenamiento intermedio.

## Practical recommendations

- Exploit simmetries and sector selection before la reducción para reducir coste.
- Archive tablas de reducción para reuso.
- Tras obtener masters, considere el método de ecuaciones diferenciales y la transformación a $\varepsilon$-form (ver `recursos/IBP.pdf`).

---
