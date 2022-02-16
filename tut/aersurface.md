---
nav_order: 1
---

# Aermod (parte 1): AERSURFACE

> Tutorial para ejecución de preprocesador de superficie del **AERMOD** (**AERSURFACE**)

El **AERSURFACE** es una herramienta que permite procesar datos de cobertura del suelo para generar los parámetros de superficie requeridos por **AERMET** (el preprocesador meteorológico del AERMET).

Los parámetros que determina el *AERSURFACE* son:
- Albedo (a0)
- Relación de Bowen (b0) 
- Rugosidad (z0) 

y los estima para cada dirección del viento y cada estación del año.


## Resumen
Para ejecutar el **AERSURFACE** necesitamos:
0. Crear *directorio de trabajo* donde colocaremos todos los archivos y ejecutables.
1. Descargar el ejecutable [aersurface.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aersurface/aersurface_exe-64.zip).
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

---

## Descarga de ejecutable:

El AERSURFACE se encuentra en la página web de USEPA, el ejecutable es: [aersurface.exe](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aersurface/aersurface_exe-64.zip).

Para descargarlo desde la terminal:
```shell
wget https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aersurface/aersurface_exe-64.zip).
```

Lo descomprimimos:
```shell
tar -xvzf aersurface_exe-64.zip
```

> :information_source: También podemos encontar el código fuente en: [aersurface_source.zip](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/related/aersurface/aersurface_source.zip).


## Descarga de mapa de usos de la tierra:

Lamentablemente nuestro pais no cuenta con un mapa de buena resolución de cobertura de suelos. 

Algunas opciones que tenemos son mapas globales:
+ MODIS/Terra+Aqua Land Cover Type CMG Yearly L3 Global 0.05 Deg.
+ Copernicus (Sentinel-2)

        ##LANDUSE: (copernicus)
        #wget https://s3-eu-west-1.amazonaws.com/vito.landcover.global/v3.0.1/2019/W060S20/W060S20_PROBAV_LC100_global_v3.0.1_2019-nrt_Discrete-Classification-map_EPSG-4326.tif
        #wget https://s3-eu-west-1.amazonaws.com/vito.landcover.global/v3.0.1/2019/W060S20/W080S20_PROBAV_LC100_global_v3.0.1_2019-nrt_Discrete-Classification-map_EPSG-4326.tif


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

