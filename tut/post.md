---
nav_order: 9
---

# Postprocesamiento

Herramientas para el postprocesamiento e interpretación de los datos de salida de modelos.
{: .fs-6 .fw-300 }

## Tabla de concentraciones máximas:
Aermod genera reportes y controles de calidad donde se puede analizar y validar la mayoría de la información, sin embargo es conveniente extraer los resultados a otros medios para poder visualizar, reportar y analizar la información.
El archivo de salida generado en la opción ``PLOTFILE``, que en el caso del tutorial denominamos: "AERPLOT_PRUEBA_NOX_MONTH.OUT", tiene los resultados de concentraciones máximas de cada receptor en un formato de tabla que será fácil de exportar.


```
* AERMOD (21112 ):  PRUEBA                                                                  03/13/22
* AERMET ( 21112):                                                                          16:00:50
* MODELING OPTIONS USED:   NonDFAULT  CONC  FLAT  FLGPOL  RURAL
*         PLOT FILE OF  HIGH   1ST HIGH MONTH VALUES FOR SOURCE GROUP: ALL     
*         FOR A TOTAL OF 10000 RECEPTORS.
*         FORMAT: (3(1X,F13.5),3(1X,F8.2),3X,A5,2X,A8,2X,A5,5X,A8,2X,I8)                                                                                                                                                  
*        X             Y      AVERAGE CONC    ZELEV    ZHILL    ZFLAG    AVE     GRP       RANK     NET ID   DATE(CONC)
* ____________  ____________  ____________   ______   ______   ______  ______  ________  ________  ________  ________
  359333.28100 6137044.02000       0.05279     0.00     0.00     1.50   MONTH  ALL         1ST     CAR1      21123124
  359383.28100 6137044.02000       0.05247     0.00     0.00     1.50   MONTH  ALL         1ST     CAR1      21123124
  359433.28100 6137044.02000       0.05216     0.00     0.00     1.50   MONTH  ALL         1ST     CAR1      21123124
  359483.28100 6137044.02000       0.05185     0.00     0.00     1.50   MONTH  ALL         1ST     CAR1      21123124

```
En esta tabla, las primeras 8 filas corresponden al contexto de la tabla y sus encabezados. Vamos a seleccionar todas las filas desde la 9, nos paramos con el cursor en la primera columna de la fila 9 y presionamos <kbd>Ctrl</kbd>+<kbd>shift</kbd>+<kbd>Fin</kbd>. Copiamos el contenido y abrimos una aplicación de hoja de cálculos como Excel.
En una hoja nueva, pegamos el contenido en la celda **A1**.

![](/tut/imgs/Excel_1.png)

Vemos que se generan líneas de texto que necesitamos se parar en campos.
Dependiendo de la configuración regional la coma o el punto pueden ser separadores de miles o decimales, si el separador de decimales es la coma, debemos reemplazar los puntos por coma. Abrimos el menú de buscar y reemplazar con <kbd>Ctrl</kbd>+<kbd>b</kbd>, vamos a buscar el caracter ".", reemplazarlo por "," y <kbd>Reemplazar todos</kbd>.

![](/tut/imgs/Excel_2.png)

Seleccionamos toda la columna **A** clickeando sobre ella y vamos a la pestaña de **Datos** y buscamos la herramienta texto en columnas. 

![](/tut/imgs/Excel_3.png)

Aseguramos que este seleccionada la opción "ancho fijo" y clickeamos <kbd>Finalizar</kbd>.

![](/tut/imgs/Excel_4.png)

Ya tenemos la información en tabla para ser procesada, pero es conveniente contar con una fila adicional de encabezado. Vamos a insertar una fila en "1", clickeando con el boton derecho y seleccionando "Insertar".
A esta nueva fila 1 le colocaremos los encabezados del plotfile que tiene la fila 7. En esta instancia ya tenemos lista la tabla de resultados para procesar.

![](/tut/imgs/Excel_5.png)

La principal utilidad de la tabla sería permitir:
 
 - Graficar ubicación de concentraciones máximas.
 - Encontrar máximos, compararlos con estándares y reportar ubicación y fecha de ocurrencia.
-  Analizar frecuencia y distribución de concentraciones máximas.

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

## AERPLOT


## Ejerecicios:



