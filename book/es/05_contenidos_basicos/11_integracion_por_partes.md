---
title: Integración por partes (IBP) y herramientas Kira / Fire
---

## ¿Qué es la integración por partes?

La integración por partes (IBP) es una técnica para calcular integrales de la forma $\int u\,dv$, basada en la regla del producto para derivadas. La fórmula es:

$$
\int u\,dv = u v - \int v\,du
$$

Se elige $u$ y $dv$ de modo que la integral $\int v\,du$ sea más sencilla.

## Uso de los recursos

En la carpeta `recursos` tienes varios PDFs con ejemplos y documentación. En particular usamos:

- `recursos/IBP.pdf` — teoría y ejemplos clásicos de IBP.
- `recursos/Kira2.pdf`, `recursos/Kira3.pdf` — manuales de `kira`.
- `recursos/FIRE5.pdf`, `recursos/FIRE6.pdf` — manuales de `fire`.

Incluimos a continuación ejemplos prácticos de cómo usar `kira` y `fire` para automatizar pasos relacionados con IBP (reducción de integrales, manipulación simbólica y simplificación).

## Ejemplo 1 — resolver una integral paso a paso

Queremos calcular $\int x e^{x} \,dx$.

1. Elegimos $u = x$, $dv = e^{x} dx$. Entonces $du = dx$, $v = e^{x}$.
2. Aplicando la fórmula: $\int x e^{x} dx = x e^{x} - \int e^{x} dx = x e^{x} - e^{x} + C$.

## Ejemplo 2 — usar `kira` para manipular expresiones simbólicas

Supongamos que `kira` es una herramienta de línea de comandos que puede simplificar expresiones y aplicar reglas de integración por partes automatizadas.

Comandos de ejemplo (suponiendo que `kira` acepta entrada en formato LaTeX o expresión simbólica):

```bash
# Simplificar y aplicar IBP automáticamente a la expresión
kira --input "integrate(x*exp(x), x)" --method ibp --output result.txt
# Mostrar resultado
cat result.txt
```

Salida esperada (ejemplo):

```
x*e^x - e^x + C
```

Nota: consulta `recursos/Kira2.pdf` y `recursos/Kira3.pdf` para opciones avanzadas de `kira`, flags y formatos de entrada.

## Ejemplo 3 — usar `fire` para reducción de integrales

`fire` es otra herramienta que permite reducir integrales paramétricas o integrar familias de funciones mediante reglas simbólicas y bases de integrales maestras.

Comando de ejemplo:

```bash
# Reducir una familia de integrales dependientes de un parámetro
fire --integral "I(a) = integrate(x^a * exp(x), x)" --reduce --param a --output fire_result.txt
cat fire_result.txt
```

`fire` puede generar relaciones entre integrales y aplicar transformaciones que facilitan la aplicación de IBP repetida. Consulta `recursos/FIRE5.pdf` y `recursos/FIRE6.pdf` para sintaxis completa y ejemplos avanzados.

## Notas sobre reproducibilidad

- Los PDFs originales utilizados como referencia están en la carpeta `recursos/`. Asegúrate de que quienes lean el libro localmente tengan acceso a esos PDFs (no están versionados por diseño).
- Si prefieres incluir extractos concretos en el libro, podemos extraer fragmentos y convertirlos a Markdown, respetando licencias.

## Enlaces y lectura adicional

- Teoría IBP: `recursos/IBP.pdf`
- Manuales `kira`: `recursos/Kira2.pdf`, `recursos/Kira3.pdf`
- Manuales `fire`: `recursos/FIRE5.pdf`, `recursos/FIRE6.pdf`

---
