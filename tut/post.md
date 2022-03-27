---
nav_order: 9
---

# Postprocesamiento

Herramientas para el postprocesamiento e interpretación de los datos de salida de modelos.
{: .fs-6 .fw-300 }
## Interpteración de los resultados:



## Herramientas para generar tabla de concentraciones máximas:



## Rosa de vientos:

Considerando que la dirección y la velocidad del viento son factores determinantes en la dispersión del contaminante, es conveniente analizar la información mediante una visualización de rosa de vientos para el período modelado.
Vamos a usar una herramienta [web](https://mesonet.agron.iastate.edu/sites/locate.php), pero existen varias alternativas ( [WRPLOTview-lakes](https://www.weblakes.com/software/freeware/wrplot-view/), [Openair-R](https://www.rdocumentation.org/packages/openair/versions/2.8-6/topics/windRose), [-Python](https://github.com/python-windrose/windrose)).

Vamos a entrar al sitio de la universidad de Iowa siguiendo el link: [https://mesonet.agron.iastate.edu/sites/locate.php](https://mesonet.agron.iastate.edu/sites/locate.php)

Por defecto,  se encuentra seleccionada la red de estaciones de Iowa, vamos a desplegar de **Select By Network** el menú, buscar "Argentina", luego pulsamos el botón <kbd>Switch Netork</kbd>.

![](/tut/imgs/WRose_1.png)

Al cargarse la red de "Argentina", se visualizan todas las estaciones del SMN. Buscamos en **Select by Station:** la fuente de información de superficie, que en este caso es "EZEIZA AERO" cuyo ID es "SAEZ" y tocamos <kbd>Select Station</kbd>.  
![](/tut/imgs/WRose_2.png)

En esta página se muestra información histórica de la estación y hasta se permite bajar datos en series de tiempo limitadas. Para crear la rosa de vientos vamos a la pestaña <kbd>Custom Wind Roses</kbd>.

![](/tut/imgs/WRose_3.png)


Vamos a elegir el mismo rango temporal que en el modelado (12/2021) y cambiamos las unidades a *"Meters per second (MPS)"* luego generamos la imagen tocando el botón <kbd>Enviar</kbd>.

![](/tut/imgs/WRose_4.png)

Al esperar unos segundos, la página genera la rosa de vientos solicitada. Esta visualización representa la dirección de origen y frecuencia de velocidades del viento.   

![](/tut/imgs/WRose_5.png)
<!-- 
https://mesonet.agron.iastate.edu/sites/dyn_windrose.phtml?station=SAEZ&network=AR__ASOS&bin0=2&bin1=5&bin2=7&bin3=10&bin4=15&bin5=20&units=mph&nsector=36&fmt=png&dpi=100&year1=2021&month1=12&day1=1&hour1=0&minute1=0&year2=2021&month2=12&day2=31&hour2=23&minute2=59
 -->

## AERPLOT


## Ejerecicios:



