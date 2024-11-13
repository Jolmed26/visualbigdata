# Visualización de grandes bases de datos 2024-B
## Jose Luis Medrano Medrano
## 210674077

# Predicción de Rotación de Personal en Empresas Manufactureras de Tala, Jalisco 📊

En este repositorio se pretende desarrollar un modelo predictivo para la rotación de personal para empresas manufacturereras.

# Abstract 📝

En México la industria manufacturera presenta un alto porcentaje de rotación de personal, esto tiene un fuerte impacto económico en las empresas y por ende en la economía del país, buscando atender esta problemática e identificando el hecho de que no existe literatura acerca de la predicción de rotación de personal en la industria manufacturera de Jalisco, esta investigación tiene como objetivo el desarrollo y evaluación de algoritmos predictivos supervisados aplicados a la rotación de personal. 

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
| NaiveBayes                    | 85.29     |
| RandomForestClassifier        | 84.55     |
| GBTClassifier                 | 86.02     |
| MultilayerPerceptronClassifier| 87.5      |

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


# Estructura de repositorio 🗂️
    
    ├── data                            <- Base de datos original.  
    |    |── README.md                  <- Descripción general del contenido del directorio.
    |    └── rotacion_personal.xlsx     <- Base de datos.  
    |      
    ├── doc                             <- Archivos de texto.
    |    └──  README.md                 <- Problema, objetivo y justificación del proyecto.
    |
    ├── results                         <- Base de datos limpia y analizada.  
    |    └──  README.md                 <- Resultados escritos del análisis EDA.
    |  
    ├── src                             <- archivos de código.    
    |    |── EDA.ipynb                  <- Archivo de código con análisis EDA.
    |    └── README.md                  <- Descripción general del contenido del directorio.
    |  
    ├── CITATION.md                     <- Cómo citar el proyecto.  
    |  
    ├── CONTRIBUTING.md                 <- Pasos para contribuir al proyecto.  
    |   
    ├── LICENSE                         <- MIT License.  
    |  
    ├── README.md                       <- Readme file principal con la descripción del proyecto.  
   