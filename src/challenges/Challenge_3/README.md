# Challenge Avanzado: Predicción de Rotación de Personal en Empresas Manufactureras de Tala, Jalisco usando Spark ML 📊

# Análisis exploratorio de datos (EDA) 🔍

Al iniciar el análisis exploratorio de datos, la base de datos tenía 16 variables, 502 entradas y 948 valores nulos, luego del proceso de limpieza de datos se concluyó con 14 variables, 495 registros y 0 valores núlos.

Se eliminaron las variables salario diario, ya que existe salario mensual y ambas aportan la misma información, y motivo de renuncia, que por su cantidad de valores faltantes y tratarse de texto abierto, su análisis va más allá del alcance de este estudio.

También se generó una nueva variable edad usando la fecha de último registro y la fecha de nacimiento, ya que las fechas no pueden ser procesadas como parte del modelo y se eliminaron las variables motivo de renuncia, fecha de ingreso, fecha de último registro y fecha de nacimiento.

Finalmente, la visualización de datos permitió determinar que los empleados auxiliares de almacén son los que tienen una mayor rotación de personal y el personal que rola turno suele trabajar menos de 100 días antes de abandonar la empresa y que no existe una diferencia significativa entre el abandono de trabajo y el género.

# Validación de modelos predictivos usando Spark ML 🧠

Se aplicaron los modelos Logistic Regression, One vs Rest, Linear SVC, Naive Bayes, Random Forest Classifier, GBT Classifier y Multileyer Perceptron Classifier. Para poder aplicar dichos modelos se siguio el siguiente proceso:

1. Se dividieron las variables categóricas y numéricas.
2. Se trataron los valores atípicos.
3. Se revisó la asimetría de las colúmnas numéricas y en la asimetría positiva se hizo una transformación log y en la negativa exp.
4. Se vectorizó la información para poder procesarla con Pyspark.
5. Se transformaron los datos ya vectorizados.
6. Se validó que no existieran valores negativos y de haberlos se reescalaron.
7. Se procesaron los datos en el modelo

### Resumen de Resultados de Modelos

| Classifier                    | Resultado |
|-------------------------------|-----------|
| LogisticRegression            | 87.5      |
| OneVsRest                     | 87.5      |
| LinearSVC                     | 87.5      |
| MultilayerPerceptronClassifier| 87.5      |
| GBTClassifier                 | 86.02     |
| NaiveBayes                    | 85.29     |
| RandomForestClassifier        | 84.55     |


### Variables con Mayor Importancia

| Feature          | Score              |
|------------------|--------------------|
| MUNICIPIO        | 0.2730014887094737 |
| ESCOLARIDAD      | 0.2355636376708327 |
| PUESTO           | 0.22732317317624565|
| AREA             | 0.15346332704132698|
| SALARIO_MENSUAL  | 0.07310767135886306|
| GENERO           | 0.03754070204325816|
| TURNO            | 0.0                |

# Conclusiones 📝

Los resultados de este análisis son positivos ya que se logró predecir con un __87.5%__ de precisión la rotación de personal, usando 7 variables con las que la mayoría de empresas de la industria manufacturera cuentan. Resulta de gran interés aplicar estos modelos a la industria y buscar que sus predicciones no se cumplan al encontrar mejoras para la retención de personal.

# Setup and Run ⚙️

1. Install the required libraries:
```shell
Python version 3.11.5

$ pip install pyspark==3.5.3
  
```
</details> 

For more details check de documentation folder.

# Get data 📥

Data is available [here](../../../results)