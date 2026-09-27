# Proyecto NovaRetail+ — Análisis de factores de comportamiento y retención

## Objetivo

Identificar qué factores del comportamiento del cliente están más fuertemente asociados con el **ingreso anual generado** en NovaRetail+, una plataforma de comercio electrónico en Latinoamérica con millones de usuarios. El análisis fue solicitado por el equipo de **Crecimiento y retención** al cierre de 2024, con un enfoque **correlacional y exploratorio** (no causal).

**Preguntas que responde el dashboard:**
- ¿Qué variable de comportamiento explica mejor el ingreso anual por cliente?
- ¿La frecuencia de visitas a la plataforma se traduce en más compras e ingresos?
- ¿Existe relación entre el gasto en publicidad dirigida y las visitas/compras del usuario?
- ¿Variables demográficas (edad, nivel de ingreso) o de satisfacción influyen en el ingreso generado?
- ¿Qué papel juega la membresía premium en el abandono (churn) de clientes?
- ¿Existe asociación entre variables categóricas como región y tipo de dispositivo?

## Datos

- **Periodo:** Corte transversal al cierre de 2024 (no longitudinal, sin estacionalidad)
- **Tamaño:** 15,000 registros × 12 columnas, sin valores nulos
- **Variables principales:**
  - `id_cliente` — identificador único del cliente
  - `edad` — edad del cliente
  - `nivel_ingreso` — ingreso anual estimado del cliente
  - `visitas_mes` — número de visitas mensuales a la app/sitio
  - `compras_mes` — número de compras realizadas en el mes
  - `gasto_publicidad_dirigida` — gasto en anuncios asignado al usuario
  - `satisfaccion` — calificación de satisfacción (escala 1–5)
  - `miembro_premium` — suscripción premium (1 = sí, 0 = no)
  - `abandono` — churn del cliente (1 = sí, 0 = no)
  - `tipo_dispositivo` — móvil, escritorio o tablet
  - `region` — norte, sur, oeste o este
  - `ingreso_anual` — **variable objetivo**: ingreso anual generado por el cliente para la empresa

## Herramientas

- Python (pandas, numpy, seaborn, matplotlib)
- Estadística: correlación de Pearson y Spearman, prueba Chi-cuadrado, V de Cramér
- Jupyter Notebook
- Tableau Public *(si se generó un dashboard interactivo a partir de estos hallazgos)*

## Principales conclusiones

1. **`compras_mes` es el motor del ingreso anual.** Correlación de Pearson r = 0.97 con `ingreso_anual`: la relación lineal casi perfecta más fuerte de todo el dataset. La recurrencia de compras mensuales es, por mucho, el mejor predictor del valor anual del cliente.

2. **Las visitas no se traducen proporcionalmente en ingresos.** `visitas_mes` correlaciona solo moderada/débilmente con `compras_mes` (r ≈ 0.35) y con `ingreso_anual` (r ≈ 0.34). Más tráfico no implica más conversión: el problema está en el embudo, no en el volumen de visitas.

3. **La publicidad dirigida impulsa tráfico, no ingresos directamente.** `gasto_publicidad_dirigida` correlaciona moderado-fuerte con `visitas_mes` (r ≈ 0.58), pero solo débilmente con `compras_mes` (r ≈ 0.21) e `ingreso_anual` (r ≈ 0.20).

4. **Las variables demográficas no explican el ingreso.** `edad`, `nivel_ingreso` y `satisfaccion` muestran correlaciones prácticamente nulas (~0.00–0.02) con `ingreso_anual` y con el resto de variables del modelo.

5. **El abandono se asocia levemente con la membresía premium.** Correlación negativa débil (≈ −0.12): los miembros premium abandonan un poco menos, pero el efecto es pequeño.

6. **Región y tipo de dispositivo son independientes.** V de Cramér ≈ 0.012 (prácticamente nula), sin riesgo de colinealidad entre ambas variables categóricas.

## Aprendizajes

- Reforzar la diferencia entre **correlación y causalidad**: aunque `compras_mes` predice fuertemente `ingreso_anual`, no se puede concluir que forzar más compras cause directamente más ingreso, ya que ambas podrían compartir una causa oculta (p. ej. poder adquisitivo real).
- Practicar el uso de **coeficientes de correlación** (Pearson, Spearman) para variables numéricas y **V de Cramér / Chi-cuadrado** para variables categóricas, entendiendo cuándo aplicar cada uno.
- Aprender a estructurar hallazgos de negocio siguiendo un formato riguroso: evidencia visual → evidencia numérica → interpretación no causal → limitaciones → implicación de negocio.
- Reconocer las limitaciones de un análisis transversal (sin estacionalidad) y la importancia de proponer próximos pasos con mayor poder explicativo, como clustering (K-Means), regresión lineal múltiple o pruebas A/B para acercarse a relaciones causales.
