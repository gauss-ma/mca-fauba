---
nav_order: 1
---
# Screen3

> Tutorial para uso de **screen3**

## Descarga

El **SCREEN3** se puede descargar del siguiente link: [``SCREEN3``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip).

Debería descargarse un archivo ``screen3.zip``, que al extraerlo contiene diversos archivos. Los archivos con extensión ``*.FOR`` son el código fuente, los ``*.DAT`` son ejemplos de archivos de entrada y los ``*.OUT`` son ejemplos de archivos de salida y el archivo ``SCREEN3.exe`` es el ejecutable compilado para windows que utilizaremos.
 

## Ejecución

Para ejecutar el **SCREEN3** simplemente vamos al directorio donde se encuentre el ejecutable ``SCREEN3.exe`` y lo ejecutamos haciendo doble click, o si estamos en la terminal:

```shell
screen3
```
De esta forma se ejecutará de forma interactiva, realizando una serie de preguntas que el usuario debe responder ingresando los valores con el teclado y apretando enter.


**SCREEN3** puede ejecutarse también utilizando un *archivo de control* para evitar tener que responder todas las preguntas cada vez que lo ejecutamos.

Un ejemplo de archivo de control es: ``EXAMPLE.DAT``, si lo abrimos veremos:

```
POINT SOURCE EXAMPLE WITH BUILDING DOWNWASH
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

Para ejecutarlo con estas opciones tenemos que ingresar por terminal a la carpeta donde se encuentra ``SCREEN3.exe`` y ``EXAMPLE.DAT``, y tipear:

```shell
screen3 < EXAMPLE.DAT
``` 
El programa se ejecutará y va a crear el archivo: ``SCREEN.OUT``


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


