---
nav_exclude: true
published: false
---

## Resumen
Se modela mediante el uso del SCREEN3 las oncentraciones de óxidos de nitrogeno [NOx] y material particulado menor a 10&mu;m [PM10] emitidas por la chimenea del emprendimiento XXXX.

Los resultados del modelo se comparan con los estándares de calidad de aire fijados por el decreto XXXX correspondiente a la autoridad de aplicación ambiental de la jurisdicción del emprendimiento.

Se verifica que para todos los contaminantes mencionados, en ninguno de los receptores analizados, se superan las concentraciones límites reguladas.


## Introducción

### Objetivo
A efectos de controlar las emisiones gaseosas y su impacto asociado, se realiza mediante modelación matemática la simulación del comportamiento de los contaminantes en la atmósfera para los efluentes gaseosos del emprendimiento XXXX ubicado en XXXXXX, provincia de XXXXX.
 El presente estudio tiene como objeto relacionar la emisión de una fuente gaseosa y la calidad del aire ambiente resultante conforme a los métodos planteados en el decreto XXXX y resolución XXXXX del organismo regulador XXXXX.

### Descripción y justificación del modelo

Para el presente estudio se selecciona el modelo SCREEN3 de la Agencia de Protección Ambiental de los Estados Unidos (US-EPA). 

SCREEN3 es un modelo de pluma gaussiana para fuente simple, que estima la maxima concentración a nivel del suelo producida por fuentes puntuales, de area, antorhas, ó fuentes de volumen, asi como las concentración en cavidades producidas por  el flujo alrededor de edificios y en zonas de inversión por fumigación costera. 
El SCREEN3 es la versión de sondeo del modelo de detalle ISC3.

 Al momento de la realización de este estudio, la US-EPA al SCREEN3 en su lista de modelos de sondeo recomendados.

El SCREEN3 modela una función de dispersión bi-gaussiana vertical en la capa convectiva representando explícitamente movimientos verticales. 

El SCREEN3 está disponible para acceso público en el repositorio web de la (US-EPA 3)[https://www.epa.gov/scram/air-quality-dispersion-modeling-screening-models].


### Sitio de estudio
La fuente de emisión corresponde al proceso de fabricación de neumáticos, cámaras y accesorios de vehículos del predio ubicado en el partido de XXXXX, en las coordenadas latitud -XX.XX longitud -XX.XX [Anexo 1 Dominio de estudio].


### Características de fuentes emisoras
   A continuación se resumen las careacterísticas de las fuentes de emision consideradas en el modelo.

| id  |  X  [m utm 21] | Y [m utm 21] | Altutud [msnm] | Altura del conducto [m] | Diámetro del conducto [m] |
|----|----|----|----|----|----|
| c1 | XXXX.XX | XXXXX.XX | XX.X | XX.X | XX.X|
| c2 | XXXX.XX | XXXXX.XX | XX.X | XX.X | XX.X|
| c3 | XXXX.XX | XXXXX.XX | XX.X | XX.X | XX.X|

**Tabla 1.** Caracteristicas de los conductos emisores.


A continuación se resumen los parámetros de emision.

| Analito | id | tipo  | Temperatura [ºC] | Velocidad [m/s] | Caudal másico [g/s] |
| ------- |----|---------|-------|------|---------|
|  NOx    | c1 | POINT   | XXX.X | XX.X | X.XXe-X |
|  NOx    | c2 | POINT   | XXX.X | XX.X | X.XXe-X |
|  NOx    | c3 | POINT   | XXX.X | XX.X | X.XXe-X |
|  PM10   | c1 | POINT   | XXX.X | XX.X | X.XXe-X |
|  PM10   | c2 | POINT   | XXX.X | XX.X | X.XXe-X |
|  PM10   | c3 | POINT   | XXX.X | XX.X | X.XXe-X |

**Tabla 2.** Parámetro de emision para cada conducto y analíto.



### Meteorología
La información meteorológica de superficie y sondeos verticales necesaria para la ejecución del modelo fue extraída de la base de datos de observaciones del Servicio Meteorológico Nacional (SMN), se representa su ubicación respecto a las fuentes en el [Anexo 7].

Se utilizó la siguiente estación de observación:


| Nombre  | Provincia  | Latitud | Longitud | Altitud | id (WMO) | id (ASCII) |
| ------- |------------|---------|----------|---------|----------|------------|
|  NOx    | XXXXX XXXX | XX.XX   | XX.XX    |  X.X    | XXXXXXX  | XXXXXXXXX  |

**Tabla 3.** Estación meteorológica utilizada.



### Configuración del modelo

Explicitar las opciones (indicando palabras clave) utilizadas en cada modelado.


#### Escenarios modelados
Explicitar los escenarios de modelado.
(Tabla con clases de estabilidad y velocidades utilizadas)


### Grilla de receptores

Se considero una grilla de 100 receptores equiespaciados cada 50 metros desde la fuente emisora considerada. 


### Datos meteorológicos
Resumir en una tabla los parámetros meteorológicos de entrada en cada caso (clases de estabilidad, velocidades de viento y temperatura).
Para representar las variables meteorológicas se utilizaron valores representativos de las siguientes variables:

| Variable |  Valor utilizado  | Estadístico  | Periodo de serie temporal considerado |
| -------- |  ---------------  | ------------ | ------------------------------------- |
| Velocidad del viento |  XX.XX  | Promedio de la serie temporal | enero 20XX hasta enero 20YY |
| Temperatura ambiente |  XX.XX  | Promedio de la serie temporal | enero 20XX hasta enero 20YY |
| Humedad relativa     |  XX.XX  | Promedio de la serie temporal | enero 20XX hasta enero 20YY |
| Presión atmosférica  |  XX.XX  | Promedio de la serie temporal | enero 20XX hasta enero 20YY |

## Resultados

### Tabla de concentraciones máximas
        Resumir en una tabla la concentración máxima calculada, explicitando distancia a la fuente, altura y condiciones meteorológicas.



### Gráfico de concentración calculada en función de la distancia
        Representar en un gráfico la concentración calculada a nivel del receptor en función de la distancia a la fuente.
	
	Poner GRAFICO Concentración vs Distancia

**Figura 1.** Gráfico concentración vs distancia.

### Receptor de máxima concentración
        Representar en un mapa un punto aproximado donde se encuentre la concentración máxima.



### Comparación con estándares reglamentarios
Comparar concentración máxima calculada con estándares de calidad de aire para el compuesto asignado y concluir el informe explicitando si cumple o no cumple con el estándar (de no cumplir aclarar la magnitud del desvío).



## Conclusión

Los resultados cumplen con los estándares vigentes al momento de realización del
estudio, correspondiendo a la columna “Estándar E°X” evaluando la concentración máxima respecto del 80% de la concentración límite. 


## Bibliografía

- “SCREEN3 Model User’s Guide”. U.S EPA. EPA-454/B-95-004. September 1995.
- “Guía metodológica para la evaluación del impacto ambiental atmosférico”. Laura Dawidowski, Darío Gómez y Silvia Reich. Honorable Cámara de Diputados de La Nación.
- “Calidad del aire - Monitoreo y modelado de contaminantes atmosféricos. Efectos en la salud pública” Porta, Andrés; Yanina Sanchez; Esteban Colman Lerner. UNLP, 2018.
Resolución 559-19 OPDS-Anexo III Instructivo para la aplicación de modelos de difusión atmosférica a efluentes gaseosos.

