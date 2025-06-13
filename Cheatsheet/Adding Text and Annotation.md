<div align="left">
  <h1> 1. Seaborn  Cheatsheet - Customizing Plot Elements

  ## Customizing Plot Elements

### 1. Build in Datasets

```shell
tips
iris
penguins
flights
diamonds
titanic
exercise
mpg
planets
anagrams
anscombe
attention
brain_networks
car_crashes
dots
dowjones
fmri
geyser
glue
healthexp
seaice
taxis
```
### 2. Load the dataset

```py
import seaborn as sns

# Load the tips dataset
tips = sns.load_dataset('tips')
```

### 3. Adding Text and Annotation

![Screenshot 2025-06-13 155851](https://github.com/user-attachments/assets/b18fc669-937a-4e47-a713-0920c8335f28)

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import matplotlib for plot customization

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Start of new code block ---

import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Create a figure and a 2x3 grid of subplots
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(20, 14)) # Increased figsize for better visibility
plt.suptitle('Titanic Data Analysis: Text & Annotation Examples', fontsize=20, color='black', y=1.02) # Global title for the figure

# --- Row 0 ---

# axes[0, 0]: Countplot - Passenger Class Distribution with plt.text
sns.countplot(x='pclass', data=df, ax=axes[0, 0], palette='viridis')
axes[0, 0].set_title('Passenger Count by Class', fontsize=14)
axes[0, 0].set_xlabel('Passenger Class (1st, 2nd, 3rd)', fontsize=12)
axes[0, 0].set_ylabel('Number of Passengers', fontsize=12)
# Add custom text using ax.text() for a specific count
# Get counts to place text accurately
class_counts = df['pclass'].value_counts().sort_index()
axes[0, 0].text(x=class_counts.index.get_loc(1), y=class_counts[1] + 10, s=f'{class_counts[1]}',
                ha='center', va='bottom', color='black', fontsize=10)
axes[0, 0].text(x=class_counts.index.get_loc(2), y=class_counts[2] + 10, s=f'{class_counts[2]}',
                ha='center', va='bottom', color='black', fontsize=10)
axes[0, 0].text(x=class_counts.index.get_loc(3), y=class_counts[3] + 10, s=f'{class_counts[3]}',
                ha='center', va='bottom', color='black', fontsize=10)


# axes[0, 1]: Histplot - Age Distribution with plt.annotate
sns.histplot(x='age', data=df.dropna(subset=['age']), kde=True, ax=axes[0, 1], color='coral', bins=25)
axes[0, 1].set_title('Age Distribution', fontsize=14)
axes[0, 1].set_xlabel('Age (Years)', fontsize=12)
axes[0, 1].set_ylabel('Frequency', fontsize=12)
# Annotate the peak age (approx. 20-30s based on common Titanic age distribution)
axes[0, 1].annotate('Young Adult Peak', xy=(25, 60), xytext=(40, 70),
                     arrowprops=dict(facecolor='black', shrink=0.05),
                     fontsize=10, color='darkred')


# axes[0, 2]: Boxplot - Fare by Passenger Class with plt.xlabel, plt.ylabel, plt.title
sns.boxplot(x='pclass', y='fare', data=df, ax=axes[0, 2], palette='cividis')
axes[0, 2].set_title('Fare Distribution by Passenger Class', fontsize=14) # ax.set_title is equivalent to plt.title on that ax
axes[0, 2].set_xlabel('Passenger Class', fontsize=12) # ax.set_xlabel is equivalent to plt.xlabel on that ax
axes[0, 2].set_ylabel('Fare (USD)', fontsize=12) # ax.set_ylabel is equivalent to plt.ylabel on that ax


# --- Row 1 ---

# axes[1, 0]: KDE Plot - Age Density by Sex
sns.kdeplot(data=df, x='age', hue='sex', fill=True, alpha=0.5, ax=axes[1, 0], palette={'male':'skyblue', 'female':'pink'})
axes[1, 0].set_title('Age Density by Gender', fontsize=14)
axes[1, 0].set_xlabel('Age', fontsize=12)
axes[1, 0].set_ylabel('Density', fontsize=12)
# Add a small text note on the plot
axes[1, 0].text(x=70, y=0.02, s='Note: Missing ages excluded.', fontsize=9, color='gray', ha='right')


# axes[1, 1]: Bar Plot - Survival Rate by Sex
survival_rate_by_sex = df.groupby('sex')['survived'].mean().reset_index()
sns.barplot(x='sex', y='survived', data=survival_rate_by_sex, ax=axes[1, 1], palette='tab10')
axes[1, 1].set_title('Survival Rate by Sex', fontsize=14)
axes[1, 1].set_xlabel('Gender', fontsize=12)
axes[1, 1].set_ylabel('Survival Rate', fontsize=12)
# Add actual survival rates on top of bars
for index, row in survival_rate_by_sex.iterrows():
    axes[1, 1].text(row.name, row.survived + 0.02, f'{row.survived:.2f}',
                    color='black', ha='center', va='bottom', fontsize=10)


# axes[1, 2]: Scatterplot - Fare vs. Age with an important point highlighted
sns.scatterplot(x='age', y='fare', data=df, ax=axes[1, 2], alpha=0.6, color='darkgreen')
axes[1, 2].set_title('Fare vs. Age', fontsize=14)
axes[1, 2].set_xlabel('Age', fontsize=12)
axes[1, 2].set_ylabel('Fare', fontsize=12)
# Annotate a high fare outlier (e.g., if there's a specific interesting point)
# Find a high fare passenger's age and fare to annotate
high_fare_passenger = df.loc[df['fare'].idxmax()]
axes[1, 2].annotate(f'Highest Fare: ${high_fare_passenger["fare"]:.0f}',
                     xy=(high_fare_passenger['age'], high_fare_passenger['fare']),
                     xytext=(high_fare_passenger['age'] + 10, high_fare_passenger['fare'] - 50), # Adjust xytext
                     arrowprops=dict(facecolor='black', shrink=0.05, width=1.5, headwidth=8),
                     fontsize=10, color='darkred', ha='left')

# Adjust layout to prevent overlapping titles/labels and ensure everything fits
plt.tight_layout(rect=[0, 0.04, 1, 0.98]) # Adjust rect to give space for suptitle and figtext

# Add global figure text using plt.figtext() - This text is relative to the figure, not axes
plt.figtext(0.5, 0.01, "Source: Titanic Dataset from Seaborn. Plots by Python & Matplotlib.",
            wrap=True, horizontalalignment='center', fontsize=10, color='gray')

# Show the plots
plt.show()

```
