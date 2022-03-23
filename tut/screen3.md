---
nav_order: 2
---

# Screen3

Tutorial para uso de **SCREEN3**
{: .fs-6 .fw-300 }

<!-- ## Resumen
En esta sección estan los pasos rápidos para la ejecución del **SCREEN3**:

1. Descargar ejecutable ``SCREEN3.exe`` y código fuente: [``screen3.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip).
2. Ejecutar ``SCREEN3.exe`` haciendo doble click sobre este.
3. Ingresar los datos que pide el programa. Los resultados se guardarán en el archivo ``SCREEN.OUT``.

En la siguientes secciones, se encuentran todos los pasos en detalle.
-->
---

## Descarga

El **SCREEN3** está disponible en la página web de [USEPA](https://www.epa.gov/). Se puede descargar del siguiente link: [``screen3.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip).

Debería descargarse un archivo comprimido ``screen3.zip``, al descomprimirlo habrá una carpeta con varios archivos. Los archivos con extensión ``*.FOR`` son el código fuente (programado en [FORTRAN](https://es.wikipedia.org/wiki/Fortran)), los ``*.DAT`` son de archivos de entrada al modelo y los ``*.OUT`` salidas. El archivo ``SCREEN3.exe`` es el ejecutable compilado para windows que utilizaremos.

## Ejecución

Para ejecutar el **SCREEN3** simplemente vamos al directorio donde se encuentre el ejecutable ``SCREEN3.exe`` y lo ejecutamos haciendo doble click:

Se va a abrir una terminal ó consola:
```shell
  ******  SCREEN3 MODEL  ******
  **** VERSION DATED 13043 ****
  
 ENTER TITLE FOR THIS RUN (UP TO 79 CHARACTERS):

```

El programa funciona de forma interactiva, realizando una serie de preguntas que el usuario debe responder desde el teclado confirmando cada entrada con <kbd>Enter</kbd>.

Vamos a realizar una corrida de prueba con los siguientes parámetros, que podrían corresponder a una chimenea en un sitio urbano en una planicie:

### Características de la fuente:

| Tipo de fuente|Analitos|ALTURA [m]|DIÁMETRO CONDUCTO[m]   | x UTM20S   | y UTM20S|
|-|-|-|-|-|-|
|Puntual|     NOx, MP, CO, SO2, TRS    | 130|  6,2 | 715072.02  |6365674.52|

En general las ubicaciones se reportan en coordenadas geográficas de latitud y longitud. Podemos [convertirlas](https://www.latlong.net/lat-long-utm.html) a UTM y usar coordenadas planas en metros.

### Parámetros de emisión:



ANALITO|CAUDAL EMISIÓN [m3/s]|EMPERATURA[K]|VELOCIDAD[m/s]|CONCENTRACIÓN[mg/Nm3]|TASA[g/s]|
|-|-|-|-|-|-|
MP|	819|	453|	27,13|	43,73|	21,6|
CO|	819|		453|	27,13|	981,87|	484,89|
NOx|	819|	453	|27,13|	196|	96,7|
SO2	|819|		453	|27,13|	2,71|	1,34|
TRS	|819|		453	|27,13|	1,26|	0,62|

### Corrida de prueba

1. Al ejecutar el programa solicita ingresar el título del proyecto. En este caso pondremos "CASO_PRUEBA"

```shell
  ******  SCREEN3 MODEL  ******
  **** VERSION DATED 13043 ****
  
 ENTER TITLE FOR THIS RUN (UP TO 79 CHARACTERS):
 CASO_PRUEBA

```

2. Nos solicita escribir una letra según el tipo de fuente, en este caso puntual (**P**).

```shell
 ENTER SOURCE TYPE: P    FOR POINT
                    F    FOR FLARE
                    A    FOR AREA
                    V    FOR VOLUME
    ALSO ENTER ANY OF THE FOLLOWING OPTIONS ON THE SAME LINE:

      N    - TO USE THE NON-REGULATORY BUT CONSERVATIVE BRODE 2
             MIXING HEIGHT OPTION,
      nn.n - TO USE AN ANEMOMETER HEIGHT OTHER THAN THE REGULATORY
             (DEFAULT) 10 METER HEIGHT.
      SS   - TO USE A NON-REGULATORY CAVITY CALCULATION ALTERNATIVE
   Example - PN 7.0 SS (entry for a point source)

  ENTER SOURCE TYPE AND ANY OF THE ABOVE OPTIONS:
P
```

3. Nos solicita el caudal másico de emisión expresado en g/s, el cual obtenemos de la tabla de datos de emisión.

```shell
 ENTER EMISSION RATE (G/S):
21.6
```

Nos pide el diámetro interno del conducto emisor en metros:
```shell
 ENTER STACK INSIDE DIAMETER (M):
6.2
```

Nos pide la velocidad de salida del gas en m/s, tambien nos brinda la posiblidad de ingresarlo como tasa volumetrica en unidas del sistema internacional ó unidades imperiales:
```shell
 ENTER STACK GAS EXIT VELOCITY OR FLOW RATE:
 OPTION 1 : EXIT VELOCITY (M/S):
  DEFAULT - ENTER NUMBER ONLY
 OPTION 2 : VOLUME FLOW RATE (M**3/S):
            EXAMPLE "VM=20.00"
 OPTION 3 : VOLUME FLOW RATE (ACFM):
            EXAMPLE "VF=1000.00"
27.13
```

Nos pide la temperatura de salida del gas en grados kelvin:
```shell
 ENTER STACK GAS EXIT TEMPERATURE (K):
453
```

Nos pide la temperatura ambiente en grados kelvin:
```shell
 ENTER AMBIENT AIR TEMPERATURE (USE 293 FOR DEFAULT) (K):
290
```

Luego ingresamos la altura sobre el nivel del suelo del receptor de interés (por lo general se utiliza 1.5 metros que sería la altura promedio de inmisión de una persona):

```shell
 ENTER RECEPTOR HEIGHT ABOVE GROUND (FOR FLAGPOLE RECEPTOR) (M):
1.5
```

Luego hay que especificar si se trata de un entorno rural (**R**) ó urbano (**U**):
```shell
 ENTER URBAN/RURAL OPTION (U=URBAN, R=RURAL):
R
```

En el siguiente paso nos pregunta si queremos considerar el efecto de deflección de la pluma por influencia de edificios cercanos (*downwash*), en este caso no lo vamos a considerar:
```shell
 CONSIDER BUILDING DOWNWASH IN CALCS?  ENTER Y OR N:
n
```

El programa nos va a preguntar si queremos considerar los efectos del terreno, en este caso vamos a asumir que estamos en una planicie y por lo tanto no lo tendremos en cuenta:
```shell
 USE COMPLEX TERRAIN SCREEN FOR TERRAIN ABOVE STACK HEIGHT?
 ENTER Y OR N:
n
```

Como pusismos que no vamos a considerar efecto del terreno nos pregunta si queremos usar terreno simple con una sola altura:
```shell
 USE SIMPLE TERRAIN SCREEN WITH TERRAIN ABOVE STACK BASE?
 ENTER Y OR N:
y
```

A continuación nos propone correr contemplando todas las combinaciones de estabilidad atmosférica y velocidades de viento (*FULL METEOROLOGY*) o valores definidos por el usuario. Vamos a utilizar FULL METEOROLOGY:
```shell
 ENTER CHOICE OF METEOROLOGY;
 1 - FULL METEOROLOGY (ALL STABILITIES & WIND SPEEDS)
 2 - INPUT SINGLE STABILITY CLASS
 3 - INPUT SINGLE STABILITY CLASS AND WIND SPEED
1
```

Nos pregunta si queremos definir las distancias de los receptores de forma automática ó ingresar cada receptor de forma manual.
```shell
 USE AUTOMATED DISTANCE ARRAY? ENTER Y OR N:
y
```

Nos pregunta la altura del terreno respecto de la base del conducto, al ser un terreno plano la altura es 0:
```shell
 ENTER TERRAIN HEIGHT ABOVE STACK BASE (M):
0
```

En este paso nos pide la distancia mínima y máxima en la que ubicar de forma automática los receptores:
```shell
 ENTER MIN AND MAX DISTANCES TO USE (M):
100 10000
```

```shell

 **********************************
 *** SCREEN AUTOMATED DISTANCES ***
 **********************************

 *** TERRAIN HEIGHT OF   10. M ABOVE STACK BASE USED FOR FOLLOWING DISTANCES ***

   DIST     CONC             U10M   USTK  MIX HT   PLUME   SIGMA   SIGMA
    (M)   (UG/M**3)   STAB  (M/S)  (M/S)    (M)   HT (M)   Y (M)   Z (M)  DWASH
 -------  ----------  ----  -----  -----  ------  ------  ------  ------  -----
  20000.    10.32        6     1.0    1.0 10000.0   11.62  500.96   60.40    NO
  25000.    7.907        6     1.0    1.0 10000.0   11.62  609.76   64.96    NO
  30000.    6.361        6     1.0    1.0 10000.0   11.62  715.60   68.93    NO
  40000.    4.581        6     1.0    1.0 10000.0   11.62  920.23   74.58    NO
  50000.    3.554        6     1.0    1.0 10000.0   11.62 1117.43   79.27    NO
 ITERATING TO FIND MAXIMUM CONCENTRATION . . .

 MAXIMUM 1-HR CONCENTRATION AT OR BEYOND 20000. M:
  20000.    10.32        6     1.0    1.0 10000.0   11.62  500.96   60.40    NO
```

Nos pregunta si queremos agregar receptores discretos:
```shell
USE DISCRETE DISTANCES?  ENTER Y OR N:
N
```

Por último nos pregunta si queremos guardar los resultados en un archivo, ponemos que si.
```shell
 DO YOU WANT TO PRINT A HARDCOPY OF THE RESULTS?  ENTER Y OR N:
Y
```

Finalmente aparecerá este mensaje que nos dice que el archivo de salida se pudo generar:
```shell
 THE OUTPUT FILE, "SCREEN.OUT  ", HAS BEEN PRINTED.
```

Una vez que hayamos respondido a todas las preguntas se va a generar dos archivos: ``SCREEN.OUT`` y ``SCREEN.DAT``. El primero contiene los resultados obtenidos de la ejecución, y el segundo sirve para volver a ejecutar el programa sin tener que responder nuevamente todas las preguntas.

## Salidas

En el archivo ``SCREEN.OUT`` vamos a encontrar registros de la corrida, las opciones utilizadas, algunos valores intermedios de la ejecución, y entre otras cosas una tabla como la siguiente:

```Text
 *** TERRAIN HEIGHT OF    0. M ABOVE STACK BASE USED FOR FOLLOWING DISTANCES ***

   DIST     CONC             U10M   USTK  MIX HT   PLUME   SIGMA   SIGMA
    (M)   (UG/M**3)   STAB  (M/S)  (M/S)    (M)   HT (M)   Y (M)   Z (M)  DWASH
 -------  ----------  ----  -----  -----  ------  ------  ------  ------  -----
    100.    0.000        0     0.0    0.0     0.0    0.00    0.00    0.00    NA
    200.    0.000        0     0.0    0.0     0.0    0.00    0.00    0.00    NA
    300.    631.6        1     1.5    2.1   480.0  125.11   90.71   82.09    SS
    400.    517.4        1     1.5    2.1   480.0  140.59  118.85  113.59    SS
    500.    494.6        6     1.0    2.0 10000.0  113.08   50.21   50.05    SS
    600.    578.0        6     1.0    2.0 10000.0  113.08   59.27   54.62    SS
    700.    638.4        6     1.0    2.0 10000.0  113.08   68.06   59.18    SS
    800.    715.3        6     1.0    2.0 10000.0  113.08   76.59   65.44    SS
    900.    699.4        6     1.0    2.0 10000.0  113.08   84.89   68.33    SS
   1000.    681.9        6     1.0    2.0 10000.0  113.08   92.97   71.13    SS

```
esta tabla muestra el valor de disintas variables en función de la distancia, con lo que podrémos graficarlas para ver como se distiribuyen.

También al final del archivo encontraremos la siguiente tabla resumen que  indica la máxima concentración encontrada, la distancia a la que ocurre y la altura:

```Text
      ***************************************
      *** SUMMARY OF SCREEN MODEL RESULTS ***
      ***************************************

  CALCULATION        MAX CONC    DIST TO   TERRAIN
   PROCEDURE        (UG/M**3)    MAX (M)    HT (M)
 --------------    -----------   ---------   -------
 SIMPLE TERRAIN       715.3          800.        0.

 BLDG. CAVITY-1       3168.          142.       --  (DIST = CAVITY LENGTH)

 BLDG. CAVITY-2       1691.          101.       --  (DIST = CAVITY LENGTH)
```



#### Ejecución automática:

**SCREEN3** puede ejecutarse también utilizando un *archivo de control* para evitar tener que responder todas las preguntas cada vez que lo ejecutamos. Para eso necesitamos el archivo ``SCREEN.DAT``, si lo abrimos veremos algo así:

```Text
CORRIDA DE EJEMPLO CON BUILDING DOWNWASH
P
  100.0
  100.0
  2.000
  15.00
  450.0
  293.0
  .0000
           1
Y
  80.00
  80.00
  100.0
N
N
           1
Y
   100.00, 1000.00
N
N
```
este archivo contiene las respuestas a las preguntas del **SCREEN3** de forma secuencial. 

Para ejecutarlo con estas opciones tenemos que ingresar por terminal a la carpeta donde se encuentra ``SCREEN3.exe`` y ``SCREEN.DAT``, por ejemplo, si la carpeta se encuentra en ``C:/Users/MCA_tutorial/screen3`` hay que tipear:

```shell 
chdir C:/Users/MCA_tutorial/screen3
```
el comando ``chdir`` (de *change directory*) en windows sirve para cambiar el directorio de trabajo. Esto nos permite tener fácil acceso a los archivos que se encuentran en la carpeta de interés.

Luego para ejecutarlo:

```shell
SCREEN3.exe < SCREEN.DAT
``` 

El programa se ejecutará y va a crear un nuevo archivo ``SCREEN.OUT``.

