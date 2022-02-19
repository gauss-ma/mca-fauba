---
nav_order: 5
---

# Aermod: AERMAP

> Tutorial para ejecución de preprocesador de terreno del **AERMOD** (**AERMAP**)

El **AERMAP** es un preprocesador del **AERMOD** que permite generar una grilla de receptores sobre un terreno complejo y calcular parámetros que permitan al **AERMOD** modelar la interacción de la pluma con el terreno.

## Resumen:

Para ejecutar el **AERMAP** necesitamos:
1. Descargar el ejecutable [aermap.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_exe.zip).
2. Definir dominio de estudio y grilla de receptores en sistema de coordenadas plano (proyectado).
3. Descargar un [modelo digital de elevación](https://www.ign.gob.ar/NuestrasActividades/Geodesia/ModeloDigitalElevaciones/Mapa) (DEM) que contenga el domino que queremos modelar.
4. Reproyectar DEM a coordenadas planas.
5. Construir un archivo de control para el aermap: [``aermap.inp``](archivos/aermod/aermap.inp)
6. Colocar todos los archivos mencionados en un directorio común.
7. Ejecutar el aermap haciendo doble click sobre el ejecutable ó si están en la terminal: `` aermap.exe < aermap.inp``.


---


## Directorio de trabajo
Al igual que en el [tutorial de AERMET](./aermet.html) vamos a asumir que estamos en el directorio de trabajo: *C:/Users/MCA_tutorial/aermod*. 


## Descarga de ejecutable:

El AERMET se encuentra en la página web de USEPA, el ejecutable es: [aermap.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_exe.zip).

Para descargarlo desde la terminal:
```shell
wget https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_exe.zip -outfile aermap_exe.zip
```

Lo descomprimimos:
```shell
tar -xvzf aermap_exe.zip
```

> :information_source: También podemos encontar el código fuente en: [aermap_source.zip](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_source.zip).


## Definición de dominio y grilla de receptores

Para este tutorial vamos a considerar una fuente puntual hipotética ubicada en la Ciudad de Buenos Aires, cuyas coordenadas son:

| Longitud, Latitud (epsg:4326)  |
|:------------------------------:|
| -58.461326, -34.577921         |

<!-- 
epsg_latlon=4326
epsg_local=32721
clat=-34.577921
clon=-58.461326
read xc yc ellipsoidh <<<$( gdaltransform -s_srs epsg:${epsg_latlon} -t_srs epsg:${epsg_local} <<< $( echo "${clon} ${clat}" ) )
-->

> :warning: Aermod no trabaja con coordenadas geográficas (lat,lon), necesita trabajar en un sistema de coordenadas plano (x,y). Usualmente utilizamos las fajas de la proyección UTM, para nuestro caso nos sirve la faja 21 sur.

Acá tenemos que considerar un aspecto muy importante. AERMOD y todos sus preprocesadores, trabajan en sistemas de coordenadas planos, y por lo tanto no podemos utilizar latitud y longitud. Es necesario ó crear un sistema de coordendas propio (por ejemplo con centro en el centro del predio ó la fuente), ó más conveniente usar un sistema de coordenadas proyectadas adecuada para el sitio.

Recomendamos este último enfoque, y es el que vamos a utilizar.  Para buenos aires un sistema apropiado puede ser el [Universal Transverse Mercator](https://es.wikipedia.org/wiki/Sistema_de_coordenadas_universal_transversal_de_Mercator) (UTM), para el hemisferio sur y la faja 21.

Si tranformamos las coordenadas de la fuente a este nuevo sistema nos queda:

| XY UTM 21S (epsg:32721)|
|:----------------------:|
|365965.26, 6172792.08     |


Cada sistema de coordenada tiene un *id* conocido como **epsg**, por ejemplo para el sistema geográfico WGS-84 el epsg es 4326. Mientras que para el que nosotros elegimos (UTM-21 Sur) es 32721.

Para pasar coordenadas de un sistema a otro podemos usa el comando ``gdaltransform`` de la herramienta ``gdal``:
```shell
gdaltransform -s_srs epsg:4326 -t_srs epsg:32721 <<< $( echo "-58.461326, -34.577921" )
365965.261111296 6172792.08081216 0
```
donde ``-t_srs`` indica el sistema de coordenadas deseado (*target spatial reference system*) y ``-s_srs`` el sistema que tenemos incialmente (*source spatial reference system*).


#### Definición de grilla de receptores.

Ahora debemos definir en que puntos del espacio queremos conocer la concentración del contaminante que queremos modelar. A estos puntos los llamamos receptores.

En nuestro ejemplo vamos a localizar los receptores de en una grilla regular cada 50 metros de distancia, y en un dominio cuadrado de 4 kilometros de lado.

Por lo tanto:
<!--
     dist=3162.0
     dx=50.0; dy=50.0
     read xini xfin yini yfin<<<$(getLimits.exe ${xc} ${yc} ${dist})
     nx=$(bc -l <<< "($xfin-$xini)/$dx")
     ny=$(bc -l <<< "($yfin-$yini)/$dy")
-->

| xc    | 365965.260 | Punto central X     |
| yc    | 6172792.08 | Punto central Y     |
| xini  | 362803.250 | Vértice sur-oeste X |
| yini  | 6169630.00 | Vértice sur-oeste Y |
| xfin  | 369127.250 | Vértice nor-este  X |
| yfin  | 6175954.00 | Vértice nor-oeste Y |

Esquema del dominio:

```
(xini,yfin)                       (xfin,yfin)
    (+)-------------------------(+)         
     |...........................|          
     |...........................| ^        
     |...........................| |        
     |............(+)............| ny       
     |..........(xc,yc)..........| |        
     |...........................| v        
     |..........<--nx-->.........|          
    (+)-------------------------(+)         
(xini,yini)                       (xfin,yini)
```



## Descarga de modelo digital de elevación:

Existen varios modelos digitales de elevación (DEM) con cobertura global, por ejemplo: *ASTER* ó *SRTM*.
Una versión ajustada a nuestro país es el modelo digital de elevación adaptado por el Instituto Geográfico Nacional (IGN), que se puede descargar entrando [aquí](https://www.ign.gob.ar/NuestrasActividades/Geodesia/ModeloDigitalElevaciones/Mapa).

Lamentablemente este servicio aún no cuenta con una API para descargar desde la terminal, asi que tendremos que hacerlo desde la página web, y luego descargarlo en nuestro directorio de trabajo.

Vamos a descargar el producto *MDE 30m*, la grilla número: *3560-18*, ya que nuestro proyecto va a estar centrado al suroeste de la Ciudad Autónoma de Buenos Aires.

El DEM que descargaremos va a estar en sistema de coordenadas geográficas (lat,lon), pero vamos a necesitar convertirlo a un sistema proyectado para trabajar. Generalmente para Argentina usamos algúna faja UTM (Universal Transverse Mercator). Por lo tanto necesitamos transformar el archivo a el nuevo sistema de coordenadas:

Una forma de hacerlo es utilizando el comando ``gdalwarp`` de la herramienta ``gdal``:

```shell
gdalwarp -tr ${dx} ${dx} -r cubicspline -t_srs epsg:${epsg_local} -te ${xini2} ${yini2} ${xfin2} ${yfin2} ${IGN-MDE} PRUEBA.tif
```

donde ``${dx}`` y ``${dy}`` es al resolución espacial del nuevo DEM (vamos a ponerlo en 50m). ``${epsg_local}`` es el código de la proyección que necesitamos, en nuestro caso va a ser UTM sur, faja 21, y por lo tanto: ``${epsg_local}`` es 32721.  ``${xini2} ${yini2} ${xfin2} ${yfin2}`` son las coordenadas de los vertices del domino de interes (en coordenadas proyectadas). Por ultimo ``${IGN_MDE}`` es el nombre del archivo descargado de la web del IGN. Finalmente para nuestro caso:

```shell
gdalwarp -tr 50 50 -r cubicspline -t_srs epsg:32721 -te ${xini2} ${yini2} ${xfin2} ${yfin2} ${IGN-MDE} PRUEBA.tif
```

## Archivo de control ``aermap.inp``

Tenemos que construir un archivo de control [``aermap.inp``](archivos/aermap/aermap.inp) para configurar la corrida de ``aermap.exe``, este es un archivo de texto, con las siguientes secciones:

+ CO: Sección de **CO**ntrol de corrida.
+ RE: Sección de **RE**ceptores.
+ OU: Sección de configuraciónde salidas (**OU**tputs).

Cada sección tiene un indicador de comienzo y final, por ejemplo **CO**:

```
CO STARTING
**       (  Definición de parámetros ... )
CO FINISHED
```

#### **CO**

En la sección de **CO** hay que definir varios parámetros:

```Text
CO STARTING
   TITLEONE  GRILLA DE RECEPTORES: PRUEBA
   TERRHGTS  EXTRACT
   DATATYPE  NED
   DATAFILE  PRUEBA.tif
   DOMAINXY  339249.72 6166414.50 -21 363249.72 6190414.50 -21
   ANCHORXY  351249.728540755 6178414.49722093 351249.728540755 6178414.49722093 -21 3
   FLAGPOLE  1.5
   RUNORNOT  RUN
CO FINISHED
```

los más relevantes son:
+ ``DATATYPE``: el tipo de archivo de entrada, por razones históricas debemos elegir ``NED``.
+ ``DATAFILE``: indica el nombre del DEM a procesar.
+ ``DOMAINXY``: indica el dominio a modelar y la faja UTM a usar (xmin ymin utmzn xmax ymax utmzn).
+ ``ANCHORXY``: se requiere para relacionar el sistema de coordenadas de de nuestra grilla con la UTM elegida.
+ ``FLAGPOLE``: define la altura sobre el nivel del piso, en metros, donde ubicará a los receptores (default: 1.5)

#### **RE**
En la sección de receptores **RE** hay que definir una grilla de receptores, lo podemos hacer con las keywords: 
+ ``GRIDCART``: define una grilla regular en coordenadas cartesianas.
+ ``GRIDPOLR``: define una grilla de circulos concentricos en coordenadas polares.

```Text
RE STARTING
RE GRIDCART GRILLA1 STA
                    XYINC -5000. 11 1000. -5000. 11 1000.
RE GRIDCART GRILLA1 END
RE FINISHED
```

Tambien existe la posiblidad de brinarle a ``aermap.exe`` una grilla propia customizada, solo necesitamos un archivo de texto con las coordendas x e y, y lo incluimos en nuestro archivo de control como:

```Text
RE STARTING
RE INCLUDED PRUEBA.REC
RE FINISHED
```

#### **OU**

Para la sección **OU** solo es necesario indicar el nombre del archivo de salida usando la keyword ``RECEPTOR``:

```Text
OU STARTING
   RECEPTOR  PRUEBA.ROU
OU FINISHED
```
en este caso el archivo de receptores lo nombramos ``PRUEBA.ROU`` (la extensión ``.ROU`` es una convención).


## Ejecución:

Para ejecutar el aermap, ponemos el ejecutable ``aermap.exe``, el DEM ``PRUEBA.tif`` y el archivo de control en un mismo directorio, y hacemos ejecutamos el programa haciendo doble click, ó si estamos en una terminal:

```shell
aermap.exe < aermap.inp
```

Se va a crear un archivo ``PRUEBA.ROU`` donde está definida la grilla de receptores y que será necesario para ejecutar el **AERMOD**.

