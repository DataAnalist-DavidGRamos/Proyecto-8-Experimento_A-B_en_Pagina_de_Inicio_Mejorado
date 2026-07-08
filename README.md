# 📊 Análisis y Corrección del Experimento: [A/B Test en la Página de Inicio](https://github.com/DataAnalist-DavidGRamos/Proyecto-8-Experimento_A-B_en_Pagina_de_Inicio-)

El objetivo de este proyecto fue hacer una revisión a fondo y limpiar el análisis de un experimento que se hizo en nuestra página de inicio. Queríamos evaluar si la nueva propuesta de diseño (**Página B**) realmente funciona mejor que la versión actual (**Página A**). Para estar completamente seguros, revisamos que el flujo de usuarios estuviera bien repartido, medimos cuánta gente compró (conversión), cuánto dinero gastaron en promedio y, lo más importante, calculamos cuánto dinero extra nos dejó cada visita que entró al sitio (**Ingreso por Visitante o RPV**).

---

## 📊 Resumen para Tomar Decisiones (Resultados Clave)

Después de auditar la información de **40,000 usuarios**, los números son claros: **la Página B es la ganadora indiscutible** y superó a la versión anterior en todo:

| Qué medimos | Página A (Diseño Actual) | Página B (Diseño Nuevo) | Qué tanto mejoró (Mejora) | Qué significa esto en la práctica |
| :--- | :---: | :---: | :---: | :--- |
| **Gente que compró (Conversión)** | 12.57% | **15.96%** | **+26.92%** | El aumento es real y no fue por casualidad o suerte. |
| **Gasto Promedio por Cliente** | $61.09 | **$68.75** | **+12.54%** | Los clientes no solo compraron más, sino que gastaron más dinero. |
| **Ganancia por cada Visita (RPV)** | $7.68 | **$10.97** | **+42.83%** | **La métrica más importante: nos dice el impacto real en dinero.** |

---

## 🧬 Organización del Trabajo: Evolución de los Archivos y Cambios

Para que cualquiera pueda revisar cómo fuimos construyendo el proyecto paso a paso, aquí dejamos el orden y los cambios que se hicieron en cada uno de los archivos del repositorio:

### 🔍 Tabla de Linaje de Código y Cambios Técnicos

| Bloque Analítico | [S9_Version_Student.ipynb](./S9%20Version_Student_Proyecto_Landing_Experiment.ipynb) | [1_Github_AB_Test_Analysis_Final.ipynb](./notebooks/1_Github_AB_Test_Analysis_Final.ipynb) | [2_AB_Test_Analysis_mejorado.ipynb](./notebooks/2_AB_Test_Analysis_mejorado.ipynb) | [3_AB_Test_Analysis_v2.ipynb](./notebooks/3_AB_Test_Analysis_v2.ipynb) | [4_Proyecto_Final_AB_Test.ipynb](./4_Proyecto_Final_AB_Test.ipynb) | Razón de la Refactorización y Mejora Obtenida &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
| :--- | :---: | :---: | :---: | :---: | :---: | :----------------------------------------------------------------------------------------------------------------------- |
| **Preparación** | Celda 1 | Celda 1<br>*(Librerías básicas)* | Celda 1<br>*(Sin cambios)* | Celda 1<br>*(Herramientas extra)* | Celda 3<br>*(Diseño visual limpio y sin alertas molestas)* | Deja las bases listas, limpia la pantalla de errores visuales y unifica los colores de las gráficas. |
| **Reparto de Usuarios** | No existente | No existente | Celda 4<br>*(Revisión por encima)* | Celda 4<br>*(Cálculo manual)* | Celda 8<br>*(Validación definitiva)* | **Garantía de equilibrio:** Nos asegura que el sistema repartió a los usuarios mitad y mitad de forma justa (SRM p=0.8572). |
| **Filtro de Contaminación** | No existente | No existente | No existente | Celda 5<br>*(Cruce de usuarios)* | Celda 8<br>*(Reporte de limpiezas = 0)* | **Garantía de limpieza:** Confirma que ningún usuario vio las dos páginas al mismo tiempo para no alterar los datos. |
| **Efecto Novedad** | No existente | No existente | No existente | Celda 6<br>*(Eje de fechas en blanco)* | Celdas 15-17<br>*(Ventas día por día)* | **Evita falsas alarmas:** Asegura que el éxito de la Página B fue constante todos los días y no solo por la novedad del estreno. |
| **Análisis de Gasto** | Vacío asignado | Celda 5<br>*(Comparativa básica)* | Celda 6<br>*(Comparativa básica)* | Celda 10-11<br>*(Ajuste por diferencias)* | Celda 23-28<br>*(Cálculo del impacto final)* | **Matemáticas precisas:** Se adaptaron los cálculos al notar que el comportamiento del gasto variaba mucho entre grupos (t de Welch). |
| **Control de Compras Altas** | No existente | No existente | No existente | Celda 12<br>*(Filtro de valores raros)* | Celda 25-29<br>*(Comparativa antes y después)* | **Datos realistas:** Demuestra que los buenos resultados son generales y no se deben a un par de compradores exageradamente ricos (Outliers IQR). |
| **Métrica Reina (RPV)** | No existente | No existente | No existente | Celda 15<br>*(Cálculo básico)* | Celda 35-37<br>*(Resolución de la paradoja)* | **Traducción a dinero:** Une las ventas y el gasto en un solo dato para ver el impacto económico real por visita (+42.83%). |
| **Solución de Errores** | No existente | No existente | Celda 15<br>*(Fallo que congelaba el código)* | Celda 18<br>*(Parche provisional)* | Celdas 21-22<br>*(Corrección definitiva de nombres)* | **Estabilidad:** Corrige el problema de raíz cambiando los nombres de las columnas que hacían que el programa fallara. |
| **Limpieza de Código** | No existente | No existente | No existente | Celda 24<br>*(Cálculos matemáticos de más)* | Celdas Eliminadas por Diseño | **Simplicidad:** Quitamos fórmulas excesivamente teóricas que no ayudaban en nada a tomar decisiones de negocio. |
| **Panel para Dirección** | Celdas vacías | Gráficos desordenados y sin textos | Gráficos individuales con alertas | Gráficos separados | Celda 46<br>*(Exportación de panel completo en imagen)* | **Listo para usar:** Agrupa las gráficas clave en una sola imagen limpia y profesional para presentar en juntas. |

---

### 🔍 Problemas Encontrados y Cómo los Solucionamos

1. **Reparación del error que congelaba el programa:**
   * *El problema:* El archivo anterior intentaba buscar información usando nombres de columnas en inglés que no existían en la base de datos real (como buscar la palabra `device` cuando en el archivo real estaba escrito en español como `dispositivo`). Esto hacía que el programa se detuviera por completo con un mensaje de error.
   * *La solución:* Ajustamos el código para que lea perfectamente el archivo real, usando las palabras correctas y limitándolo a analizar los datos categóricos reales que sí tenemos a la mano (`traffic_source` y `user_type`).
2. **Controlar el "Efecto Novedad" revisando el paso de los días:**
   * *El problema:* A veces, un diseño nuevo parece exitoso al principio simplemente porque a la gente le da curiosidad hacer clic, pero con los días el interés cae. En las pruebas anteriores no se explicaba si esto estaba pasando.
   * *La solución:* Analizamos el comportamiento de las ventas día por día durante las 4 semanas que duró el experimento. El nuevo diseño se mantuvo arriba y estable todo el tiempo, lo que demuestra que su éxito es real y permanente.
3. **Manejo de compradores exageradamente altos (Outliers):**
   * *El problema:* Si una sola persona entra y compra una cantidad exagerada de dinero, puede alterar el promedio y hacernos creer que la página es un éxito cuando en realidad fue un golpe de suerte.
   * *La solución:* Identificamos y separamos las compras "raras" o fuera de lo común usando el método de Rango Intercuartílico (IQR) aislando 71 casos en el grupo A y 89 en el grupo B. Al volver a calcular los promedios sin ellos (A: \$58.27 | B: \$65.88), la nueva página seguía siendo igual de ganadora, lo que demuestra que el resultado es sólido.

---

## 📈 Evolución de las Gráficas y Reportes Visuales

Mejoramos las imágenes y reportes visuales a lo largo del proyecto para que la información se entienda a primera vista:

### 1. Evolución de la Distribución de Gasto
![Evolución de la Distribución de Gasto](images/boxplot_gasto_evolucion.png)
* *Antes:* Las gráficas eran muy básicas, no tenían explicaciones claras y el programa arrojaba advertencias de código obsoleto.
* *Ahora:* Diseñamos una vista limpia que compara ambos grupos directamente, marca visualmente dónde está el promedio real y limpia los datos exagerados para no confundir al lector.

### 2. Comportamiento de Ventas por Canal de Tráfico
![Tasa de Conversión por Canal de Tráfico](images/conversion_by_traffic.png)
* *Antes:* Se usaban barras que solo mostraban el total de personas, haciendo imposible comparar qué canal funcionaba mejor.
* *Ahora:* Muestra los porcentajes reales de éxito de cada canal y destaca visualmente que las estrategias de **Email** y **Anuncios (Ads)** son las más potentes, confirmando a la vez que los canales se distribuyeron de manera equitativa entre los grupos ($p = 0.3119$).

### 3. Éxito según el Tipo de Usuario
![Tasa de Conversión por Tipo de Usuario](images/user_type_interaction.png)
* *Antes:* Gráficas acumuladas difíciles de leer y sin los números de los porcentajes a la vista.
* *Ahora:* Muestra de forma directa cómo reaccionan los usuarios nuevos y los que ya nos conocen. Los datos confirman que la nueva página funciona mejor para ambos grupos por igual ($p = 0.7966$), por lo que no hace falta crear diseños personalizados para cada uno.

### 4. Panel de Control Unificado (Listo para Presentaciones)
![Dashboard Ejecutivo Consolidado](images/executive_dashboard.png)
* *Ahora:* Creamos un panel completo que junta las 6 gráficas más importantes en una sola imagen. Es ideal para enviarlo directamente al equipo directivo o usarlo en presentaciones de negocio sin tener que explicar líneas de código.

---

## 🧪 Pruebas que Aseguran el Resultado (Método de Trabajo)

Para garantizar que nadie tomara decisiones basadas en un golpe de suerte, validamos matemáticamente los datos:

1. **Verificación de Muestras (SRM Check):** Confirmamos que los usuarios se dividieron de forma casi perfecta ($A = 19,982$ frente a $B = 20,018$), con un p-valor de **0.8572**, asegurando que el experimento es justo y equilibrado.
2. **Comparación de lo que Gastan (Ticket Promedio):** Confirmamos mediante una prueba **t de Welch** ($p < 0.001$) y una prueba no paramétrica **Mann-Whitney U** que el aumento en el dinero que gastan los compradores de la Página B es real.
3. **Comparación de Ventas (Conversión):** Aplicamos una prueba **Z de proporciones** ($p < 0.001$), demostrando que la ventaja en conversión de la Página B está completamente respaldada por las matemáticas.
4. **Análisis de Canales y Clientes (Chi-cuadrado):** Evaluamos minuciosamente el origen del tráfico y confirmamos que la Página B es **universalmente mejor**, sin importar si el usuario viene de redes sociales, correos o si es la primera vez que nos visita.

---

## 💡 Conclusiones y Recomendaciones de Negocio

1. **Lanzar el nuevo diseño al 100% de los usuarios:** Recomendamos implementar la **Página B** de manera definitiva para todo el público. El incremento del **+42.83%** en los ingresos que genera cada visita se traducirá en un impacto de dinero directo y masivo para la compañía.
2. **Potenciar los mejores canales:** Ya que el **Email** y los **Anuncios (Ads)** son los canales que mejor reaccionan y más compran con este nuevo diseño, sugerimos enfocar los esfuerzos y el presupuesto de marketing en estas opciones.
3. **Mantener un diseño único:** Como el nuevo diseño demostró ser un éxito tanto para clientes nuevos como para los antiguos, no hay necesidad de gastar tiempo ni dinero del equipo de tecnología en crear versiones personalizadas por ahora. Un solo diseño es suficiente.

---

## 🛠️ Herramientas Utilizadas
* **Lenguaje:** Python
* **Librerías para el tratamiento de datos:** Pandas, Numpy, Scipy y Statsmodels
* **Diseño de Gráficas:** Matplotlib y Seaborn

---

## 📂 Estructura del Repositorio

```text
├── 📂 data/
│   └── 📄 landing_experiment.csv       # Archivo original con los 40,000 datos del experimento
├── 📂 notebooks/                       # Historial de versiones del proyecto
│   ├── 📓 1_Github_AB_Test_Analysis_Final.ipynb  # Primera versión con análisis básico
│   ├── 📓 2_AB_Test_Analysis_mejorado.ipynb      # Intento de mejora que tenía el error de nombres
│   └── 📓 3_AB_Test_Analysis_v2.ipynb            # Versión donde se agregaron los cálculos robustos
├── 📂 images/                          # Carpeta con las imágenes creadas para este reporte
│   ├── 🖼️ boxplot_gasto_evolucion.png  # Gráfica de cuánto dinero gastan (Comparativa)
│   ├── 🖼️ conversion_by_traffic.png    # Resultados de ventas según de dónde viene el usuario
│   ├── 🖼️ executive_dashboard.png      # Panel completo listo para la dirección
│   └── 🖼️ user_type_interaction.png    # Resultados según si el cliente es nuevo o viejo
├── 📄 4_Proyecto_Final_AB_Test.ipynb  # [Archivo Final de Producción] Versión limpia, corregida y funcionando
├── 📄 README.md                        # Este reporte explicativo
└── 📄 S9 Version_Student_Proyecto_Landing_Experiment.ipynb # Plantilla escolar en blanco
```
---

### AUTOR:
David Germán Ramos Rodríguez
[LinkedIn](https://www.linkedin.com/in/david-g-ramos/) | 
[Sitio Web](https://dataanalist-davidgramos.github.io/mi-sitio-web/)
