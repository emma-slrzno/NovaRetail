<a id="top"></a>

# 🛍️ Proyecto NovaRetail · NovaRetail Project

**Análisis de factores de comportamiento y retención · Behavior and retention factors analysis**

**🌎 Idioma / Language:** [🇪🇸 Español](#es) · [🇬🇧 English](#en)

---

<a id="es"></a>

## 🇪🇸 Español

Análisis exploratorio de qué factores del comportamiento del cliente están más asociados con el **ingreso anual generado** en NovaRetail+, solicitado por el equipo de **Crecimiento y retención** al cierre de 2024.

### 1. Problema o contexto de negocio

NovaRetail+ es una plataforma de comercio electrónico en Latinoamérica con millones de usuarios. El equipo de Crecimiento y retención invierte en tráfico, publicidad dirigida y membresías, pero necesita saber **qué comportamientos de los clientes realmente se asocian con más ingreso** para decidir dónde enfocar esfuerzos y presupuesto.

### 2. Objetivo del análisis

Identificar qué variables de comportamiento se asocian más fuertemente con el `ingreso_anual` por cliente, con un enfoque **correlacional y exploratorio (no causal)**.

**Preguntas que responde el dashboard:**
- ¿Qué variable de comportamiento explica mejor el ingreso anual por cliente?
- ¿La frecuencia de visitas a la plataforma se traduce en más compras e ingresos?
- ¿Existe relación entre el gasto en publicidad dirigida y las visitas/compras del usuario?
- ¿Variables demográficas (edad, nivel de ingreso) o de satisfacción influyen en el ingreso generado?
- ¿Qué papel juega la membresía premium en el abandono (churn) de clientes?
- ¿Existe asociación entre variables categóricas como región y tipo de dispositivo?

### 3. Dataset utilizado

- **Periodo:** corte transversal al cierre de 2024 (no longitudinal, sin estacionalidad).
- **Tamaño:** 15,000 registros × 12 columnas, sin valores nulos.

| Variable | Descripción |
|----------|-------------|
| `id_cliente` | Identificador único del cliente |
| `edad` | Edad del cliente |
| `nivel_ingreso` | Ingreso anual estimado del cliente |
| `visitas_mes` | Número de visitas mensuales a la app/sitio |
| `compras_mes` | Número de compras realizadas en el mes |
| `gasto_publicidad_dirigida` | Gasto en anuncios asignado al usuario |
| `satisfaccion` | Calificación de satisfacción (escala 1–5) |
| `miembro_premium` | Suscripción premium (1 = sí, 0 = no) |
| `abandono` | Churn del cliente (1 = sí, 0 = no) |
| `tipo_dispositivo` | Móvil, escritorio o tablet |
| `region` | Norte, sur, oeste o este |
| `ingreso_anual` | **Variable objetivo:** ingreso anual generado por el cliente para la empresa |

### 4. Herramientas y tecnologías

- **Python:** pandas, numpy, seaborn, matplotlib
- **Estadística:** correlación de Pearson y Spearman, prueba Chi-cuadrado, V de Cramér
- **Jupyter Notebook**
- **Tableau Public** para el dashboard interactivo

### 5. Proceso realizado

1. **Exploración del dataset:** revisión de estructura, tipos de variables y valores nulos.
2. **Variables numéricas:** correlaciones de **Pearson** (relaciones lineales) y **Spearman** (relaciones monótonas) con `ingreso_anual` y entre variables de comportamiento.
3. **Variables categóricas:** asociación entre `region` y `tipo_dispositivo` con **Chi-cuadrado** y **V de Cramér**.
4. **Interpretación:** cada hallazgo se estructuró como evidencia visual → evidencia numérica → interpretación no causal → limitaciones → implicación de negocio.
5. **Visualización:** dashboard interactivo en Tableau Public.

### 6. Principales hallazgos

| Relación | Correlación | Lectura |
|----------|------------:|---------|
| `compras_mes` ↔ `ingreso_anual` | r = 0.97 | Casi perfecta |
| `gasto_publicidad_dirigida` ↔ `visitas_mes` | r ≈ 0.58 | Moderada-fuerte |
| `visitas_mes` ↔ `compras_mes` | r ≈ 0.35 | Moderada-débil |
| `visitas_mes` ↔ `ingreso_anual` | r ≈ 0.34 | Moderada-débil |
| `gasto_publicidad_dirigida` ↔ `compras_mes` | r ≈ 0.21 | Débil |
| `gasto_publicidad_dirigida` ↔ `ingreso_anual` | r ≈ 0.20 | Débil |
| `miembro_premium` ↔ `abandono` | r ≈ −0.12 | Débil, negativa |
| `edad`, `nivel_ingreso`, `satisfaccion` ↔ `ingreso_anual` | ~0.00–0.02 | Prácticamente nula |
| `region` ↔ `tipo_dispositivo` | V de Cramér ≈ 0.012 | Prácticamente nula |

1. **`compras_mes` es el principal predictor del ingreso anual.** Es la relación lineal más fuerte de todo el dataset: la recurrencia de compras mensuales es, por mucho, el mejor indicador del valor anual del cliente.
2. **Las visitas no se traducen proporcionalmente en ingresos.** Más tráfico no implica más conversión; el cuello de botella parece estar en el embudo, no en el volumen de visitas.
3. **La publicidad dirigida se asocia con tráfico, no tanto con ingresos.** Se relaciona de forma moderada-fuerte con las visitas, pero solo débilmente con compras e ingreso anual.
4. **Las variables demográficas y la satisfacción no explican el ingreso.** Edad, nivel de ingreso y satisfacción muestran correlaciones prácticamente nulas con `ingreso_anual` y con el resto de variables.
5. **El abandono se asocia levemente con la membresía premium.** Los miembros premium abandonan un poco menos, pero el efecto es pequeño.
6. **Región y tipo de dispositivo son independientes.** No hay riesgo de colinealidad entre ambas variables categóricas.

### 7. Recomendaciones e impacto para el negocio

Dado que el análisis es correlacional, estas recomendaciones deben validarse (idealmente con pruebas A/B) antes de escalarlas:

1. **Enfocar la estrategia en la recurrencia de compra.** Programas de lealtad, recordatorios de recompra y ofertas para clientes con pocas compras mensuales atacan la variable más asociada con el ingreso.
2. **Diagnosticar el embudo visita → compra.** Como las visitas se convierten poco en compras, conviene analizar dónde se pierden los usuarios (producto, carrito, checkout) en lugar de buscar solo más tráfico.
3. **Evaluar la publicidad dirigida por compras e ingresos, no por visitas.** Medirla con costo por compra o ingreso incremental evita sobreinvertir en una palanca que genera tráfico pero se asocia débilmente con ingreso.
4. **Segmentar por comportamiento, no por demografía.** Edad, nivel de ingreso, región y dispositivo no distinguen el valor del cliente; los segmentos conductuales (p. ej. con clustering K-Means) son más prometedores.
5. **Probar la membresía premium como palanca de retención antes de invertir en ella.** La asociación con menor churn es real pero pequeña, por lo que conviene validarla con un experimento.

### 8. Limitaciones

- **Correlación no es causalidad:** que `compras_mes` prediga `ingreso_anual` no implica que forzar más compras genere más ingreso; ambas pueden compartir una causa oculta, como el poder adquisitivo real.
- **Relación posiblemente muy directa:** al ser el ingreso anual generado por las compras del cliente, una correlación de 0.97 puede reflejar una relación casi mecánica entre ambas variables más que un hallazgo "descubierto". Conviene tratar `compras_mes` como una descripción del ingreso y no como un factor independiente.
- **Corte transversal:** sin dimensión temporal ni estacionalidad, no se puede ver cómo evolucionan los clientes.
- **Próximos pasos con mayor poder explicativo:** clustering (K-Means), regresión lineal múltiple, datos longitudinales y pruebas A/B.

### 9. Aprendizajes

- Diferenciar **correlación y causalidad**.
- Aplicar **Pearson y Spearman** en variables numéricas y **V de Cramér / Chi-cuadrado** en categóricas, entendiendo cuándo usar cada uno.
- Estructurar hallazgos de negocio con rigor: evidencia visual → evidencia numérica → interpretación no causal → limitaciones → implicación de negocio.
- Reconocer las limitaciones de un análisis transversal y proponer próximos pasos.

### 10. Contacto

- 💼 LinkedIn: [Emma Solórzano Hernández Jáuregui](https://www.linkedin.com/in/emma-solorzano-hernandez-jauregui-200301345/)
- 📊 Tableau Public: [Ver perfil](https://public.tableau.com/app/profile/emma.solorzano7415/vizzes)

[⬆️ Volver arriba](#top) · [🇬🇧 Read in English](#en)

---

<a id="en"></a>

## 🇬🇧 English

Exploratory analysis of which customer behavior factors are most associated with the **annual revenue generated** on NovaRetail+, requested by the **Growth and Retention** team at the end of 2024.

### 1. Business problem and context

NovaRetail+ is an e-commerce platform in Latin America with millions of users. The Growth and Retention team invests in traffic, targeted advertising, and memberships, but needs to know **which customer behaviors are actually associated with higher revenue** to decide where to focus effort and budget.

### 2. Analysis objective

Identify which behavior variables are most strongly associated with `ingreso_anual` (annual revenue) per customer, using a **correlational and exploratory (non-causal)** approach.

**Questions the dashboard answers:**
- Which behavior variable best explains annual revenue per customer?
- Does visit frequency translate into more purchases and revenue?
- Is there a relationship between targeted advertising spend and user visits/purchases?
- Do demographic variables (age, income level) or satisfaction influence the revenue generated?
- What role does the premium membership play in customer churn?
- Is there an association between categorical variables such as region and device type?

### 3. Dataset

- **Period:** cross-sectional snapshot at the end of 2024 (not longitudinal, no seasonality).
- **Size:** 15,000 records × 12 columns, no missing values.

| Variable | Description |
|----------|-------------|
| `id_cliente` | Unique customer identifier |
| `edad` | Customer age |
| `nivel_ingreso` | Customer's estimated annual income |
| `visitas_mes` | Monthly visits to the app/site |
| `compras_mes` | Purchases made in the month |
| `gasto_publicidad_dirigida` | Ad spend allocated to the user |
| `satisfaccion` | Satisfaction rating (1–5 scale) |
| `miembro_premium` | Premium subscription (1 = yes, 0 = no) |
| `abandono` | Customer churn (1 = yes, 0 = no) |
| `tipo_dispositivo` | Mobile, desktop, or tablet |
| `region` | North, south, west, or east |
| `ingreso_anual` | **Target variable:** annual revenue generated by the customer for the company |

### 4. Tools and technologies

- **Python:** pandas, numpy, seaborn, matplotlib
- **Statistics:** Pearson and Spearman correlation, Chi-square test, Cramér's V
- **Jupyter Notebook**
- **Tableau Public** for the interactive dashboard

### 5. Process

1. **Dataset exploration:** review of structure, variable types, and missing values.
2. **Numeric variables:** **Pearson** (linear relationships) and **Spearman** (monotonic relationships) correlations with `ingreso_anual` and among behavior variables.
3. **Categorical variables:** association between `region` and `tipo_dispositivo` using **Chi-square** and **Cramér's V**.
4. **Interpretation:** each finding was structured as visual evidence → numerical evidence → non-causal interpretation → limitations → business implication.
5. **Visualization:** interactive dashboard on Tableau Public.

### 6. Key findings

| Relationship | Correlation | Reading |
|--------------|------------:|---------|
| `compras_mes` ↔ `ingreso_anual` | r = 0.97 | Almost perfect |
| `gasto_publicidad_dirigida` ↔ `visitas_mes` | r ≈ 0.58 | Moderate-strong |
| `visitas_mes` ↔ `compras_mes` | r ≈ 0.35 | Moderate-weak |
| `visitas_mes` ↔ `ingreso_anual` | r ≈ 0.34 | Moderate-weak |
| `gasto_publicidad_dirigida` ↔ `compras_mes` | r ≈ 0.21 | Weak |
| `gasto_publicidad_dirigida` ↔ `ingreso_anual` | r ≈ 0.20 | Weak |
| `miembro_premium` ↔ `abandono` | r ≈ −0.12 | Weak, negative |
| `edad`, `nivel_ingreso`, `satisfaccion` ↔ `ingreso_anual` | ~0.00–0.02 | Practically none |
| `region` ↔ `tipo_dispositivo` | Cramér's V ≈ 0.012 | Practically none |

1. **`compras_mes` is the main predictor of annual revenue.** It is the strongest linear relationship in the whole dataset: monthly purchase recurrence is by far the best indicator of a customer's annual value.
2. **Visits do not translate proportionally into revenue.** More traffic does not imply more conversion; the bottleneck seems to be in the funnel, not in visit volume.
3. **Targeted advertising is associated with traffic, not so much with revenue.** It relates moderately-strongly to visits, but only weakly to purchases and annual revenue.
4. **Demographic variables and satisfaction do not explain revenue.** Age, income level, and satisfaction show practically null correlations with `ingreso_anual` and with the rest of the variables.
5. **Churn is slightly associated with premium membership.** Premium members churn a little less, but the effect is small.
6. **Region and device type are independent.** There is no collinearity risk between these two categorical variables.

### 7. Recommendations and business impact

Since the analysis is correlational, these recommendations should be validated (ideally with A/B tests) before scaling them:

1. **Focus the strategy on purchase recurrence.** Loyalty programs, repurchase reminders, and offers for customers with few monthly purchases target the variable most associated with revenue.
2. **Diagnose the visit → purchase funnel.** Since visits convert poorly into purchases, analyze where users drop off (product, cart, checkout) instead of only seeking more traffic.
3. **Evaluate targeted advertising by purchases and revenue, not visits.** Measuring it by cost per purchase or incremental revenue avoids over-investing in a lever that drives traffic but is only weakly associated with revenue.
4. **Segment by behavior, not demographics.** Age, income level, region, and device do not distinguish customer value; behavioral segments (e.g., via K-Means clustering) are more promising.
5. **Test premium membership as a retention lever before investing in it.** The association with lower churn is real but small, so it should be validated with an experiment.

### 8. Limitations

- **Correlation is not causation:** that `compras_mes` predicts `ingreso_anual` does not mean that forcing more purchases will generate more revenue; both may share a hidden cause, such as actual purchasing power.
- **Possibly very direct relationship:** since annual revenue is generated by the customer's purchases, a 0.97 correlation may reflect an almost mechanical link between the two variables rather than a "discovered" insight. `compras_mes` is better treated as a description of revenue than as an independent factor.
- **Cross-sectional data:** with no time dimension or seasonality, it is not possible to see how customers evolve.
- **Next steps with greater explanatory power:** clustering (K-Means), multiple linear regression, longitudinal data, and A/B tests.

### 9. Lessons learned

- Distinguishing **correlation from causation**.
- Applying **Pearson and Spearman** to numeric variables and **Cramér's V / Chi-square** to categorical ones, understanding when to use each.
- Structuring business findings rigorously: visual evidence → numerical evidence → non-causal interpretation → limitations → business implication.
- Recognizing the limitations of a cross-sectional analysis and proposing next steps.

### 10. Contact

- 💼 LinkedIn: [Emma Solórzano Hernández Jáuregui](https://www.linkedin.com/in/emma-solorzano-hernandez-jauregui-200301345/)
- 📊 Tableau Public: [View profile](https://public.tableau.com/app/profile/emma.solorzano7415/vizzes)

[⬆️ Back to top](#top) · [🇪🇸 Leer en español](#es)
