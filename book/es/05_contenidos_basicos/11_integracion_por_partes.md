---
title: Integración por partes (IBP) y herramientas Kira / Fire
---
## Qué significa IBP para integrales de Feynman

En el contexto de las integrales de Feynman, las identidades de integración por partes (IBP) son relaciones lineales obtenidas a partir de integrales de derivadas totales en el espacio de los momentos de bucle, dentro de la regularización dimensional. Relacionan integrales con diferentes potencias de propagadores y permiten reducir cualquier integral de una familia a un conjunto finito de integrales maestras. Una vez identificadas las integrales maestras, normalmente se construyen ecuaciones diferenciales para ellas y se busca transformarlas a la forma en $\varepsilon$ para resolverlas en términos de integrales iteradas.

Definición — integral de Feynman:

Una integral de Feynman asociada a un grafo $G$ con $l$ bucles y $n$ propagadores se expresa habitualmente como

$$
I(\nu_1,\dots,\nu_n)=\int \prod_{j=1}^l \frac{d^Dk_j}{i\pi^{D/2}}\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\, ,
$$

donde los $D_i$ son los inversos de propagador y los enteros $\nu_i$ sus potencias.

Definición — IBP (integración por partes) en el contexto de integrales de Feynman:

En la regularización dimensional la integral de una derivada total se anula (no hay términos de contorno). Para cualquier momento de bucle $k_i$ y cualquier vector $q$ construido a partir de momentos externos y de bucle:

$$
0=\int \prod_{j=1}^l d^Dk_j\;\frac{\partial}{\partial k_i^\mu}\Bigl\{q^\mu\;\frac{1}{D_1^{\nu_1}\cdots D_n^{\nu_n}}\Bigr\}\,.
$$

Al expandir esta ecuación se obtienen relaciones lineales entre integrales de Feynman con los índices $\nu_j$ desplazados; estas son las identidades IBP. Generando suficientes identidades y aplicando un criterio de ordenación (algoritmo de Laporta) se reduce la familia a una base finita de integrales maestras.

Consecuencias y flujo de trabajo:

- Reducción: las identidades IBP permiten reducir integrales genéricas a integrales maestras mediante eliminación algebraica.
- Integrales maestras: sólo es necesario calcular las integrales maestras explícitamente; forman una base que depende del criterio de ordenación elegido.
- Herramientas: programas públicos como FIRE, Reduze y Kira realizan reducciones IBP, usando métodos de campo finito y álgebra lineal dispersa para mejorar rendimiento.

Ejemplo (bosquejo):

Para la función de dos puntos de un bucle con masas iguales, las identidades IBP permiten reducir integrales con índices $(\nu_1,\nu_2)$ a las maestras $I_{1,1}$ e $I_{1,0}$ (burbuja y tadpole). Consulte la referencia para la derivación completa y diagramas; las topologías burbuja y tadpole se muestran en las Figuras \@ref(fig-burbuja) y \@ref(fig-tadpole).

```{figure} _static/images/bubble.png
:name: fig-burbuja
:align: center
:width: 40%

Topología burbuja (dos puntos, un bucle).
```

```{figure} _static/images/tadpole.png
:name: fig-tadpole
:align: center
:width: 25%

Topología tadpole (un punto, un bucle).
```

Observaciones:

- Diferentes elecciones de orden (dot-basis, ISP-basis) conducen a conjuntos de maestras distintos en la práctica.
- La reducción IBP es algebraica sobre funciones racionales en variables cinemáticas y la dimensión $D$; la simplificación de funciones racionales suele ser el cuello de botella en rendimiento.

Referencia (APA): Weinzierl, S. (2022). Feynman Integrals. arXiv:2201.03593. https://arxiv.org/abs/2201.03593

## Uso de FIRE6 para reducción IBP

FIRE6 es un programa público para reducir integrales de Feynman a integrales maestras; incorpora reducción con aritmética modular y un backend en C++ pensado para problemas grandes. Flujo típico: preparar un "start file" en Mathematica (momentos, propagadores, reemplazos), generar reglas de LiteRed opcionalmente, guardar el start y ejecutar la reducción mediante el binario C++ de FIRE6.

Ejemplo mínimo (start file en Mathematica):

```
Get["FIRE6.m"]; 
Internal = {k1, k2};
External = {p1, p2, p3};
Propagators = {-k1[2], -(k1 + p1 + p2)[2], -k2[2], ...(etc.)};
Replacements = {p1[2] -> 0, p2[2] -> 0, p1 p2 -> s/2};
PrepareIBP[]; 
Prepare[]; 
SaveStart["doublebox"]; Quit[];
```

Ejemplo de archivo de configuración C++ (`doublebox.conf`):

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

Ejecutar con:

```bash
bin/FIRE6 -c examples/doublebox
```

El fichero `doublebox.tables` contiene las expresiones reducidas (integrales en términos de maestras) que pueden cargarse en Mathematica con `LoadTables`.

Consulta el manual de FIRE6 (`recursos/FIRE6.pdf`) para instalación y opciones avanzadas.

Cita: Smirnov, A.V. y Chukharev, F.S. (2020). FIRE6: Feynman Integral REduction with modular arithmetic. Computer Physics Communications, 247, 106877. DOI: 10.1016/j.cpc.2019.106877


---
