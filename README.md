# Visualización de Grandes Bases de Datos 2024-B
## Jose Luis Medrano Medrano
## 210674077

# [Challenge 1 Básico: Global Terrorism 🌍](src/challenges/Challenge_1)

Se realizó un análisis exploratorio de un dataset de terrorismo global usando pyspak. 

## Resultados 📝

### Top 5 de países con más incidentes 

| Country                       | Resultado |
|-------------------------------|-----------|
| Iraq                          | 24,636    |
| Pakistan                      | 14,368    |
| Afghanistan                   | 12,731    |
| India                         | 11,960    |
| Colombia                      | 11,960    |


### Frecuencia de incidentes del 2012 al 2017

| Year             | Frequency          |
|------------------|--------------------|
| 2017             | 10,900             |
| 2016             | 13,587             |
| 2015             | 14,965             |
| 2014             | 16,903             |
| 2013             | 12,036             |
| 2012             | 8,522              |


## Conclusiones 🔍

A partir de este análisis exploratorio, podemos concluir que el tipo de ataque terrorista más común involucra explosiones. Esto probablemente se deba al amplio impacto y la relativa facilidad de ejecución de este tipo de ataques, los cuales tienden a ser tanto impactantes como eficientes en términos de alcance.

Además, los países en el Medio Oriente son particularmente vulnerables a estos tipos de ataques, lo que resalta los desafíos geopolíticos y de seguridad que enfrenta esa región.


# [Challenge 2 Intermedio: Spark Machine Learning Wine Quality 🍷](src/challenges/Challenge_2)

Se realiza un modelo de Machine Learning usando Pyspark de un data set de calidad del vino.

## Resultados 📝

### Estadística descriptiva de algunas variables

| Summary | Quality | Alcohol | Fixed Acidity | pH |
|---------|---------|---------|---------------|-----|
| Count   | 1599    | 1599    | 1599          | 1599 |
| Mean    | 5.636   | 10.423  | 8.320         | 3.311 |
| Stddev  | 0.808   | 1.066   | 1.741         | 0.154 |
| Min     | 3       | 8.4     | 4.6           | 2.74 |
| 25%     | 5       | 9.5     | 7.1           | 3.21 |
| 50%     | 6       | 10.2    | 7.9           | 3.31 |
| 75%     | 6       | 11.1    | 9.2           | 3.4  |
| Max     | 8       | 14.9    | 15.9          | 4.01 |



### Variable objetivo

| Quality | Count |
|---------|-------|
| 6       | 638   |
| 3       | 10    |
| 5       | 681   |
| 4       | 53    |
| 8       | 18    |
| 7       | 199   |



## Conclusiones 🔍

Este análisis fue particularmente desafiante debido a que los datos estaban desbalanceados. Sin embargo, al consolidar los datos en dos clases alta calidad y baja calidad pudimos predecir con un __87%__ de precisión la calidad del vino, asegurando resultados más equilibrados y confiables.


# [Challenge 3 Avanzado: Predicción de Rotación de Personal usando Spark ML 📊](src/challenges/Challenge_3)

Se aplicaron los modelos Logistic Regression, One vs Rest, Linear SVC, Naive Bayes, Random Forest Classifier, GBT Classifier y Multileyer Perceptron Classifier para predecir la rotación de personal.

## Proceso de validación de modelos predictivos usando Spark ML 🧠

1. Se dividieron las variables categóricas y numéricas.
2. Se trataron los valores atípicos.
3. Se revisó la asimetría de las colúmnas numéricas y en la asimetría positiva se hizo una transformación log y en la negativa exp.
4. Se vectorizó la información para poder procesarla con Pyspark.
5. Se transformaron los datos ya vectorizados.
6. Se validó que no existieran valores negativos y de haberlos se reescalaron.
7. Se procesaron los datos en el modelo

## Resultados 📝

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

## Conclusiones 🔍

Los resultados de este análisis son positivos ya que se logró predecir con un __87.5%__ de precisión la rotación de personal, usando 7 variables con las que la mayoría de empresas de la industria manufacturera cuentan.

# Estructura de repositorio 🗂️
    
    ├── data                                <- Base de datos original.  
    |    |── ejercicios_avanzados           <- directorio con files de datos
    |    |── ejercicios_basicos             <- directorio con carpetas de multiples datos
    |    └── README.md                      <- Descripción general del contenido del directorio.
    |      
    ├── doc                                 <- Archivos de texto.
    |    └──  README.md                     <- Problema, objetivo y justificación del proyecto.
    |
    ├── results                             <- Base de datos limpia y analizada.  
    |    |── mapa_terrorismo.html           <- Resultado de challenge terrorismo
    |    |── rotacion_personal_clean.csv    <- Data frame previamente tratado para challenge 3
    |    |── ApacheSpark_JoseMedrano.pdf    <- Certificado de curso de Apache Spark
    |    └── README.md                      <- Resultados escritos del análisis EDA.
    |  
    ├── src                                 <- archivos de código.    
    |    |── challenges                     <- directorio con challenges
    |    |── notebooks                      <- directorio con notebooks de ejercicios
    |    └── README.md                      <- Descripción general del contenido del directorio.
    |  
    ├── CITATION.md                         <- Cómo citar el proyecto.  
    |  
    ├── CONTRIBUTING.md                     <- Pasos para contribuir al proyecto.  
    |   
    ├── LICENSE                             <- MIT License.  
    |  
    ├── README.md                           <- Readme file principal con la descripción del proyecto.  
   