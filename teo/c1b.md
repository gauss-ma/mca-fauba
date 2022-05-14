---
nav_order: 1
published: false
---

# Modelos de transporte

En esta unidad vamos a repasar cuales son los fundamentos de los modelos de transporte, y las expresiones generales de algunos modelos que serán de utilizados en el curso.
{: .fs-6 .fw-300 }

<!-- center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center -->


## Resumen

### Modelos de Puff Gaussiano

Los *puffs gaussianos*, son modelos utilizados para representar el cambio en el tiempo y el espacio de la concentración de contaminantes para eventos de emisión discretas.
Utilizan la función gaussiana donde $\sigma =\sqrt{2Kt}$ y &mu; representa la posición del puff en cada instante.

### Modelos de Pluma Gaussiana
Las *plumas gaussianas* son modelos utilizados para representar la distribución de un contaminante en el espacio para eventos de emisión continuas y sostenidas en el tiempo, para condiciones promedio atmosféricas. 
Son la solución estacionaria de la ecuación de transporte. Y su expresión general es:

<p>
$$ c_{(x,y)} = \dfrac{Q}{u\sqrt{2\pi}\sigma} \exp\bigg[ \dfrac{- (x-\mu)^2}{2\sigma^2}  \bigg] \exp^{-\lambda t} $$
</p>

donde Q es tasa de emisión, y $\sigma=\sqrt{2Kx/u}$.

### Adaptaciones al modelo de Pluma Gaussiana

Existe una serie de modificaciones al modelo original de pluma gaussiana que nos va a permitir contemplar algunos efectos produciendo valores más realistas, entre ellos:
+ Dispersión en las 3 dimensiones de la pluma.
+ Incoporación de altura del emisor.
+ Corregir modelo de pluma para receptores muy cercanos.
+ Coeficientes difusivos en base a clases de estabilidad.
+ Rebote/reflexión de la pluma con el terreno.
+ Elevación de la pluma (*plume rise*) por empuje térmico y momentum.
+ Deflección de la pluma por efecto de edificios (*downwash*)
+ Efecto de la pluma sobre terrenos complejos.
+ Rebote/reflexión en límites de inversión térmica.

## Ejercicios

1. Indique en la ecuacción de tranporte cuál es el término que describe únicamente el fenómeno de advección. Haga lo mismo para la difusión y el decaimiento.
2. Bajo un transporte puramente advectivo, cómo cambia la concentración en el tiempo para un punto si la velocdad del viento es cero? Cómo cambia si la velocidad es negativa y la concentración disminuye con la distancia?
3. Bajo un transporte puramente difusivo ¿Cómo cambia la concentrción en el tiempo para un punto donde la concentración inicialmente tiene un máximo local? ¿Cómo cambia si la concentración en dicho punto es un mínimo local?
4. ¿Cuál es la interpretación de &mu; y de &sigma; en la función gaussiana?


## Bibliografía
- "Air Dispersion Modeling, Foundations and Applications". De Visscher A. Wiley. 2013.
