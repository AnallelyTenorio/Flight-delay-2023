# Flight-delay-2023
Proyecto de curso SkillupData de Laboratoria

# Informe Detallado del Análisis de Retrasos y Cancelaciones de Vuelos

## Resumen Ejecutivo

Este informe presenta un análisis exploratorio y segmentado de los datos de vuelos de 2023 con el objetivo de identificar patrones, causas y rutas con mayor impacto en los retrasos y cancelaciones. Los hallazgos clave incluyen:

*   Una baja tasa general de cancelaciones y desvíos, con el clima como la causa principal de las cancelaciones.
*   Los retrasos en la llegada son más frecuentes que las cancelaciones, siendo la "Aeronave Tarde" y las causas atribuidas a la "Aerolínea" las que acumulan la mayor cantidad de minutos de retraso.
*   Se identifican aerolíneas y aeropuertos con mayores tasas de retraso y volumen de vuelos, lo que permite enfocar los esfuerzos de mejora.
*   El análisis por ruta revela corredores aéreos específicos que experimentan una alta frecuencia y severidad de retrasos.

Estos resultados proporcionan una base sólida para comprender los factores que contribuyen a la puntualidad de los vuelos y pueden guiar la toma de decisiones operativas y estratégicas para mitigar los retrasos y mejorar la experiencia del pasajero.

Resumen del estado general de los vuelos:
------------------------------
Total de vuelos: 538,837

Conteo por categoría:

*   Operados y No Desviados (A tiempo o antes): 324,622 (60.24%)
*   Operados y No Desviados (Retrasados a la llegada): 202,575 (37.59%)
*    Cancelados: 10,295 (1.91%)
*   Desviados: 1,345 (0.25%)




Nota: Los porcentajes se basan en el total de vuelos.

<img width="886" height="530" alt="image" src="https://github.com/user-attachments/assets/7a6a78f7-00aa-4284-be6f-975d7eaadf1d" />

## Análisis de Retrasos en Vuelos Operados

Esta sección se centra en los vuelos que no fueron cancelados ni desviados, pero que experimentaron retrasos a la llegada (`ARR_DELAY > 0`). Analizamos las contribuciones de las diferentes causas de retraso (`DELAY_DUE_...`) a los minutos totales de retraso y al número de vuelos afectados.

<img width="897" height="528" alt="image" src="https://github.com/user-attachments/assets/8bb3396c-904f-426a-8824-0321c4fc8211" />
<img width="899" height="523" alt="image" src="https://github.com/user-attachments/assets/48b2b7c5-ad82-4b5f-be3e-ad4dbf8330a9" />

Recordatorio de la interpretación de las causas de retraso:
- DELAY_DUE_CARRIER: Aerolínea
- DELAY_DUE_WEATHER: Clima
- DELAY_DUE_NAS: Sistema Nacional del Espacio Aéreo
- DELAY_DUE_SECURITY: Seguridad
- DELAY_DUE_LATE_AIRCRAFT: Aeronave Tarde
- DELAY_DUE_UNKNOWN: Desconocido

## Análisis por Aerolínea

Esta sección examina el rendimiento de cada aerolínea en términos de volumen de vuelos, tasas de cancelación, desvío y, principalmente, retrasos. Identificamos las aerolíneas con el mayor y menor porcentaje de vuelos retrasados para comprender mejor su puntualidad operativa.
<img width="900" height="532" alt="image" src="https://github.com/user-attachments/assets/06f74e5f-eff9-4887-a875-8eb93f48e634" />
<img width="899" height="532" alt="image" src="https://github.com/user-attachments/assets/6a25d156-6ba8-4796-b19e-b05de63e8a03" />

## Análisis por Aeropuerto

Esta sección agrupa los datos por aeropuerto de origen (`ORIGIN`) y destino (`DEST`) para identificar aquellos con mayor volumen de vuelos, mayores tiempos de rodaje (TAXI_OUT y TAXI_IN) y, especialmente, los que presentan mayores porcentajes de retraso en salidas y llegadas.

<img width="898" height="529" alt="image" src="https://github.com/user-attachments/assets/2196d5bf-e2f6-46a7-8edc-d36edf37987e" />
<img width="897" height="530" alt="image" src="https://github.com/user-attachments/assets/3575842a-6906-45ec-8c04-8a1f3201544d" />

 ## Análisis por Ruta

Esta sección profundiza en el rendimiento de rutas aéreas específicas, identificando aquellas que presentan una mayor frecuencia y severidad de retrasos. Analizamos métricas clave a nivel de par origen-destino para resaltar los corredores aéreos que podrían requerir una atención especial.

**Criterios de análisis por ruta.**  
- Solo se consideran rutas con **≥100 vuelos** (robustece los promedios).  
- **Frecuencia**: % de vuelos con `ARR_DELAY ≥ 15 min`.  
- **Severidad**: `avg_pos_arr_delay` (minutos **solo** en vuelos retrasados).  
- Umbrales del cuadrante: **40%** (frecuencia) y **60 min** (severidad).

### Rutas con Mayor Frecuencia de Retrasos
<img width="885" height="530" alt="image" src="https://github.com/user-attachments/assets/5161480e-51a8-4b42-b055-b7d03a920e56" />
**Figura 1. Top rutas por FRECUENCIA de retraso (ARR_DELAY ≥ 15 min).**  
Muestra las rutas donde es **más probable** que un vuelo llegue con demora. Estas rutas representan corredores con **problemas recurrentes de puntualidad**, por lo que son candidatas a acciones de mejora operativa.

### Rutas con Mayor Severidad de Retrasos
<img width="885" height="528" alt="image" src="https://github.com/user-attachments/assets/a6ce30de-aaaa-4965-8357-268a10f039a0" />
**Figura 2. Top rutas por SEVERIDAD del retraso (avg_pos_arr_delay).**  
Indica dónde, **cuando ocurre el retraso**, la demora es **más prolongada**. Señala posibles **cuellos de botella** (rotaciones, puertas, congestión) que amplifican el tiempo de recuperación.

<img width="713" height="631" alt="image" src="https://github.com/user-attachments/assets/fc919096-715c-4816-a551-15c7d9be7ed3" />
### Interpretación de la Figura 3

La Figura 3 se construye con rutas de **≥100 vuelos** y define los cuadrantes con cortes en **40%** de frecuencia y **60 min** de severidad.
El **cuadrante de Frecuencia vs Severidad por Ruta (≥100 vuelos)**, que permite visualizar la relación entre la **probabilidad de retraso** y la **duración promedio de dichos retrasos**.

Cada punto representa una ruta aérea (ORIGIN–DEST), y el tamaño del punto indica el **volumen total de vuelos**.  
Las líneas punteadas dividen el gráfico en cuatro cuadrantes según los umbrales definidos:

- **Eje X (frecuencia)**: porcentaje de vuelos con retraso (ARR_DELAY ≥ 15 min).  
- **Eje Y (severidad)**: minutos promedio de retraso en vuelos retrasados (avg_pos_arr_delay).  

Se destacan las rutas **AMA–DFW**, **FAR–DEN** y **SRQ–CLT**, ubicadas en el **cuadrante superior derecho**, que combina **alta frecuencia y alta severidad de retrasos**, lo que las posiciona como **corredores aéreos críticos** dentro del sistema.  
Estas rutas deben considerarse prioritarias para la implementación de acciones correctivas, ya que impactan tanto en el número de vuelos afectados como en la magnitud de los retrasos.

La mayoría de las rutas se agrupan en el **cuadrante inferior izquierdo**, con retrasos menos frecuentes y de menor duración, reflejando un **comportamiento operativo estable** en la mayor parte de la red.  
El cuadrante superior izquierdo, por su parte, muestra rutas donde los retrasos son poco frecuentes, pero **muy prolongados cuando ocurren**, mientras que el inferior derecho representa rutas con **retrasos frecuentes pero leves**.

En conjunto, esta visualización permite **priorizar rutas según su impacto** combinando tres dimensiones: frecuencia, severidad y volumen de vuelos.

<img width="716" height="104" alt="image" src="https://github.com/user-attachments/assets/3b1ccb2e-8f8e-4a7a-a538-055a41450c16" />

**Tabla A.1. Rutas “rojas” (alta frecuencia y alta severidad).**  
Listado de rutas con **probabilidad alta de retraso (ARR_DELAY ≥ 15 min)** y **demora prolongada cuando ocurre**.  
Incluye una estimación de **vuelos retrasados** y una métrica de **impacto** (frecuencia × severidad × volumen) para priorización operativa.

## 🧩 Conclusiones y Recomendaciones

Basado en el análisis exploratorio y segmentado de los datos de vuelos de 2023, se pueden extraer las siguientes conclusiones y considerar las siguientes recomendaciones:

---

### ✈️ Conclusiones Clave

**Panorama general.**  
En 2023 predominaron los vuelos operados sin desvío; sin embargo, **~38% de los vuelos llegaron con retraso**, lo que refleja un área de oportunidad relevante en la puntualidad del sistema aéreo.

**Causas de retraso.**  
En minutos totales,las mayores contribuciones provienen de **Aeronave Tarde** (`DELAY_DUE_LATE_AIRCRAFT`) y **Aerolínea** (`DELAY_DUE_CARRIER`) …
, lo que apunta a factores operativos internos como principal origen de las demoras. El **Clima**, aunque menos frecuente, genera los retrasos más severos cuando ocurre.

**Aerolíneas.**  
Se observan **brechas claras de desempeño en puntualidad**: aerolíneas como **Hawaiian** y **Frontier** concentran los mayores porcentajes de vuelos retrasados, mientras que **Southwest** y **Delta** se posicionan entre las más consistentes.

**Aeropuertos.**  
Como origen, los grandes hubs (ATL, DEN, DFW, ORD…) concentran la mayor cantidad de operaciones, mientras que algunos destinos como **Pago Pago (TT)**, **Lincoln (NE)** y **North Bend (OR)** presentan **tasas de retraso excepcionalmente altas**, probablemente relacionadas con condiciones meteorológicas, limitaciones de infraestructura o restricciones operativas locales.

**Rutas con mayor frecuencia de retraso (ARR_DELAY ≥ 15 min).**  
Destacan varios pares origen–destino con **más de 100 vuelos** y tasas de retraso cercanas o superiores a **45%**, como **BQN–MCO**, **SFO–HNL**, **LAX–ASE**, **DEN–ASE** y **SLC–JFK**. Estos corredores representan **zonas críticas de alta probabilidad de retraso**, donde la puntualidad es un desafío recurrente.

**Rutas con mayor severidad del retraso (flights_total > 100).**  
El nuevo filtrado permite identificar rutas con un número suficiente de vuelos para un análisis robusto. En este grupo, destacan **AMA–DFW**, **FAR–DEN**, **DEN–JFK** y **SRQ–CLT**, con **promedios de demora superiores a 40 minutos** y, en algunos casos, **retrasos medios por vuelo retrasado (avg_pos_arr_delay)** que superan los **90 minutos**.  
Estos resultados evidencian **cuellos de botella operativos y de coordinación**, probablemente vinculados con congestión en aeropuertos hub, rotación de aeronaves y tiempos de conexión ajustados.

**Relación frecuencia–severidad.**  
El contraste entre ambas métricas muestra que **no todas las rutas con alta frecuencia presentan alta severidad**, y viceversa. Sin embargo, los corredores donde **ambos factores coinciden** representan los puntos de mayor impacto operativo y deben ser priorizados para acciones correctivas.

---

### 💡 Recomendaciones

**1. Focalizar esfuerzos en rutas críticas.**  
- Priorizar la atención en rutas con alta severidad y volumen significativo, como **AMA–DFW**, **FAR–DEN**, **SRQ–CLT** y **ATL–PNS**.  
- Evaluar la **asignación de flota, buffers de programación y coordinación de turnos** en estos corredores para reducir los retrasos acumulados.

**2. Optimización de operaciones y rotación de aeronaves.**  
- Implementar monitoreo de **“Aeronave Tarde”** para identificar tramos que propagan demoras en cadena.  
- Reajustar **tiempos de rotación** y revisar las políticas de despacho en aeropuertos con alta densidad de tráfico.

**3. Análisis complementarios y monitoreo continuo.**  
- Crear un **cuadrante Frecuencia–Severidad** para priorizar rutas según su impacto.  
- Incorporar variables **temporales (mes, día, franja horaria)** para identificar patrones estacionales y congestión en horas pico.  
- Medir la **dispersión de retrasos (percentiles P90 y P95)** para detectar rutas con alta variabilidad operativa.

**4. Coordinación interinstitucional.**  
- Establecer **mesas de trabajo con aerolíneas y aeropuertos** de mayor incidencia para diseñar planes de mejora de puntualidad.  
- Compartir indicadores clave (minutos promedio, causas por categoría, porcentaje de vuelos a tiempo) y monitorear resultados de forma trimestral.

**5. Enriquecer la base analítica.**  
- Integrar datos de **meteorología, tráfico aéreo y capacidad de pista** para modelar las causas de retraso con mayor precisión.  
- Desarrollar dashboards interactivos que faciliten el **seguimiento en tiempo real** de los indicadores de puntualidad.

---

> **En síntesis**, el análisis confirma que los retrasos en 2023 se deben principalmente a **factores operativos internos**, especialmente la **Aeronave Tarde** y la **gestión de las aerolíneas**, con rutas específicas donde la frecuencia y la severidad convergen.  
> Concentrar esfuerzos en estos corredores prioritarios, mejorar la coordinación de flotas y ajustar la programación de operaciones son pasos clave para **reducir los minutos promedio de demora y mejorar la experiencia del pasajero**.

# Links de interes
Presentación
https://docs.google.com/presentation/d/1yEfJ--k30hbx9kNJ_JyDdGUICSFpCpVoMSXVRQKFTYU/edit?usp=sharing
Notebook
https://colab.research.google.com/drive/1o2oqR70UVN0jXKHvzeRgFGkTk_3gQoVt?usp=sharing











