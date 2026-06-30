# 🚀 Análisis de Experimento A/B: Optimización y Gobierno de Landing Page

Este repositorio contiene un análisis exhaustivo y la evolución metodológica de un **experimento A/B** diseñado para evaluar la efectividad de una nueva versión de landing page (Página B) frente a la original (Página A). El objetivo principal fue determinar el impacto tanto en la **tasa de conversión** como en el **valor promedio de transacción (Ticket Promedio)**, unificando el rendimiento a través de la métrica reina: **Revenue Per Visitor (RPV)**.

## 📊 Resumen Ejecutivo (KPIs Maestros Consolidados)

Tras analizar una muestra auditada de **40,000 usuarios**, los resultados indican que la **Página B es significativamente superior** en todas las métricas clave:

| Métrica | Página A (Control) | Página B (Variante) | Mejora (Lift) | Impacto Práctico |
| :--- | :---: | :---: | :---: | :--- |
| **Tasa de Conversión** | 12.57% | **15.96%** | **+26.92%** | Límites de IC 95% sin solapamiento. |
| **Gasto Promedio** | $61.09 | **$68.75** | **+12.54%** | Diferencia robusta ante Outliers. |
| **Revenue Per Visitor** | $7.68 | **$10.97** | **+42.84%** | **Métrica Reina de Impacto Financiero.** |

---

## 🧬 Gobierno de Datos: Evolución del Repositorio y Auditoría de Celdas

Para asegurar la reproducibilidad y la transparencia institucional, se documenta la transición exacta entre los notebooks que integran el historial del repositorio:

### 🔍 Tabla de Linaje de Código y Cambios Técnicos

| Bloque Analítico | `S9 Version_Student_Proyecto_Landing_Experiment.ipynb` | `1_Github_AB_Test_Analysis_Final.ipynb` | `2_AB_Test_Analysis_mejorado.ipynb` | `3_AB_Test_Analysis_v2.ipynb` | `4_Proyecto_Final_AB_Test.ipynb` | Razón de la Refactorización y Mejora Obtenida |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **Carga de Entorno** | Celda 1 | Celda 1 *(Librerías estándar)* | Celda 1 *(Sin cambios)* | Celda 1 *(Añade multipletests)* | Celda 2 *(Configuración estética global, supresión de alertas)* | Profesionaliza el entorno ocultando advertencias de sintaxis y fijando una paleta homogénea (`Set2`). |
| **Control SRM (Muestra)** | No existente | No existente | Celda 4 *(Mapeo plano)* | Celda 4 *(Cálculo Chi² manual)* | Celda 5 *(Validación robusta p=0.8572)* | **Eliminación de sesgo:** Asegura matemáticamente que el ruteo de usuarios fue totalmente balanceado y limpio. |
| **Filtro de Contaminación** | No existente | No existente | No existente | Celda 5 *(Cruce de IDs)* | Celda 6 *(Reporte de duplicados = 0)* | **Garantía de Rigor:** Valida que ningún usuario haya sido expuesto a ambas variantes de manera simultánea. |
| **Efecto Novedad** | No existente | No existente | No existente | Celda 6 *(Eje de tiempo vacío)* | Celdas 7-8 *(Serie diaria + Análisis de estabilidad)* | **Protección de Falsos Positivos:** Confirma que el éxito de B es estable y duradero, no una anomalía inicial. |
| **Análisis de Gasto** | Vacío asignado | Celda 5 *(t-test estándar)* | Celda 6 *(t-test estándar)* | Celda 10-11 *(Levene + t-Welch + MWU)* | Celda 11-13 *(Añade Cohen's d = 0.2498)* | **Precisión Estadística:** Levene detectó varianzas distintas, obligando a cambiar a una robusta **t de Welch**. |
| **Control de Outliers** | No existente | No existente | No existente | Celda 12 *(Filtro estadístico IQR)* | Celda 14-15 *(Comparativa de medias con/sin atípicos)* | **Robustez del Negocio:** Demuestra que la mejora en gasto no se debe a compradores masivos anómalos aislados. |
| **Métrica Reina (RPV)** | No existente | No existente | No existente | Celda 15 *(Cálculo simple)* | Celda 16-18 *(Resolución formal de la Paradoja)* | **Traducción Financiera:** Unifica conversión y ticket promedio para reflejar un aumento directo del **+42.8%** por visita. |
| **Resolución del Error Crítico** | No existente | No existente | Celda 15 *(Detiene ejecución por `KeyError: 'device'`)* | Celda 18 *(Parchado rudimentario)* | Celdas 19-23 *(Mapeo dinámico de variables reales)* | **Estabilidad de Software:** Elimina referencias a columnas muertas inexistentes en el archivo físico del dataset. |
| **Reducción de Ruido** | No existente | No existente | No existente | Celda 24 *(Agrega V de Cramér / Bonferroni)* | Celdas Eliminadas por Diseño | **Navaja de Ockham:** Remoción de sobre-ingeniería matemática que no aportaba valor a la toma de decisiones. |
| **Dashboard Ejecutivo** | Celdas vacías | Gráficos dispersos sin anotaciones | Gráficos individuales con `FutureWarning` | Celdas de dibujo independientes | Celda 26 *(Exportación de panel unificado PNG)* | **Estándar de Production-Ready:** Consolida métricas clave en una única imagen lista para el C-Level. |

---

### 🔍 Análisis de Defectos y Decisiones Clave

1. **Resolución del Error Crítico de Variables Inexistentes (`KeyError: 'device'`):**
   * *Defecto:* `2_AB_Test_Analysis_mejorado.ipynb` heredaba bucles iterativos automáticos sobre variables teóricas como `['region', 'device', 'traffic_source', 'user_type']`. Al ejecutarlo, pandas detenía la compilación mediante un `KeyError` debido a que estas columnas no existen en la estructura física del archivo.
   * *Solución:* En `4_Proyecto_Final_AB_Test.ipynb` se mapeó la estructura real del dataset, restringiendo quirúrgicamente el código a interactuar con las variables categóricas reales: `traffic_source` y `user_type`.
2. **Mitigación del "Efecto Novedad" mediante Análisis Temporal:**
   * *Defecto:* En `3_AB_Test_Analysis_v2.ipynb` la sección existía formalmente pero carecía de interpretación analítica, dejando una sección ciega sobre si el éxito inicial era transitorio.
   * *Solución:* En `4_Proyecto_Final_AB_Test.ipynb` se calculó la serie diaria de la tasa de conversión. El comportamiento de la Página B demostró ser superior y estable día a día durante todo el periodo, descartando anomalías por curiosidad transitoria del usuario.
3. **Control Clínico de Outliers mediante Rango Intercuartílico (IQR):**
   * *Defecto:* Riesgo latente de inflación de medias debido a compras de usuarios anómalos aislados.
   * *Solución:* Se aislaron los outliers de gasto (71 en la variante A y 89 en la variante B). Al recalcular y verificar que las medias sin outliers mantenían la misma brecha estructural, se validó la robustez de los resultados comerciales en el archivo de producción final.

---

## 📈 Visualización de la Evolución de los Gráficos

Para demostrar visualmente la madurez analítica del proyecto en este repositorio, se estructuró la evolución gráfica en tres ejes fundamentales:

### 1. Evolución de la Distribución de Gasto (`img/boxplot_gasto_evolucion.png`)
* **Notebooks anteriores:** En `1_Github_AB_Test_Analysis_Final.ipynb` y `2_AB_Test_Analysis_mejorado.ipynb`, los boxplots eran rudimentarios, carecían de etiquetas claras y generaban advertencias `FutureWarning` constantes debido a parámetros obsoletos en la librería Seaborn.
* **Notebook Final:** En `4_Proyecto_Final_AB_Test.ipynb`, se implementó una vista comparativa limpia usando `hue='landing'`, removiendo advertencias y añadiendo marcas explícitas de la media aritmética junto con el aislamiento estadístico de los outliers calculados por IQR.

### 2. Monitoreo y Control del Sesgo (`img/srm_check_comparison.png`)
* Pasó de ser un conteo ciego de filas a un gráfico de barras balanceado que contrasta las frecuencias observadas vs las teóricas esperadas, desplegando en el título el estadístico de la prueba de Chi-cuadrado ($p = 0.8572$) para evidenciar un entorno experimental perfectamente controlado.

### 3. Visualización del Impacto Financiero Real (`img/rpv_impact_metric.png`)
* Esta gráfica se introdujo exclusivamente en el notebook final de producción para resolver la paradoja del Tamaño de Efecto Pequeño ($d = 0.24$). Al plasmar de forma ejecutiva cómo el Revenue Per Visitor se eleva un **+42.8%**, se simplifica la interpretación de la estadística avanzada en métricas de dinero real para la mesa directiva.

---

## 🧪 Metodología Estadística (Parámetros Finales)

Para garantizar que los resultados no fueran producto del azar, se aplicaron pruebas de hipótesis con un nivel de significancia del 5% ($\alpha = 0.05$):

1. **Garantía de Asignación (SRM Check):** Prueba Chi-cuadrado sobre volúmenes de tráfico ($A=19,982$; $B=20,018$) resultando en un $p$-valor de **0.8572** (Muestra balanceada).
2. **Comparación de Gasto (Ticket Promedio):** Test de Levene (varianzas no homogéneas) seguido por una **t de Welch** (`equal_var=False`), obteniendo un $p$-valor de **1.06e-20** (Confirmado de manera no paramétrica mediante Mann-Whitney U).
3. **Comparación de Conversión:** **Z-Test de Proporciones**, resultando en un $p$-valor de **0.0000**. Los Intervalos de Confianza al 95% para proporciones confirmaron la total separación física de ambas variantes.
4. **Análisis Categórico (Chi-cuadrado):**
   * **Fuente de Tráfico:** Asociación significativa con la conversión ($p=0.034$), liderada por los canales de `Email` y `Ads`.
   * **Tipo de Usuario:** Sin evidencia de asociación ($p=0.473$), confirmando que la Página B es **universalmente superior** para clientes nuevos y recurrentes.

---

## 💡 Conclusiones y Recomendaciones Económicas

1. **Implementación Definitiva al 100%:** Se recomienda migrar la totalidad del tráfico a la **Página B**. El aparente impacto individual pequeño se transforma en un **Lift masivo del +42.8% en el Revenue Per Visitor (RPV)** al multiplicarse por el tráfico a escala de la compañía.
2. **Estrategia de Canales:** Los canales de **Email** y **Ads/Referral** muestran la respuesta más reactiva al cambio de diseño de interfaz. Se aconseja canalizar e incrementar la pauta publicitaria hacia ellos utilizando la Versión B.
3. **Propuesta de Valor Universal:** La prueba de Chi-cuadrado confirmó que la Página B beneficia por igual a usuarios nuevos y recurrentes. Se desaconseja realizar desarrollos técnicos de personalización por segmentos en esta etapa, optimizando el presupuesto operativo de la empresa.

---

## 🛠️ Tecnologías Utilizadas
* **Lenguaje:** Python 3.10+
* **Librerías de Análisis:** Pandas, Numpy, Scipy.stats, Statsmodels
* **Visualización:** Matplotlib, Seaborn

---

## 📂 Estructura del Repositorio

```text
├── 📂 .github/workflows/           # Configuración de Integración Continua (CI)
├── 📂 archive/                      # Historial de iteraciones del proyecto (Linaje)
│   ├── 📓 1_Github_AB_Test_Analysis_Final.ipynb  # Primera versión funcional básica
│   ├── 📓 2_AB_Test_Analysis_mejorado.ipynb      # Intento de mejora con error de índice
│   └── 📓 3_AB_Test_Analysis_v2.ipynb            # Incorporación de pruebas robustas
├── 📂 data/                         # Almacenamiento de sets de datos
│   └── 📄 landing_experiment.csv    # Datos físicos del experimento A/B (40,000 registros)
├── 📂 images/                       # Activos visuales y gráficos exportados para el README
│   ├── 🖼️ boxplot_gasto_evolucion.png  # Comparativa visual de distribución (V1 vs V4)
│   ├── 🖼️ conversion_by_traffic.png    # Eficiencia por canales de adquisición
│   ├── 🖼️ executive_dashboard.png     # Panel consolidado para C-Level
│   └── 🖼️ user_type_interaction.png   # Interacción universal del tipo de usuario
├── 📂 src/                          # Scripts de producción y utilidades auxiliares
│   └── 📄 utils.py                 # Funciones estadísticas modulares
├── 📄 .gitignore                    # Exclusión de entornos virtuales y cachés (.ipynb_checkpoints)
├── 📄 4_Proyecto_Final_AB_Test.ipynb # [Entregable de Producción] Versión óptima final limpia
├── 📄 LICENSE                       # Licencia de uso del código
├── 📄 README.md                     # Documentación principal del repositorio (Este archivo)
└── 📄 S9 Version_Student_Proyecto_Landing_Experiment.ipynb # Plantilla académica original vacía
```



---
## Autor

David Germán Ramos Rodríguez
[LinkedIn](https://www.linkedin.com/in/david-g-ramos/) |
[Portfolio](https://dataanalist-davidgramos.github.io/mi-sitio-web/)
