---
nav_exclude: true
has_children: false
---

# Modelado de la Calidad del Aire

Material didáctico del curso de *Modelado de la Calidad del Aire* (MCA), dictado en la Facultad de Agronomía, Universidad de Buenos Aires.

---

## Clases 2023
#### Clase 1 (10/05):
+ Presentaciónes:  [Contexto histórico y normativo](./files/MCA23_1_Contexto.pdf) y  [Ecuación de transporte](./files/MCA23_1_EcTransporte.pdf)
+ Lectura:  [Cronología calidadde aire](./files/Heirdon_AirPollutionHistorical.pdf) y [Ecuación de Transporte](./files/MCA_Apunte_01_EcTransporte.pdf)

#### Clase 2 (17/05):
+ Presentaciónes: [Presentación de modelos](./files/MCA_3_Introduccion_Modelado_Dispersión.pdf) y [Modelos gaussianos](./files/MCA_4_Presentando_Modelo_Gausiano.pdf)
+ Lectura: [Guia uso screen](./tut/archivos/screen3/S2_SCREEN3 Instrucciones Guía Uso.pdf) y [Introducción gaussianos - De Visscher](./files/CAP2-DE_VISSSCHER-PRIMER.pdf)

#### Clase 3 (24/05):
+ Presentación: [Video tutorial](https://youtu.be/YP510pY2EiU)
+ Lectura: [Guia uso aermet](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/met/aermet/aermet_userguide.pdf)

#### Clase 4 (31/05):
+ Presentación: [Video tutorial](https://www.youtube.com/watch?v=7gPrE61wqc4)
+ Lectura: [Guia uso aermod](https://gaftp.epa.gov/Air/aqmg/SCRAM/models/preferred/aermod/aermod_userguide.pdf)

#### Clase 5 (07/06):
+ Presentación: [Modelos Gaussianos](./files/MCA_Clases_ModDispersion.pdf) y [Fundamentos de AERMOD (Parte 1)](./files/MCA_Clases_AERMOD_parte1.pdf)
+ Lectura: [Modelos Gaussianos](./files/MCA_Apunte_02_ModDispersion.pdf) <!--y [Fundamentos de AERMOD (Parte 1)](./files/MCA_Apunte_02_AERMOD.pdf)-->

#### Clase 6 (14/06):
+ Presentación: [Meteorología de Capa Límite](./files/MCA_Clases_Meteo.pdf) 
+ Lectura: [Cap. 18 - Práctical Meteorology (Stull)](./files/Stull_Practical_Meteorology-Chap18_PBL.pdf) 

---

### Docente responsable
+ Bormioli, Marcelo G.

### Docentes a cargo
+ Espada, Ramiro A.
+ Medrano, Luciano M.

### Cronograma

|Clase|Fecha  | Teórica | Práctica  |  TP   |
|:----|:-----:|:--------|:----------|:-----:|
|  1  | 10/05 | Contexto & Ecuación de transporte | -                             | -                                   |
|  2  | 17/05 | Modelos Gaussianos                | [Screen3](./tut/screen3.html) | Explicación [TP 1](./tps/tp1.html)  |
|  3  | 24/05 |                                   | [AERMET](./tut/aermet.html)   | -                                   |
|  4  | 31/05 |                                   | [AERMOD](./tut/aermod.html)   | Entrega **TP1**                     |
|  5  | 07/06 | Fundamentos de AERMOD             | -                             | Explicación [TP 2](./tps/tp2.html)  |
|  6  | 14/06 | Meteorología                      | -                             | Avances [TP 2](./tps/tp2.html)      |
|  7  | 21/06 |                                   | -                             | Exposición [TP 2](./tps/tp2.html)   |
|  8  | 28/06 | *Evaluación integradora*          | -                             | Entrega **TP2**                     |


### Lugar y horario
+ Miercoles 18 a 21hs, aula 4, Pabellón Lorenzo Parodi (Av. San Martín).


### Requisitos de aprobación:

El  curso se aprueba con:
- una asistencia mayor o igual al 75%,
- nota final promedio igual o mayor que 4 (cuatro).

La nota final es la resultante del promedio ponderado según se detalla a continuación (equivalente a haber alcanzado el 60% de los objetivos y conocimientos).

| Instancia | Porcentaje de nota final |
|:----------|:-----------------:|
| TP 1                         | 25% |  
| TP 2 + Informe + Exposición  | 50% |
| Evaluación final integradora | 25% |

El TP2 (abarcador del núcleo del curso) consta en realizar una presentación oral grupal y luego el informe final. Durante la presentación oral se deberá defender (aprox. 15 min) con preguntas y/o comentarios, donde se evaluará a cada integrante del grupo con preguntas conceptuales sencillas sobre la realización del trabajo. Esto implica que cada integrante del grupo debe tener cabal conocimiento de lo realizado.

La evaluación final integradora consta de preguntas conceptuales con poco desarrollo sin necesidad de cálculo. Con esto demuestran la atención en clase, la comprensión de los contenidos y participación en todos los pasos de los trabajos prácticos.


### Contenidos:
- **Unidad 1:** Introducción de la calidad del aire. Descripción Lagrangiana y Euleriana. La ecuación de transporte. Soluciónes analíticas a la ecuación de transporte. Modelos Gaussianos.
- **Unidad 2:** Marco legal en Argentina y exigencias de modelados de la dispersión de contaminantes atmosféricos. Desarrollo Histórico de modelos de calidad de aire.
- **Unidad 3:** Influencia de las condiciones meteorológicas en la dispersión de contaminantes en la atmósfera: Radiación y Balance de calor en la atmósfera. Turbulencia y Capa Límite Planetaria (PBL). Altura de capa de mezcla (Turbulenta y Convectiva). Estructura vertical de la PBL. Tratamiento de la información meteorológica.
- **Unidad 4:** Modelos de sondeo: Fundamentos e implementación de modelo simple según normativa local. Fundamentos e implementación de modelo SCREEN3. 
- **Unidad 5:** Modelos de detalle: Fundamentos e implementación del AERMOD y sus preprocesadores (AERMAP, AERSURFACE, BPIPPRM y AERMET). 

### Correlativas
+ Física aplicada
+ Estadística general
+ Química de la contaminación y toxicología

### Creditos
DOS (2) créditos = TREINTA Y DOS (32) horas.

### Bibliografía

+ "Air Dispersion Modeling, Foundations and Applications". De Visscher A. Wiley. 2013.
+ "SCREEN3 Model User’s Guide". U.S EPA. EPA-454/B-95-004. September 1995.
+ "AERMOD Model Formulation and Evaluation", U.S.EPA. EPA-454/ R-18-003. April, 2018.
+ "Guía metodológica para la evaluación del impacto ambiental atmosférico". Laura Dawidowski, Darío Gómez y Silvia Reich. Honorable Cámara de Diputados de La Nación.
+ "Calidad del aire - Monitoreo y modelado de contaminantes atmosféricos. Efectos en la salud pública" Porta, Andrés; Yanina Sanchez; Esteban Colman Lerner. UNLP, 2018.
+ Resolución 559-19 OPDS-Anexo III Instructivo para la aplicación de modelos de difusión atmosférica a efluentes gaseosos. 
<!-- + "Description of the HYSPLIT 4 modeling system". Roland R. Draxler. Air Resources Laboratory (ARL). Silver Spring, Maryland. December 1997.-->

### Bibliografía complementaria

+ "Introduction to Atmospheric Chemistry". Jacob D.J. Princeton University Press, 1999.
+ "Practical Meteorology: An Algebra-based Survey of Atmospheric Science". Stull Rolland. AVP International, University of British Columbia, 2016.
+ "A User's Guide for the CALPUFF Dispersion Model (Version 5)". Joseph S. Scire, et al. Earth Tech Inc. January 2000.

### Bibliografía avanzada

+ “Modeling of Atmospheric Chemistry”. Brasseur G.P & Jacob D.J Cambridge University Press. May 2017.
+ “Fundamentals of Atmospheric Modeling” (2nd edition). Jacobson M.Z. Cambridge University Press. June 2012.

