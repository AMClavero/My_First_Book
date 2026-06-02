---
title: Integration by Parts (IBP) and Kira / Fire tools
---
## What IBP means for Feynman integrals

In the context of Feynman integrals, integration-by-parts (IBP) identities are linear relations obtained from integrals of total derivatives in loop-momentum space within dimensional regularisation. They relate integrals with different propagator powers and permit reduction of any integral in a family to a finite set of master integrals. Once master integrals are identified, one typically constructs differential equations for them and attempts to bring the system into an $\varepsilon$-form to obtain analytic solutions in terms of iterated integrals.

Definition — Feynman integral:

A Feynman integral associated to a graph $G$ with $l$ loops and $n$ propagators is commonly written as

$$
I(\nu_1,\dots,\nu_n)=\int \prod_{j=1}^l \frac{d^Dk_j}{i\pi^{D/2}}\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\, ,
$$

where the $D_i$ denote inverse propagators and the integers $\nu_i$ their powers.

Definition — IBP (integration by parts) for Feynman integrals:

Within dimensional regularisation the integral of a total derivative vanishes (no boundary terms). For any loop momentum $k_i$ and any vector $q$ constructed from external and loop momenta,

$$
0=\int \prod_{j=1}^l d^Dk_j\;\frac{\partial}{\partial k_i^\mu}\Bigl\{q^\mu\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\Bigr\}\,.
$$

Expanding this equation yields linear relations among Feynman integrals with shifted indices $\nu_j$; these are the IBP identities. By generating sufficiently many such identities and applying an ordering (Laporta algorithm), one reduces the family to a finite basis of master integrals.

Key consequences and workflow:

- Reduction: IBP identities reduce generic integrals to master integrals using linear-algebraic elimination.
- Master integrals: Only master integrals need explicit computation; they form a basis dependent on the chosen ordering.
- Tools: Public programs such as FIRE, Reduze and Kira perform IBP reductions, often using finite-field and sparse linear algebra techniques for performance.

Example (sketch):

For the one-loop two-point function with equal masses, IBP relations allow reduction of integrals with indices $(\nu_1,\nu_2)$ to the masters $I_{1,1}$ and $I_{1,0}$ (bubble and tadpole). See the referenced chapter for the full derivation and diagrams.

Remarks:

- Different ordering choices (dot-basis, ISP-basis) lead to different practical master sets.
- IBP reduction is algebraic over rational functions in kinematic variables and the dimension $D$; simplification of rational functions is typically the performance bottleneck.

Reference: material summarized and converted from `recursos/IBP.pdf` (chapter on iterated integrals and section 6.1 on IBP).

---
