## Spark Machine Learning Model function and Data Preprocessing function

To use functions df_treat and ClassTrainEval you have to follow the nexst steps:  

#### 1. Import required libraries and start your Spark Session

```shell
from pyspark.sql import SparkSession
from pyspark.ml.feature import VectorAssembler
from pyspark.sql.types import *
from pyspark.sql.functions import *
from pyspark.ml.feature import StringIndexer
from pyspark.ml.feature import MinMaxScaler
from pyspark.sql import functions as F

from pyspark.ml.classification import *
from pyspark.ml.evaluation import *
from pyspark.sql.functions import *
from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
```
```shell
spark = SparkSession.builder.appName("rotacion").master("local[*]").config("spark.executor.memory", "2g").config("spark.driver.memory", "2g").getOrCreate()


cores = spark._jsc.sc().getExecutorMemoryStatus().keySet().size()

print("Se tienen ", cores, "núcleo(s)")

spark
```

#### 2. Load your data as Spark data frame

You have to import your data, make sure that your path is correct.

```shell
df = spark.read.csv('rotacion_personal_clean.csv',inferSchema=True,header=True)
```

#### 3. Check your data schema

You have to validate that all your variables are formated under the right format.

```shell
df.printSchema()
```

## Data frame treatment function

This function will rename the target variable, divide the data into numeric and string DataFrames, treat outliers, check asymmetry using log or exp transformations as needed, handle negative values and rescale if necessary, and vectorize the data.



#### 1. Update your target variable

In this case "ESTATUS" is my target variable, make sure to update to yours if needed.

```shell
def df_treat(df,input_columns,target,treat_outliers=False,treat_neg=False):

    # Puede ser que target no sea string
    df_renamed = df.withColumn("label_str",df[target].cast(StringType()))

    # variable target string -> numeric/dummy/boolean/onehotencoder
    indexer = StringIndexer(inputCol="label_str",
                            outputCol="label") # por default pyspark target es "label"
    df_indexed = indexer.fit(df_renamed).transform(df_renamed)
    print(df_indexed.groupBy("ESTATUS","label").count().show())
```

#### 2. Set funtion parameters

You have to set function parameters accordingly,  

```shell
input_columns = input_columns[1:-1] # la última entrada es la variable objetivo
target = 'ESTATUS' # variable objetivo
estatus_count = df.select(countDistinct("ESTATUS")).collect() #Cuenta valors únicos en la variable objetivo
estatuses = estatus_count[0][0] # Buscamos el valor total del conteo
```
#### 3. Call the function

Apply the function to your DF

```shell
test1_data = df_treat(df,input_columns,target,treat_outliers=False,treat_neg=False)
test1_data.limit(5).toPandas()
```

## Data frame Classification, Training and Evaluation function

This function will identify which models you are setting and train, perform and evaluate each model chosen.

#### 1. Update model parameters

Each model has its own parameters you will see those chose by me but you are free to update them.

```shell
 if Mtype == "MultilayerPerceptronClassifier":
            # se especifican las capas de la red neuronal
            # Capa de entrada de características de tamaño, dos intermedias de características +1 y del mismo tamaño que las características y salida de tamaño número de clases
            # Nota: validacion cruzada no puede utilizarse aquí
            features_count = len(features[0][0])
            layers = [features_count, features_count+1, features_count, classes]
            MPC_classifier = MultilayerPerceptronClassifier(maxIter=100, layers=layers, blockSize=128, seed=1234)
            fitModel = MPC_classifier.fit(train)
            return fitModel
```

#### 2. Chose your models

Make a list of those models that you are intersted in ussing, you can commento those that you won't use.

```shell
classifiers = [
               LogisticRegression()
              ,OneVsRest()
              ,LinearSVC()
              ,NaiveBayes()
              ,RandomForestClassifier()
              ,GBTClassifier()
              ,DecisionTreeClassifier()
              ,MultilayerPerceptronClassifier()
              ]
```

#### 3. Get ready

Split your data into train and evaluation, chose the porcentages you want to use.

```shell
train,test = test1_data.randomSplit([0.7,0.3])
features = test1_data.select(['features']).collect()
folds = 2
```

#### 4. Call the function

You already did everything now it is just a matter of calling your function.

```shell
for classifier in classifiers:
    new_result = ClassTrainEval(classifier,features,estatuses,folds,train,test)
    results = results.union(new_result)
results = results.where("Classifier!='Place Holder'")
print("!!!!!Resultados finales!!!!!!!!")
results.show(100,False)
```