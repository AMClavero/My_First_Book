---
title: Integration by Parts (IBP) and Kira / Fire tools
---

## What is integration by parts?

Integration by parts (IBP) is a technique to compute integrals of the form $\int u\,dv$, based on the product rule for derivatives. Formula:

$$
\int u\,dv = u v - \int v\,du
$$

Choose $u$ and $dv$ so that $\int v\,du$ is simpler.

## Using the resources

In the repository `recursos` folder there are several PDFs used as reference:

- `recursos/IBP.pdf` — theory and basic examples.
- `recursos/Kira2.pdf`, `recursos/Kira3.pdf` — `kira` manuals.
- `recursos/FIRE5.pdf`, `recursos/FIRE6.pdf` — `fire` manuals.

Below are practical examples showing how to use `kira` and `fire` to assist IBP tasks (integral reduction, symbolic manipulation, simplification).

## Example 1 — a step-by-step integral

Compute $\int x e^{x} \,dx$.

1. Let $u = x$, $dv = e^{x} dx$. Then $du = dx$, $v = e^{x}$.
2. Apply the formula: $\int x e^{x} dx = x e^{x} - \int e^{x} dx = x e^{x} - e^{x} + C$.

## Example 2 — using `kira` for symbolic manipulation

Assuming `kira` can read simple expressions and apply IBP automatically:

```bash
# Apply IBP automatically and save result
kira --input "integrate(x*exp(x), x)" --method ibp --output result.txt
cat result.txt
```

Expected output:

```
x*e^x - e^x + C
```

Consult `recursos/Kira2.pdf` and `recursos/Kira3.pdf` for detailed options.

## Example 3 — using `fire` to reduce integral families

`fire` can reduce parameter-dependent integrals and find relations between them.

```bash
# Reduce family I(a) = ∫ x^a e^x dx
fire --integral "I(a) = integrate(x^a * exp(x), x)" --reduce --param a --output fire_result.txt
cat fire_result.txt
```

See `recursos/FIRE5.pdf` and `recursos/FIRE6.pdf` for full syntax and advanced examples.

## Reproducibility notes

- Reference PDFs are in `recursos/` and are not committed by default. Ensure readers have them locally.
- If desired, we can extract small licensed excerpts into Markdown with proper attribution.

---
