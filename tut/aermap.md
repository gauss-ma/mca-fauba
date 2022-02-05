---
nav_order:3
---

# Aermod (parte 2): AERMAP

> Tutorial para ejecución de preprocesador de terreno del **AERMOD** (**AERMAP**)

El **AERMAP** es un preprocesador del **AERMOD** que permite generar una grilla de receptores sobre un terreno complejo y calcular parámetros que permitan al **AERMOD** modelar la interacción de la pluma con el terreno.


Para ejecutar el **AERMAP** necesitamos:
1. Descargar el ejecutable ``aermap.exe``.
2. Descargar un modelo digital de elevación que contenga el domino que queremos modelar.
3. Construir un archivo de control para el aermap ``aermap.inp``
4. Ejecutar el aermap: `` aermap.exe < aermap.inp``.

## Descarga de ejecutable:

El link para descargar el ejecutable es: [aermap.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_exe.zip), también podemos encontar el código fuente en: [aermap_source.zip](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aermap/aermap_source.zip).

## Descarga de modelo digital de elevación:

Existen varios productos digitales de elevación con cobertura global, por ejemplo ASTER ó SRTM.
Una versión ajustada a nuestro país es el modelo digital de elevación adaptado por el Instituto Geográfico Nacional (IGN), que se puede descargar entrando [aquí](https://www.ign.gob.ar/NuestrasActividades/Geodesia/ModeloDigitalElevaciones/Mapa).

Este DEM va a estar en sistema de coordenadas geográficas (lat,lon), pero vamos a necesitar convertirlo a un sistema proyectado para trabajar. Generalmente para Argentina usamos algúna faja UTM (Universal Transverse Mercator). Por lo tanto necesitamos transformar el archivo a el nuevo sistema de coordenadas:

Una forma de hacerlo es utilizando ``gdal``:

```shell
$>  gdalwarp -tr ${dx} ${dx} -r cubicspline -t_srs epsg:${epsg_local} -te ${xini2} ${yini2} ${xfin2} ${yfin2} ${inp_dem} ${dem_file}
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
$> aermap.exe < aermap.inp
```

Se va a crear un archivo ``PRUEBA.ROU`` donde está definida la grilla de receptores y que será necesario para ejecutar el **AERMOD**.
