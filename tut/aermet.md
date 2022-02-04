---
nav_order: 2
---
# Aermod (parte 1): AERMET

> Tutorial para ejecución de preprocesador meteorológico del aermod (**AERMET**)

Los pasos generales a seguir son:
1. Descargar el ejecutable ``aermet.exe``.
2. Descargar datos meteorológicos: superficiales y radiosondeos.
3. Colocar todo lo anterior en un directorio.
4. Construir archivos de control para cada etapa: 
	+ ``ETAPA1.INP``, extracción y control de calidad de datos.
	+ ``ETAPA2.INP``, fusión de datos de superficie y radiosondeos.
	+ ``ETAPA3.INP``, cálculo de parámetros de capa límite.
5. Ejecutar ``aermet.exe`` para cada una de las estapas:  ``aermet.exe < ETAPAx.INP``


## Descarga de ejecutable

Link de descarga del [AERMET](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/met/aermet/aermet_source.zip)

Se descargará un archivo con extensión ``.zip``, al descomprimirlo habrá un archivo con extensión ``.exe`` que es el ejecutable.


## Descarga de datos meteorológicos:

Para la ejecución del **AERMET** es requisito disponer de datos meteorológicos de superficie y radiosondeos. 

Para descargar datos meteorológicos tienen que buscar la estación más cercana al proyecto a modelar que cuente con buena disponibilidad de datos. Cada estación meteorológica tiene un *id* definido globalmente por la Organización Mundial de Meteorología (WMO), en este documento pueden ver los datos generales con id de las estaciones meteorológicas de la red Argentina: [estaciones_smn.csv](archivos/aermet/estaciones_smn.csv).

### Meteorología de superficie: 

Los datos de meteorología de superficie se pueden descargar del [Integrated Surface Database (ISD)](ftp://ftp.ncdc.noaa.gov/pub/data/noaa/)

También se pueden descargar desde terminal con ``WGET``:
```shell
$> wget ftp://ftp.ncdc.noaa.gov/pub/data/noaa/${year}/${id_sfc}0-99999-${year}.gz
```
donde ``${year}`` es el año de interés, y ``${id_sfc} `` es el id de la estación de superficie.

Se va a descargar un archivo con extensión ``.gz``, es un archivo comprimido, hay que descomprimirlo, y dentro habrá un archivo ``ascii`` del siguiente tipo:

```
0159875530999992021010100004-34450-058583FM-12+000399999V0203401N003119999999N007000199+02431+00891101231ADDAY101021AY201021KA1120M+02901KA2120N+02001MA1999999101201MD1310071+9999MW1041REMSYN07087553 31957 03406 10243 20089 30120 40123 53007 70400 333 10290 20200=
0101875530999992021010100004-34453-058590FM-15+000399999V0203401N003612200019N007000199+02401+00901999999ADDGF100991999999999999999999MA1101201999999REMMET048METAR SADF 010000Z 34007KT 7000 NSC 24/09 Q1012=
0117875530999992021010101004-34450-058583FM-12+000399999V0203401N003619999999N009000199+02291+01141101281ADDAY101021AY201021MA1999999101241MD1210111+9999MW1041REMSYN05487553 41959 03407 10229 20114 30124 40128 52011 70400=
0101875530999992021010101004-34453-058590FM-15+000399999V0203301N004612200019N009000199+02301+01101999999ADDGF100991999999999999999999MA1101201999999REMMET048METAR SADF 010100Z 33009KT 9000 NSC 23/11 Q1012=
... (continúa)
```

### Radiosondeos:

Los radiosondeos se descargan de [NOAA/ESRL Radiosonde Database](https://ruc.noaa.gov/raobs)


Se puede descargar desde terminal con ``CURL``:

```bash
$> curl -L "https://ruc.noaa.gov/raobs/GetRaobs.cgi?shour=0z%2C+12z+ONLY&ltype=Mandatory&wunits=Tenths+of+Meters%2FSecond&bdate=${byr}${bmon}${bday}00&edate=${eyr}${emon}${eday}23&access=WMO+Station+Identifier&view=NO&StationIDs=${id_up}&osort=Station+Series+Sort&oformat=FSL+format+%28ASCII+text%29"
```
donde ``${byr}``, ``${bmon}``, ``${bday}`` son el año, mes y dia del primer sondeo y ``${eyr}``, ``${emon}``, ``${eday}`` el año, mes y día del ultimo sondeo requerido.  ``${id_up}`` es el *id* de la estación meteorológica de interés.

Se va a descargar un archivo ``ascii`` cuyo contenido es:

```
   254     12      5      JAN    2019
      1  99999  87576  34.82S 58.53W    20   1127
      2    200   1230    741     20  99999      3
      3          SAEZ                99999     ms
      9  10120     20    244    154      5     36
      4  10000    124    232    132    360     82
      4   9250    797    182    102    360    108
      4   8500   1515    150    -50     20     62
      4   7000   3136     78    -82    245    108
      4   5000   5820    -91   -311    255    118
      4   4000   7500   -221   -431    265    185
      4   3000   9550   -363   -573    255    345
      4   2500  10800   -445   -615    270    427
      4   2000  12260   -517   -697    280    468
      4   1500  14080   -625   -785    285    422
      4   1000  16550   -671   -861    275    185
      4    700  18680   -709   -939    230    103
      4    500  20680   -631   -911    170     46
      4    300  23870   -543   -853     90     72
      4    200  26490   -481   -811     90    123
    254     12      6      JAN    2019
      1  99999  87576  34.82S 58.53W    20   1132
... (continúa)
```

### Datos sitio-especificas
En caso de disponer datos de una estación meteorológica privada también es posible incorporar los datos al modelo, solo es necesario que estén en algun formato tipo tabla, como puede ser una planilla de excell. 


## Ejecución

Lo primero que necesitamos es crear un directorio de trabajo y colocar dentro el ejecutable ``aermet.exe`` y los datos de entrada meteorológicos que aquí llamaremos ``PRUEBA.ISH`` (superficie) y ``PRUEBA.FSL`` (radiosondeo).

El **AERMET** se ejecuta en 3 etapas a las que llamaremos: **ETAPA1**, **ETAPA2** y **ETAPA3**. Cada una de estas necesita un *archivo de control* que permiten configurar la corrida, que llamaremos ``ETAPA1.INP``, ``ETAPA2.INP`` y ``ETAPA3.INP``.


### Etapa 1:  Lectura y procesamiento de datos de entrada.

En esta etapa tenemos que proveer al **AERMET** con los archivos de entrada y parámetros para extraerlos.

Vamos a tener que construir un archivo de control donde vamos a especificar las rutas a los archivos de entrada, las fechas de extracción, ubicación y parámetros de las estaciones meteorológicas entre otros.

Este archivo de control lo nombraremos: [ETAPA1.INP](archivos/aermet/ETAPA1.INP) y se divide en las siguientes secciones:

+ ``JOB ``: en esta se especifican los nombres de archivos con información de la ejecución.
+ ``SURFACE ``: se brinda la ruta al archivo de superficie, el formato, y las fechas de incio y fin de la corrida.
+ ``UPPER ``: se brinda la ruta al archivo de radiosondeo, el formato, y las fechas de incio y fin de la corrida.
+ ``ONSITE `` (opcional): se brinda la ruta al archivo de observaciones in-situ y formato.

Por ejemplo:
```
** ETAPA 1: Lectura y procesamiento de datos de entrada.
JOB
MESSAGES ETAPA1.MSG
REPORT   ETAPA1.RPT
**    Datos horarios de superficie:
SURFACE
DATA       PRUEBA.ISH ISHD
EXTRACT    EXTRACT_SFC.DSK
XDATES     2021/12/01 TO 21/12/31
LOCATION   9875530  34.450S  058.583W  3  +0003
AUDIT      WDIR WSPD CLHT RHUM
QAOUT      QA_SFC.OUT
**    Datos de sondeos verticales:
UPPERAIR
DATA       PRUEBA.FSL FSL
EXTRACT    EXTRACT_UA.DSK
XDATES     2021/12/01 TO 21/12/31
LOCATION   87576  34.82S  58.53W  3
AUDIT      UAPR  UAHT  UATT  UATD  UAWD  UAWS
QAOUT      QA_UA.OUT
```

Notar que todas las lineas que comienzan con ``**`` son interpretadas como *comentarios*, y por lo tanto el programa las ignora.

En la carpeta de trabajo (donde debe estar el ejecutable), guardamos este archivo con el nombre ``ETAPA1.INP``, y luego lo copiamos como ``aermet.inp`` y ejecutamos el AERMET.EXE haciendo doble click.

Si estamos en una terminal, solo es necesario ejecutar la siguiente linea:
```bash
$> aermet.exe < ETAPA1.INP
```

Si todo sale bien se van a crear los siguientes archivos:
+ ``ETAPA1.MSG`` y ``ETAPA1.RPT`` nos brindan información de como fue la ejecución, y en caso de haber un error ahi habrán mensajes de alerta ó error.
+ ``EXTRACT_SFC.OUT`` y ``EXTRACT_UA.OUT`` contienen los datos extraidos de los archivos meteorológicos de superficie y radiosondeos respectivamente.
+ ``QA_SFC.OUT`` y ``QA_UA.OUT`` archivos con información de variables auditadas que serviran par el siguiente paso.
+ ``Discarded_ISHD_Records.dat`` si algun registro no cumple los parametros de calidad entonces se descartan y se guardan en este archivo para su revisión.


### Etapa 2: Fusión (merge) de archivos

En esta etapa se fusionan los datos de superficie con los meteorológicos.
También necesitamos crear un archivo de control: [ETAPA2.INP](archivos/aermet/ETAPA2.INP) que tiene las siguientes secciones:
+ ``JOB ``
+ ``SURFACE ``
+ ``UPPER ``
+ ``ONSITE `` (opcional)
+ ``MERGE`` 

Por ejemplo:

```
** Stage 2: Merge de datos.
JOB
MESSAGES ETAPA2.MSG
REPORT   ETAPA2.RPT
SURFACE
QAOUT  QA_SFC.OUT
UPPERAIR
QAOUT  QA_UA.OUT
MERGE
OUTPUT PRUEBA.MRG
XDATES 2021/12/01 TO 21/12/31
```

Guardamos este archivo con el nombre ``ETAPA1.INP``, y luego lo copiamos como ``aermet.inp`` y ejecutamos el AERMET.EXE haciendo doble click ó en la terminal:


```bash
$> copy  ETAPA2.INP aermet.inp
$> AERMET.EXE
```

Se van a crear los siguientes archivos:
+ ``ETAPA2.MSG`` y ``ETAPA2.RPT`` nos brindan información de warnings y errores.
+ ``PRUEBA.MRG`` contienen los datos fusionados que serán utilizados en el siguiente paso.


### Etapa 3: Cálculo de parametros de capa límite

Este es el úlitmo paso, y es donde se relizan los cálculos que serviran como información de entrada al **AERMOD**.

Vamos a crear nuestro archivo de control: [ETAPA3.INP](./archivos/aermet/ETAPA3.INP) que tiene sólo dos secciones:
+ ``JOB``: lo mismo que en los pasos anteriores.
+ ``METPREP``: en esta secciones especificamos el archivo de salida del ETAPA2, y luego una serie de flags que hacen referencia a métodos a emplear para el cálculo de los parámetros y como utilizar la información. También se brindan archivos con información de parámetros de superficie del suelo cerca a las estaciones.

Por ejemplo:
```
** Stage 3 - Estimación de parametros de la capa límite y creación de .SFC y .PFL
JOB
MESSAGES ETAPA3.MSG
REPORT   ETAPA3.RPT
METPREP
DATA        PRUEBA.MRG
LOCATION    A212 34.450S 058.583W  3
XDATES      2021/12/01 TO 21/12/31
OUTPUT      PRUEBA.SFC
PROFILE     PRUEBA.PFL
** Métodos para precesamiento de datos:
METHOD   WIND_DIR  RANDOM
METHOD   REFLEVEL  SUBNWS
NWS_HGT  WIND      10.0
METHOD   UASELECT SUNRISE
UAWINDOW -12 12
AERSURF AERSURFACE.OUT
AERSURF2 AERSURFACE2.OUT
```

Para ejecutar esta etapa se procede igual que en las anteriores:
```shell
$> AERMET.EXE < ETAPA3.INP
```

Si todo sale bien se van a crear dos archivos necesarios para la ejecución del **AERMOD**:

- ``.SFC``: contiene los datos de superficie procesados.
- ``.PFL``: contiene los datos de perfiles vericales procesados.

