---
nav_order: 4
---

# Aermod: AERMAP

> Tutorial para ejecución de preprocesador de terreno del **AERMOD** (**AERMAP**)

El **AERMAP** es un preprocesador del **AERMOD** que permite generar una grilla de receptores sobre un terreno complejo y calcular parámetros que permitan al **AERMOD** modelar la interacción de la pluma con el terreno.


Para ejecutar el **AERMAP** necesitamos:
1. Descargar el ejecutable [aermap.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_exe.zip).
2. Definir dominio de estudio, grilla de receptores en sistema de coordenadas *local*.
3. Descargar un [modelo digital de elevación](https://www.ign.gob.ar/NuestrasActividades/Geodesia/ModeloDigitalElevaciones/Mapa) (DEM) que contenga el domino que queremos modelar.
4. Reproyectar DEM a coordenadas planas.
5. Construir un archivo de control para el aermap: [``aermap.inp``](archivos/aermod/aermap.inp)
6. Colocar todos los archivos mencionados en un directorio común.
7. Ejecutar el aermap haciendo doble click sobre el ejecutable ó si están en la terminal: `` aermap.exe < aermap.inp``.

## Directorio de trabajo
Al igual que en el [tutorial de AERMET](aermet.md) vamos a asumir que estamos en el directorio de trabajo: *C:/Users/MCA_tutorial/aermod*. En caso de no estar en ese directorio se pude ir ejecutando:

```shell
cd C:/Users/MCA_tutorial/aermod
```

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

Para este tutorial vamos a considerar una fuente hipotética ubicada en la Ciudad de Buenos Aires.
<!-- 
epsg_latlon=4326
epsg_local=32721
clat=-34.577921
clon=-58.461326
read xc yc ellipsoidh <<<$( gdaltransform -s_srs epsg:${epsg_latlon} -t_srs epsg:${epsg_local} <<< $( echo "${clon} ${clat}" ) )
-->

| Longitud, Latitud (epsg:4326)  | XY UTM 21S (epsg:32721)|
|-----------------------|----------------------|
| -58.461326, -34.577921 | 365965.3, 6172792.0 |

> :warning: Aermod no trabaja con coordenadas geográficas (lat,lon), necesita trabajar en un sistema de coordenadas plano (x,y). Usualmente utilizamos las fajas de la proyección UTM, para nuestro caso nos sirve la faja 21 sur.

La grilla de receptores la vamos a hacer cada 50 metros, y en un dominio cuadrado de 4 kilometros de lado.

Por lo tanto:
<!--
     dist=3162.0
     dx=50.0; dy=50.0
     read xini xfin yini yfin<<<$(getLimits.exe ${xc} ${yc} ${dist})
     nx=$(bc -l <<< "($xfin-$xini)/$dx")
     ny=$(bc -l <<< "($yfin-$yini)/$dy")
-->

| xc    | 365965.3   |
| yc    | 6172792.0  |
| xc    | 362803.250 |
| xini  | 362803.250 |
| xfin  | 369127.250 |
| yini  | 6169630.00 |
| yfin  | 6175954.00 |


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

Una forma de hacerlo es utilizando ``gdal``:

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

```
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

```
RE STARTING
RE GRIDCART GRILLA1 STA
                    XYINC -5000. 11 1000. -5000. 11 1000.
RE GRIDCART GRILLA1 END
RE FINISHED
```


Tambien existe la posiblidad de brinarle a ``aermap.exe`` una grilla propia customizada, solo necesitamos un archivo de texto con las coordendas x e y, y lo incluimos en nuestro archivo de control como:

```
RE STARTING
RE INCLUDED PRUEBA.REC
RE FINISHED
```

#### **OU**

Para la sección **OU** solo es necesario indicar el nombre del archivo de salida usando la keyword ``RECEPTOR``:

```
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

