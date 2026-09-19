 # PA4 | ECE2112 | EXPERIMENT 4 | PUNONGBAYAN
### **DATA WRANGLING AND DATA VISUALIZATION**
#### Submitted by: Punongbayan, AJ Andriz J. | 2ECE-A | 09.19.2026

This repository showcases the objective and detailed discussion of the experiment from the Programming Assignment 4 last September 8, 2026 where the class discussed Module 4 - **Data Wrangling and Data Visualization**

---
### **Objectives**
---
At the end of this laboratory activity, the student should be able to:

1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.

The students are also expected to use the same ECE Board Exam 2 dataset supplied for Experiment 4. Work in a Jupyter Notebook using Pandas and a Python plotting library used in class. Use the dataset’s existing column labels, including Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.
- Derive all tables and plot values from the dataset. Do not manually type rows, category means, or plotted values.
- When applying more than one condition, make every condition explicit in the filtering expression.
- Keep the original DataFrame unchanged.
- Every graph must have a title, axis labels, readable category labels, and a consistent scale appropriate to the data.

---
### **Programming Problems**
---
#### **A. VISAYAS COMMUNICATION DATAFRAME**

Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order:
`Name, Gender, Math, Electronics, Average`
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

**CODE**
```
df = pd.read_excel('board2.xlsx') // this reads and stores the board2 file to *df*
df ['Average'] = (df.Math + df.Electronics + df.GEAS + df.Communication)/4 //this adds a new column labelled 'Average' with the function of getting the average of all subjects

display (df)

VisComm = df[(df['Hometown'] == 'Visayas') & 
             (df['Track'] == 'Communication')
             ][['Name', 'Gender', 'Math', 'Electronics', 'Average']] // this sets viscomm as the new data frame that filters out other columns to 'Name', 'Gender', 'Math', 'Electronics', 'Average' and data values only to those whose hometown is 'Visayas' and track is 'Communication'

display (VisComm)

print ("Number of rows:", len (VisComm))
```


---
#### **B. VISAYAS FEMALE DATAFRAME**

Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only:
`Name, Track, GEAS, Electronics, Average`
Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.

**CODE**
```
VisFemale = df[(df['Hometown']=='Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
display (VisFemale)

// this sets visfemale as the new data frame that filters out the other columns to 'Name', 'Track', 'GEAS', 'Electronics', 'Average' and data values only to those in visayas and the gender is female

print ("\nFemale Students in Visayas whose average in GEAS and Electronics is atleast 60")
display (VisFemale[VisFemale['Average']>=60])
```



---
#### **C. CATEGORY-AVERAGE VISUALIZATION**

Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.

a. For each feature, compute the mean of Average for every category using Pandas.
b. Display the three summary tables.
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown.
d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

**Interpretation rule**: Describe the observed dataset only. A difference in group means does not, by itself, establish that a feature causes a higher board-exam score.

**CODE**
```
mean_track = df.groupby('Track')['Average'].mean().reset_index()
mean_gender = df.groupby('Gender')['Average'].mean().reset_index()
mean_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

print("\nMean Average by Track")
display(mean_track)

print("\nMean Average by Gender")
display(mean_gender)

print("\nMean Average by Hometown")
display(mean_hometown)

fig, axes = plt.subplots(1, 3, figsize=(18, 5), sharey=True)
fig.suptitle('Mean of Board Exam Average across the three Categorical Features', fontsize=16, fontweight='bold')

axes[0].bar(mean_track['Track'], mean_track['Average'], color='#2b5c8f')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average Score')
axes[0].set_ylim(0, 100)

axes[1].bar(mean_gender['Gender'], mean_gender['Average'], color='#2e7d32')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average Score')

axes[2].bar(mean_hometown['Hometown'], mean_hometown['Average'], color='#e65100')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average Score')

plt.tight_layout()
plt.show()

highest_track = mean_track.loc[mean_track['Average'].idxmax(), 'Track']
highest_gender = mean_gender.loc[mean_gender['Average'].idxmax(), 'Gender']
highest_hometown = mean_hometown.loc[mean_hometown['Average'].idxmax(), 'Hometown']

print("\nInterpretation Statements")
print(f"\n1. Among the tracks, the {highest_track} track obtained the highest sample mean for Average.")
print(f"2. Between genders, {highest_gender} students achieved the highest sample mean for Average.")
print(f"3. Across the hometown regions, students from {highest_hometown} recorded the highest sample mean for Average.")
```

### **END OF NOTEBOOK**
