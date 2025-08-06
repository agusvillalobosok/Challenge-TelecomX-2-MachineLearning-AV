Informe de Análisis de Cancelación de Clientes
Introducción
La empresa Telecom X es proveedora de servicios de internet, televisión por cable y streaming. Está enfrentando una alta tasa de cancelación de suscripción al servicio por parte de sus clientes. Por lo tanto, decidió montar el proyecto "Churn de Clientes" o evasión de clientes, contratándome para realizar un análisis de datos y así comprender los factores que llevan a la pérdida de clientes y reducción de ganancias, entre otros resultados que no favorecen a la empresa.
Objetivo del análisis
El propósito fue identificar los factores clave que influyen en la cancelación de clientes (Baja_cliente) utilizando modelos de Machine Learning, y desarrollar estrategias de retención basadas en estos hallazgos. 
Preparación de los datos para el modelado
Antes de entrenar cualquier modelo de Machine Learning, aplicamos una serie de técnicas de preprocesamiento para garantizar que los datos estuvieran limpios, coherentes y listos para su análisis:
a) Tratamiento de datos
Valores faltantes: Se verificaron y trataron los valores nulos (si existían).



Outliers: Se inspeccionaron mediante boxplots para detectar posibles valores atípicos, especialmente en variables como Total_Tarifas_Cliente y Meses_de_Contrato.
b) Codificación de variables categóricas
Se aplicó Label Encoding para transformar las variables categóricas en formato numérico, necesario para modelos como Random Forest o KNN empleados más adelante.
c) Normalización / Escalado
Se utilizó StandardScaler para escalar las variables numéricas, especialmente importante para modelos sensibles a la escala como KNN y SVM.
Análisis de correlación entre variables
  Correlación
Se aplicó análisis de correlación (Pearson) para evaluar la relación entre variables numéricas y la variable objetivo Baja_cliente.


Se utilizaron matrices de correlación para identificar multicolinealidad y detectar variables redundantes o no informativas.

También se analizó la correlación entre variables específicas y la cancelación, como:
Meses_de_Contrato × Baja_cliente


Total_Tarifas_Cliente × Baja_cliente


(Ver gráficos de boxplots en la sección Tratamiento de datos para visualizar la distribución de las variables y sus posibles patrones). 

Las etapas anteriores fueron un punto clave para:
- Mejorar la precisión de los modelos.
- Reducir el tiempo de entrenamiento.
- Evitar problemas como overfitting por exceso de variables irrelevantes.
- Obtener interpretabilidad en los factores que influyen en la cancelación.
Desarrollo de los modelos.  
El proceso de creación de los modelos de Machine Learning se desarrolló cuidadosamente en varias etapas para asegurar su precisión, interpretabilidad y utilidad práctica en la predicción de la cancelación de clientes. A continuación, se detalla el enfoque utilizado para entrenar y evaluar los modelos Random Forest y KNN.
Modelo de predicción con Random Forest.
¿Qué es? Random Forest es un modelo de tipo ensemble, que construye múltiples árboles de decisión y promedia sus resultados. Es robusto frente a sobreajuste y muy útil para clasificación y estimación de importancia de variables.
Etapas del desarrollo:
Selección de características (features):


Se seleccionaron las variables relevantes a partir del análisis de correlación y la importancia de variables. 


Variables como Meses_de_Contrato, Total_Tarifas_Cliente, y Contrato_Mensual mostraron fuerte impacto en la cancelación. 


División de los datos:


Se dividió el conjunto de datos en entrenamiento (80%) y prueba (20%) para validar el modelo sin sesgos. 
Entrenamiento del modelo:




Predicción y evaluación:
Se evaluó el modelo con métricas como Accuracy, Precision, Recall y F1-score.
El rendimiento fue sólido: Accuracy 0.76, F1-score para clase 1: 0.77.
Importancia de variables:
El modelo proporcionó un ranking claro de las variables que más influyeron en la predicción, permitiendo identificar áreas clave para retención de clientes.

Modelo de predicción con KNN (K-Nearest Neighbors).
KNN es un modelo basado en distancia que clasifica un punto según las etiquetas de sus vecinos más cercanos. Es intuitivo y no paramétrico, pero muy sensible a la escala de las variables.
Etapas del desarrollo:
Normalización de datos:


Se aplicó escalado con StandardScaler para igualar la influencia de todas las variables en el cálculo de distancias.
Entrenamiento del modelo:
Se eligió un valor de k tras probar varios valores (validación cruzada o por defecto k=5), valor óptimo 10. (Los datos también se separaron en una proporción de 80-20 %.
Evaluación:
Se evaluó con las mismas métricas de clasificación.


Obtuvo un rendimiento similar al de Random Forest: Accuracy 0.75, F1-score para clase 1: 0.76.
Modelos Evaluados y Rendimiento
Modelo
Accuracy
Precision (1)
Recall (1)
F1-Score (1)
Random Forest
0.76
0.74
0.80
0.77
KNN
0.75
0.73
0.79
0.76

Comparación final
Modelo
Ventajas principales
Métrica F1 (Class 1)
Random Forest
Alta precisión, interpretable, manejo de variables
0.77
KNN
Fácil de entender, no necesita entrenamiento complejo
0.76


Variables más influyentes
Se utilizaron métodos como coeficientes (Logística, SVM), importancia de variables (Random Forest), y Permutation Importance (KNN, MLP), como herramientas extras para saber el comportamiento de las variables claves en los modelos:
Meses_de_Contrato: Clientes con pocos meses son más propensos a cancelar.
Total_Tarifas_Cliente: Tarifas elevadas se asocian con mayor tasa de cancelación.
Soporte_tecnico: La falta de soporte técnico está relacionada con cancelaciones.
Servicio_Streaming: Clientes sin este servicio cancelan más a menudo.
Atencion_cliente: Poca interacción o mal servicio predice cancelación.
Análisis Crítico
No se detectaron problemas graves de overfitting ni underfitting. Las métricas de entrenamiento y prueba fueron coherentes. Regularización en regresión y límites como max_depth en Random Forest ayudaron a estabilizar los modelos. Las pruebas de matriz dieron el siguiente resultado. La efectividad de los modelos (tomando como referencia el accuracy, que mide el porcentaje de predicciones correctas) es de 76% para el modelo de Random Forest y de 75% para el modelo de KNN. 

Estrategias de Retención Recomendadas
Incentivar la permanencia: Ofrecer beneficios especiales a los nuevos clientes durante los primeros 3–6 meses.
Revisar tarifas altas: Realizar análisis de precios para identificar planes poco competitivos y ofrecer opciones más flexibles.
Mejorar el soporte técnico: Implementar resolución rápida de problemas y mejorar la disponibilidad del servicio técnico.
Fomentar servicios de valor agregado: Promover servicios como streaming o bundles con descuentos.
Atención personalizada: Aplicar sistemas de seguimiento proactivo para detectar insatisfacción temprana.
Conclusión General
El análisis demostró que es posible predecir con alta precisión la cancelación de clientes, especialmente usando modelos como Random Forest y Redes Neuronales. Los factores que más influyen están relacionados con la duración del contrato, costos, calidad de servicios y atención al cliente. Estas conclusiones permiten a la empresa anticiparse a la pérdida de clientes y tomar medidas preventivas efectivas.

Gracias por su atención. 
Informe elaborado por Agustín Villalobos. 
