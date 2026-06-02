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

Para la función de dos puntos de un bucle con masas iguales, las identidades IBP permiten reducir integrales con índices $(\nu_1,\nu_2)$ a las maestras $I_{1,1}$ e $I_{1,0}$ (burbuja y tadpole). Consulte la referencia para la derivación completa y los diagramas.

Observaciones:

- Diferentes elecciones de orden (dot-basis, ISP-basis) conducen a conjuntos de maestras distintos en la práctica.
- La reducción IBP es algebraica sobre funciones racionales en variables cinemáticas y la dimensión $D$; la simplificación de funciones racionales suele ser el cuello de botella en rendimiento.

Referencia: contenido resumido y convertido desde `recursos/IBP.pdf` (capítulo sobre integrales iteradas y sección 6.1 sobre IBP).

---
