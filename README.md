# lab07-house-prices

Laboratorio de Inteligencia de Negocios: EDA y predicción de precios con regresión lineal de mínimos cuadrados (`LinearRegression`).

## Ejecutar en DataSpell

1. Abrir esta carpeta y elegir el intérprete Conda `lab02_alca` (Python 3.11).
2. Extraer los datos oficiales en `house-prices-advanced-regression-techniques/`: `train.csv`, `test.csv`, `sample_submission.csv` y `data_description.txt`.
3. Abrir `house_prices.ipynb` y ejecutar sus celdas en orden con esta carpeta como directorio de trabajo.

DataSpell inicia el servidor Jupyter. No se necesitan `.env`, credenciales ni KaggleHub para descargar y enviar desde el navegador. Las dependencias están documentadas en `requirements.txt`.

## Versión simplificada

El notebook usa pasos directos: lectura con pandas, revisión de faltantes, histogramas, gráficos de dispersión, regresión simple, preparación de una regresión múltiple, evaluación y CSV. No contiene mapas de calor, diagramas de cajas, pipelines, ColumnTransformer ni validación cruzada.

El único regresor es `LinearRegression`. La regresión simple utiliza superficie; la múltiple utiliza nueve características numéricas y tres categóricas, convertidas con `pd.get_dummies`. Las medianas se calculan exclusivamente en entrenamiento. El precio se transforma con `np.log` y las predicciones vuelven a USD con `np.exp`. La superficie se transforma con `np.log1p`. Los atípicos se conservan.

Se reservan 292 viviendas (20%, semilla 42) para validación y se realiza el EDA sobre las 1,168 restantes. No se buscan parámetros sobre validación. La múltiple se evalúa y después se entrena con todo `train.csv` para generar el envío. La consigna debe confirmarse si exige estrictamente una variable: el PDF enseña regresión simple y esa alternativa también está incluida.

## Resultados y envío

Las métricas actualizadas aparecen en la sección 8 del notebook y en `outputs/metricas_validacion.csv`. El error local es una estimación, no un score confirmado del leaderboard. Cero significa predicción perfecta; no es un requisito realista. El R² no es porcentaje de aciertos.

- `outputs/submission.csv`: envío de la regresión múltiple, con 1,459 filas.
- `outputs/submission_simple.csv`: alternativa de una sola variable.

En Kaggle seleccionar **Submit Predictions** y adjuntar el archivo adecuado. Registrar el score recibido en la última sección del notebook. Todavía no se ha enviado desde este proyecto. Publicar el notebook es una operación independiente.

Los datos originales, credenciales y CSV generados están excluidos de Git. El notebook conserva resultados y gráficos. Se trabaja en `main`, con commits por etapa, sin PRs.

## Fuentes

- [Competencia y evaluación](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview/description).
- [Datos oficiales](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data).
- [LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html).
- Material del profesor: `PPT-BI-S07-RLAZO-202602.pdf`, consultado localmente, no incluido en Git.
