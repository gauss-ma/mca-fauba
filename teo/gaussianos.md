---
nav_order: 3
published: true
---

# Modelos Gaussianos

En esta clase vamos a presentar algunas soluciones analíticas a la ecuación de transporte conocidas como Modelos Gaussianos.
{: .fs-6 .fw-300 }

## Resumen

### Modelos de Puff Gaussiano

Los *puffs gaussianos*, son modelos utilizados para representar el cambio en el tiempo y el espacio de la concentración de contaminantes emitido en un evento discreto por una fuente puntual.

  $$
  c_{(x,y,z,t)} = \dfrac{M}{\sqrt{2\pi}^3\sigma_x\sigma_y\sigma_z} \exp \bigg[ - \dfrac{(x-ut)^2}{2\sigma_x^2} \bigg] \exp \bigg[ -\dfrac{y^2}{2\sigma_y^2} \bigg] \exp \bigg[ - \dfrac{z^2}{2\sigma_z^2} \bigg] 
  $$

Utilizan la función gaussiana donde $\sigma =\sqrt{2\,K\,t}$ y &mu; representa la posición del puff en cada instante. $M$ es la masa total emitida (la masa del *Puff*).

### Modelos de Pluma Gaussiana

Las *plumas gaussianas* son modelos utilizados para representar la distribución de un contaminante en el espacio para eventos de emisión continuas y sostenidas en el tiempo, para condiciones promedio atmosféricas. 

Son la solución estacionaria de la ecuación de transporte. Y su expresión general es:

  $$
  c_{(x,y,z)} = \dfrac{Q}{u\sqrt{2\pi}^2\sigma_y\sigma_z} \exp \bigg[ -\dfrac{y^2}{2\sigma_y^2} \bigg] \exp \bigg[ - \dfrac{z^2}{2\sigma_z^2} \bigg] 
  $$

en este caso Q representa la tasa de emisión, y $\sigma=\sqrt{2Kx/u}$. Este modelo no contempla mezcla en $x$ ya que lo supone despreciable frente a la advección.

### Adaptaciones al modelo de Pluma Gaussiana

Existe una serie de modificaciones al modelo original de pluma gaussiana podemos relizar para contemplar fenómenos que nos brinden una aproximación más realista de nuestro modelo, entre estas modificiaciones podemos nombrar:

+ Incoporación de altura del emisor.
+ Elevación de la pluma (*plume rise*) por empuje térmico y momentum.
+ Deflección de la pluma por efecto de edificios (*downwash*)
+ Rebote/reflexión de la pluma con el terreno.
+ Rebote/reflexión en límites de inversión térmica.
+ Efecto de la pluma sobre terrenos complejos.
+ Corregir modelo de pluma para receptores muy cercanos.
+ Tratamiento especial para vientos calmos.
+ Coeficientes difusivos en base a clases de estabilidad.

<!--
## Ejercicios
1. Indique en la ecuacción de tranporte cuál es el término que describe únicamente el fenómeno de advección. Haga lo mismo para la difusión y el decaimiento.
2. Bajo un transporte puramente advectivo, cómo cambia la concentración en el tiempo para un punto si la velocdad del viento es cero? Cómo cambia si la velocidad es negativa y la concentración disminuye con la distancia?
3. Bajo un transporte puramente difusivo ¿Cómo cambia la concentrción en el tiempo para un punto donde la concentración inicialmente tiene un máximo local? ¿Cómo cambia si la concentración en dicho punto es un mínimo local?
4. ¿Cuál es la interpretación de &mu; y de &sigma; en la función gaussiana?
-->

## Bibliografía
- "Air Dispersion Modeling, Foundations and Applications". De Visscher A. Wiley. 2013.

