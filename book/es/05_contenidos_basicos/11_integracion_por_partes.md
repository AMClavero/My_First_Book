---
title: Integración por partes (IBP) y herramientas Kira / Fire
---

## ¿Qué es la integración por partes (IBP) en integrales de Feynman?

En el contexto de integrales de Feynman, las identidades de integración por partes (IBP) son relaciones obtenidas al considerar integrales de derivadas totales en el espacio de momentos de bucle dentro de la regularización dimensional. Dicha propiedad (ausencia de términos de frontera) genera ecuaciones lineales que relacionan integrales con distintos exponentes de propagadores. Estas ecuaciones permiten reducir cualquier integral de la familia a una combinación lineal de un conjunto finito de integrales maestras (master integrals).

Consecuencia práctica: una vez que se ha reducido la familia de integrales a sus masters, se pueden construir sistemas de ecuaciones diferenciales para esos masters y resolverlos (por ejemplo, transformando el sistema a la llamada forma $\varepsilon$-form), recuperando las soluciones en términos de integrales iteradas.

Referencia: extracto de `recursos/IBP.pdf` (capítulo sobre iterated integrals, sección 6.1 y ejemplos de reducción).

## Resumen de los PDFs usados

- `recursos/IBP.pdf`: explica la derivación de las identidades IBP, demuestra cómo construir relaciones lineales entre integrales (ej. un caso de una integral de 1-loop con dos propagadores) y discute la reducción a integrales maestras y el papel de las ecuaciones diferenciales.
- `recursos/Kira2.pdf`, `recursos/Kira3.pdf`: manuales y ejemplos de `kira` (configuración de topologías, definición de integrales y ejecución de trabajos de reducción).
- `recursos/FIRE5.pdf`, `recursos/FIRE6.pdf`: guía de uso de `FIRE` para generar y resolver las identidades IBP, extracción de integrales maestras y workflows para producir tablas de reducción.

## Cómo construir un job mínimo para `FIRE` (orientativo)

1. Definir la topología y los propagadores en un fichero de entrada (por ejemplo `fire_input.m` si se usa formato Mathematica-like).
2. Ejecutar la reducción:

```bash
# sintaxis orientativa; adapte según su instalación de FIRE
fire --input fire_input.m --reduce --output fire_reduction.tables
```

3. Inspeccionar `fire_reduction.tables` para obtener las expresiones de cada integral en términos de master integrals.

Notas: `FIRE` genera sistemas lineales grandes; suele usarse en combinación con herramientas para seleccionar sectores, paralelizar y guardar tablas intermedias.

## Cómo preparar un job mínimo para `kira` (orientativo)

1. Crear un fichero con la definición de la topología, las integrales y las reglas (ej. `kira_job.yaml` o formato que requiera la versión instalada).
2. Ejecutar:

```bash
kira --job kira_job.yaml --output kira_results.txt
```

o, en interfaces que aceptan comandos directos:

```bash
kira --reduce "I(indices) = definition" --method ibp --out kira_results.txt
```

Recomendación: consulte `recursos/Kira2.pdf` y `recursos/Kira3.pdf` para parámetros, formatos de topología y opciones de paralelización.

## Pistas prácticas y recomendaciones

- Compruebe siempre las simetrías del grafo para reducir el número de integrales independientes antes de la reducción.
- Use estrategias de sector decomposition / selección de reducción para limitar el coste computacional.
- Genere y almacene tablas de reducción intermedias para reusar resultados.
- Tras obtener los masters, considere usar el método de ecuaciones diferenciales y buscar una transformación al $\varepsilon$-form si fuese posible (ver `recursos/IBP.pdf`).

## Reproducibilidad y licencias

He resumido y reinterpretado el material presente en los PDFs de `recursos/`. Si quieres que incorpore citas textuales o fragmentos largos, indícamelo y los extraigo (añadiendo la referencia BibTeX en `book/_static/references.bib` si procede).

---

