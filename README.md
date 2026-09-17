# ECE2112-PA-4

Isaac Benedict R. Deangkinay

  This repository contains the code itself in python language containing three problems that utilizes Pandas with Data Wrangling and Visualization in order to create solutions in running each code for specific type of problems that needs wrangling and visualization of tables. In this specific assignment, the code utilized ```board2.xlsx``` in order to perform data wrangling and data visualization on a data frame inside the excel file.
  
  ### Universal Function
```python
import pandas as pd
import matplotlib.pyplot as plt

ECE_BOARD_EXAM_2 = pd.read_excel('board2.xlsx')
display(ECE_BOARD_EXAM_2)

df = pd.DataFrame(data, columns=['index']).copy()
```
These functions will work through all the three problems of the assignment. 

* ```import pandas as pd``` imports pandas as a shortened version pd for every beginning line of each code that utilizes pandas functions.
* ```import matplotlib.pyplot as plt``` imports matplot.lib as a shortened version plt for every beginning of a code that plots a chart.
* ```ECE_BOARD_EXAM_2 = pd.read_excel('board2.xlsx')``` reads a specific .xlsx file located in the directory where the .ipynb file is. It will then be displayed using ```display(ECE_BOARD_EXAM_2)```
* ```df = pd.DataFrame(data, columns=['index']).copy()``` this specific function will only be utilized on pandas' syntax that requires slicing data frames. The extension ```.copy()``` allocates a separate memory for each df, allowing modifications without warning. (This is only applied when the code displays a warning where it says "A value is trying to be set on a copy of a slice from a DataFrame.")

# A. VISAYAS COMMUNICATION DATAFRAME
> OBJECTIVES: Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order: Name, Gender, Math, Electronics, Average Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

## Discussion
### Functions 
```python
VisComm = ECE_BOARD_EXAM_2.loc[(ECE_BOARD_EXAM_2['Hometown']=='Visayas') & (ECE_BOARD_EXAM_2['Track']=='Communication')].copy()
```
This filters two specific categories where the condition of the ```Hometown``` index will only be in ```Visayas``` and the ```Track``` will only be in ```Communication```. Running this function will slice the dataset leaving only the two specific conditions of the index.

```python
VisComm['Average'] = VisComm[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
```
This will select four subject grade columns and calculates the row wise average across those four subjects using ```.mean(axis=1)```. This will be stored within a dataframe named ```VisComm```

```python
VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]
```
This filters and reorders ```Viscomm``` in order to keep specific categories which are Name, Gender, Math, Electronics, and the Average.

```python
display(VisComm)
print('Number of rows', len(VisComm))
```
This will display the filtered ```Viscomm``` together with a printed number of rows with the length of the data frame, in this case, it is 5.

# B. VISAYAS FEMALE DATAFRAME
>OBJECTIVES: Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only: Name, Track, GEAS, Electronics, Average Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.

## Discussion
### Functions
```python
VisFemale = ECE_BOARD_EXAM_2.loc[(ECE_BOARD_EXAM_2['Gender']=='Female') & (ECE_BOARD_EXAM_2['Hometown']=='Visayas')].copy()
```
This filters two specific categories where the condition of the ```Gender``` index will only be in ```Female``` and the ```Hometown``` will only be in ```Visayas```. Running this function will slice the dataset leaving only the two specific conditions of the index.

```python
VisFemale['Average'] = VisFemale[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
```
This will select four subject grade columns and calculates the row wise average across those four subjects using ```.mean(axis=1)```. This will be stored within a dataframe named ```VisFemale```

```python
VisFemale = VisFemale [['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
```
This filters and reorders ```VisFemale``` in order to keep specific categories which are Name, Track, GEAS, Electronics, and the Average.


```python
display(VisFemale)
```
This displays the filtered ```VisFemale```.

```python
VisFemale = VisFemale.loc[(VisFemale['Average']>=60)]
display(VisFemale)
```
This will filter once again ```VisFemale``` and reorder it using a specific condition of an Average of atleast 60 and select only those who got 60 and above as an average. This will then be displayed using the function ```display(VisFemale)```

# C. CATEGORY-AVERAGE VISUALIZATION
>OBJECTIVES: Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown.
>* For each feature, compute the mean of Average for every category using Pandas.
>* Display the three summary tables.
>* Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown.
>* Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.
>  
>Interpretation rule: Describe the observed dataset only. A difference in group means does not, by itself, establish that a feature causes a higher board-exam score.

## Discussion
### Functions
```python
Track_mean = ECE_BOARD_EXAM_2[['Name', 'Track', 'Math', 'Electronics', 'GEAS', 'Communication']].copy()
Track_mean['Average'] = ECE_BOARD_EXAM_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
Track_mean = Track_mean.pivot_table(index = ['Track'], values = 'Average').reset_index()

Gender_mean = ECE_BOARD_EXAM_2[['Name', 'Gender', 'Math', 'Electronics', 'GEAS', 'Communication']].copy()
Gender_mean['Average'] = ECE_BOARD_EXAM_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
Gender_mean = Gender_mean.pivot_table(index = ['Gender'], values = 'Average').reset_index()

Hometown_mean = ECE_BOARD_EXAM_2[['Name', 'Hometown', 'Math', 'Electronics', 'GEAS', 'Communication']].copy()
Hometown_mean['Average'] = ECE_BOARD_EXAM_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
Hometown_mean = Hometown_mean.pivot_table(index = ['Hometown'], values = 'Average').reset_index()
```
These functions will act similarly to each specific chosen index. 

```data_mean = ECE_BOARD_EXAM_2[['Name', 'data', 'Math', 'Electronics', 'GEAS', 'Communication']]``` will only select a specific data to be stored in a specific dataframe, in this case it has three, Track_mean, Gender_mean, and Hometown_mean. 

```data_mean['Average'] = ECE_BOARD_EXAM_2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)``` This will select four subject grade columns and calculates the row-wise average across those four subjects using ```.mean(axis=1)```. This will be stored within a specific dataframe which will be named either Track_mean, Gender_mean, and Hometown_mean. 

```data_mean = data_mean.pivot_table(index = ['data'], values = 'Average').reset_index()``` calculates the overall mean of the average column grouped by each category. ```.reset_index``` transforms the grouped index back into a regular dataframe columns for a chart visualization.

```display(data_mean)``` will display all the specific category mean, mainly Track, Gender, and Hometown.

```python
fig, axes = plt.subplots(1, 3, figsize=(18,5))

axes[0].bar(Track_mean['Track'], Track_mean['Average'])
axes[0].set(title = 'Mean Average by Track')
axes[0].set(xlabel = 'Track')
axes[0].set(ylabel = 'Mean Average')
axes[0].set(ylim = (0, 70))

axes[1].bar(Gender_mean['Gender'], Gender_mean['Average'])
axes[1].set(title = 'Mean Average by Gender')
axes[1].set(xlabel = 'Gender')
axes[1].set(ylabel = 'Mean Average')
axes[1].set(ylim = (0, 70))

axes[2].bar(Hometown_mean['Hometown'], Hometown_mean['Average'])
axes[2].set(title = 'Mean Average by Hometown')
axes[2].set(xlabel = 'Hometown')
axes[2].set(ylabel = 'Mean Average')
axes[2].set(ylim = (0, 70))
```
These sets of function will work similarly and will display three types of charts.

```plt.subplots(1, 3 figsize=(18,5))``` initializes a single horizontal figure window containing 3 subplots arranged side-by-side with a width of 18 inches and a height of 5 inches.

```axes[0]``` will be th first chart which is equivalent to the Track_mean.

```axes[1]``` will be the second chart which is equivalent to the Gender_mean

```axes[2]``` will be the third chart which is equivalent to the Hometown_mean

```.bar(dataframe_mean['dataframe'], dataframe_mean['Average'])``` will display the average in a bar graph with their values at the left side y-axis.

```.set(title = 'Mean Average by dataframe')``` will display its title. Together with ```.set(xlabel = 'dataframe')``` will display the values of the x axis based on the specific category. ```.set(ylabel = 'Average')``` will display the word "Average" with respect to the y-axis.

## HISTORY OF README FILE
* September 17, 2026: Creation of the repository and readme file. Creating an in depth discussion from problems 1 - 3

### Thank you and Godbless!
