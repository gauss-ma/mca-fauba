---
nav_order: 4
published: false
---

# SCREEN3

Fundamentos del modelo screen3.
{: .fs-6 .fw-300 }

<!--center><iframe width="400" aspect-ratio="0.5625"
src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center-->

## Resumen

SCREEN3 usa un modelo de pluma gausiana que incorpora parametros de las fuentes emisoras y meteorológicos para estimar concentraciones de contaminantes de fuentes que emiten de forma continua.

Se asume que el contaminante no reacciona con otros compuestos de la atmósfera, ni hay otros mecanìsmos de remoción (deposición seca ni húmeda)

<!-- The Gaussian model equations and the interactions of the source-related and meteorological factors are described in Volume II of the ISC user's guide (EPA, 1995b), and in the Workbook of Atmospheric Dispersion Estimates (Turner, 1970).-->

La ecuación base para determinar la concentración a nivel del suelo sobre el eje de la pluma es:

<p>\[
X = \dfrac{Q}{2\pi u_s \sigma_y\sigma_z} \exp^{-\dfrac{(z_r -h_e)^2}{2\sigma_z^2}} + \exp^{-\dfrac{(z_r + h_e)^2}{2\sigma_z^2}} 
+ \sum_{N=1}^k  
                \exp^{-\dfrac{(z_r -h_e-2Nz_i)^2}{2\sigma_z^2}} 
              + \exp^{-\dfrac{(z_r +h_e-2Nz_i)^2}{2\sigma_z^2}} 
              + \exp^{-\dfrac{(z_r -h_e+2Nz_i)^2}{2\sigma_z^2}} 
              + \exp^{-\dfrac{(z_r +h_e+2Nz_i)^2}{2\sigma_z^2}} 
\]</p>
donde: $X$ es la concentración [g/m3], $Q$: tasa de emisión [g/s], $u_s$: velocidad del viento a la altura de emisión, $z_r$: altura del emisor, h: altura del eje de la pluma, $z_i$ altura de mezcla, &sigma; son los parametros de dispersión.

Para condiciones estables, ó alturas de mezcla mayores a 10km la mezcla vertical se asume que no tiene limite y por lo tanto la sumatoria es igual a cero.

Para fuentes areales se utiliza un algoritmo de integración numérica, y para fuentes de volumen se utiliza un método de punto virtual.

### Peor escenario:
El SCREEN3 examina un rango de clases de estabilidad y velocidades del viento para identificar el peor escenario posible que resulte en la máxima concentración en el receptor.

```
|     |       Velocidad del viento a 10m [m/s]            |
|Clase| 1 |1.5| 2 |2.5| 3 |3.5| 4 |4.5| 5 | 8 | 10| 15| 20|
|=====|===|===|===|===|===|===|===|===|===|===|===|===|===|
| A   |###|###|###|###|###|   |   |   |   |   |   |   |   |
| B   |###|###|###|###|###|###|###|###|###|   |   |   |   |
| C   |###|###|###|###|###|###|###|###|###|###|###|   |   |
| D   |###|###|###|###|###|###|###|###|###|###|###|###|###|
| E   |###|###|###|###|###|###|###|###|###|   |   |   |   |
| F   |###|###|###|###|###|###|###|   |   |   |   |   |   |

```

la velocidad a la altura de la fuente se estima utilizando un perfil de vientos logaritmicos.

### Altura de mezcla (z<sub>m</sub>)

La altura de mezcla para condiciones neturales e inestables (clases de A-D), asume mezcla mecánica y se calcula según la siguiente fórmula (Randerson, 1984):

$$ z_m = 0.3\,u^* / f $$

Usando el perfil logritmico de velocidades (con z0=0.3m) se puede estimar u*:

$$ u^* = 0.1 u_{10} $$

Usando las ultimas dos expresiones:

$$ z_m = 320 u_{10} $$


### Plume rise

Flujo de flotación:

$$ F_b= g\, v_s\, d_s^2 (T_s-T_a) / (4 T_s) $$

Para flares (antorchas):

$$ F_b = 1.66\,10^-5 \, H $$

donde $H$ es la tasa total de calor emitido (cal/s).


El flujo de cantidad de movimiento:

$$ F_s= v_s^2 d_s^2 T_a/ (4T_s) $$

### Parametros de dispersión (&sigma;)

Para el cálculo de &sigma;<sub>y</sub> y &sigma;<sub>z</sub> se utilizan funciones que ajustan a las curvas de Pasquill-Gifford.


$$\sigma_y = 465 .11628 (x) \tan(TH)$$

donde $TH=  0.017453293 [c - d\,\ln(x)]$

Para el coeficiente de dispersión vertical:

$$ \sigma_z=a\,x^b $$

donde los coeficientes a y b están tabulados.

Para el caso de fuentes de volúmen las coordenadas x  e y son modificadas para contemplar las dimensiones de la fuente.

$$
 x_y = \bigg(\dfrac{\sigma_{y0}}{p} \bigg)^{1/q} \qquad x_z = \bigg(\dfrac{\sigma_{z0}}{a} \bigg)^{1/b}
$$
 
### Dispersión inducida por flotación

$$
\sigma_{ye}= \sqrt{ \sigma_y^2 + (\Delta h / 3.5)^2 }
\qquad 
\sigma_{ze}= \sqrt{ \sigma_z^2 + (\Delta h / 3.5)^2 }
$$

### Downwash


En presencia de edificios:

$$ h_c = h_b (1 + 1.6 \exp{(-1.3\,L/h_b)} $$


Concentración dentro de la cavidad:

$$ X= Q / 1.5 A_p u $$


Para edificios cortos ($L/h_c \leq 2$)

$$ x_r =\dfrac{A\, W}{1 + B\,(W/h_b)}$$

Para edificios alargados ($L/h_c \gt 2 $)


$$ x_r = \dfrac{1.75 \, W}{1+0.25 (W/h_c)}$$


### Fumigación

$$ x_{max} = u \,t_m$$

$$ x_{max} = (u p_a \, c_p/R) \, (\Delta\theta/z)	(h_i-h_s) [(h_i-h_2)/2] $$


$$ X_f= \dfrac{Q}{\sqrt{2\pi} u\,(\sigma_{ye} + h/8) (h_e+2\sigma_{ze})} $$


### Fumigación costera

$$h_t = A\sqrt{x} $$

$$x_{max} = ((h_e+2\sigma_{ze})/6)^2 - x_s $$


### Terreno complejo

$$ X= \dfrac{2.032 Q}{\sigma_{ze}\, u \,x} \exp{(\frac{-h_e^2}{2\sigma_{ze}^2})} $$


## Ejercicios

[Trabajo Práctico Nº1](../tps/tp1.md)

## Bibliografía

- "SCREEN3 Model User’s Guide". U.S EPA. EPA-454/B-95-004. September 1995.

