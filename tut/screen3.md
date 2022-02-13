---
nav_order: 1
---
# Screen3

> Tutorial para uso de **SCREEN3**

Los pasos para la ejecución del **SCREEN3** son:
1. Descargar ejecutable ``SCREEN3.exe`` y código fuente: [``screen3.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip).
2. Ejecutar ``SCREEN3.exe`` haciendo doble click sobre este.
3. Ingresar los datos que pide el programa. los resultados se guardarán en el archivo ``SCREEN.OUT``.


## Descarga

El **SCREEN3** está disponible en la página web de [USEPA](https://www.epa.gov/). Se puede descargar del siguiente link: [``screen3.zip``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip).

Debería descargarse un archivo comprimido ``screen3.zip``, al descomprimirlo habrá una carpeta con diversos archivos. Los archivos con extensión ``*.FOR`` son el código fuente (programado en FORTRAN), los ``*.DAT`` son ejemplos de archivos de entrada al modelo y los ``*.OUT`` son ejemplos de archivos de salida. El archivo ``SCREEN3.exe`` es el ejecutable compilado para windows que utilizaremos.

## Ejecución

Para ejecutar el **SCREEN3** simplemente vamos al directorio donde se encuentre el ejecutable ``SCREEN3.exe`` y lo ejecutamos haciendo doble click:

Se va a abrir una terminal ó consola:
```
  ******  SCREEN3 MODEL  ******
  **** VERSION DATED 13043 ****
  
 ENTER TITLE FOR THIS RUN (UP TO 79 CHARACTERS):

```

El programa funciona de forma interactiva, realizando una serie de preguntas que el usuario debe responder ingresando las respuestas desde el teclado y luego apretando enter.

Algunos datos que va a pedir son:
+ Titulo del proyecto.
+ Tipo de fuente: Punto (**P**), Flare/Antorcha (**F**), Area (**A**), Volumen (**V**).
+ Tasa de Emision en [g/s].
+ Altura de la Fuente emisora [m].
+ Diámetro interno del conducto [m]
+ Velocidad de salida [m/s] 
+ Temperatura de salida [ºK]
+ Temperatura Ambiente [ºK]
+ Altura sobre el nivel del suelo de los receptores (**flag pole**) [m]
+ Opción Urbana (**U**) ó Rural (**R**)
+ Opción para contemplar *downwash* producido por edificios.
+ Opción para contemplar terreno complejo.
+ Opción de meteorología:
	1. FULL METEOROLOGY (todas las estabilidades y velocidades de viento)
	2. INPUT SINGLE STABILITY CLASS
	3. INPUT SINGLE STABILITY CLASS AND WIND SPEED
+ Opciones para grilla de receptores (automática ó manual)
+ Altura de topográfia sobre la base del emisor.
+ Opción de calculo sobre un receptor discreto.
+ Opción para guardar archivo de salida. 

Una vez que hayamos respondido a todas las preguntas se va a generar dos archivos: ``SCREEN.OUT`` y ``SCREEN.DAT``. El primero contiene los resultados obtenidos de la ejecución, y el segundo sirve para volver a ejecutar el programa sin tener que responder nuevamente todas las preguntas.

## Salidas

En el archivo ``SCREEN.OUT`` vamos a encontrar registros de la corrida, las opciones utilizadas, algunos valores intermedios de la ejecución, y entre otras cosas una tabla como la siguiente:

```
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

```
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

```
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

