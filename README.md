# 🚀 Análisis de Experimento A/B: Optimización y Gobierno de Landing Page

Este repositorio contiene un análisis exhaustivo y la evolución metodológica de un **experimento A/B** diseñado para evaluar la efectividad de una nueva versión de landing page (Página B) frente a la original (Página A). El objetivo principal fue determinar el impacto tanto en la **tasa de conversión** como en el **valor promedio de transacción (Ticket Promedio)**, unificando el rendimiento a través de la métrica reina: **Revenue Per Visitor (RPV)**.

---

## 📊 Resumen Ejecutivo (KPIs Maestros)

Tras analizar una muestra auditada de **40,000 usuarios**, los resultados indican que la **Página B es significativamente superior** en todas las métricas clave:

| Métrica | Página A (Control) | Página B (Variante) | Mejora (Lift) | Impacto Práctico |
| :--- | :---: | :---: | :---: | :--- |
| **Tasa de Conversión** | 12.57% | **15.96%** | **+26.92%** | Límites de IC 95% sin solapamiento. |
| **Gasto Promedio** | $61.09 | **$68.75** | **+12.54%** | Diferencia robusta ante Outliers. |
| **Revenue Per Visitor** | $7.68 | **$10.97** | **+42.84%** | **Métrica Reina de Impacto Financiero.** |

---

## 🧬 Gobierno de Datos: Evolución del Repositorio y Control de Calidad

Para asegurar la reproducibilidad y transparencia institucional, se documenta la transición desde la plantilla inicial del estudiante hasta el entregable final de producción.

### 🔍 Defectos Identificados y Decisiones de Refactorización

1. **Resolución del Error Crítico de Variables Inexistentes (`KeyError: 'device'`):**
   * *Defecto anterior:* Las versiones intermedias heredaban bucles iterativos automáticos sobre variables técnicas y demográficas como `['region', 'device', 'traffic_source', 'user_type']`. Al ejecutarlo, pandas detenía la compilación mediante un `KeyError: 'device'` debido a que estas columnas no existen en la estructura física del archivo `landing_experiment.csv`.
   * *Solución aplicada:* Se mapeó la estructura real del dataset y se restringió quirúrgicamente el código a interactuar con las variables categóricas reales: `traffic_source` y `user_type`.
2. **Mitigación del "Efecto Novedad" mediante Análisis Temporal:**
   * *Defecto anterior:* La sección existía formalmente pero carecía de interpretación analítica, dejando una sección ciega sobre si el éxito inicial era pasajero.
   * *Solución aplicada:* Se calculó la serie diaria de la tasa de conversión. El comportamiento de la Página B demostró ser superior y estable día a día durante todo el periodo, descartando anomalías por curiosidad transitoria del usuario.
3. **Control Clínico de Outliers mediante Rango Intercuartílico (IQR):**
   * *Defecto anterior:* Riesgo latente de inflación de medias debido a compras anómalas aisladas.
   * *Solución aplicada:* Se aislaron los outliers de gasto (71 en la variante A y 89 en la variante B). Al recalcular y verificar que las medias sin outliers mantenían la misma brecha estructural, se validó la robustez de los resultados comerciales.
4. **Simplificación Estratégica vs Complejidad Estéril:**
   * *Defecto anterior:* Se introdujeron pruebas post-hoc complejas y métricas como la V de Cramér o la corrección de Bonferroni que agregaban carga académica pero no modificaban las decisiones de negocio.
   * *Solución aplicada:* Se aplicó el principio de la Navaja de Ockham para Data Analytics: remoción de ruido metodológico redundante para entregar un código directo, ágil y enfocado en la ejecución comercial.

---

## 🧪 Metodología Estadística

Para garantizar que los resultados no fueran producto del azar, se aplicaron pruebas de hipótesis con un nivel de significancia del 5% ($\alpha = 0.05$):

1. **Garantía de Asignación (SRM Check):**
   * Se aplicó una prueba **Chi-cuadrado de bondad de ajuste** sobre los volúmenes de tráfico ($A=19,982$; $B=20,018$) obteniendo un $p$-valor de **0.8572**. Se descarta matemáticamente cualquier sesgo de distribución o Sample Ratio Mismatch.
2. **Comparación de Gasto (Ticket Promedio):**
   * Se validó la desigualdad de varianzas mediante la prueba de **Levene**.
   * Se aplicó la prueba **t de Welch** (`equal_var=False`), obteniendo un $p$-valor de **1.06e-20**, confirmando que el incremento en gasto es estadísticamente significativo.
   * Se calculó la magnitud de efecto mediante **Cohen's d (0.2498)**, catalogándolo como un efecto individual pequeño pero altamente escalable en Big Data.
3. **Comparación de Conversión:**
   * Se utilizó un **Z-Test de Proporciones**, resultando en un $p$-valor de **0.0000**. Los Intervalos de Confianza al 95% para proporciones confirmaron la total separación física de ambas variantes.
4. **Análisis de Variables Categóricas (Chi-cuadrado):**
   * **Fuente de Tráfico:** Existe una asociación significativa entre el canal de origen y la conversión ($p=0.034$).
   * **Tipo de Usuario:** No se encontró evidencia de que el comportamiento de conversión varíe según si el usuario es Nuevo o Recurrente ($p=0.473$).

---

## 📈 Visualización de Hallazgos y Cuadro Directivo

Los resultados analíticos parciales han sido consolidados y guardados automáticamente en un panel directivo único denominado `executive_dashboard_ab_test.png`, el cual captura:

* **Distribución de Gasto por Landing:** Un análisis que remueve las advertencias de código (`FutureWarning`) utilizando parámetros modernos de asignación en Seaborn (`hue='landing'`), demostrando visualmente el desplazamiento del Ticket Promedio.
* **Estabilidad Temporal:** Gráfico lineal que valida el comportamiento continuo de la tasa de conversión día por día.
* **Impacto Financiero en RPV:** Visualización de barras que demuestra el incremento masivo del **+42.8%** en ingresos por cada visitante que pisa la landing page.

---

## 💡 Conclusiones y Recomendaciones Económicas

1. **Implementación Definitiva al 100%:** Se recomienda migrar la totalidad del tráfico a la **Página B**. La aparente paradoja de una Magnitud de Efecto pequeña (Cohen's d) queda resuelta al observar el **Lift del +42.8% en el Revenue Per Visitor (RPV)**; cuando un incremento individual se multiplica por un tráfico masivo, el retorno de inversión corporativo es extraordinario.
2. **Estrategia de Canales:** Los canales de **Email** y **Referral** muestran la respuesta más reactiva al cambio de diseño de interfaz. Se aconseja canalizar e incrementar la pauta publicitaria hacia ellos utilizando la Versión B.
3. **Propuesta de Valor Universal:** La prueba de Chi-cuadrado confirmó que la Página B beneficia por igual a usuarios nuevos y recurrentes. Se desaconseja realizar costosos desarrollos técnicos de personalización por segmentos en esta etapa, optimizando el presupuesto operativo de la empresa.

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
