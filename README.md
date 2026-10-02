# lab07-house-prices

Laboratorio de Inteligencia de Negocios: EDA y solución de House Prices mediante regresión lineal de mínimos cuadrados (`LinearRegression`).

## Ejecutar en DataSpell

1. Abrir esta carpeta y seleccionar el intérprete del entorno Conda `lab02_alca` (Python 3.11).
2. Descargar los datos oficiales después de aceptar las reglas de Kaggle y extraerlos en `house-prices-advanced-regression-techniques/`.
3. Verificar que allí estén `train.csv`, `test.csv`, `sample_submission.csv` y `data_description.txt`.
4. Abrir `house_prices.ipynb` y ejecutar todas las celdas en orden, con la carpeta del proyecto como directorio de trabajo.

No es necesario ejecutar `jupyter notebook` manualmente. El entorno existente ya tiene las dependencias; `requirements.txt` documenta las versiones verificadas. No se requieren `.env`, tokens ni KaggleHub para el flujo por navegador. No subir los datos ni credenciales a Git.

## Método

El notebook presenta EDA, regresión simple de precio sobre superficie, comprobación manual de mínimos cuadrados y una extensión múltiple con un grupo de características numéricas y categóricas. Todos los modelos usan `LinearRegression`; no se usan otros regresores.

Se reserva 20% para validación antes del EDA. Dentro del 80% restante, una validación cruzada de cinco particiones compara modelos lineales sobre logaritmos. La imputación y la codificación se ajustan exclusivamente en entrenamiento mediante pipelines. Los atípicos se muestran y conservan. El modelo seleccionado se evalúa una vez sobre validación y luego se reentrena con todos los datos conocidos.

La extensión múltiple está separada del ejemplo simple y queda sujeta a confirmar si el profesor permite varios predictores. El PDF de clase trata regresión simple; no demuestra por sí mismo que la múltiple esté prohibida.

## Resultados locales verificados

Partición reproducible: `random_state=42`, 1,168 filas de desarrollo y 292 de validación.

| Modelo | MAE USD | RMSE USD | R² | RMSE log |
| --- | ---: | ---: | ---: | ---: |
| Simple original | 38,341.20 | 58,471.76 | 0.5543 | 0.28751 |
| Múltiple sobre log(precio) | 16,270.63 | 27,467.17 | 0.9016 | 0.12943 |

RMSE log promedio de validación cruzada del modelo múltiple: **0.13258**, desviación estándar entre particiones: **0.01690**. Son métricas locales, no un resultado confirmado de Kaggle. Cero significa error perfecto; no es un requisito realista. El R² no se interpreta como porcentaje de aciertos.

## Archivos generados

- `outputs/submission.csv`: 1,459 precios del modelo seleccionado por validación cruzada (múltiple en la ejecución verificada).
- `outputs/submission_simple.csv`: alternativa estrictamente simple, si la consigna lo exige.
- `outputs/metricas_validacion.csv` y `outputs/metricas_cv.csv`: resultados locales.

Los CSV generados se excluyen de Git y se recrean al ejecutar el notebook. El notebook guardado incluye salidas y gráficos para revisar y presentar.

## Enviar a Kaggle

En la competencia, seleccionar **Submit Predictions**, adjuntar `outputs/submission.csv` y registrar el score recibido en la última sección del notebook. Si el profesor exige una variable, enviar `submission_simple.csv`. No enviar precios logarítmicos. Estar en el leaderboard requiere completar y evaluar el envío: todavía no se ha enviado desde este proyecto.

Git se trabaja sobre `main`, con commits por avance, sin necesidad de GitFlow ni PRs.

## Fuentes

- [Competencia y evaluación](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview/description).
- [Datos oficiales y diccionario](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data).
- [Documentación de LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html).
- Material del curso: `PPT-BI-S07-RLAZO-202602.pdf`, diapositivas 5–7 y 15–18; consultado localmente y no incluido en el repositorio.
