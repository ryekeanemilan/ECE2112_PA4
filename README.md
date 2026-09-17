# ECE2112_PA4

# Part A: Visayas Communication DataFrame

**Task:** Create a DataFrame named `VisComm` that isolates students specifically from the Visayas region who are enrolled in the Communication track[cite: 3]. After applying these filters to the source dataset, the final table must display only the students' names, genders, math scores, electronics scores, and overall averages in that exact order[cite: 3]. Both filtering conditions must be applied to the source dataset before the columns are selected[cite: 3].

---

To start, the Pandas and Matplotlib libraries are imported, and the raw dataset is loaded into a DataFrame using `pd.read_excel()`[cite: 2]. Since the provided dataset does not come with a pre-calculated average, a new `Average` column must be created manually. This is done by adding the scores from Math, Electronics, GEAS, and Communication, then dividing by four to establish a clean mean for every student[cite: 2].

```
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_excel('board2.xlsx')
df['Average'] = (df['Math'] + df['Electronics'] + df['GEAS'] + df['Communication']) / 4
```

With the data ready and the average computed, a boolean condition is set up to find rows where the `Hometown` is exactly 'Visayas' and the `Track` is 'Communication'. A separate list specifies the exact columns to keep so that the table is not cluttered with unnecessary data. Using the `.loc` accessor, the DataFrame is filtered by both the row condition and the column list simultaneously, storing the precise result in the `VisComm` variable[cite: 2]. The `print()` statement provides a clean header, and the `display()` function is called to render the filtered table neatly in the notebook[cite: 2].

```
row = (df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')
column = ['Name', 'Gender', 'Math', 'Electronics', 'Average']

VisComm = df.loc [row, column]
print("Part A: VisComm DataFrame")
display(VisComm)
```


# Part B: Visayas Female DataFrame

**Task:** Construct a DataFrame named `VisFemale` to filter out students from the Visayas region who identify as female, retaining only their names, tracks, GEAS scores, electronics scores, and averages[cite: 3]. After displaying this initial table, apply a secondary filter to showcase only the females from Visayas who achieved an average score of 60 or higher[cite: 3]. This secondary filter must not overwrite the original `VisFemale` DataFrame[cite: 3].

---

The approach here is very similar to the first part, but the filtering criteria are updated. The row filter now strictly targets students from the Visayas who are female, and the column list swaps out Gender and Math for Track and GEAS[cite: 2]. The `.loc` function applies these updated parameters to slice out the `VisFemale` DataFrame, which is immediately displayed to verify the base results[cite: 2].

```
row = (df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')
column = ['Name', 'Track', 'GEAS', 'Electronics', 'Average']

VisFemale = df.loc[row, column]
print("\nPart B: VisFemale DataFrame")
display(VisFemale)
```

For the final requirement of this section, the code must display a narrowed-down version of the newly created table based on academic performance. By placing the conditional bracket `VisFemale['Average'] >= 60` directly inside the `display()` function, the notebook successfully evaluates the scores and outputs only the passing students[cite: 2]. Because this operation happens entirely within the display call, it fulfills the requirement of not permanently altering or overwriting the original `VisFemale` variable in memory[cite: 2].

```
print("\nPart B: VisFemale with Average >= 60")
display(VisFemale[VisFemale['Average'] >= 60])
```


# Part C: Category-Average Visualization

**Task:** Examine how the students' average scores vary across their track, gender, and hometown[cite: 3]. Compute the mean average for each category, display their summary tables, and generate a single figure with three distinct bar charts to visually communicate the category with the highest sample mean for each feature[cite: 3]. This analysis describes the observed dataset only and does not establish that a feature causes a higher board-exam score[cite: 3].

---



```

```

---

**Read Me File Version History**

September 17, 2026 - Uploaded the finished `ipynb` file

September 17, 2026 - Started writing the README file

September 17, 2026 - Finished the repository
