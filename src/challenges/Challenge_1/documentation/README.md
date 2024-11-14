## Descriptive analysis (EDA)

To perform a descriptive analysis you have to follow the nexst steps:  

#### 1. Import required libraries

```shell
$ pip install folium==0.18.0
$ pip install pyspark==3.5.3
$ pip install matplotlib==3.8.0
$ pip install seaborn==0.13.2
```

#### 2. Data check

You have to check your data to see if there are missing values or negatives and wor from there to have it clean and perform the analysis.

```shell
null_counts = df.isnull().sum()
print(null_counts)  
```

#### 3. Create cross table

A good way to start checking your date is with cross tables that allows you to see if there are any intersting information.

```shell
df['iyear'].value_counts()  
```
```shell
df['iyear'].value_counts().reset_index().rename(columns={"index": "Year", "iyear": "Frequency"})
```

#### 4. Plot some data

After you identify some variables that can be intersting to relate, you can now plot them to see if there are intersint relations.

```shell
# Get the top 10 countries with the most cases
source = (
    df['country_txt']
    .value_counts()
    .reset_index()
    .rename(columns={"index": "Country", "country_txt": "Frequency"})
    .head(10)  # Keep only the top 10
    .to_pandas()
)

# Plot
plt.bar(source['Country'], source['Frequency'])
plt.xlabel("Country")
plt.ylabel("Frequency")
plt.title("Top 10 Countries by Frequency")
plt.xticks(rotation=90)  # Rotate country names vertically
plt.show()
```