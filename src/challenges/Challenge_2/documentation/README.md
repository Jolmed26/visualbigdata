## Spark Machin Learning Model

To perform a descriptive analysis you have to follow the nexst steps:  

#### 1. Import required libraries and start your Spark Session

```shell
from pyspark.sql import SparkSession
from itertools import chain
from pyspark.sql.functions import count, mean, when, lit, create_map, regexp_extract, desc, col

spark = SparkSession.builder.appName('classification').getOrCreate()
```

#### 2. Load your data as Spark data frame

You have to import your data, make sure that your path is correct.

```shell
df = spark.read.csv('winequality-red.csv', header=True, inferSchema=True, sep=';') 
```

#### 3. Check your data schema

You have to validate that all your variables are formated under the right format.

```shell
df.limit(5).toPandas()
```

## Exploratory data analysis (EDA)

Start the exploratory analysis to identify variables that will be transformed and remove outliers.

#### 1. Checking variable means

You have to perform the cariable mean check by sets since your data frame is huge.

```shell
df.groupBy('quality').mean('fixed acidity', 'volatile acidity', 'citric acid', 'residual sugar').show()
```

#### 2. Check your data distribution

Transform your df to a pandas df to plot it and check distribution

```shell
pandas_df = df.toPandas()
```

Plot your data to check distributions

```shell
import matplotlib.pyplot as plt
import seaborn as sns

fig, axes = plt.subplots(4, 3, figsize=(15, 16))
fig.tight_layout(pad=3.0)

columns = pandas_df.columns.drop('quality')
for i, column in enumerate(columns):
    row, col = divmod(i, 3)
    sns.histplot(pandas_df[column], kde=True, ax=axes[row, col])
    axes[row, col].set_title(f"Distribution of {column}")
    axes[row, col].set_xlabel("")
    axes[row, col].set_ylabel("Frequency")

for j in range(len(columns), 12):
    fig.delaxes(axes[3, j - 9])

plt.show()
```

## Normalize data

Normlize data using Box-Cox

#### 1. Import required libraries

```shell
import pyspark.sql.functions as F
from pyspark.ml.feature import VectorAssembler, StandardScaler
from scipy.stats import boxcox
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

#### 2. Selecting variables that will be normalized

Make sure your are chosing all the variables  you need to normilize.

```shell
skewed_columns = ['fixed acidity', 'volatile acidity', 'residual sugar', 'chlorides',
                  'free sulfur dioxide', 'total sulfur dioxide', 'sulphates', 'alcohol']
```

#### 3. Perform the normalization

We have to work in pandas since boxcox is not available in Spark. 

```shell
pandas_df = df.toPandas()

transformed_columns = {}
for column in skewed_columns:
    transformed_columns[f'{column}_boxcox'], _ = boxcox(pandas_df[column])

transformed_df = pd.DataFrame(transformed_columns)

fig, axes = plt.subplots(3, 3, figsize=(15, 12))
fig.tight_layout(pad=3.0)

for i, column in enumerate(skewed_columns):
    row, col = divmod(i, 3)
    sns.histplot(transformed_df[f'{column}_boxcox'], kde=True, ax=axes[row, col])
    axes[row, col].set_title(f"Box-Cox Transformed Distribution of {column}")
    axes[row, col].set_xlabel("")
    axes[row, col].set_ylabel("Frequency")

for j in range(len(skewed_columns), 9):
    fig.delaxes(axes[j // 3, j % 3])

plt.show()
```

## Model construction


To construct the model you would have to follow next steps once you worked your df and have it ready to work with:

#### 1. Import required libraries

```shell
from pyspark.ml.feature import StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression,\
                    RandomForestClassifier, GBTClassifier
from pyspark.ml.evaluation import MulticlassClassificationEvaluator
from pyspark.ml import Pipeline
from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
from pyspark.ml.feature import StandardScaler
from pyspark.ml.feature import VectorAssembler
```


#### 2. Vectorize data

To work with spark you have to vectorize data using the next code

```shell
vec_asmbl = VectorAssembler(inputCols=df.columns[:10],
                           outputCol='features')

df1 = vec_asmbl.transform(df).select('features', 'y_binary')
df1.show(4, truncate=False)
```

#### 3. Scaled Features 

To get better results data have to be scaled using standar scaler:

```shell
scaler = StandardScaler(inputCol="features", outputCol="scaledFeatures",
                        withStd=True, withMean=True)

scalerModel = scaler.fit(df1)

scaledData = scalerModel.transform(df1)

scaledData.show(4, truncate=False)
```

#### 4. Get the clasifier set and get your data split

This is quite simple, you have to ser your classifier, in this model we use LogisticRegression.

```shell
# Deffine the clasifier 
ridge = LogisticRegression(labelCol='y_binary',
                        maxIter=100,
                        elasticNetParam=0, # Ridge regression is choosen
                        regParam=0.03)

model = ridge.fit(train_df)
pred = model.transform(valid_df)
evaluator.evaluate(pred)

# Spliting data into test and training
train_df, valid_df = scaledData.randomSplit([0.7, 0.3])
```
Make sure of update your `test_size` to what you need for your model, in this case, this values gave extraordinary results.

#### 3. Evaluate your model

To evaluate your model you will use accuracy:

```shell
evaluator = MulticlassClassificationEvaluator(labelCol='y_binary',
                                          metricName='accuracy')
```


```shell
evaluator.evaluate(pred)
```



