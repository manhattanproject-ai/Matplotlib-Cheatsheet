# Matplotlib-Cheatsheet

# Matplotlib CheatSheet for Developers

## Introduction-What-is-Matplotlib?

> Matplotlib is a comprehensive plotting library for Python that allows you to create static, animated, and interactive visualizations. It provides an object-oriented API for embedding plots into applications using general-purpose GUI toolkits, and also offers a procedural "pyplot" interface that mimics MATLAB's plotting style. It's widely used for creating a vast range of charts, graphs, and figures, from simple line plots and scatter plots to complex 3D visualizations, histograms, heatmaps, and more, making it a foundational tool for data visualization in the Python ecosystem.


## 1. Importing Matplotlib and Dependencies

> This section covers how to bring the Matplotlib library and other necessary tools into your Python environment to start plotting.

|Command | description|
|----------|-------------|
|`import matplotlib.pyplot as plt`|Imports the pyplot module of Matplotlib, which provides a MATLAB-like plotting interface. plt is the standard alias.| 
|`import matplotlib as mpl` | Imports the core matplotlib library, often used for configuring global settings or accessing lower-level functionalities. mpl is a common alias.|
|`import numpy as np` | Imports the numpy library, which is frequently used alongside Matplotlib for numerical operations and array creation. np is the standard alias.|
|`%matplotlib inline` | (Jupyter/IPython Magic Command) Ensures that Matplotlib plots are displayed directly within the notebook output, rather than in a separate window.|
|`%matplotlib notebook` | (Jupyter/IPython Magic Command) Provides interactive plots within the notebook, allowing zooming, panning, and resizing.|

## 2. Basic Plotting

> Learn the fundamental commands to create simple plots like line graphs, scatter plots, and bar charts from your data.

|Command | description|
|----------|-------------|
|`plt.figure()`|	Creates a new figure, which acts as a container for all the plot elements (axes, titles, labels, etc.). You can specify figsize=(width, height) in inches to control its size.|
|`plt.plot(x, y)`|	Creates a 2D line plot where x is the data for the horizontal axis and y is the data for the vertical axis. It connects points with lines by default.|
|`plt.scatter(x, y)`|	Creates a 2D scatter plot, where each point (x, y) is represented by a marker. Ideal for showing the relationship between two numerical variables.|
|`plt.bar(x, height)`|	Creates a bar plot. x typically represents categories, and height represents the value for each category.|
|`plt.hist(x, bins)`|	Creates a histogram, which displays the distribution of a single numerical variable x. bins defines the number or edges of the bins.|
|`plt.boxplot(data)`|	Creates a box plot, visualizing the distribution of numerical data through quartiles, showing central tendency and potential outliers.|
|`plt.pie(x, labels)`|	Creates a pie chart, showing the proportional distribution of categorical data. x is the size of each slice, and labels are the names for each slice.|
|`plt.show()`|	Displays all open figures. This command is essential to render the plots you've created.|
|`plt.xlabel("Label")`|	Sets the label for the x-axis of the current plot.|
|`plt.ylabel("Label")`|	Sets the label for the y-axis of the current plot.|
|`plt.title("Title")`|	Sets the title of the current plot.|
|`plt.grid(True)`|	Adds a grid to the plot, helping with readability and data estimation.|
|`plt.xlim(min, max)`|	Sets the limits for the x-axis.|
|`plt.ylim(min, max)`|	Sets the limits for the y-axis.|

## 3. Customizing Plot Elements

> Discover how to modify visual aspects such as line styles, marker shapes, and background colors to enhance your plot's appearance.

|Command | description|
|----------|-------------|
|`plt.title('My Plot Title')`|	Sets the title of the current plot.|
|`plt.xlabel('X-axis Label')`|	Sets the label for the x-axis.|
|`plt.ylabel('Y-axis Label')`|	Sets the label for the y-axis.|
|`plt.xlim(xmin, xmax)`|	Sets the limits for the x-axis.|
|`plt.ylim(ymin, ymax)`|	Sets the limits for the y-axis.|
|`plt.xticks([0, 1, 2], ['Label1', 'Label2', 'Label3'])`|	Sets custom tick locations and labels for the x-axis.|
|`plt.yticks([0, 0.5, 1], ['Low', 'Medium', 'High'])`|	Sets custom tick locations and labels for the y-axis.|
|`plt.tick_params(axis='x', rotation=45)`|	Customizes tick parameters (e.g., rotating x-axis tick labels).|
|`plt.grid(True)`|	Displays a grid on the plot. plt.grid(False) removes it.|
|`plt.grid(axis='y', linestyle='--', alpha=0.7)`|	Customizes grid lines for a specific axis with a specific style and transparency.|
|`plt.legend(['Series 1', 'Series 2'])`|	Displays a legend for the plotted series. Labels are provided in the plot command (e.g., plt.plot(x, y, label='Series 1')).|
|`plt.annotate('Annotation Text', xy=(x_point, y_point), xytext=(x_text, y_text), arrowprops=dict(facecolor='black', shrink=0.05))`|	Adds an annotation with text, an arrow pointing from text to a specific point.|
|`plt.text(x_coord, y_coord, 'Some Text', fontsize=12, color='red')`|	Adds arbitrary text to the plot at specified coordinates.|
|`plt.setp(lines, color='r', linewidth=2.0)`|	Sets multiple properties for a list of plot elements (e.g., lines).|
|`plt.rcParams['figure.figsize'] = (10, 6)`|	Sets the default figure size (width, height in inches) for all subsequent plots.|
|`plt.figure(figsize=(10, 6))`|	Creates a new figure with a specific size.|
|`plt.plot(x, y, color='blue', linestyle='--', linewidth=2, marker='o', markersize=8, alpha=0.7)`|	Customizes line/marker appearance directly in the plot command.|
|`plt.bar(x, y, color='green', width=0.8, edgecolor='black')`|	Customizes bar plot appearance.|
|`plt.scatter(x, y, s=50, c='red', alpha=0.6, marker='^')`|	Customizes scatter plot markers. s for size, c for color, marker for shape.|
|`ax.set_facecolor('lightgray')`|	Sets the background color of the axes (requires fig, ax = plt.subplots()).|
|`fig.patch.set_facecolor('lightblue')`|	Sets the background color of the entire figure (requires fig, ax = plt.subplots()).|
|`plt.tick_params(axis='both', which='major', labelsize=10)`|	Adjusts tick parameters for both major and minor ticks.|

## 4. Working with Multiple Plots

> Explore methods for arranging several plots side-by-side or on top of each other within a single figure.

|Command | description|
|----------|-------------|
|`plt.figure()`|	Creates a new figure, which acts as a container for your plots. You can specify figsize=(width, height) in inches.|
|`plt.subplot(nrows, ncols, index)`|	Creates a single subplot within a grid. nrows is the number of rows, ncols is the number of columns, and index specifies the position (1-based, top-left is 1).|
|`fig.add_subplot(nrows, ncols, index)`|	Adds an Axes object to the current figure. Similar to plt.subplot, but used when you explicitly have a Figure object (fig = plt.figure()).|
|`fig.subplots(nrows, ncols)`|	Creates a grid of subplots (multiple Axes objects) at once. Returns a fig object and an ax object (or an array of ax objects if nrows or ncols > 1). This is often the preferred method for creating grids.|
|`plt.tight_layout()`|	Automatically adjusts subplot parameters for a tight layout, preventing labels from overlapping.|
|`fig.tight_layout()`|	Same as plt.tight_layout(), but called on a specific Figure object.|
|`plt.subplots_adjust()`|	Allows fine-grained control over subplot spacing (e.g., left, right, bottom, top, wspace, hspace).|
|`ax.twinx()`|	Creates a twin Axes that shares the x-axis with ax, but has an independent y-axis. Useful for plotting two different metrics on the same x-scale.|
|`ax.twiny()`|	Creates a twin Axes that shares the y-axis with ax, but has an independent x-axis. Less common than twinx().|

## 5. Adding Text and Annotations

> Understand how to add descriptive titles, labels, custom text, and explanatory arrows directly onto your visualizations.

|Command | description|
|----------|-------------|
|`plt.text(x, y, s, **kwargs)`|	Add text s to the Axes at data coordinates (x, y).|
|`ax.text(x, y, s, **kwargs)`|	(Object-oriented method) Add text s to specific Axes object ax at data coordinates (x, y).|
|`plt.annotate(s, xy, xytext, **kwargs)`|	Add an annotation s with an arrow. xy is the point to annotate (data coordinates), and xytext is the position to place the text (data coordinates).|
|`ax.annotate(s, xy, xytext, **kwargs)`|	(Object-oriented method) Add an annotation s with an arrow to specific Axes object ax.|
|`plt.xlabel(label, **kwargs)`|	Set the label for the x-axis.|
|`ax.set_xlabel(label, **kwargs)`|	(Object-oriented method) Set the label for the x-axis of ax.|
|`plt.ylabel(label, **kwargs)`|	Set the label for the y-axis.|
|`ax.set_ylabel(label, **kwargs)`|	(Object-oriented method) Set the label for the y-axis of ax.|
|`plt.title(label, **kwargs)`|	Set a title for the current plot.|
|`ax.set_title(label, **kwargs)`|	(Object-oriented method) Set a title for ax.|
|`plt.suptitle(label, **kwargs)`|	Add a super title to the figure (for multiple subplots).|
|`fig.suptitle(label, **kwargs)`|	(Object-oriented method) Add a super title to a Figure object fig.|
|`plt.figtext(x, y, s, **kwargs)`|	Add text s to the Figure at figure coordinates (x, y) (0 to 1 range).|
|`fig.text(x, y, s, **kwargs)`|	(Object-oriented method) Add text s to a Figure object fig at figure coordinates (x, y)|

## 6. Saving Plots

> Find out how to save your created figures in various image formats (like PNG, JPG, PDF) for sharing or further use.

|Command | description|
|----------|-------------|
|`plt.savefig('my_plot.png')`|	Saves the currently active figure to a file named 'my_plot.png' in the current working directory. You can specify different file formats by changing the extension (e.g., .pdf, .svg, .jpg).|
|`plt.savefig('my_plot.pdf', dpi=300)`|	Saves the figure with a specified resolution of 300 dots per inch (DPI). Higher DPI results in a higher quality image, especially for printing.|
|`plt.savefig('my_plot.png', bbox_inches='tight')`|	Saves the figure by automatically trimming whitespace around the figure, ensuring the plot fits tightly within the saved image.|
|`plt.savefig('my_plot.png', transparent=True)`|	Saves the figure with a transparent background. Useful for overlaying plots or for images that need to blend into a webpage.|
|`plt.savefig('my_plot.png', facecolor='white', edgecolor='none')`|	Sets the face color and edge color of the figure's canvas when saving. edgecolor='none' removes the border.|
|`fig.savefig('specific_figure.png')`|	If you explicitly created a Figure object (e.g., fig, ax = plt.subplots()), you can use its savefig method to save that specific figure, rather than relying on the currently active figure.|

## 7. Specialized Plot Types

> Dive into advanced visualizations beyond the basics, including statistical plots, 3D graphs, and image displays.

|Command | description|
|----------|-------------|
|`plt.hist(x)`|	Creates a histogram of the data in x, showing its distribution.|
|`plt.bar(x, height)`|	Generates a bar plot with bars centered at x coordinates and corresponding height values.|
|`plt.barh(y, width)`|	Creates a horizontal bar plot with bars centered at y coordinates and corresponding width values.|
|`plt.pie(x, labels=...)`|	Draws a pie chart for numerical data x, often with labels for slices.|
|`plt.boxplot(x)`|	Generates a box and whisker plot of x, displaying distribution and outliers.|
|`plt.violinplot(x)`|	Creates a violin plot of x, showing the distribution similar to a box plot but with kernel density estimation.|
|`plt.imshow(Z)`|	Displays data as an image (e.g., heatmaps or 2D arrays), where Z is a 2D array.|
|`plt.contour(X, Y, Z)`|	Creates a contour plot of 2D data, drawing lines of constant Z values.|
|`plt.contourf(X, Y, Z)`|	Creates a filled contour plot, similar to contour but fills the areas between contour lines.|
|`plt.quiver(X, Y, U, V)`|	Plots a 2D field of arrows, useful for vector fields (e.g., flow data).|
|`plt.stem(x, y)`|	Creates a stem plot, often used for discrete sequences.|
|`plt.fill_between(x, y1, y2)`|	Fills the area between two horizontal curves.|
|`plt.fill_betweenx(y, x1, x2)`|	Fills the area between two vertical curves.|
|`plt.stackplot(x, y)`|	Draws a stacked area plot, where successive datasets are stacked on top of each other.|
|`plt.scatter(x, y)`|	Creates a scatter plot of x vs. y values.|
|`plt.plot(x, y)`|	Draws a line plot of x vs. y values.|
|`plt.errorbar(x, y, yerr=...)`|	Plots x and y with error bars.|

## 8. Figure and Axes Management

> Master the control over the overall drawing area (figure) and the individual plotting regions (axes) to precisely control layout and dimensions.

|Command | description|
|----------|-------------|
|`plt.figure()`|	Creates a new figure, which is the overall window or page that all plots will be drawn on. Can specify figsize=(width, height) in inches.|
|`fig = plt.figure()`|	Assigns the created figure object to a variable fig for further customization.|
|`plt.axes()`|	Adds a single axes (a subplot) to the current figure. Useful for creating a single plot within the figure.|
|`ax = plt.axes()`|	Assigns the created axes object to a variable ax for further customization (e.g., ax.set_xlabel()).|
|`plt.subplot(nrows, ncols, index)`|	Creates a grid of subplots within a figure. nrows is the number of rows, ncols is the number of columns, and index specifies the position of the current subplot (starting from 1, top-left).|
|`fig, ax = plt.subplots()`|	A common and recommended way to create a figure and a single axes (subplot) simultaneously. Returns both the figure (fig) and axes (ax) objects.|
|`fig, axes = plt.subplots(nrows, ncols)`|	Creates a figure and a grid of nrows x ncols subplots. axes will be a NumPy array of axes objects.|
|`plt.tight_layout()`|	Automatically adjusts subplot parameters for a tight layout, preventing labels from overlapping. Should be called before plt.show().|
|`fig.add_subplot(nrows, ncols, index)`|	Similar to plt.subplot(), but used directly on a fig object to add a subplot.|
|`ax.remove()`|	Removes an axes object from the figure.|
|`fig.clear()`|	Clears the entire figure, removing all axes.|
|`plt.clf()`|	Clears the current figure, similar to fig.clear().|
|`plt.cla()`|	Clears the current axes, but leaves the axes in the figure.|
|`ax.set_xlim(left, right)`|	Sets the x-axis limits of the specified axes (ax).|
|`ax.set_ylim(bottom, top)`|	Sets the y-axis limits of the specified axes (ax).|
|`ax.autoscale(enable=True, axis='both', tight=None)`|	Adjusts axes limits to fit data. axis='x', 'y', or 'both'.|
|`ax.set_aspect('auto'/'equal'/'num')`|	Sets the aspect ratio of the axes. 'equal' makes x and y units the same length.|
|`fig.get_size_inches()`|	Returns the current figure size in inches as a tuple (width, height).|
|`fig.set_size_inches(width, height)`|	Sets the figure size in inches.|
|`plt.gcf()`|	Get the current figure.|
|`plt.gca()`|	Get the current axes.|
|`ax.grid(True)`|	Displays a grid on the axes. Can specify axis='x', 'y', or 'both'.|

## 9. Color Customization

> Learn techniques for choosing and applying specific colors, color palettes, and gradients to different elements of your plots.

|Command | description|
|----------|-------------|
|`plt.plot(..., color='red')`|	Sets the color of a line or points using a string name (e.g., 'red', 'blue', 'green', 'purple').|
|`plt.plot(..., color='#FF5733')`|	Sets the color using a hexadecimal RGB string (e.g., '#RRGGBB').|
|`plt.plot(..., color=(0.1, 0.2, 0.3))`|	Sets the color using an RGB tuple (values from 0.0 to 1.0, e.g., (red, green, blue)).|
|`plt.plot(..., c='b')`|	Shorthand for color. Sets the color using a single-character shorthand (e.g., 'b' for blue, 'g' for green, 'r' for red, 'k' for black, 'w' for white, 'm' for magenta, 'y' for yellow, 'c' for cyan).|
|`plt.scatter(..., c=data_array)`|	For scatter plots, c can be an array of values to map colors to points based on data.|
|`plt.hist(..., color='skyblue')`|	Sets the color for histogram bars.|
|`plt.bar(..., color=['red', 'green', 'blue'])`|	Sets colors for individual bars in a bar plot using a list of colors.|
|`plt.cm.<cmap_name>`|	Accesses a built-in Matplotlib colormap (e.g., plt.cm.viridis, plt.cm.RdBu).|
|`plt.set_cmap('viridis')`|	Sets the default colormap for the current figure.|
|`ax.set_facecolor('lightgray')`|	Sets the background color of a specific axes object.|
|`fig.patch.set_facecolor('white')`|	Sets the background color of the entire figure.|
|`plt.colorbar(..., cmap='viridis')`|	Creates a colorbar for a plot, specifying the colormap to use.|
|`plt.plot(..., alpha=0.5)`|	Sets the transparency (alpha value) of the plot element, ranging from 0.0 (fully transparent) to 1.0 (fully opaque).|


## 10. Legends and Labels

> This section provides commands to clearly identify plotted data series and label your axes effectively for better data interpretation.

|Command | description|
|----------|-------------|
|`plt.title('My Plot Title')`|	Sets the main title of the current plot.|
|`plt.xlabel('X-axis Label')`|	Sets the label for the x-axis.|
|`plt.ylabel('Y-axis Label')`|	Sets the label for the y-axis.|
|`ax.set_title('My Plot Title')`|	Sets the title of a specific Axes object (ax).|
|`ax.set_xlabel('X-axis Label')`|	Sets the label for the x-axis of a specific Axes object (ax).|
|`ax.set_ylabel('Y-axis Label')`|	Sets the label for the y-axis of a specific Axes object (ax).|
|`plt.text(x, y, 'Text', ...)`|	Adds arbitrary text at specified x, y coordinates in data units.|
|`ax.text(x, y, 'Text', ...)`|	Adds arbitrary text to a specific Axes object ax at x, y coordinates.|
|`plt.annotate('Text', xy=(x, y), xytext=(x_arrow, y_arrow), arrowprops=dict(...))`|	Adds an annotation with optional arrow. xy is the point to annotate, xytext is where the text is placed.|
|`ax.annotate('Text', xy=(x, y), xytext=(x_arrow, y_arrow), arrowprops=dict(...))`|	Adds an annotation to a specific Axes object ax with optional arrow.|
|`plt.legend(['Label 1', 'Label 2'], ...)`|	Displays a legend for labeled plot elements. If label is set in plt.plot(), you don't need to pass the list.|
|`ax.legend()`|	Displays a legend for labeled plot elements on a specific Axes object ax.|
|`plt.tick_params(axis='x', labelsize=10)`|	Customizes tick parameters for an axis (e.g., labelsize for tick label font size, rotation for angle).|
|`ax.tick_params(axis='y', length=5)`|	Customizes tick parameters for a specific Axes object ax.|
|`plt.xticks(ticks, labels, rotation=angle)`|	Sets the locations and labels of x-axis ticks.|
|`plt.yticks(ticks, labels, rotation=angle)`|	Sets the locations and labels of y-axis ticks.|





























