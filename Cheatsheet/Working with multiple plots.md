<div align="left">
  <h1> 1. Seaborn  Cheatsheet - Working with multiple plots

  ## Working with multiple plots

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

### 3. Baseline - Building multiple plots

![Screenshot 2025-06-13 145515](https://github.com/user-attachments/assets/d66cb87a-cd34-4d22-8110-9509d5b5102b)


```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import matplotlib for plotting functionalities

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Implementation of plt.figure(), plt.subplot(), fig.add_subplot() ---

# 1. Create a figure explicitly using plt.figure()
# This creates a new figure, which is the overall window/area where plots are drawn.
fig = plt.figure(figsize=(15, 7)) # Optional: set the size of the figure

# 2. Use plt.subplot(nrows, ncols, index) to add subplots
# This method directly adds a subplot to the current figure and makes it the active axes.
# Here, we create a 2x2 grid, and select the first subplot (top-left).
ax1 = plt.subplot(2, 2, 1) # 2 rows, 2 columns, 1st subplot
ax1.hist(df['age'].dropna(), bins=20, color='skyblue', edgecolor='black')
ax1.set_title('Age Distribution')
ax1.set_xlabel('Age')
ax1.set_ylabel('Count')

# Select the second subplot (top-right)
ax2 = plt.subplot(2, 2, 2) # 2 rows, 2 columns, 2nd subplot
ax2.hist(df['fare'], bins=30, color='lightcoral', edgecolor='black')
ax2.set_title('Fare Distribution')
ax2.set_xlabel('Fare')
ax2.set_ylabel('Count')

# Select the third subplot (bottom-left)
ax3 = plt.subplot(2, 2, 3) # 2 rows, 2 columns, 3rd subplot
sns.countplot(x='pclass', data=df, ax=ax3, palette='viridis')
ax3.set_title('Passenger Class Count')
ax3.set_xlabel('P-Class')
ax3.set_ylabel('Count')


# 3. Use fig.add_subplot(nrows, ncols, index) to add another subplot
# This method is called on the figure object itself. It returns an Axes object.
ax4 = fig.add_subplot(2, 2, 4) # 2 rows, 2 columns, 4th subplot
sns.countplot(x='sex', data=df, ax=ax4, palette='rocket')
ax4.set_title('Gender Count')
ax4.set_xlabel('Gender')
ax4.set_ylabel('Count')

# Adjust layout to prevent titles/labels from overlapping
plt.tight_layout()

# In a real scenario, you would then call plt.show() to display the figure.
# For this code block, we are just demonstrating the setup.
plt.show()

```

### 4. Baseline - Building multiple plots + create a grid of subplots

![Screenshot 2025-06-13 145648](https://github.com/user-attachments/assets/5739a6b8-d338-4fc4-8dfa-3a08e6b55213)


```py
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd # pandas is implicitly used by seaborn's load_dataset

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Create a figure and a 2x3 grid of subplots
# fig is the Figure object, axes is a 2D array of Axes objects
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(18, 10)) # Adjust figsize for better readability
plt.figure() # This creates a new, empty figure. It's not typically used immediately before fig,axes = plt.subplots()
             # as subplots() itself creates a figure. I'll include it here to match your specific command,
             # but note it creates an extra empty plot window if not handled. For direct usage
             # with subplots, it's often more concise to just use fig, axes = plt.subplots().

# Plot 1: Histogram of Age
sns.histplot(df['age'], bins=20, kde=True, ax=axes[0, 0] , color='red')
axes[0, 0].set_title('Age Distribution')
axes[0, 0].set_xlabel('Age')
axes[0, 0].set_ylabel('Count')

# Plot 2: Countplot of Sex
sns.countplot(x='sex', data=df, ax=axes[0, 1] , color='magenta')
axes[0, 1].set_title('Passenger Sex Distribution')
axes[0, 1].set_xlabel('Sex')
axes[0, 1].set_ylabel('Count')

# Plot 3: Boxplot of Fare by Pclass
sns.boxplot(x='pclass', y='fare', data=df, ax=axes[0, 2] , palette='Set1')
axes[0, 2].set_title('Fare by Passenger Class')
axes[0, 2].set_xlabel('Passenger Class')
axes[0, 2].set_ylabel('Fare')

# Plot 4: Scatterplot of Age vs Fare (colored by Survived)
sns.scatterplot(x='age', y='fare', hue='survived', data=df, ax=axes[1, 0], alpha=0.6 )
axes[1, 0].set_title('Age vs Fare (by Survival)')
axes[1, 0].set_xlabel('Age')
axes[1, 0].set_ylabel('Fare')

# Plot 5: KDE Plot of Age, differentiated by Survival
sns.kdeplot(x='age', hue='survived', data=df, fill=True, common_norm=False, ax=axes[1, 1])
axes[1, 1].set_title('Age Density by Survival')
axes[1, 1].set_xlabel('Age')
axes[1, 1].set_ylabel('Density')

# Plot 6: Barplot of Survival Rate by Pclass
sns.barplot(x='pclass', y='survived', data=df, ax=axes[1, 2] , color = 'purple')
axes[1, 2].set_title('Survival Rate by Passenger Class')
axes[1, 2].set_xlabel('Passenger Class')
axes[1, 2].set_ylabel('Survival Rate')

# Adjust layout to prevent overlapping titles/labels
plt.tight_layout()

# Display the plots
plt.show()

```

