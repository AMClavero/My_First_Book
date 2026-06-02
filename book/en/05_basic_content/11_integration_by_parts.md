
---
title: Integration by Parts (IBP) and Kira / Fire tools
---
## What IBP means for Feynman integrals

In the context of Feynman integrals, integration-by-parts (IBP) identities are linear relations obtained from integrals of total derivatives in loop-momentum space within dimensional regularisation. They relate integrals with different propagator powers and allow reduction of any integral in a family to a finite set of master integrals. Once master integrals are identified, one typically constructs differential equations for them and attempts to transform them to an $\varepsilon$-form to solve them in terms of iterated integrals.

### Definition — Feynman integral:

A Feynman integral associated to a graph $G$ with $l$ loops and $n$ propagators is commonly written as

$$
I(\nu_1,\dots,\nu_n)=\int \prod_{j=1}^l \frac{d^Dk_j}{i\pi^{D/2}}\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\, ,
$$

where the $D_i$ denote inverse propagators and the integers $\nu_i$ their powers.

### Definition — IBP (integration by parts) for Feynman integrals:

Within dimensional regularisation the integral of a total derivative vanishes (no boundary terms). For any loop momentum $k_i$ and any vector $q$ constructed from external and loop momenta:

$$
0=\int \prod_{j=1}^l d^Dk_j\;\frac{\partial}{\partial k_i^\mu}\Bigl\{q^\mu\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\Bigr\}\,.
$$

Expanding this equation yields linear relations among Feynman integrals with shifted indices $\nu_j$; these are the IBP identities. By generating sufficiently many identities and applying an ordering criterion (Laporta algorithm) one reduces the family to a finite basis of master integrals.

### Key consequences and workflow:

- Reduction: IBP identities allow reduction of generic integrals to master integrals by algebraic elimination.
- Master integrals: only the master integrals need to be computed explicitly; they form a basis that depends on the chosen ordering criterion.
- Tools: public programs such as FIRE, Reduze and Kira perform IBP reductions, using finite-field methods and sparse linear algebra to improve performance.

Example (sketch):

For the one-loop two-point function with equal masses, IBP relations allow reduction of integrals with indices $(\nu_1,\nu_2)$ to the masters $I_{1,1}$ and $I_{1,0}$ (bubble and tadpole). See the referenced chapter for the full derivation and diagrams; the bubble and tadpole topologies are shown in {numref}`fig-bubble` and {numref}`fig-tadpole`.

---
# Integration by Parts (IBP) and Kira / Fire tools
---
## What IBP means for Feynman integrals

In the context of Feynman integrals, integration-by-parts (IBP) identities are linear relations obtained from integrals of total derivatives in loop-momentum space within dimensional regularisation. They relate integrals with different propagator powers and allow reduction of any integral in a family to a finite set of master integrals. Once master integrals are identified, one typically constructs differential equations for them and attempts to transform them to an $\varepsilon$-form to solve them in terms of iterated integrals.

### Definition — Feynman integral:

A Feynman integral associated to a graph $G$ with $l$ loops and $n$ propagators is commonly written as

$$
I(\nu_1,\dots,\nu_n)=\int \prod_{j=1}^l \frac{d^Dk_j}{i\pi^{D/2}}\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\, ,
$$

where the $D_i$ denote inverse propagators and the integers $\nu_i$ their powers.

### Definition — IBP (integration by parts) for Feynman integrals:

Within dimensional regularisation the integral of a total derivative vanishes (no boundary terms). For any loop momentum $k_i$ and any vector $q$ constructed from external and loop momenta:

$$
0=\int \prod_{j=1}^l d^Dk_j\;\frac{\partial}{\partial k_i^\mu}\Bigl\{q^\mu\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\Bigr\}\,.
$$

Expanding this equation yields linear relations among Feynman integrals with shifted indices $\nu_j$; these are the IBP identities. By generating sufficiently many identities and applying an ordering criterion (Laporta algorithm) one reduces the family to a finite basis of master integrals.

### Key consequences and workflow:

- Reduction: IBP identities allow reduction of generic integrals to master integrals by algebraic elimination.
- Master integrals: only the master integrals need to be computed explicitly; they form a basis that depends on the chosen ordering criterion.
- Tools: public programs such as FIRE, Reduze and Kira perform IBP reductions, using finite-field methods and sparse linear algebra to improve performance.

Example (sketch):

For the one-loop two-point function with equal masses, IBP relations allow reduction of integrals with indices $(\nu_1,\nu_2)$ to the masters $I_{1,1}$ and $I_{1,0}$ (bubble and tadpole). See the referenced chapter for the full derivation and diagrams; the bubble and tadpole topologies are shown in {numref}`fig-bubble` and {numref}`fig-tadpole`.

```{figure} _static/images/bubble.png
:name: fig-bubble
:align: center
:width: 40%

Bubble (one-loop two-point) topology.
```

```{figure} _static/images/tadpole.png
:name: fig-tadpole
:align: center
:width: 25%

Tadpole (one-loop one-point) topology.
```

### Remarks:

- Different ordering choices (dot-basis, ISP-basis) lead to different practical master sets.
- IBP reduction is algebraic over rational functions in kinematic variables and the dimension $D$; simplification of rational functions is typically the performance bottleneck.

Reference (APA): Weinzierl, S. (2022). Feynman Integrals. arXiv:2201.03593. https://arxiv.org/abs/2201.03593

## Using FIRE6 for IBP reduction

FIRE6 is a public program to reduce Feynman integrals to master integrals; it implements modular-arithmetic reductions and a C++ backend designed for large problems. Typical workflow: prepare a Mathematica "start" file describing the family (momenta, propagators, replacements), optionally generate LiteRed rules, save the start file and run the C++ FIRE6 reduction with a small config file.

Minimal example (start file in Mathematica):

```mathematica
Get["FIRE6.m"]; 
Internal = {k1, k2};
External = {p1, p2, p3};
Propagators = {-k1[2], -(k1 + p1 + p2)[2], -k2[2], ...(etc.)};
Replacements = {p1[2] -> 0, p2[2] -> 0, p1 p2 -> s/2};
PrepareIBP[]; 
Prepare[]; 
SaveStart["doublebox"]; Quit[];
```

Example C++ config file (`doublebox.conf`):

```
#threads           4
#fthreads          4
#variables         d,s,t
#start
#folder            examples/
#problem           1 doublebox.start
#integrals         doublebox.m
#output            ../tests/outputs/doublebox.tables
```

Run with:

```bash
bin/FIRE6 -c examples/doublebox
```

The file `doublebox.tables` contains the reduced expressions (integrals expressed in terms of masters) which can be loaded into Mathematica with `LoadTables`.

See the FIRE6 manual (`recursos/FIRE6.pdf`) for installation and advanced options.

Citation: Smirnov, A.V. & Chukharev, F.S. (2020). FIRE6: Feynman Integral REduction with modular arithmetic. Computer Physics Communications, 247, 106877. DOI: 10.1016/j.cpc.2019.106877

---
