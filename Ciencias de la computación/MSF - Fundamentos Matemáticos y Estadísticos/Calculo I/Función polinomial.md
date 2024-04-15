La función polinómica $P_n : \mathbb{R} → \mathbb{R}$ de grado $n$ está definido por:

$$
\large P_n(x) = c_nx^n + c_n−1x^{n−1} + \ ... \ + c_1x + c_0 = \sum_{k = 0}^{n} c_n-k{{^x{{^{{^{n-k}}}}}}}
$$

Donde $c_n \neq 0$. Para la función polinómica $DP_n = CP_n = \mathbb{R}$. Para obtener la forma de la gráfica de la función polinomial es útil la siguiente propiedad de los polinomios, llamada: **propiedad asintótica**. 

## Propiedad asintótica

Para valores |x| muy grandes:

$$
 \huge c_n x{{^n}} + c_{n−1}x{{^{n-1}}} + \cdots  + c_1x + c_0 \simeq  c_nx{{^n}}
$$

El comportamiento asintótico muestra que las gráficas de los polinomios de grado par, para valores x muy grandes, se parecen a la gráfica de la función potencia $x^n$ para n par, para x cerca de cero se comportará de acuerdo al número de raíces que tenga el polinomio. Un comportamiento análogo se tiene para polinomios de grado impar. A continuación se muestran gráficos para explicar este comportamiento.


```functionplot
---
title: f (x) = (x^2-1)(x^2-4)(x^2-9)
xLabel: 
yLabel: 
bounds: [-10,10,-10,10]
disableZoom: false
grid: true
---
f (x) = (x^2-1)(x^2-4)(x^2-9)
```

