---
nav_order: 2
published: true
---

# Ecuación de transporte

En esta unidad vamos a deducir la ecuación que describe el transporte de cualquier especie química en la atmósfera, y presentar una solución analítica que puede obtenerse a partir de algunas simplificaciónes y supuestos.
{: .fs-6 .fw-300 }

<!-- center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center -->


## Resumen

Modelar la calidad del aire consiste en representar la concentración de determinadas especies químicas en el aire, su variación en el espacio y en el tiempo. 

Tal representación se puede realizar haciendo uso del concepto de funcion matemática, es decir un objeto que relaciona las coordenadas en el espacio y el tiempo *(x,y,z,t)* con valores de concentración de algún contaminante en particular *c*.

La **ecuación de transporte** es una ecuación diferencial basada en el principio de conservación de masa que describe como cambia esta función que estamos buscando en el tiempo y el espacio, y se puede deducir considerando todos los procesos que agregan ó extraen masa de un volúmen arbitrario en la atmósfera, su expresión general en una dimensión es:

  $$
  \dfrac{\partial c}{\partial t} = E - \lambda\,c - u \dfrac{\partial c}{\partial x} + K \dfrac{\partial^2 c}{\partial x^2} 
  $$

esta ecuación expresa como se modifica la concentración de un compuesto *c* en el tiempo, considerando los procesos de:
+ Emisión
+ Reacciones químicas ó *decaimiento*
+ Arrastre por el viento (*advección*)
+ Mezclado turbulento (*difusión*)

No se conoce una solución general a esta ecuación, pero si realizamos los siguientes supuestos y simplifiacaciones:
- La velocidad del viento es constante en el tiempo y espacio.
- La difusión turbulenta en el sentido de la dirección del viento es despreciable.
- El contaminante en un tiempo inicial se encuentra concentrado en un punto.

podemos llegar a una solución analítica, cuya fórmula general es:

  $$ 
  c_{(x,t)} = \dfrac{M}{\sqrt{2\pi}\sigma} \exp\bigg[ \dfrac{- (x-\mu)^2}{2\sigma^2}  \bigg] \exp\bigg[ -\lambda t \bigg] 
  $$

los modelos basados en esta solución para describir como se dispersan los contaminantes se conocen como **modelos gaussianos**, y son el objeto de estudio de este curso.

## Bibliografía
- "Air Dispersion Modeling, Foundations and Applications". De Visscher A. Wiley. 2013.

