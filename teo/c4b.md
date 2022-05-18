---
nav_order: 7
published: false
---


# AERMOD

Fundamentos del AERMOD.
{: .fs-6 .fw-300 }

<!-- center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center -->


## Resumen:



### Cálculo de perfiles

AERMOD utiliza los parámetros de capa límite y relaciones de similitud para computar perfiles verticales de:
- dirección del viento
- intensidad del viento
- temperatura
- grdiente de temperatura potencial
- turbulencia vertical &sigma;<sub>w</sub>
- turbulencia lateral  &sigma;<sub>v</sub>

### Cálculo de variables efectivas

Las plumas se extienden espacialmente pero los cáculos de una pluma puede tomar un solo valor de condiciones atmosféricas, aunque estas condiciones cambien en el espacio. Esto es un fuente de error pero puede reducirse usando valores adecuados promedio para asegurarse representatividad.
En AERMOD el proceso de calcular variables efectivas puede resumirse en:
- Calculo de altura del centroide de la pluma (H<sub>p</sub>) 
- Calculo de &sigma;<sub>z</sub> en base a los valores de &sigma;<sub>w</sub> y H<sub>p</sub>
- Se considera el menor de los intervalo entre H<sub>p</sub> y el receptor ó entre H<sub>p</sub> y 2.15&sigma;<sub>z</sub> en la dirección del receptor.
- La variable de interés es integrada entre el intervalo vertical deifinido en el paso previo y dividido por el dicho intervalo para obtener la variable efectiva.



### Formula general

La concentración total se expresa como la contribución de una pluma horizontal (que impacta el terreno) y una pluma que contornea el relieve:
 
$$
C_T = f \, C_{(x_r,y_r,z_r)} + (1-f) C_{(x_r,y_r,z_p)}
$$

donde :

$$
f = 0.5(1+\varphi)
$$



### Prediccón de concentraciones:


$$
 C_{(x,y,z)} = \frac{Q}{u} \varphi_y(x,y) \, \varphi_z(x,z)
$$



Además AERMOD simula 5 diferentes tipo de plumas dependiento en la estabilidad atmosférica y la uicación por debajo de la capa límite:
- directa
- indirecta
- penetrada
- injectada
- estable

En condiciones estables la pluma se calcula como gaussianas en las componentes verticales y horizontales.

Bajo condiciones convectivas (L<0) la componente horizontl sigue siendo gaussiana mientras que en la vertical resulta de la combinación de tres tipos de plumas:
1. Pluma directa en la capa de mezcla.
2. Pluma indirecta que se eleva y tiende al techo de la capa de mezcla
3. Pluma penetrada que se inyecta en la capa de mezcla pero debido la flotación penetra en la capa estable.



$$
z_c = h_s + \Delta h + \dfrac{wx}{u}
$$


$$
p_w = \dfrac{\lambda_1}{\sqrt{2\pi}\sigma_{w1}} \exp{\bigg(- \dfrac{(w-w_1)^2}{2\sigma_{w1}^2} \bigg)} +  \dfrac{\lambda_2}{\sqrt{2\pi}\sigma_{w2}} \exp{\bigg(- \dfrac{(w-w_2)^2}{2\sigma_{w2}^2} \bigg)}
$$




$$
C_d(x,y,z) = \dfrac{Q f_b}{\sqrt{2\pi} u }  F_y \sum_{j=1}^2 \sum_{m=0}^\infty \dfrac{\lambda_j}{\sigma_{zj}}	\bigg[ \exp(\dfrac{(z-\Psi_{dj}-2mz_j)^2}{2\sigma^2_{zj}}) + \exp(\dfrac{(z+\Psi_{dj}-2mz_j)^2}{2\sigma^2_{zj}})  \bigg]
$$


### Plume rise

$$
\Delta z = \bigg(   \dfrac{3F_m x}{0.6^2 \overline{u}^2 }   +  \dfrac{3F_b x^2}{2 0.6^2 \overline{u}^3 }   \bigg)^{1/3}
$$



$$
F_m = w_s^2r_s^2 \dfrac{T}{T_s} \qquad   F_b=gw_sr_s^2 \dfrac{\Delta T}{T_s}
$$



$$
\Delta h = \bigg[ 2.6^3 P_s + (2/3)^3 \bigg]^{1/3} \Delta h_h
$$

$$ P_s=\dfrac{F_b}{uN^2_h \Delta h_h^3 } $$

$$N=\sqrt{\dfrac{g}{\theta_{h_mix}} \bigg( \dfrac{\partial \theta}{\partial z}\bigg)_{z>h_{mix}}} $$



### Estimación de coeficientes


$$
\sigma_y = \sqrt{\sigma^2_{y,0} + 0.08 (\Delta h)^2 } \qquad \sigma_z = \sqrt{\sigma^2_{z,0} + 0.08 (\Delta h)^2 }
$$





$$
\sigma_{y,0}=\dfrac{}{\tilde{u} [ 1+78z_{PG}\tilde{\sigma}_v x / (z_{max}\tilde{u}h_{mix}) ]^{0.3} }
$$



## Ejercicios:


## Bibliografía:
- "AERMOD Model Formulation and Evaluation", U.S.EPA. EPA-454/ R-18-003. April, 2018.

