---
title: AERSURFACE
description: Tutorial de preprocesamiento de propiedades de superficie.
nav_order: 0
---


# Aermod: AERSURFACE

> Tutorial para el preprocesamiento de datos de superficie aermod (**AERSURFACE**)


El **AERSURFACE** es un preprocesador que nos permite estimar parámetros de superficie representativos para las cercanías de la estación meteorológica, usando datos de usos de suelo, canopeo e impermeabilidad del suelo.
Este programa relaciona una clasificación de cobertura del suelo (pastizal, urbano, agua), a una distancia de la estación meteorológica de superficie, para inferir los siguientes parámetos:

1. albedo &alpha;
2. proporción (ratio) de bowen $B_{0}$
3. largo de rugosidad de superficie $z_{0}$ 

Este programa necesita datos que requieren un formato de clasificación particular del servicio geológico de estados unidos ([NLCD](https://www.mrlc.gov/)) y que en consecuencia no esta disponible en nuestro país. 

Esta clasificación de cobertura del suelo el USGS define las sifuientes clases:


<!-- https://grasswiki.osgeo.org/wiki/File:NLCD_2016_Land_Cover_example.png -->
|Clase|Descrpición|
|---|---|
11|Open Water
12|Perennial Snow/Ice
21|Developed, Open Space
22|Developed, Low Intensity
23|Developed, Medium Intensity
24|Developed, High Intensity
31|Barren Land
41|Deciduous Forest
42|Evergreen Forest
43|Mixed Forest
52|Shrub/Scrub
71|Herbaceous
81|Hay/Pasture
82|Cultivated Crops
90|Woody Wetlands
95|Emergent Herbaceous Wetlands

Para determinar la clase dominante se debe analizar la siguiente información.

1. albedo &alpha;:
    - Media aritmética de región de 10 km x 10 km centrada en la esración meeorológica. 

2. proporción (ratio) de bowen $B_{0}$
   - Media *geométrica* de región de 10 km x 10 km centrada en la esración meeorológica.
 
3. largo de rugosidad de superficie $z_{0}$
   - asd

![aersurface_radio](imgs/aersurface_radio.png)

Cada seccion va a representar una cobertura distinta, con parámetros de albedo, bowen y rugosidad distintas. 

Por estos motivos estamos imposibilitados a usarlo directamente.
La alternativa de generación de esta información es a partir del procesamiento realizado por el usuario teniendo en cuenta las siguientes directivas. El objetivo es generar el archivo ``AERSURFACE.OUT`` de forma manual, ya que este es un archivo de texto con algunas especificaciones, por ejemplo este es el contenido de un ``AERSURFACE.OUT``:

```Text
 FREQ_SECT  SEASONAL  3
   SECTOR   1  0   30
   SECTOR   2  30  360
**------------------------------------------------|
**          | season | section | a0  | b0  | z0   |
**----------|--------|---------|-----|-----|------|
   SITE_CHAR    1        1      0.18  0.70  0.01
   SITE_CHAR    2        1      0.15  0.30  0.015
   SITE_CHAR    3        1      0.15  0.50  0.02
   SITE_CHAR    4        1      0.15  0.70  0.015
   SITE_CHAR    1        2      0.18  1.00  0.30
   SITE_CHAR    2        2      0.16  0.80  0.40
   SITE_CHAR    3        2      0.16  0.80  0.40
   SITE_CHAR    4        2      0.16  0.80  0.40
**----------|--------|---------|-----|-----|------|
```

Vemos que se presentan *keywords* y un formato de tabla. Recordemos que ``**`` convierte la línea en un comentario, y por lo tanto no tiene ningún efecto.

Antes de explicar que define cada *keyword* tenemos que saber que vamos a considerar un área circular de 1km de radio alrededor del la estación meteorológica y vamos a definir radialmente secciones con distintas propiedades de la superficie:



A su vez estas propiedades pueden cambiar en el tiempo: mensual, estacional ó anualmente.

La palabra clave ``FREQ_SECT`` permite definir como queremos que cambien los parámetros de superficie en el tiempo: (``ANNUAL``, ``SEASONAL`` ó ``MONTHLY``)  y el numero de sectores con superficies distintas alrededor de la estación meteorológica.

Con la keyword ``SECTOR`` se define para cada sector cual es el angulo de inicio y fin que lo define. Siempre considerando que el 0 se encuentra en el norte, y que avanza de forma antioraria.

Por último para cada sector y cada season hay que definir los valores de albedo, bowen y rugosidad usando la keyword: ``SITE_CHAR``.