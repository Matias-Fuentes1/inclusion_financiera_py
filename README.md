# Global Findex Brasil · Barreras de Ahorro en la Juventud

## ¿De qué se trata?
Este es uno de mis proyectos de portfolio, originado como desafío técnico y reconstruido después para corregir un error metodológico que cometí en la primera versión: analicé un archivo de indicadores agregados (por país/año/grupo) como si fueran observaciones individuales, lo cual invalida cualquier correlación calculada sobre esa base.

En esta versión trabajé exclusivamente con **microdatos individuales** (Global Findex, World Bank Microdata Library) y apliqué **ponderación poblacional** (`wgt`) para que cada resultado refleje a la población real de Brasil y no un sesgo de la muestra encuestada.

La pregunta que guió todo el análisis fue una sola: **¿por qué los jóvenes de Brasil ahorran o no, y qué rol juega el acceso a billeteras digitales en esa decisión?**

---

## Dataset
Descargado desde [World Bank Microdata Library — Global Findex](https://microdata.worldbank.org/). Encuesta individual sobre inclusión financiera en Brasil, con 144.090 registros a nivel de persona.

| Variable | Qué representa |
|---|---|
| `saved` | Si la persona ahorró en el último año (sí/no) |
| `female` | Género del encuestado |
| `inc_q` | Quintil de ingreso del hogar (1 a 5) |
| `account_mob` | Si posee cuenta de dinero móvil / billetera digital |
| `wgt` | Factor de expansión poblacional |

---

## Qué hice con los datos antes de analizar
El primer intento sobre este mismo tema usó una base de indicadores ya resumidos por país/año/grupo — un error de unidad de análisis que invalidaba cualquier correlación. Antes de tocar cualquier métrica en esta versión:

* **Validación de unidad de análisis:** descarté el archivo de indicadores agregados (8.577 filas) y cargué la base de microdatos individuales (144.090 registros) para evitar la falacia ecológica.
* **Filtro y segmentación:** filtré Brasil y definí "jóvenes" como el rango 15-24 años, según el criterio del Banco Mundial.
* **Ponderación:** todas las tasas se calculan como suma ponderada (`ahorro × wgt`) sobre suma de pesos, no como promedio simple — así cada cifra refleja representatividad poblacional real.
* **Transparencia de nulos:** reporté explícitamente los registros sin dato válido de ahorro o de billetera digital y los excluí del cálculo, en vez de asumir un valor por defecto que no está en los datos.
* **Independencia de grupos:** todas las comparaciones (jóvenes vs. adultos, género, quintiles de ingreso) se hacen sobre subconjuntos disjuntos de la misma base individual, reportando tamaño de muestra por subgrupo.

---

## Lo que encontré

### El "Digital Premium": la brecha más marcada del análisis
Los jóvenes con billetera digital ahorran a una tasa de **74.76%**, frente a **32.43%** de quienes no la tienen — una diferencia de **+42.33 puntos porcentuales**. Es la asociación más fuerte de todo el dataset.

| Canal | Tasa de ahorro ponderada |
|---|---|
| Con billetera digital | 74.76% |
| Sin billetera digital | 32.43% |

### La brecha de género es tan grande como la brecha de ingresos
Entre los jóvenes, la brecha de ahorro por género (**28.27%**) es casi idéntica a la brecha por nivel de ingreso (**30.78%**). Un hombre joven del quintil más pobre ahorra más (**63.9%**) que una mujer joven del quintil más rico (**53.2%**).

### La brecha de género se amplifica con el ingreso, no se achica
En el quintil más bajo la brecha de género es de 17.7 puntos; en el quintil más alto se dispara a 38.3 puntos. El ingreso alto no cierra la brecha — la agranda.

### Estas son asociaciones, no causas
El análisis es transversal (una sola foto en el tiempo). Las diferencias por canal digital y por género son correlacionales y no permiten, con estos datos, afirmar qué causa qué. Las interpretaciones conductuales (contabilidad mental, sobrecarga cognitiva, sesgo de statu quo) son hipótesis razonables a partir de la literatura de economía del comportamiento, no hallazgos medidos directamente en el dataset.

---

## Qué haría con esta información
1. **Pilotear un mecanismo de ahorro por defecto (ej. redondeo automático vía Pix):** dado el tamaño del Digital Premium, vale la pena testear si reducir la fricción de decisión mueve la tasa de ahorro en el grupo que hoy no tiene billetera digital. No proyectaría una tasa de adopción o retención sin antes correr un piloto controlado — el 74.76% observado es tasa de ahorro general, no retención de una feature que no existe todavía.
2. **Investigar la brecha de género con datos que no tengo acá:** antes de diseñar una intervención específica, haría falta una encuesta de uso del tiempo o carga de trabajo doméstico para confirmar o descartar la hipótesis de sobrecarga cognitiva.
3. **Priorizar el quintil alto en cualquier intervención de género:** contraintuitivamente, es donde la brecha es más grande, no donde el problema "ya está resuelto por tener plata".

---

## El notebook
Documentado en 5 secciones para que el proceso completo sea auditable, desde la carga de datos hasta las limitaciones del análisis:

* **Carga y Limpieza:** validación de unidad de análisis, ponderación, tratamiento transparente de nulos.
* **EDA:** cálculo de brechas de género e ingreso sobre subgrupos independientes.
* **Conexión Conductual:** cuantificación del Digital Premium.
* **Conclusiones y Recomendaciones:** síntesis de hallazgos separada explícitamente de las hipótesis interpretativas, y limitaciones metodológicas declaradas.

---

*Herramientas: Python · Pandas · Matplotlib/Seaborn · Global Findex Microdata*
