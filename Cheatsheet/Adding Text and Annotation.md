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

### 3. Understanding the Canvas: Figure and Axes

#### A. Figure: This is the entire window or canvas that contains all your plot elements. Think of it as the piece of paper you draw on. You typically create it using plt.figure() or implicitly with plt.subplots().
#### B. Axes: This is the actual plotting area within the Figure where your data is drawn. Each Axes object has its own x-axis, y-axis, title, and labels. A single Figure can contain multiple Axes objects (subplots). You usually get Axes objects from plt.subplots().

<img width="683" height="465" alt="Screenshot 2025-07-13 205509" src="https://github.com/user-attachments/assets/98a963b4-2f8f-4cb5-bebc-5d9206dee4b2" />

```py
import matplotlib.pyplot as plt

# Create a Figure and a single Axes (subplot)
# fig is the Figure object, ax is the Axes object
fig, ax = plt.subplots(figsize=(8, 5))

# Add a simple plot to demonstrate
ax.plot([0, 1, 2], [10, 15, 12])

# Set basic labels and title for the Axes
ax.set_title('Simple Plot Example')
ax.set_xlabel('X-axis Label')
ax.set_ylabel('Y-axis Label')

# Display the plot
plt.show()
```

### 4. Adding Simple Text within an Axes (ax.text())

The ax.text() method allows you to place arbitrary text at specific data coordinates on your plot.
#### A. x, y: The data coordinates where the text should be placed.
#### B. s: The string of text to display.
#### C. ha (horizontal alignment): 'left', 'center', 'right'.
#### D. va (vertical alignment): 'top', 'center', 'bottom', 'baseline'.
#### E. fontsize, color, fontweight: Control text appearance.
#### F. bbox: A dictionary to create a background box around the text (e.g., dict(facecolor='yellow', alpha=0.5)).

<img width="698" height="468" alt="Screenshot 2025-07-13 205657" src="https://github.com/user-attachments/assets/367d5321-3949-4b8a-a790-d6158e609c58" />

```py
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots(figsize=(8, 5))
x_data = np.linspace(0, 10, 50)
y_data = np.sin(x_data) + np.random.normal(0, 0.1, 50)
ax.plot(x_data, y_data)

ax.set_title('Plot with Simple Text')
ax.set_xlabel('Time')
ax.set_ylabel('Value')

# Add text at a specific point
ax.text(x=2, y=0.8, s='Important Peak!', fontsize=12, color='red',
        ha='center', va='bottom')

# Add text with a background box
ax.text(x=8, y=-0.5, s='Data Range', fontsize=10, color='blue',
        bbox=dict(facecolor='lightblue', alpha=0.6, edgecolor='blue', boxstyle='round,pad=0.5'))

plt.show()
```

### 5. Annotating Specific Points with Arrows (ax.annotate())

The ax.annotate() method is used to add text with an optional arrow pointing from the text to a specific data point, making it ideal for highlighting features.
#### A. text: The string of text for the annotation.
#### B. xy: The (x, y) coordinates of the data point being annotated (where the arrow points to).
#### C. xytext: The (x, y) coordinates where the text itself should be placed.
#### D. arrowprops: A dictionary to customize the arrow. Common keys:
   * facecolor: Color of the arrow.
   * shrink: Shrink the arrow from both ends (0 to 1).
   * width: Width of the arrow shaft.
   * headwidth: Width of the arrow head.
   * headlength: Length of the arrow head.
   * connectionstyle: Style of the connection (e.g., 'arc3,rad=0.3').
#### E. fontsize, color, ha, va: Text properties, similar to ax.text()

<img width="683" height="468" alt="Screenshot 2025-07-13 205816" src="https://github.com/user-attachments/assets/f6b59f49-aab6-4050-a0f7-5abd05a3d07b" />

    
```py
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots(figsize=(8, 5))
x_data = np.arange(10)
y_data = np.array([5, 7, 8, 10, 12, 15, 13, 11, 9, 6])
ax.plot(x_data, y_data, marker='o')

ax.set_title('Plot with Annotation')
ax.set_xlabel('Index')
ax.set_ylabel('Value')

# Annotate the maximum value
max_idx = np.argmax(y_data)
ax.annotate('Maximum Value!',
            xy=(x_data[max_idx], y_data[max_idx]), # Pointing to (5, 15)
            xytext=(x_data[max_idx] + 2, y_data[max_idx] - 3), # Text position
            arrowprops=dict(facecolor='purple', shrink=0.05, width=2, headwidth=8),
            fontsize=12, color='purple', ha='left')

plt.show()
```

### 6. Figure-Level Text: plt.suptitle() and plt.figtext()

Sometimes you need text that applies to the entire figure, especially when you have multiple subplots.
#### A. plt.suptitle(): Adds a super title to the entire Figure.
   * t: The title string.
   * fontsize, color, fontweight: Text properties.
   * y: Vertical position (0 to 1, relative to figure height).
#### B. plt.figtext(): Adds text anywhere on the Figure, specified by relative coordinates (0 to 1).
   * x, y: Relative coordinates (0 to 1) within the Figure.
   * s: The text string.
   * ha, va: Horizontal and vertical alignment.
   * wrap: If True, wraps text automatically.

<img width="1187" height="539" alt="Screenshot 2025-07-13 205920" src="https://github.com/user-attachments/assets/0f27cb55-1ae0-4294-8edb-a3badeade4a7" />


```py
import matplotlib.pyplot as plt
import numpy as np

# Create a Figure with 2 subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

ax1.plot(np.random.rand(10))
ax1.set_title('Subplot 1')

ax2.plot(np.random.rand(10), color='orange')
ax2.set_title('Subplot 2')

# Add a super title to the entire figure
plt.suptitle('Overall Figure Title', fontsize=16, fontweight='bold', color='darkblue', y=1.05)

# Add a source note at the bottom of the figure
plt.figtext(0.5, 0.01, "Data Source: Generated Randomly. Plots by Matplotlib.",
            wrap=True, horizontalalignment='center', fontsize=9, color='gray')

plt.tight_layout(rect=[0, 0.05, 1, 0.95]) # Adjust layout to make space for suptitle and figtext
plt.show()
```

### 7. Comprehensive Example: Combining Text and Annotations

This example demonstrates how to use ax.text(), ax.annotate(), ax.set_title(), ax.set_xlabel(), ax.set_ylabel(), plt.suptitle(), and plt.figtext() together to create a detailed and informative multi-panel plot.

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
