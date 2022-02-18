---
nav_order: 0
---

# Shell

> Tutorial sobre uso de consola de comandos.

## Estructura de directorios en windows:

Para los fines de este curso vamos a asumir que un computadora puede almacenar 3 tipos de elementos:
- *directorios* ó carpetas
- *archivos* de lectura/escritura
- *ejecutables*, binarios ó programas

Cada sistema operativo viene con una estructura de directorios particular, en el caso de Windows en general vamos a tener la siguiente estructura:

```mermaid
graph TD;
    C:/ --> Windows/;
    C:/ --> Program Files/;
    C:/ --> Users/;
    Users/ --> Public/;
    Users/ --> Usuario1/;
    Users/ --> Usuario2/;
    Users/ --> ...;
    Users/ --> UsuarioN/;
    Windows/ --> Assembly/;
    Windows/ --> Boot/;
    Windows/ --> Containers/;
    Windows/ --> ...;
    Windows/ --> System/;
    Windows/ --> System32/;
    Windows/ --> System64/;
    Program Files/ --> AMD;
    Program Files/ --> Common Files;
    Program Files/ --> Git
    Program Files/ --> Internet Explorer
    Program Files/ --> Microsoft Office
    Program Files/ --> ...
    Program Files/ --> WindowsPowerShell
    Program Files/ --> WinRAR
    Program Files/ --> WinZip
```

``C:/`` es el directorio *raiz* ó *madre*, representa el espacio del disco donde está instalado el sistema operativo.

En ``C:/Windows`` se almacenan archivos y ejecutables relacionados con el funcionamiento interno del sistema operativo.
En ``C:/Program Files`` se alamacenan todos los aplicaciones (archivos y ejecutables) instalados por el usuario.
En ``C:/Users`` hay una serie de subdirectorios que cada una representa los archivos y ejecutables correspondiente a cada usuario / sesión.
Dentro de la carpeta de cada usuario suelen estar las típicas carpetas: *Desktop*, *Documents*, *Downloads*, *Images*, *Music*, etc.

## Shell
La *shell*, consola ó terminal, es un programa que te permite interactuar con el sistema operativo, navegar en el sistema de archivos, crear, copiar y mover archivos, ejcutar programas y aplicaciones, entre otras muchas cosas.


## Abrir shell

Normalmente hay multiples terminales instaladas en windows que se pueden utilizar, las más comunes son:
- ``cmd``
- ``PowerShell``

En este curso utilizaremos la segunda, ya que cuenta con algunas aplicaciones preinstaladas que nos serán de utilizada y además la sintaxis de los comandos que utiliza son universales y sirven para otros sistemas operativos también (MacOS y Linux).


Para abrirla se abre el buscador de programas y archivos y se tipea *PowerShell*, al ejectuarlo se abre una ventana:

```shell
C:/Users/>
```

Lo que aparece antes del cursor se denomina *promt* e indica la ubicación actual del usuario en el sistema de carpetas.

## Principales comandos

### Ver directorio de trabajo actúal (``pwd``)

Para ver en que directorio estamos parados ejecutamos el siguiente comando:
```shell
pwd
```

### Navegar / cambiar de directorio (``cd``)

Si queremos movernos hacia otro directorio usamos el comando:
```shell
cd C:/Users/MiUsuario
```

### Listar archivos en directorio (``ls``)

Para ver los archivos y directorios presentes en el directorio actual ejecutamos:
```shell
ls
```

### Crear nuevo directorio (``mkdir``)
Si queremos crear una nueva carpeta:
```shell
mkdir MiNuevaCarpeta
```

### Crear archivo de texto:
```shell
touch miArchivo.txt
```

Si lo queremos editar hay muchas opciones, una es utilizar el editor de textos: "notepad"
```shell
notepad miArchivo.txt
```
se va a abrir el documento con dicho programa, se puede utilizar y al cerrar volvemos al shell.

Una forma de ver el contenido del archivo es:
```shell
cat miArchivo.txt
```

otra forma es con el comando ``less``:
```shell
less miArchivo.txt
```

### Copiar archivo (``cp``)
```shell
cp miArchivo.txt C:/Users/miUsuario/miArchivo.txt
```


### Mover archivo (``mv``)
la sintaxis de ``mv`` es igual que ``cp`` 
```shell
mv miArchivo.txt C:/Users/miUsuario/miArchivo.txt
```

también puede usarse ``mv`` para renombrar un archivo:
```shell
mv miArchivo.txt miArchivo_2.txt
```

### Linkear archivos (``ln``)

```shell
ln
```

### Descomprimir (``tar``)

```shell
tar
```

### Ejecutar programa

```shell
./programa.exe
```

