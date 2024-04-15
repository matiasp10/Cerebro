La función $f : \mathbb{R}^+ → \mathbb{R}$ definida por $f(x) = log_a x$ se llama **logaritmo de x en base a**, aquí suponemos que $a > 1$. El logaritmo de $x$ en base $a$ es un _número y_  tal que $a^y = x$, esto es, las expresiones

$$
\huge	y = log_ax \enspace y \enspace a^y = x
$$
son equivalentes.

El dominio de la función logaritmo es R+ y el codominio R. Algunas propiedades de la función logaritmo son:

- $\large log_aa = 1$
- $\large log_a1 = 0$
- $\large log_a(xz) = log_ax + log_az$
- $\large log_a\frac{x}{z} = log_ax - log_az$
- $\large log_ax^z = z.log_ax$

La gráfica de la función logaritmo tiene el siguiente aspecto:


```functionplot
---
title: f(x) = log10(x)
xLabel: 
yLabel: 
bounds: [-1,10,-2,1]
disableZoom: false
grid: true
---
f(x) = log10(x)
```

Las bases más usadas son $a = 10$ y $a = e \simeq  2.718282$. Si $a = 10$ se escribe $log x$ en vez de $log_{10} x$ y se conoce con el nombre de **logaritmo decimal**. Si $a = e$ se escribe $ln x$ en vez de $log_e x$ y se llama **logaritmo neperiano o natural**.

