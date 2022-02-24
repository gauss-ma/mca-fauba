---
nav_order: 8
---
# Aermod: AERMOD

> Tutorial para uso de **AERMOD**

## Resumen

Para ejecutar el **AERMOD** se deben seguir los siguientes pasos:
1. Descargar ejecutable [``aermod_exe.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_exe.zip), descomprimir y colocar el ejecutable ``aermod.exe`` en el directorio de trabajo.
2. Ejecutar **AERMET** para obtener archivos meteorológicos: [``PRUEBA.SFC``](./archivos/aermod/PRUEBA.SFC) y [``PRUEBA.FSL``](./archivos/aermod/PRUEBA.PFL).
3. Obtener parámetros de emisión de las fuentes a considerar.
3. Obtener parámetros para grilla de receptores.
4. Construir archivo de control: [``aermod.inp``](archivos/aermod/aermod.inp)
5. Colocar todos los archivos mencionados en un directorio de trabajo común.
6. Ejecutar **AERMOD** haciendo doble click sobre ``aermod.exe``

---


## Descarga
El aermod se puede descargar de la web de la USEPA: [``aermod_exe.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_exe.zip), es necesario descomprimirlo y luego colocar el ejcutable ``aermod.exe`` en el directorio de trabajo.

> :information_source: También es posible descargar el código fuente: [aeremod_source.zip](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_source.zip).

## Preparación de datos de entrada

Para poder ejecutar el **AERMOD** es necesario contar con:

+ **Archivos meteorológicos.** ``PRUEBA.SFC`` y ``PRUEBA.FSL`` generados por el **AERMET**.
+ **Información de Receptores.**
  - Punto central del predio donde se encuentran las fuentes (``xc`` ``yc``).
  - Dominio de modelado (limites: ``xmin`` ``xmax`` ``ymin`` ``ymax``).
  - Espacio entre receptores ``dx`` (generalmente usamos 50 metros).
  - En caso de querer considerar receptores críticos, sus coordenadas.
+ **Información de Emisiones.** depende del tipo de fuente emisora, para una fuente puntual es:
  - coordenadas, altura y diámetro del emisor.
  - caudal másico emitido [g/s]
  - temperatura  del efluente [ºK]
  - velocidad de salida [m/s]
+ **Información de Edificios.** Si hubiera edificios que influencien el flujo en las vecindades del emisor también es necesario conocer las coordenadas de sus vértices y altura promedio.


### Escritura de archivo de control ``aermod.inp``.

**AERMOD** al ser ejecutado busca un archivo de control con nombre ``aermod.inp``. En este se especifica la ubicacion de los archivos de entrada, opciones y configuración de la corrida.
Un ejemplo de archivo de control ``aermod.inp``:

```Text
** CONTROL
CO STARTING
   TITLEONE  PRUEBA
   MODELOPT  CONC  DEFAULT
   AVERTIME  MONTH 
   POLLUTID  NO2
   RUNORNOT  RUN
   EVENTFIL  OUTPUT.LOG
   ERRORFIL  ERRORS.LOG
   FLAGPOLE  1.5
CO FINISHED 
   
** EMISORES / FUENTES
SO STARTING
   ELEVUNIT  METERS
   LOCATION  FUENTE1 POINT 350930 6177751 30.00
   SRCPARAM  FUENTE1 4.62E-04 0  11
   SRCGROUP  ALL 
SO FINISHED

** GRILLA DE RECEPTORES
RE STARTING
   INCLUDED  PRUEBA.ROU
RE FINISHED 

** METEOROLOGIA
ME STARTING
   SURFFILE  PRUEBA.SFC
   PROFFILE  PRUEBA.PFL
   SURFDATA  87553 2021 SAEZ
   UAIRDATA  87576 2021 SAEZ
   PROFBASE  0.0  METERS
ME FINISHED

** OUTPUT OPTIONS
OU STARTING
   RECTABLE  ALLAVE  FIRST-THIRD
   MAXTABLE  ALLAVE  50
   SUMMFILE  AERTEST_PRUEBA_NO2_MONTH.SUM
   PLOTFILE  MONTH  ALL  FIRST  AERPLOT_PRUEBA_NO2_MONTH.OUT
OU FINISHED
```

Este archivo se estructura en las siguientes secciones:
+ **CO**: especificaciones generales de ejecución.
+ **SO**: especificaciones de fuentes (**SO**urces).
+ **RE**: especificaciones de **RE**ceptores.
+ **ME**: especificaciones de información **ME**teorologica.
+ **EV**: especificaciones de procesamiento de **EV**entos (opcional).
+ **OU**: especifiaciones generales de archivos de salida (**OU**tput).

hay que especificar siempre el inicio y finalización de cada seccion, por ejemplo:

```
CO STARTING
**      ....
**	(especificaciones de seccion de COntrol)
**      ....
CO FINISHED
```

Cada especificación sigue la siguiente notación:

```
KEYWORD <arg1> <arg2> ... <argN>
```

donde ``KEYWORD`` son palabras reservadas para definir parámetros de ejecución, y ``arg1``, ``arg2``, ... son "argumentos" ó los valores que toma la keyword. Por ejemplo:
```Text
TITLEONE PRUEBA
```
la keyword es ``TITLEONE`` que sirve para especificar el nombre del proyecto. y ``PRUEBA`` es el valor que toma, en este caso entonces el titulo del proyecto será *PRUEBA*.

Revisar la lista de KEYWORDS en: [Keywords](refs/KEYWORDSaermod.md), en este tutorial solo se describen algunos de los más importantes.


#### **CO**

En esta sección se definen opciones generales para la corrida.

```Text
CO STARTING
   TITLEONE  PRUEBA
   MODELOPT  CONC  DEFAULT
   AVERTIME  MONTH 
   POLLUTID  NO2
   RUNORNOT  RUN
   EVENTFIL  OUTPUT.LOG
   ERRORFIL  ERRORS.LOG
CO FINISHED 
```
Los parámetros más importantes son:
+ ``MODELOPT`` define las opciones generales de la corrida, tiene muchos argumentos posibles. Los más importantes son DEFAULT que indica que se usan opciones regulatorias, y CONC que indica que se calcularán concentraciones. Para correr sin topografía se puede usar el argumento FLAT, caso contrario ELEV será utilizado que indica que si se considerará la topofrafía.
+ ``AVERTIME``: es el periodo de promediado de las concentraciones se expresa en horas, opciones válidas son: 1,2,3,4,6,8,12 ó 24. También son argumentos válidos: MONTH y ANNUAL.
+ ``POLLUTID``: es simplemente el nombre del contaminante, puede ser cualquiera, y no tiene mayor consecuencia salvo que se defina: como **NO2** ó **PM25**, en tal caso **AERMOD** interpreta que se debe a dichos contaminantes y reajusta algunos parámetros y rutinas para tratarlos.


#### EMISORES: **SO**

En esta sección se enumeran las fuentes emisoras y sus parámetros de emisión.

```Text
SO STARTING
   ELEVUNIT  METERS
   LOCATION  PUNTO1 POINT 350922 6177681 33.00
   SRCPARAM  PUNTO1 1.82E-03 4.0 380.0 10.1 0.7
   LOCATION  MIAREA2 AREAPOLY 350930 6177751 30.00
   SRCPARAM  MIAREA2 4.62E-04 0  11
   AREAVERT  MIAREA2 350930 6177751 350890 6177737 350785 6177775 350756 6177792 350765 6177827 350791 6177824 350797 6177914 350922 6177888 350959 6177847 350930 6177751 350930 6177751
   SRCGROUP  ALL 
SO FINISHED
```

la keyword ``LOCATION`` define una fuente, su tipo, su id (nombre) y su ubicación:
```
   LOCATION  <nombre>  <tipo>  <x> <y> <z>
```
los tipos de fuente más comunes son: ``POINT``, ``LINE`` y ``AERAPOLY``.

la keyword ``SRCPARAM`` define los parámetros de emisión para cada fuente y sus argumentos dependen del tipo de fuente definida en ``LOCATION``, para un POINT sería:

```
   SRCPARAM <nombre> <Q> <H> <T> <U> <D>
```
donde, Q: caudal emitido [g/s], H:altura del conducto [m], T: Temperatura de salida [ºK], U: velocidad de salida [m/s] y D: diámetro del conducto [m].


> :warning: **Es importante destacar que las coordenadas de emisores (y también receptores) deben ser coordenadas planas cartesianas, ya que el aermod no puede hacer los cálculos con coordenadas de latitud y longitud.**


#### RECEPTORES **RE**


La forma más sencilla de definir un receptor es utilizando la keyword ``DISCCART``:

```Text
RE STARTING
   DISCCART 339250.72 6166414.50
   DISCCART 339300.72 6166414.50
   DISCCART 339400.72 6166414.50
(...continúa...)
RE FINISHED
```
 
``DISCCART`` toma como argumentos la posción *x* e *y* (en metros) del receptor a considerar. También acepta como arumentos opcionales, la altura del terreno en esa ubicación, y otros parámetros necesarios para contemplar la influencia de la topografía sobre la pluma.

Comunmente nos encontramos en el caso de tener que definir muchos receptores, en forma de grillas regulares, ó concéntricas, que usando ``DISCCART`` involucraría muchas lineas para especificar. Para simplificar el trabajo exsten keywords que nos permiten definir grillas regulares de forma sencilla:
+ ``GRIDCART``: define una grilla regular en coordenadas cartesianas.
+ ``GRIDPOLR``: define una grilla de circulos concentricos en coordenadas polares.



Por ejemplo para usar ``GRIDCART``:

```Text
RE STARTING
   GRIDCART  CAR1 STA
                  XYINC ${xmin} ${nx} ${dx} ${ymin} ${ny} ${dy}
   GRIDCART  CAR1 END
RE STARTING
```

``XYINC`` toma como argumentos:
- coordenada X del vértice sur-oeste del dominio: ``xmin``
- el numero de receptores en la dimensión X: ``nx``
- el *paso* ó incremento en la dimensión X: ``dx`` (generalmente 50 metros)
- coordenada Y del vértice sur-oeste del dominio :``ymin``
- el numero de receptores en la dimensión Y: ``ny``
- el *paso* ó incremento en la dimensión Y: ``dy`` (generalmente 50 metros)


En nuestro caso tenemos que definir una grilla con separación de 50 metros. En un dominio cuadrado de XXXxXXX metros. Por lo tanto vamos tendríamos que usar:

```Text
RE STARTING
   GRIDCART  CAR1 STA
                  XYINC 348342.21 100 50.0 6413521.12 100 50.0
   GRIDCART  CAR1 END
RE STARTING
```


#### METEOROLOGÍA **ME**

En esta sección se indica la ubicación de los archivos meteorológicos de superficie y radiosondeos (con las keywords: ``SURFFILE`` y ``PROFFILE`` respectivamente), y luego algunos parámetros que no son de mayor relevancia:

```Text
ME STARTING  
   SURFFILE  PRUEBA.SFC
   PROFFILE  PRUEBA.PFL
   SURFDATA  9875530 2021 A212
   UAIRDATA  87576 2021 SAEZ
   PROFBASE  0.0  METERS
ME FINISHED  
```

la keyword ``PROFBASE`` indica cual es la altura de base para definir el perfil de temperatura potencial y es obligatorio.


#### OPCIONES DE SALIDA **OU**
Esta sección incluye todas las opciones de escritura de los datos de salida.

```Text
OU STARTING  
   RECTABLE  ALLAVE  FIRST-THIRD
   MAXTABLE  ALLAVE  50
   SUMMFILE  AERTEST_PRUEBA_NO2_MONTH.SUM
   PLOTFILE  MONTH  ALL  FIRST  AERPLOT_PRUEBA_NO2_MONTH.OUT
OU FINISHED
```

+ ``MAXTABLE`` sirve para definir la tabla de máximos valores totales encontrados.
+ ``RECTABLE`` sirve para definir la tabla de máximos valores por receptor.
+ ``SUMMFILE`` define el nombre del archivo de salida que posee además de informamción sobre la corrida y fechas procesadas, la tabla con las máximas concentraciones encontradas.
+ ``PLOTFILE`` sirven para definir el nombre del archivo de salida con la tabla de máximos valores encontrados por receptor (sirve para hacer los mapas de concentraciones máximas), requiere la definición del periodo temporal y el grupo de emisore a considerar, también da la posibilidad de  mostrar los máximos totales (FIRST) ó descartarlos y usar los segundos (SECOND) , terceros (THIRD), etc.


## Ejecución

Para ejecutar el **AERMOD** se colocan los siguientes archivos en el directorio de trabajo:
- Ejecutable: ``aermod.exe``
- Archivo de control ``aermod.inp``
- Archivos meteorológicos: ``PRUEBA.SFC``, ``PRUEBA.FSL``

Luego se ejecuta con *doble click* en el ejecutable.


Si todo sale bien, se van a crear los archivos especificados con las keywords ``SUMFILE`` y ``PLOTFILE`` de la sección **OUT**, en nuestro caso:
+ AERTEST_PRUEBA_NO2_MONTH.SUM
+ AERPLOT_PRUEBA_NO2_MONTH.SUM

El primero contiene las tablas con los máximas concentraciones encontradas para todos los receptores para el periodo modelado.
El segundo tiene una tabla con la máxima concentración encontrada para cada receptor.

