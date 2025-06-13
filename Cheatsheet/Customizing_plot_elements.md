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

### 3. Baseline Customization

![Screenshot 2025-06-13 131634](https://github.com/user-attachments/assets/3c795fd4-ba3a-4c9f-9ce6-6388f771e514)

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import matplotlib for plot customization

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Start of new code block ---

# Define x and y data for the plot
# Using 'age' for x-axis and 'fare' for y-axis
x_data = df['age']
y_data = df['fare']

# Define the custom limits for the axes
# Inspecting df['age'].describe() and df['fare'].describe() would help
# age: min ~0.42, max ~80.0
# fare: min ~0.0, max ~512.3292
xmin, xmax = 0, 85
ymin, ymax = -10, 200 # Extend a bit beyond the typical range to show clipping effect/control

# Create a figure and axes with a specific size
plt.figure(figsize=(10, 6))

# Create a scatter plot
plt.scatter(x_data, y_data, alpha=0.6, s=20) # s is marker size, alpha for transparency

# Set the plot title and axis labels
plt.title('Age vs. Fare on Titanic')
plt.xlabel('Age')
plt.ylabel('Fare')

# Set custom limits for the x and y axes
plt.xlim(xmin, xmax)
plt.ylim(ymin, ymax)

# Add a grid for better readability (optional)
plt.grid(True, linestyle='--', alpha=0.7)

# Display the plot
plt.show()

```

### 4. Baseline Customization + Custom ticks

![Screenshot 2025-06-13 132703](https://github.com/user-attachments/assets/a70ca7b9-02b6-491a-9d0b-5d3add7568de)

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import matplotlib for plot customization

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Start of custom plot code ---

# Define the data for plotting (e.g., age and fare for a scatter plot)
# We'll also drop NaNs from 'age' to ensure a clean plot
plot_data = df.dropna(subset=['age', 'fare'])

# Set the figure size
plt.figure(figsize=(10, 6))

# Create a scatter plot (or any other plot type)
# This is where your actual plot generation would go
plt.scatter(plot_data['age'], plot_data['fare'], alpha=0.6)

# Define limits for axes
xmin, xmax = 0, 80  # Age ranges from 0 to 80
ymin, ymax = 0, 300 # Fare ranges, let's cap at 200 for better visualization

# Set plot title and axis labels
plt.title('Passenger Age vs. Fare on Titanic')
plt.xlabel('Age')
plt.ylabel('Fare')

# Set custom axis limits
plt.xlim(xmin, xmax)
plt.ylim(ymin, ymax)

# Set custom x-axis ticks and labels
# Corresponding to ages: 0, 40, 80
plt.xticks([0, 40, 80], ['Young', 'Middle-aged', 'Elderly'])

# Set custom y-axis ticks and labels
# Corresponding to fares: 0, 100, 200 , 300
plt.yticks([0, 100, 200 , 300], ['Low', 'Standard', 'High' , 'Premium' ])

# Rotate x-axis tick labels for better readability if they overlap
plt.tick_params(axis='x', rotation=45)

# Display the plot
plt.grid(True, linestyle='--', alpha=0.7) # Optional: Add a grid for better readability
plt.tight_layout() # Adjust layout to prevent labels from overlapping
plt.show()

```
### 5. Baseline Customization + Custom ticks + adding legends

![Screenshot 2025-06-13 132833](https://github.com/user-attachments/assets/707be215-9eaa-4b9e-b42e-61a8e644587c)


```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Start of the requested code block ---

# Prepare data for plotting
# For demonstration, let's plot 'age' vs 'fare' for two different passenger classes
# to make the legend command relevant.
# We'll use pclass 1 and pclass 3 as examples.
class1_passengers = df[df['pclass'] == 1]
#class2_passengers = df[df['pclass'] == 2]
class3_passengers = df[df['pclass'] == 3]

# Define bounds for xlim and ylim
# We'll base these on the typical range of age and fare, but adjust for clipping effect
xmin, xmax = 0, 80  # Age ranges from 0 to 80+
ymin, ymax = 0, 300 # Fare can be up to 512, but setting a max for display

# Create the figure and axes
plt.figure(figsize=(10, 6))

# Plot the data
plt.scatter(class1_passengers['age'], class1_passengers['fare'], alpha=0.6, label='Class 1 Passengers')
#plt.scatter(class2_passengers['age'], class2_passengers['fare'], alpha=0.6, label='Class 2 Passengers')
plt.scatter(class3_passengers['age'], class3_passengers['fare'], alpha=0.6, label='Class 3 Passengers')


# Apply the requested customization commands
plt.title('Age vs Fare by Passenger Class on Titanic')
plt.xlabel('Age (Years)')
plt.ylabel('Fare ($)')

# Set x and y axis limits
plt.xlim(xmin, xmax)
plt.ylim(ymin, ymax)

# Set custom x-axis ticks and labels
# Based on age, let's use 0, 20, 40, 60, 80
plt.xticks([0, 20, 40, 60, 80], ['0', 'Youth', 'Adult', 'Senior', '80+'])

# Set custom y-axis ticks and labels
# Based on fare, let's use 0, 100, 200, 300
plt.yticks([0, 100, 200, 300], ['Low', 'Medium', 'High', 'Very High'])

# Rotate x-axis tick labels for better readability if they overlap
plt.tick_params(axis='x', rotation=45)

# Add a legend for the plotted series
plt.legend() # Labels are taken from the 'label' argument in plt.scatter/plot calls

# Display the plot
plt.show()

```

### 6. Baseline Customization + Custom ticks + adding legends + add annotations

![Screenshot 2025-06-13 133045](https://github.com/user-attachments/assets/ebb8a051-e04e-416a-bd21-bd261d8cd481)


```py
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import numpy as np # Needed for NaN handling and range for plotting

# Load the titanic dataset
df = sns.load_dataset('titanic')


# Prepare data for plotting: Age vs Fare, split by Survived status
# Drop rows with NaN values in 'age' or 'fare' for cleaner plotting
df_plot = df.dropna(subset=['age', 'fare'])

# Create a figure with a specified size
plt.figure(figsize=(10, 6))

# Plot 'Fare' against 'Age', distinguishing survivors and non-survivors for the legend
plt.scatter(df_plot[df_plot['survived'] == 0]['age'],
            df_plot[df_plot['survived'] == 0]['fare'],
            alpha=0.6, label='Not Survived', s=50) # s is size of points
plt.scatter(df_plot[df_plot['survived'] == 1]['age'],
            df_plot[df_plot['survived'] == 1]['fare'],
            alpha=0.6, label='Survived', s=50)


# Set the title of the plot
plt.title('Passenger Age vs. Fare on the Titanic')

# Set labels for the x and y axes
plt.xlabel('Age (Years)')
plt.ylabel('Fare ($)')

# Set explicit limits for the x and y axes based on data range
# Add some padding to min/max for better visualization
age_min, age_max = df_plot['age'].min(), df_plot['age'].max()
fare_min, fare_max = df_plot['fare'].min(), df_plot['fare'].max()
plt.xlim(age_min - 5, age_max + 5)
plt.ylim(0, fare_max + 20) # Start from 0 for fare, add padding to max

# Set custom x-axis ticks and their labels
# Example: Age groups for readability
plt.xticks([0, 18, 30, 50, 70], ['Child', 'Young Adult', 'Adult', 'Middle-Aged', 'Senior'])

# Set custom y-axis ticks and their labels
# Example: Fare categories
plt.yticks([0, 50, 100, 200, 300, 500], ['Very Low', 'Low', 'Medium', 'High', 'Very High', 'Luxury'])

# Rotate x-axis tick labels for better readability if they overlap
plt.tick_params(axis='x', rotation=45)

# Add a legend to distinguish the plotted series
plt.legend()

# Add an annotation to highlight a specific point or area on the plot
# For example, highlighting a common cluster or an interesting outlier
# Let's annotate a point around median age and lower-middle fare
example_age = df_plot['age'].median()
example_fare = df_plot['fare'].quantile(0.25) # 25th percentile fare
plt.annotate(
    'Common Passenger Group',
    xy=(example_age, example_fare), # Point to annotate (Age 28, Fare ~15)
    xytext=(example_age + 20, example_fare + 50), # Position of the annotation text
    arrowprops=dict(facecolor='black', shrink=0.05, width=1, headwidth=8),
    fontsize=9,
    color='darkred'
)

# Display the plot
plt.show()

```

### 7. Baseline Customization + Custom ticks + adding legends + add arbitrary text

![Screenshot 2025-06-13 133223](https://github.com/user-attachments/assets/ac329d95-e1b1-4ce0-9fcb-b78a04e0131e)

```py
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Start of Plotting Code ---

# Filter data for males and females to create two series for the legend
males = df[df['sex'] == 'male']
females = df[df['sex'] == 'female']

# Define plot dimensions
plt.figure(figsize=(10, 6))

# Create the scatter plots for males and females
# We are plotting 'age' on x-axis and 'fare' on y-axis
plt.scatter(males['age'], males['fare'], alpha=0.6, label='Male Passengers', s=20)
plt.scatter(females['age'], females['fare'], alpha=0.6, label='Female Passengers', s=20)


# Set plot title and labels
plt.title('Passenger Fare vs. Age on Titanic')
plt.xlabel('Age (Years)')
plt.ylabel('Fare ($)')

# Set axis limits
# Based on typical age and fare ranges on Titanic (fare outliers will be cut for clarity)
xmin, xmax = 0, 80
ymin, ymax = 0, 150 # Clipping max fare for better visualization, as some fares are very high
plt.xlim(xmin, xmax)
plt.ylim(ymin, ymax)

# Customize x-axis ticks and labels
plt.xticks([0, 20, 40, 60, 80], ['Child', 'Young Adult', 'Adult', 'Senior Adult', 'Elderly'])

# Customize y-axis ticks and labels
plt.yticks([0, 50, 100, 150], ['Low Fare', 'Medium Fare', 'High Fare', 'Very High Fare'])

# Rotate x-axis tick labels for better readability if they overlap
plt.tick_params(axis='x', rotation=45)

# Add a legend to distinguish the series
plt.legend(['Male Passengers', 'Female Passengers']) # Legend labels correspond to the scatter plots

# Add text annotation on the plot
# Choose coordinates within the plot's limits (age ~50, fare ~120)
x_coord_text = 50
y_coord_text = 120
plt.text(x_coord_text, y_coord_text, 'Note: Some outliers removed for clarity', fontsize=12, color='red', ha='center' )

# Display the plot
plt.grid(True, linestyle='--', alpha=0.7) # Optional: Add a grid for better


# Display the plot
plt.show()

```




