---
layout: posts
title: "Kaggle: Data Visualization"
date: 2025-08-02
category: Learning-notes
---
- This course teaches how to leverage Seaborn to make a useful yet simple way to make a data visualization. 
- Start with making a line chart with a command `sns.lineplot(data=the_dataset_name)`. `sns` stands for an alias of Seaborn library.
- A good to know part here is the `spotify_data = pd.read_csv(spotify_filepath, index_col="Date", parse_dates=True)`, it's good to know that we can consider define a column be the index and parse a column if we have a date data type (imo, this can be a wise data cleaning approach).
- Next, we learn Bar chart and Heatmaps (chart), it has different ways to write the code. The Bar chart uses `sns.barplot(x=flight_data.index, y=flight_data['NK'])`, the x-axis and y-axis needs to be defined. While the Heatmaps, `sns.heatmap(data=flight_data, annot=True)`, similar to the Line chart, with additional `annot` argument for displaying the value (number) of the data on each cell.
- For the Scatter plot, it becomes more advanced. It has similar techniques with the Bar chart, defining x and y axis, but instead using `.index` as the x-axis, it can be more flexible (at least by the course) `sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'])`
- We also learn how to make regression plot, `sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges'])`, just add the line of code below the scatter plot chart so it can combined together.
- Figure below shows a use of 3 variables: `bmi`, `charges`, and `smoker`. It applies on `sns.scatterplot()` to show relationship of 3 variables.

![Scatter Plot](/assets/images/posts/learning-notes/kaggle-data-viz/scatter-plot.png "Scatter Plot Illustration"){: .post-figure }

- This is the explanation of above plot, `This scatter plot shows that while nonsmokers to tend to pay slightly more with increasing BMI, smokers pay MUCH more.`
- There's more plot to mention such as `sns.lmplot` and `sns.swarmplot` which has different approaches for visualizing data.

- `Histogram`, is't same with Bar plot. It uses a range of value on the x-axis which makes the bar-graph doesn't exactly on the category axis.

![Histogram Plot](/assets/images/posts/learning-notes/kaggle-data-viz/histogram-plot.png "Histogram Plot Illustration"){: .post-figure }

- Kernel Density Estimate (KDE), is a smoothed histogram

- Different types of data categories:
	- **Trends** - A trend is defined as a pattern of change.
	- **Relationship** - Between one and another features
	- **Distribution** 
- Not that important, but good to know. `sns.set_style("dark")` a command to give a style to our graph/plot. Put or define the code before we make our plot.