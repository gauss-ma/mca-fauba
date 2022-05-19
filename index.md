---
nav_exclude: true
has_children: false
---

# Modelado de la Calidad del Aire

Material didáctico del curso de *Modelado de la Calidad del Aire* (MCA), dictado en la Facultad de Agronomía, Universidad de Buenos Aires.

---

AVISOS! 
{: .label .label-red }
+ Empezamos el viernes 20/5, 18hs en el pabellon **UBALLES** centro de computos.

---


### Docente responsable
+ Bormioli, Marcelo G.

### Docentes a cargo
+ Espada, Ramiro A.
+ Medrano, Luciano M.

### Cronograma

|Clase| Fecha | Teórica | Práctica |   TP  |
|:---|:-----:|:--------|:---------:|:-----:|
| 1  | 13/5  | **NO HAY CLASE**                                                         |     -      | - |
| 2  | 20/5  | [Contexto](./teo/c0a.html) & [Ecuación de transporte](./teo/c0a.html)  |     -      | - |
| 3  | 27/5  | [Modelos gaussianos](./teo/c1b.html) & [Fundamentos SCREEN3            ](./teo/c2.html)| [Screen3](./tut/screen3.html) |Explicación [TP 1](./tps/tp1.html)   |
| 4  | 03/6  | [Meteorología](./teo/c3.html)  |  |  Explicación [TP 2](./tps/tp2.html)   |
| 6  | 10/6  | [AERMET](./teo/c4a.html) & [AERMOD](./teo/c6.html) |  [aermet](./tut/aermet.html) &  [aermod](./tut/aermod.html)  ||
| 5  | 17/6  | **FERIADO NACIONAL**                             | -                                  | Entrega **TP1**                      |
| 7  | 24/6  | **AERMAP** y **BPIP**                            |                                    | Trabajo sobre [TP 2](./tps/tp2.html) |
| 8  | 01/7  | Estimación de Emisiones                          | [Posprocesamiento](./tut/pos.html) | Trabajo sobre [TP 2](./tps/tp2.html) |
| 9  | 08/7  | *Exposición de TP2*                              | -                                  | Trabajo sobre [TP 2](./tps/tp2.html) |
| 10 | 15/7  | *Evaluación integradora*                         | -                                  | Entrega **TP2**                      | 


### Lugar y horario
El curso se dicta en el Aula **UTI UBALLES** (pabellón Uballes), los viernes de 18 a 21 horas.


### Requisitos de aprobación:

El  curso se aprueba con:
- una asistencia mayor o igual al 75%,
- y nota final promedio igual o mayor que 4 (cuatro).

Dicha nota final es la resultante del promedio ponderado según se detalla a continuación
(equivalente a haber alcanzado el 60% de los objetivos y conocimientos).

| 25% | TP 1				|
| 50% | TP 2 + Informe + exposición     |
| 25% | Evaluación final integradora    |

El TP2 (abarcador del núcleo del curso) consta en realizar una presentación oral grupal y luego el
informe final. Durante la presentación oral se deberá defender (aprox. 15 min) con preguntas y/o comentarios, donde se evaluará a cada integrante del grupo con preguntas conceptuales sencillas sobre la realización del trabajo. Esto implica que cada integrante del grupo debe tener cabal conocimiento de lo realizado.

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
+ "Guía metodológica para la evaluación del impacto ambiental atmosférico". Laura Dawidowski, Darío Gómez y Silvia Reich. Honorable Cámara de Diputados de La Nación.
+ "Calidad del aire - Monitoreo y modelado de contaminantes atmosféricos. Efectos en la salud pública" Porta, Andrés; Yanina Sanchez; Esteban Colman Lerner. UNLP, 2018.
+ Resolución 559-19 OPDS-Anexo III Instructivo para la aplicación de modelos de difusión atmosférica a efluentes gaseosos. 

### Bibliografía complementaria

+ "Introduction to Atmospheric Chemistry". Jacob D.J. Princeton University Press, 1999.
+ "Practical Meteorology: An Algebra-based Survey of Atmospheric Science". Stull Rolland. AVP International, University of British Columbia, 2016.

### Bibliografía avanzada

+ “Modeling of Atmospheric Chemistry”. Brasseur G.P & Jacob D.J Cambridge University Press. May 2017.
+ “Fundamentals of Atmospheric Modeling” (2nd edition). Jacobson M.Z. Cambridge University Press. June 2012.
