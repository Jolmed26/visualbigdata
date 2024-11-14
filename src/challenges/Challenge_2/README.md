# Challenge Intermedio: Spark Machine Learning Wine Quality 🍷

En este estudio se realizó un modelo predictivo usando Spark para un data set de vino, donde lo que se busca predecir es la calidad del vino.

# Análisis exploratorio de datos (EDA) 🔍

Del análisis exploratorio de datos se obtienen las siguientes tablas que resultan de gran interés.


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



# Conclusiones 📝

Este análisis fue particularmente desafiante debido a que los datos estaban desbalanceados. Sin embargo, al consolidar los datos en dos clases alta calidad y baja calidad pudimos predecir con un __87%__ de precisión la calidad del vino, asegurando resultados más equilibrados y confiables.

# Setup and Run ⚙️

1. Install the required libraries:
```shell
Python version 3.11.5

$ pip install folium==0.18.0
$ pip install pyspark==3.5.3
$ pip install matplotlib==3.8.0
$ pip install seaborn==0.13.2 
```

# Get data 📥

Data is available [here](https://archive.ics.uci.edu/ml/datasets/Wine+Quality)


</details>For more details check de documentation folder.