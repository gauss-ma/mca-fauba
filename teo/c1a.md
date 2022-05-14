---
nav_order: 1
published: true
---

# Modelos de transporte

En esta unidad vamos a repasar cuales son los fundamentos de los modelos de transporte, y las expresiones generales de algunos modelos que serán de utilizados en el curso.
{: .fs-6 .fw-300 }

<!-- center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center -->


## Resumen
Los modelos de transporte de contaminantes son funciones matemáticas que satisfacen la ecuación diferencial de *conservación de masa*, también conocida como **ecuación de transporte**:

<p>
\[ \dfrac{\partial c}{\partial t} = E - \lambda\,c - u \dfrac{\partial c}{\partial x} + K \dfrac{\partial^2 c}{\partial x^2} \]
</p>

esta ecuación expresa como se modifica la concentración de un compuesto *c* en el tiempo, considerando los procesos de:
+ Emisiónes
+ Reacciones químicas ó *decaimiento*
+ Arrastre por el viento (*advección*)
+ Mezclado turbulento (*difusión*)

No se conoce una solución general a esta ecuación, pero si realizamos los siguientes supuestos y simplifiacaciones:
- La velocidad del viento es constante en el tiempo y espacio.
- La difusión turbulenta en el sentido de la dirección del viento es despreciable.
- El contaminante en un tiempo inicial se encuentra concentrado en un punto.

podemos llegar a una solución analítica, cuya fórmula general es:

<p>
$$ c_{(x,t)} = \dfrac{M}{\sqrt{2\pi}\sigma} \exp\bigg[ \dfrac{- (x-\mu)^2}{2\sigma^2}  \bigg] \exp^{-\lambda t} $$
</p>

los modelos basados en esta solución para describir como se dispersan los contaminantes se conocen como **modelos gaussianos**, y son el objeto de estudio de este curso.

## Bibliografía
- "Air Dispersion Modeling, Foundations and Applications". De Visscher A. Wiley. 2013.

