---
nav_order: 1
---


# Screen3

> Tutorial para uso de **screen3**


## Descarga

Link de descarga del [``SCREEN3``](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/screening/screen3/screen3.zip)

Debería descargarse un archivo ``screen3.zip``, que al extraerlo contiene el siguiente arbol de archivos:

```
screen3
├── DEPVAR.INC
├── EXAMPLE.DAT
├── examplenew.out
├── EXAMPLE.OUT
├── examplnrnew.out
├── EXAMPNR.DAT
├── exampnrnew.out
├── EXAMPNR.OUT
├── MAIN.INC
├── README.TXT
├── SCREEN3A.FOR
├── SCREEN3B.FOR
├── SCREEN3C.FOR
└── SCREEN3.exe
```

Los archivos ``*.FOR`` son el código fuente, y el archivo ``SCREEN3.exe`` es el ejecutable compilado para windows que utilizaremos.
 

## Preparación de datos de entrada

El screen3 funciona interactivamente, sin embargo se puede ejecutar de forma automática utilziando un archivo de control ``*.DAT``.

Por ejemplo si abrimos el archivo de texto EXAMPLE.DAT veremos:

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


## Ejecución

Para ejecutar el screen3 utilizando un archivo de control escribimos en la terminal:

```shell
screen3 < EXAMPLE.DAT
```

Para ejecutarlo de forma interactiva:

```shell
screen3
``` 

## Salidas


