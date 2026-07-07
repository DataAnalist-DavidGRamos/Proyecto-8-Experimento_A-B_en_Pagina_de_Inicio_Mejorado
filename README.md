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

# Fijamos la semilla para que el dataset sea idéntico en cada ejecución
np.random.seed(42)
n_clientes = 2000

id_orden = [f"ORD-{np.random.randint(10000, 99999)}" for _ in range(n_clientes)]
edad     = np.random.randint(18, 90, size=n_clientes)

# Saldo de cuenta simulado. La distribución normal puede producir negativos;
# eso lo corregimos en la Fase 4 como un error de dominio, no como outlier estadístico
balance  = np.random.normal(50000, 25000, size=n_clientes)

# p= controla qué probabilidad tiene cada opción al muestrear
productos   = np.random.choice([1, 2, 3, 4], size=n_clientes, p=[0.4, 0.45, 0.1, 0.05])
miembro_act = np.random.choice([0, 1],        size=n_clientes, p=[0.4, 0.6])

# Mezclamos formatos para simular entradas manuales inconsistentes
tarjeta = np.random.choice(
    ['SÍ', 'NO', 'si', 'no', '?', 'N/A'], size=n_clientes,
    p=[0.5, 0.3, 0.1, 0.05, 0.03, 0.02]
)

# Nombres de ciudad con errores de codificación y espacios extra
ciudades_sucias = [
    'Bogotá', 'Bogota', 'Bogot√±',
    'Medellín', 'Medellin', 'Medell√edn',
    'Ciudad de M√©xico', 'CDMX', 'Monterrey  '
]
ciudad     = np.random.choice(ciudades_sucias, size=n_clientes)
fecha_alta = np.random.choice(
    ["2024-10-15", "15/10/2024", "Oct 15, 2024", "2024/10/15"],
    size=n_clientes
)

# La probabilidad de churn sube si el cliente es mayor de 55 o tiene un solo producto
prob_churn = 0.1 + (edad > 55)*0.2 + (productos == 1)*0.15 - (miembro_act == 1)*0.15
prob_churn = np.clip(prob_churn, 0.05, 0.95)
churn      = np.random.binomial(1, prob_churn)

df_sucio = pd.DataFrame({
    'id_orden': id_orden, 'fecha_alta': fecha_alta, 'ciudad': ciudad,
    'edad': edad, 'balance': balance, 'num_productos': productos,
    'miembro_activo': miembro_act, 'tiene_tarjeta': tarjeta, 'churn': churn
})

# Inyectamos nulos. Cada .sample() tiene su propio random_state para que
# el resultado no dependa del estado global del generador — si alguien agrega
# código antes de estas líneas, el dataset no cambia
df_sucio.loc[df_sucio.sample(frac=0.03, random_state=42).index, 'balance'] = np.nan
df_sucio.loc[df_sucio.sample(frac=0.02, random_state=43).index, 'edad']    = np.nan

# -9999.0 es la bandera que usan algunos sistemas cuando el campo no tiene valor
df_sucio.loc[df_sucio.sample(frac=0.01, random_state=44).index, 'balance'] = -9999.0

# Duplicamos 30 registros para simular registros repetidos
duplicados = df_sucio.sample(n=30, random_state=42)
df = pd.concat([df_sucio, duplicados], ignore_index=True)

print(f"Dataset generado: {df.shape[0]} filas × {df.shape[1]} columnas")
---

### 🔍 Análisis de Defectos y Decisiones Clave

1. **Resolución del Error Crítico de Variables Inexistentes (`KeyError: 'device'`):**
   * *Defecto:* El archivo `<a href="./notebooks/2_AB_Test_Analysis_mejorado.ipynb">2_AB_Test_Analysis_mejorado.ipynb</a>` heredaba bucles iterativos automáticos sobre variables teóricas como `['region', 'device', 'traffic_source', 'user_type']`. Al ejecutarlo, pandas detenía la compilación mediante un `KeyError` debido a que estas columnas no existen en la estructura física del archivo.
   * *Solución:* En `<a href="./4_Proyecto_Final_AB_Test.ipynb">4_Proyecto_Final_AB_Test.ipynb</a>` se mapeó la estructura real del dataset, restringiendo quirúrgicamente el código a interactuar con las variables categóricas reales: `traffic_source` y `user_type`.
2. **Mitigación del "Efecto Novedad" mediante Análisis Temporal:**
   * *Defecto:* En `<a href="./notebooks/3_AB_Test_Analysis_v2.ipynb">3_AB_Test_Analysis_v2.ipynb</a>` la sección existía formalmente pero carecía de interpretación analítica, dejando una sección ciega sobre si el éxito inicial era transitorio.
   * *Solución:* En `<a href="./4_Proyecto_Final_AB_Test.ipynb">4_Proyecto_Final_AB_Test.ipynb</a>` se calculó la serie diaria de la tasa de conversión. El comportamiento de la Página B demostró ser superior y estable día a día durante todo el periodo, descartando anomalías por curiosidad transitoria del usuario.
3. **Control Clínico de Outliers mediante Rango Intercuartílico (IQR):**
   * *Defecto:* Riesgo latente de inflación de medias debido a compras de usuarios anómalos aislados.
   * *Solución:* Se aislaron los outliers de gasto (71 en la variante A y 89 en la variante B). Al recalcular y verificar que las medias sin outliers mantenían la misma brecha estructural, se validó la robustez de los resultados comerciales en el archivo de producción final.

---

## 📈 Visualización de la Evolución de los Gráficos

Para demostrar visualmente la madurez analítica del proyecto en este repositorio, se estructuró la evolución gráfica en tres ejes fundamentales:

### 1. Evolución de la Distribución de Gasto (`images/boxplot_gasto_evolucion.png`)
* **Notebooks anteriores:** En `<a href="./notebooks/1_Github_AB_Test_Analysis_Final.ipynb">1_Github_AB_Test_Analysis_Final.ipynb</a>` y `<a href="./notebooks/2_AB_Test_Analysis_mejorado.ipynb">2_AB_Test_Analysis_mejorado.ipynb</a>`, los boxplots eran rudimentarios, carecían de etiquetas claras y generaban advertencias `FutureWarning` constantes debido a parámetros obsoletos en la librería Seaborn.
* **Notebook Final:** En `<a href="./4_Proyecto_Final_AB_Test.ipynb">4_Proyecto_Final_AB_Test.ipynb</a>`, se implementó una vista comparativa limpia usando `hue='landing'`, removiendo advertencias y añadiendo marcas explícitas de la media aritmética junto con el aislamiento estadístico de los outliers calculados por IQR.

### 2. Monitoreo y Control del Sesgo (`images/srm_check_comparison.png`)
* Pasó de ser un conteo ciego de filas a un gráfico de barras balanceado que contrasta las frecuencias observadas vs las teóricas esperadas, desplegando en el título el estadístico de la prueba de Chi-cuadrado ($p = 0.8572$) para evidenciar un entorno experimental perfectamente controlado.

### 3. Visualización del Impacto Financiero Real (`images/rpv_impact_metric.png`)
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
├── 📂 notebooks/                      # Historial de iteraciones del proyecto (Linaje)
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
