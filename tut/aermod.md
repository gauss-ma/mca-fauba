---
nav_order: 5
---
# Aermod (parte 3): AERMOD

> Tutorial para uso de **AERMOD**

Para ejecutar el **AERMOD** se deben seguir los siguientes pasos:
1. Descargar ejecutable [``aermod.exe``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_exe.zip).
2. Ejecutar **AERMET** para obtener archivos meteorológicos: [``PRUEBA.SFC``](archivos/aermod/PRUEBA.SFC) y [``PRUEBA.FSL``](archivos/aermod/PRUEBA.PFL).
3. Ejecutar **AERMAP** para obtener el archivo de receptores: [``PRUEBA.ROU``](archivos/aermod/PRUEBA.ROU).
4. Construir archivo de control: [``aermod.inp``](archivos/aermod/aermod.inp)
5. Colocar todos los archivos mencionados en un directorio de trabajo común.
6. Ejecutar **AERMOD**: ``aermod.exe < aermod.inp ``

## Descarga
Link de descarga de ejecutable: [``aermod.exe``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_exe.zip), también es posible descargar el código fuente: [aeremod_source.zip](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_source.zip).

## Preparación de datos de entrada

Para poder ejecutar el **AERMOD** es necesario contar con:

+ Archivos meteorológicos: ``*.SFC`` y ``*.FSL`` generados por el **AERMET**.
+ Información de Receptores: ``*.ROU`` generado por **AERMAP**.
+ Información de Emisiones: Depende del tipo de fuente emisora, pero generalmente es caudal másico emitido [g/s], temperatura  del efluente, velocidad de salida, coordenadas y altura del emisor.
+ Información de Edificios: Si hubiera edificios que influencien el flujo en las vecindades del emisor también es necesario conocer las coordenadas de sus vértices y altura promedio.


### Escritura de archivo de control ``aermod.inp``.

**AERMOD** al ser ejecutado busca un archivo de control con nombre ``aermod.inp``. En este se especifica la ubicacion de los archivos de entrada, opciones y configuración de la corrida.

El ``aermod.inp`` se estructura en las siguientes secciones:
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

Cada especificación sigue la siguiente estructura general:

```
KEYWORD <arg1> <arg2> ... <argN>
```

Revisar la lista de KEYWORDS en: [Keywords](refs/KEYWORDSaermod.md), en esta tutorial solo se describen los más importantes.


#### **CO**

En esta sección se definen opciones generales para la corrida.

```
CO STARTING
   TITLEONE  PRUEBA
   MODELOPT  CONC  DEFAULT
   AVERTIME  MONTH 
   POLLUTID  ETHYLMERCAPTANO
   RUNORNOT  RUN
   EVENTFIL  OUTPUT.LOG
   ERRORFIL  ERRORS.LOG
CO FINISHED 
```
Los parámetros más importantes son:
+ ``MODELOPT`` define las opciones generales de la corrida, tiene muchos argumentos posibles. Los más importantes son DEFAULT que indica que se usan opciones regulatorias, y CONC que indica que se calcularán concentraciones. Para correr sin topografía se puede usar el argumento FLAT, caso contrario ELEV será utilizado que indica que si se considerará la topofrafía.
+ ``AVERTIME``: es el periodo de promediado de las concentraciones se expresa en horas, opciones válidas son: 1,2,3,4,6,8,12 ó 24. También son argumentos válidos: MONTH y ANNUAL.
+ ``POLLUTID``: es simplemente el nombre del contaminante, puede ser cualquiera, y no tiene mayor consecuencia salvo que se defina: como **NO2** ó **PM25**, en tal caso **AERMOD** interpreta que se debe a dichos contaminantes y reajusta algunos parámetros y rutinas para tratarlos.


#### **SO**

En esta sección se enumeran las fuentes emisoras y sus parámetros de emisión.

```
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


#### **RE**

Si se ejecutó el **AERMAP** esta paso es muy sencillo, simplemente hay que linkear al archivo de salida ``*.ROU`` con la keyword: ``INCLUDED`` que toma como argumento el nombre del archivo de salida del aermap.

```
RE STARTING
   INCLUDED  PRUEBA.ROU
RE FINISHED 
```

Esta sección tambien tiene keywords para crear una grilla de receptores en caso de no haber utilizado el **AERMAP**.


#### **ME**

En esta sección se indica la ubicación de los archivos meteorológicos de superficie y radiosondeos (con las keywords: ``SURFFILE`` y ``PROFFILE`` respectivamente), y luego algunos parámetros que no son de mayor relevancia:

```
ME STARTING  
   SURFFILE  PRUEBA.SFC
   PROFFILE  PRUEBA.PFL
   SURFDATA  9875530 2021 A212
   UAIRDATA  87576 2021 SAEZ
   PROFBASE  0.0  METERS
ME FINISHED  
```

la keyword ``PROFBASE`` indica cual es la altura de base para definir el perfil de temperatura potencial y es obligatorio.


#### **OU**
Esta sección incluye todas las opciones de escritura de los datos de salida.

```
OU STARTING  
   RECTABLE  ALLAVE  FIRST-THIRD
   MAXTABLE  ALLAVE  50
   SUMMFILE  AERTEST_PRUEBA_ETHYLMERCAPTANO_MONTH.SUM
   PLOTFILE  MONTH  ALL  FIRST  AERPLOT_PRUEBA_ETHYLMERCAPTANO_MONTH.OUT
OU FINISHED
```

+ ``MAXTABLE`` sirve para definir la tabla de máximos valores totales encontrados.
+ ``RECTABLE`` sirve para definir la tabla de máximos valores por receptor.
+ ``SUMMFILE`` define el nombre del archivo de salida que posee además de informamción sobre la corrida y fechas procesadas, la tabla con las máximas concentraciones encontradas.
+ ``PLOTFILE`` sirven para definir el nombre del archivo de salida con la tabla de máximos valores encontrados por receptor (sirve para hacer los mapas de concentraciones máximas), requiere la definición del periodo temporal y el grupo de emisore a considerar, también da la posibilidad de  mostrar los máximos totales (FIRST) ó descartarlos y usar los segundos (SECOND) , terceros (THIRD), etc.



## Ejecución

Para ejecutar el **AERMOD** se coloca en una misma carpeta al ejecutable (``aermod.exe``), el archivo de control (``aermod.inp``) y todos los archivos de entrada especificados en ``aermod.inp`` (``PRUEBA.SFC``, ``PRUEBA.FSL``, ``PRUEBA.ROU``, etc.). Luego se ejecuta con *doble click* en el ejecutable, ó si estamos en la terminal:

```shell
$> aermod.exe
```



