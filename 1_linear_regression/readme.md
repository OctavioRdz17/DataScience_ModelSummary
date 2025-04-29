# Regresión Lineal

La regresión lineal es un modelo fundamental que busca establecer una relación lineal entre una variable dependiente (o de respuesta) y una o más variables independientes (o predictoras). En su forma más simple, la regresión lineal simple involucra una única variable predicadora, y la relación se representa mediante una línea recta. Cuando hay múltiples variables predictoras, hablamos de regresión lineal múltiple, y la relación se visualiza como un hiperplano en un espacio de dimensiones superiores.

La idea central es encontrar la "mejor" línea (o hiperplano) que se ajuste a los datos observados, minimizando la diferencia entre los valores predichos por la línea y los valores reales de la variable dependiente.

### Matemática

La ecuación de regresión con más de un término toma la forma siguiente:

y = b0 + b1X1 + b2X2 + ... + bkXk

Donde x1,x2,…,xn son las múltiples variables independientes y β1,β2,…,βn son sus respectivos coeficientes.

El objetivo es estimar los coeficientes β0,β1,…,βn que minimicen la suma de los cuadrados de los errores (método de los mínimos cuadrados ordinarios - OLS):

```markdown
### En la ecuación de regresión, las letras representan lo siguiente: 
y es la variable de respuesta
b0 es la constante
b1, b2, ..., bk son los coeficientes
X1, X2, ..., Xk son los valores del término
```

### **Parámetros:**

Los parámetros del modelo de regresión lineal son los coeficientes β0,β1,…,βn. Estos son los valores que el algoritmo aprende a partir de los datos de entrenamiento.

### **Hiperparámetros:**

La regresión lineal en su forma básica tiene pocos hiperparámetros. Sin embargo, las decisiones sobre la inclusión de términos de interacción entre variables predictoras o la transformación de las variables predictoras podrían considerarse como hiperparámetros que se ajustan antes del entrenamiento del modelo.

### **Casos de uso:**

- **Predicción de precios de viviendas:** Utilizar características como el tamaño, la ubicación y el número de habitaciones para predecir el precio de una casa.
- **Pronóstico de ventas:** Estimar las ventas futuras basándose en datos históricos de ventas, gasto en publicidad y otros factores.
- **Análisis de tendencias:** Identificar y cuantificar la relación entre variables, como el impacto del gasto en marketing en los ingresos.
- **Modelado de relaciones causales:** Aunque con precaución, la regresión lineal puede ayudar a entender cómo un cambio en una variable independiente afecta a la variable dependiente.

### **¿Cómo difiere de otros modelos parecidos?**

- **Regresión Logística:** Mientras que la regresión lineal predice un valor numérico continuo, la regresión logística se utiliza para problemas de **clasificación binaria** (dos clases).
- **Otros modelos de regresión (Polinomial, Ridge, Lasso):** La regresión lineal asume una relación lineal. Otros modelos de regresión pueden modelar relaciones no lineales (regresión polinomial) o incorporar técnicas de regularización para evitar el sobreajuste (Ridge y Lasso).

### Más información relevante:

- **Supuestos de la regresión lineal:** Es importante tener en cuenta los supuestos subyacentes a la regresión lineal (linealidad, independencia de los errores, homocedasticidad, normalidad de los errores) para asegurar la validez del modelo.
- **Evaluación del modelo:** El rendimiento de un modelo de regresión lineal se evalúa utilizando métricas como el error cuadrático medio (MSE), la raíz del error cuadrático medio (RMSE), el error absoluto medio (MAE) y el coeficiente de determinación (R2).
- **Ingeniería de características:** La calidad de las variables predictoras es crucial para el rendimiento del modelo. La ingeniería de características, que implica la creación de nuevas variables a partir de las existentes, puede mejorar significativamente la capacidad predictiva.

### linealidad, independencia de los errores, homocedasticidad, normalidad de los errores

### 1. Linealidad

**¿Qué significa?**

Este supuesto establece que debe existir una relación lineal entre la variable dependiente (la que quieres predecir) y las variables independientes (las que usas para predecir). En otras palabras, el cambio en la variable dependiente debido a un cambio unitario en una variable independiente debe ser constante a lo largo de todo el rango de esa variable independiente.

**¿Por qué es importante?**

Si la relación real entre las variables es no lineal, un modelo de regresión lineal intentará ajustarla con una línea recta, lo que llevará a predicciones inexactas y un modelo que no captura la verdadera relación entre las variables.

**¿Cómo verificarlo?**

- **Gráficos de dispersión:** Visualiza la relación entre cada variable independiente y la variable dependiente. Busca patrones curvos o no lineales.
- **Gráficos de residuos vs. valores ajustados:** Después de ajustar el modelo, grafica los residuos (la diferencia entre los valores reales y los predichos) contra los valores predichos. Si el supuesto de linealidad se cumple, los residuos deberían mostrar una dispersión aleatoria alrededor de cero, sin ningún patrón discernible (como una curva).
- **Component-Plus-Residual Plots (CR Plots):** Estos gráficos pueden ayudar a identificar no linealidades en la relación entre cada predictor y la variable de respuesta, ajustando por los otros predictores en el modelo.

**¿Qué hacer si no se cumple?**

- **Transformación de variables:** Aplicar funciones no lineales (como logaritmos, polinomios, raíces cuadradas) a las variables independientes o dependiente puede ayudar a linealizar la relación.
- **Incluir términos polinómicos:** Si la relación parece ser una curva, puedes incluir términos de orden superior de las variables independientes (por ejemplo, x2, x3) en el modelo.
- **Usar modelos no lineales:** Si la relación es inherentemente no lineal, considera usar modelos de regresión no lineal.

### 2. Independencia de los errores (o residuos)

**¿Qué significa?**

Este supuesto indica que los errores (o residuos) del modelo no deben estar correlacionados entre sí. En otras palabras, el error asociado con una observación no debe influir en el error asociado con otra observación.

**¿Por qué es importante?**

La correlación entre los errores puede ocurrir especialmente en datos de series de tiempo (donde las observaciones están ordenadas en el tiempo) o en datos agrupados. La violación de este supuesto puede llevar a estimaciones ineficientes de los coeficientes de regresión y a conclusiones incorrectas sobre la significancia estadística de las variables predictoras. Los errores estándar de los coeficientes pueden subestimarse, lo que lleva a pensar que una variable es significativa cuando en realidad no lo es.

**¿Cómo verificarlo?**

- **Gráficos de residuos vs. tiempo (para datos de series de tiempo):** Busca patrones en los residuos a lo largo del tiempo. Una tendencia o patrón cíclico podría indicar autocorrelación.
- **Prueba de Durbin-Watson:** Esta prueba estadística cuantifica la autocorrelación en los residuos. Un valor cercano a 2 indica poca o ninguna autocorrelación. Valores cercanos a 0 sugieren autocorrelación positiva, y valores cercanos a 4 sugieren autocorrelación negativa.
- **Función de autocorrelación (ACF) y función de autocorrelación parcial (PACF):** Para datos de series de tiempo, estos gráficos pueden ayudar a identificar la presencia y el orden de la autocorrelación.

**¿Qué hacer si no se cumple?**

- **Modelos de series de tiempo:** Si tienes datos de series de tiempo con autocorrelación, considera usar modelos específicos para series de tiempo como ARIMA.
- **Incluir variables omitidas:** A veces, la autocorrelación puede ser un indicio de que una variable importante ha sido omitida del modelo. Incluirla podría reducir la correlación en los residuos.
- **Transformaciones:** En algunos casos, las transformaciones de los datos pueden ayudar.

### 3. Homocedasticidad

**¿Qué significa?**

Este supuesto establece que la varianza de los errores (o residuos) debe ser constante para todos los niveles de las variables independientes. En otras palabras, la dispersión de los residuos debe ser similar a lo largo de la línea de regresión.

**¿Por qué es importante?**

La heterocedasticidad (la violación de la homocedasticidad) ocurre cuando la varianza de los errores no es constante. Esto puede llevar a estimaciones ineficientes de los coeficientes de regresión y a errores estándar incorrectos, lo que afecta la validez de las pruebas de hipótesis y los intervalos de confianza. Por ejemplo, si la varianza de los errores aumenta con el valor de una variable independiente, las predicciones para valores más altos de esa variable serán menos precisas, pero el modelo podría no reflejar esta incertidumbre.

**¿Cómo verificarlo?**

- **Gráficos de residuos vs. valores ajustados:** Busca patrones en la dispersión de los residuos. Si la varianza no es constante, podrías observar una forma de embudo (donde la dispersión aumenta o disminuye con los valores ajustados) o cualquier otro patrón no aleatorio.
- **Gráficos de escala-ubicación:** Estos gráficos muestran la raíz cuadrada de los residuos estandarizados contra los valores ajustados. Pueden ser útiles para detectar patrones de heterocedasticidad.
- **Pruebas estadísticas:** Existen pruebas formales para la homocedasticidad, como la prueba de Breusch-Pagan, la prueba de White y la prueba de Goldfeld-Quandt.

**¿Qué hacer si no se cumple?**

- **Transformación de la variable dependiente:** Transformaciones como el logaritmo o la raíz cuadrada pueden a menudo estabilizar la varianza de los errores.
- **Regresión de mínimos cuadrados ponderados (WLS):** Si se conoce la estructura de la heterocedasticidad (por ejemplo, si la varianza es proporcional a una variable independiente), se pueden asignar pesos diferentes a las observaciones en el proceso de ajuste para dar menos peso a las observaciones con mayor varianza de error.
- **Estimadores robustos de errores estándar:** Algunos métodos pueden proporcionar errores estándar consistentes incluso en presencia de heterocedasticidad (por ejemplo, los estimadores robustos de Huber-White).

### 4. Normalidad de los errores (o residuos)

**¿Qué significa?**

Este supuesto establece que los errores (o residuos) del modelo deben seguir una distribución normal.

**¿Por qué es importante?**

La normalidad de los errores es importante principalmente para realizar pruebas de hipótesis y construir intervalos de confianza para los coeficientes de regresión, especialmente en muestras pequeñas. El teorema del límite central nos dice que a medida que el tamaño de la muestra aumenta, la distribución de las medias muestrales se aproxima a una distribución normal, 1  incluso si la distribución de la población original no es normal. Por lo tanto, este supuesto es menos crítico en muestras grandes. Sin embargo, en muestras pequeñas, las desviaciones significativas de la normalidad pueden afectar la validez de las inferencias estadísticas.

**¿Cómo verificarlo?**

- **Histograma de los residuos:** Visualiza la distribución de los residuos. Debería tener una forma aproximadamente de campana.
- **Gráfico de probabilidad normal (Q-Q plot):** Este gráfico compara los cuantiles de la distribución de los residuos con los cuantiles de una distribución normal estándar. Si los residuos están distribuidos normalmente, los puntos deberían caer aproximadamente a lo largo de una línea recta. Las desviaciones de la línea recta sugieren no normalidad.
- **Pruebas estadísticas de normalidad:** Existen pruebas formales como la prueba de Shapiro-Wilk, la prueba de Kolmogorov-Smirnov y la prueba de Jarque-Bera para evaluar si una muestra de datos proviene de una distribución normal. Sin embargo, estas pruebas pueden ser sensibles al tamaño de la muestra y pueden no ser siempre la mejor guía en la práctica.

**¿Qué hacer si no se cumple?**

- **Transformación de variables:** Al igual que con la no linealidad y la heterocedasticidad, la transformación de la variable dependiente a veces puede ayudar a que los residuos sean más normales.
- **Eliminar valores atípicos (outliers):** Los valores atípicos pueden tener un gran impacto en la distribución de los residuos y pueden ser la causa de la no normalidad. Sin embargo, la eliminación de valores atípicos debe hacerse con precaución y justificación.
- **Usar métodos no paramétricos:** Si la no normalidad es severa y no se puede corregir con transformaciones, considera usar métodos de regresión no paramétricos que no asumen una distribución específica para los errores.
- **En muestras grandes:** Si tienes una muestra grande, la violación del supuesto de normalidad puede ser menos preocupante debido al teorema del límite central.

**En resumen:**

Es importante recordar que estos supuestos son ideales y que los datos del mundo real a menudo no los cumplen perfectamente. Sin embargo, comprender estos supuestos y cómo evaluarlos te permitirá tomar decisiones informadas sobre la validez de tu modelo de regresión lineal y aplicar las correcciones necesarias cuando sea apropiado. La violación de estos supuestos no necesariamente invalida por completo el modelo, pero puede afectar la interpretación de los resultados y la confiabilidad de las inferencias estadísticas.