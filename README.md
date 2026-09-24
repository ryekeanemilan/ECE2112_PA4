# ECE2112_PA4

# Part A: Visayas Communication DataFrame

**Task:** Create a DataFrame named `VisComm` that isolates students specifically from the Visayas region who are enrolled in the Communication track. After applying these filters to the source dataset, the final table must display only the students' names, genders, math scores, electronics scores, and overall averages in that exact order. Both filtering conditions must be applied to the source dataset before the columns are selected.

---

To start, the Pandas and Matplotlib libraries are imported, and the raw dataset is brought to life as a Dataframe using `pd.read_excel()`. Since the provided dataset does not include an' Average' column, a new `Average` column must be computed manually and added. This is done by adding the scores from Math, Electronics, GEAS, and Communication, then dividing by 4 to obtain a mean for each student.

```
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_excel('board2.xlsx')
df['Average'] = (df['Math'] + df['Electronics'] + df['GEAS'] + df['Communication']) / 4
```

A boolean condition is set up to find people where their `Hometown` is  exactly 'Visayas' and the `Track` is 'Communication'. A separate specifies the only required columns tasked for this problem. Using `.loc`  the DataFrame is filtered by both the row condition and the column list at the same time, storing the result in `VisComm`. The `print()` statement provides a clean header, and the `display()` function is called to act as a check for the processed table.

```
row = (df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')
column = ['Name', 'Gender', 'Math', 'Electronics', 'Average']

VisComm = df.loc [row, column]
print("Part A: VisComm DataFrame")
display(VisComm)
```


# Part B: Visayas Female DataFrame

**Task:** Construct a DataFrame named `VisFemale` to filter out students from the Visayas region who identify as female, retaining only their names, tracks, GEAS scores, electronics scores, and averages. After displaying this initial table, apply a secondary filter to showcase only the females from Visayas who achieved an average score of 60 or higher. This secondary filter must not overwrite the original `VisFemale` DataFrame.

---

The approach here is very similar to the first part, but the filtering criteria are updated. The row filter now strictly targets students from the Visayas who are female, and the column list swaps out Gender and Math for Track and GEAS. The `.loc` function applies these updated parameters to slice out the `VisFemale` DataFrame, which is immediately displayed to verify the base results.

```
row = (df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')
column = ['Name', 'Track', 'GEAS', 'Electronics', 'Average']

VisFemale = df.loc[row, column]
print("\nPart B: VisFemale DataFrame")
display(VisFemale)
```

For the final requirement of this section, the code must display a narrowed-down version of the newly created table based on academic performance. By placing the conditional bracket `VisFemale['Average'] >= 60` directly inside the `display()` function, the notebook successfully evaluates the scores and outputs only the passing students. 

```
print("\nPart B: VisFemale with Average >= 60")
display(VisFemale[VisFemale['Average'] >= 60])
```


# Part C: Category-Average Visualization

**Task:** Examine how the students' average scores vary across their track, gender, and hometown. Compute the mean average for each category, display their summary tables, and generate a single figure with three distinct bar charts to visually communicate the category with the highest sample mean for each feature. This analysis describes the observed dataset only and does not establish that a feature causes a higher board-exam score.

---

The mean averages are obtained through the `pivot_table()` function. By default, it automatically calculates the mean of the Average values grouped by the specified index, which in this case are Track, Gender, and Hometown. `reset_index()` at the end turns those indexes back into regular columns, so the resulting data is clean and easy to plot. The `print()` and `display()` functions then output these three summary tables directly to the notebook for checking.

```
Track_Average = df.pivot_table(index = 'Track', values = 'Average').reset_index()

Gender_Average = df.pivot_table(index = 'Gender', values = 'Average').reset_index()

Hometown_Average = df.pivot_table(index = 'Hometown', values = 'Average').reset_index()

print("\nTrack Average:")
display(Track_Average)

print("\nGender Average:")
display(Gender_Average)

print("\nHometown Average:")
display(Hometown_Average)
```

`plt.subplots(1, 3)` creates a single figure containing one row with three side-by-side plotting slots. The `figsize=(20, 5)` argument makes the entire figure wide enough to accommodate all three charts comfortably without squishing the data or overlapping the text.

```
fig, axes = plt.subplots(1, 3, figsize=(20, 5))
```
Each slot is filled using the `.bar()` function. For each chart, it passes the categorical column for the x-axis and the calculated averages for the y-axis. Every subplot is given a specific title using `.set_title()` and clear x and y labels using `.set()`.
```
axes[0].bar(Track_Average['Track'], Track_Average['Average'])
axes[0].set_title('Mean Average by Track')
axes[0].set(xlabel = "Track")
axes[0].set(ylabel = "Mean Average")

axes[1].bar(Gender_Average['Gender'], Gender_Average['Average'])
axes[1].set_title('Mean Average by Gender')
axes[1].set(xlabel = "Gender")
axes[1].set(ylabel = "Mean Average")

axes[2].bar(Hometown_Average['Hometown'], Hometown_Average['Average'])
axes[2].set_title('Mean Average by Hometown')
axes[2].set(xlabel = "Hometown")
axes[2].set(ylabel = "Mean Average")
```

`fig.text()` embeds the text directly onto the bottom-left corner of the bar chart image itself. To ensure the text block doesn't overlap with the charts, `plt.tight_layout(rect=[0, 0.15, 1, 1])` squeezes the plots upward, leaving a 15% margin at the bottom before `.show()` renders the final graphic.

```
interpretation = ("1. Track: The Communiations Track has the highest mean average.\n"
                   "2. Gender: Males recorded the highest mean average \n"
                   "3. Students from Luzon have the highest mean average" )

fig.text(0.001 , 0.01, interpretation)
plt.tight_layout(rect=[0, 0.15, 1, 1])
plt.show()
```

---

**Read Me File Version History**

September 17, 2026 - Uploaded the finished `ipynb` file

September 17, 2026 - Started writing the README file

September 17, 2026 - Finished the repository
