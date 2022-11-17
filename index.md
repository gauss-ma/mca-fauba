---
nav_exclude: true
has_children: false
---

# Modelado de la Calidad del Aire

Material didáctico del curso de *Modelado de la Calidad del Aire* (MCA), dictado en la Facultad de Agronomía, Universidad de Buenos Aires.

---

### Material de clase:

Clase 1:
+ [Introducción al curso](./files/MCA_1_Presentación.ppt)
+ [Contexto histórico y normativo](./files/MCA_1_Contexto.pdf)
+ [Ecuación de transporte](./files/MCA_1_EcTransporte.pdf)

Clase 2:
+ [Modelos Gaussianos](./files/MCA_2_Gaussianos.pdf)
+ [Screen3 - Fundamentos](./files/MCA_2_Screen3.ppt)
+ [Tutorial Screen3](./tut/screen3.html)

Clase 3:
+ [Tutorial AERMET](./tut/aermet.html)

Clase 4:
+ [Meteorología de Capa Límite](./files/MCA_4_MeteorologiaCLP.pdf)
+ [Tutorial AERMOD](./tut/aermod.html)

Clase 5:
+ [Postprocesamiento](./tut/post.html)

Clase 6:
+ Trabajo sobre [TP N°2.](./tps/tp2.html)

Clase 7:
+ Exposición sobre [Estimación de Emisiones](./files/CHARLA_EMISIONES.pdf) 

---

### Docente responsable
+ Bormioli, Marcelo G.

### Docentes a cargo
+ Espada, Ramiro A.
+ Medrano, Luciano M.

### Docente invitada
+ Gómez Arismendi, Sabrina

### Cronograma

|Clase|Fecha| Teórica | Práctica  |  TP   |
|:---|:----:|:--------|:----------|:-----:|
| 1  | 20/5 | [Contexto](./teo/contexto.html) & [Ecuación de transporte](./teo/ectransp.html) | - | - |
| 2  | 27/5 | [Modelos Gaussianos](./teo/gaussianos.html) | *Hands-on* [Screen3](./tut/screen3.html) | |
| 3  | 03/6 | - | *Hands-on* [AERMET](tut/aermet.html) | Explicación [TP 1](./tps/tp1.html)  |
| 4  | 10/6 | [Meteorología](./teo/meteorologia.html) | *Hands-on* [AERMOD](./tut/aermod.html)| Explicación [TP 2](./tps/tp2.html) |
| 5  | 17/6 | **FERIADO NACIONAL** | - | Entrega **TP1** |
| 6  | 24/6 | - | [Posprocesamiento](./tut/pos.html) | Avances [TP 2](./tps/tp2.html) 	|
| 7  | 01/7 | - | - | Avances [TP 2](./tps/tp2.html) |
| 8  | 08/7 | Fundamentos [AERMOD](./teo/aermod.html) & [Estimación de Emisiones](./files/CHARLA_EMISIONES.pdf) | - | Exposición [TP 2](./tps/tp2.html) |
| 9  | 15/7 | *Evaluación integradora* | - | Entrega **TP2** | 

[Cronográma detallado](./files/Cronograma.pdf){: .btn .btn-outline }

### Lugar y horario
El curso se dicta en el Aula **UTI UBALLES** (pabellón Uballes), los viernes de 18 a 21 horas.

### Requisitos de aprobación:

El  curso se aprueba con:
- una asistencia mayor o igual al 75%,
- nota final promedio igual o mayor que 4 (cuatro).

La nota final es la resultante del promedio ponderado según se detalla a continuación
(equivalente a haber alcanzado el 60% de los objetivos y conocimientos).

| Instancia | Porcentaje de nota final |
|:----------|:-----------------:|
| TP 1                         | 25% |  
| TP 2 + Informe + Exposición  | 50% |
| Evaluación final integradora | 25% |

El TP2 (abarcador del núcleo del curso) consta en realizar una presentación oral grupal y luego el informe final. Durante la presentación oral se deberá defender (aprox. 15 min) con preguntas y/o comentarios, donde se evaluará a cada integrante del grupo con preguntas conceptuales sencillas sobre la realización del trabajo. Esto implica que cada integrante del grupo debe tener cabal conocimiento de lo realizado.

La evaluación final integradora consta de preguntas conceptuales con poco desarrollo sin necesidad de cálculo. Con esto demuestran la atención en clase, la comprensión de los contenidos y participación en todos los pasos de los trabajos prácticos.


### Contenidos:
- **Unidad 1:** Introducción físico-matemática: Repaso de análisis matemático (Derivadas parciales y ecuaciones diferenciales). Función Gaussiana y Función Error. Ecuaciones de difusión y de transporte. Unidades de concentración de contaminantes en aire y caudales de emisión
- **Unidad 2:** Introducción normativa: Requerimientos legales en Argentina sobre exigencias de modelados de la dispersión de contaminantes atmosféricos. Uso en la normativa Internacional y Normas IRAM/ISO
- **Unidad 3:** Desarrollo Histórico de modelos de calidad de aire: Primeras aplicaciones de modelado de dispersión, evolución de modelos predecesores. Estudios científicos de base. Desarrollos locales. Casos de ejemplo de aplicación. Introducción al modelado de la dispersión de contaminantes en la atmósfera. Ecuación de transporte: advección, difusión, fuentes y sumideros. Formulación Euleriana y Lagrangiana. Soluciones analíticas de la ecuación de transporte para estado transitorio y estacionario. Modelos gaussianos, modelos lagrangianos y modelos mixtos.
- **Unidad 4:** Influencia de las condiciones meteorológicas en la dispersión de contaminantes en la atmósfera: Radiación y Balance de calor en la atmósfera. Turbulencia y Capa Límite Planetaria (PBL). Altura de mezcla Turbulenta y Convectiva. Estructura vertical de la PBL. Tratamiento de la información meteorológica. Calidad de los resultados. Factores de incertidumbre. 
- **Unidad 5:** Nociones de cálculo de emisiones. Interpretación de protocolos de monitoreo de emisiones. Estimaciones mediante AP-42 metodología general. Ejemplos de aplicaciones a voladura de polvos en caminos y pilas, rellenos sanitarios, tanques de almacenamiento, entre otros. 
- **Unidad 6:** Modelos de Sondeo: Fundamentos e implementación de modelo simple según normativa local. Fundamentos y uso de modelo SCREEN3. Modelos de detalle: Fundamentos e implementación del AERMOD y sus preprocesadores: AERMAP, AERSURFACE, BPIPPRM y AERMET. Parámetros micro-meteorológicos de Capa Límite Convectiva y Estable (calor sensible, velocidad de fricción, longitud de Monin-Obukhov). Temperatura potencial y estabilidad. Clases de estabilidad. Efectos de la superficie, topografía, edificios (downwash), fumigación costera y flotación en el desarrollo vertical de la pluma. Herramientas para el pre-procesamiento y post-procesamiento:
Interpretación y visualización de resultados, isopletas de concentración, tablas de frecuencia de excedencias de concentración límite. Tiempos de promediado. 

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
+ "Description of the HYSPLIT 4 modeling system". Roland R. Draxler. Air Resources Laboratory (ARL). Silver Spring, Maryland. December 1997.
+ "A User's Guide for the CALPUFF Dispersion Model (Version 5)". Joseph S. Scire, et al. Earth Tech Inc. January 2000.
+ "Guía metodológica para la evaluación del impacto ambiental atmosférico". Laura Dawidowski, Darío Gómez y Silvia Reich. Honorable Cámara de Diputados de La Nación.
+ "Calidad del aire - Monitoreo y modelado de contaminantes atmosféricos. Efectos en la salud pública" Porta, Andrés; Yanina Sanchez; Esteban Colman Lerner. UNLP, 2018.
+ Resolución 559-19 OPDS-Anexo III Instructivo para la aplicación de modelos de difusión atmosférica a efluentes gaseosos. 

### Bibliografía complementaria

+ "Introduction to Atmospheric Chemistry". Jacob D.J. Princeton University Press, 1999.
+ "Practical Meteorology: An Algebra-based Survey of Atmospheric Science". Stull Rolland. AVP International, University of British Columbia, 2016.

### Bibliografía avanzada

+ “Modeling of Atmospheric Chemistry”. Brasseur G.P & Jacob D.J Cambridge University Press. May 2017.
+ “Fundamentals of Atmospheric Modeling” (2nd edition). Jacobson M.Z. Cambridge University Press. June 2012.

