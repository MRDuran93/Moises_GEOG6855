# A Practical Introduction to Google Colab for Data Analysis Workflows

## Learning Resources Used
(URL: https://www.youtube.com/watch?v=lFL-FRsn75M)

I relied on a YouTube tutorial titled *“Data analysis and graphing in Python using Google Colab”* to learn the basics of Google Colab. The video provides a clear walkthrough of the Google Colab interface, with a main focus on data preprocessing, exploratory data analysis (EDA), and visualization using Python. The presenter walks through each step of the workflow, including how to import packages, upload data files, and apply techniques for cleaning, exploring, and analyzing data within the Colab environment.

What I found most valuable is that the tutorial presents a very straightforward technical application of graphing (which I needed a year ago), making it well suited for learners looking to ease their understanding of data handling and visualization workflows in Google Colab.

---

## Using Google Colab for Data Analysis: Practical Workflow Example

For this practical case, Google Colab is used to perform real data analysis tasks by applying Python-based preprocessing and exploratory data analysis (EDA) to an example dataset. The workflow begins by setting up the Colab environment and importing commonly used Python libraries for data manipulation and visualization. In Google Colab, libraries are imported in the same way as in a local Python environment:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

If a required package is not available by default, Google Colab allows users to install it directly within the notebook using pip. This is done by prefixing the command with an exclamation mark:

```python
!pip install pandas seaborn
```
Because Colab runtimes are temporary, installed packages do not persist between sessions, and this installation step must be repeated whenever a new runtime is started.

**Data Upload and Initial Exploration**

Once the environment is set up, the dataset can be uploaded directly into the Colab session. One common approach is using the built-in file upload tool:

```python
from google.colab import files
uploaded = files.upload()
```

After uploading the dataset, it can be read into a pandas DataFrame and explored using standard inspection methods. Initial exploration is performed using functions such as ```info()``` and ```describe()``` to examine the dataset structure, data types, record counts, and the presence of missing values:

```python
df = pd.read_csv("titanic.csv")
df.info()
df.describe()
```

This step helps identify columns with null values, such as age-related variables or categorical attributes, and provides an overview of the dataset before further processing.

**Data Preprocessing and Feature Engineering**

Data preprocessing is a central component of the workflow. Columns may be renamed for clarity, and missing values are identified and addressed based on the analysis needs. For example, column renaming can be performed as follows:

```python
df.rename(columns={"Pclass": "class", "Fare": "fare"}, inplace=True)
```

The tutorial also demonstrates basic feature engineering techniques, including the creation of new categorical variables using conditional logic. For instance, passengers can be grouped by age categories:

```python
def is_old_func(row):
  return row['age'] > 60
titanic['is_old'] = titanic.apply(is_old_func, axis='columns')

#other form to define a new column
titanic.eval ('is_baby = age < 15', inplace = True)
```

Categorical variables such as passenger class can also be converted into numerical representations to support further analysis. These steps illustrate how Google Colab supports rapid iteration when modifying and testing data transformations in an interactive environment.

**Exploratory Data Analysis and Visualization**

After preprocessing, the workflow moves into exploratory data analysis and visualization. Google Colab integrates seamlessly with Python plotting libraries, allowing users to generate figures directly within the notebook. For example, age distributions can be visualized using histograms:

```python
plt.hist(df["Age"], bins=30)
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()
```

Additional visualizations, such as box plots and scatter plots, are used to explore relationships between variables like age, fare, and passenger class. Correlation heatmaps help identify positive and negative relationships among numerical variables:

```python
sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
plt.show()
```

These visual outputs are rendered inline, making it easy to interpret results and refine analysis without leaving the notebook environment.

**Summary**

Overall, this example demonstrates how Google Colab can be used to install required packages, manage datasets, and execute custom Python code in a cloud-based environment. By following a similar workflow, users with prior programming experience can quickly adapt their own scripts or notebooks to Google Colab.
