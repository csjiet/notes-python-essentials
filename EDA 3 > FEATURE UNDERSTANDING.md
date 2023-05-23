Analysing and visualizing the data frame - with a focus of the relationship between 1 feature and the result. (2D)

- Premise:
	- Analysis (E.g., Statistical distributions that we want to see, to emphasise/ improve your hypothesis)
		- *It is good to know "in detail", what are the strengths of each distribution, and why do we want to visualize it that way. With that robust understanding, we would not waste time on irrelevant plots.* Our goal is to understand/ gather as much information about the data, at the shortest amount of time (if we are in a competition), or exhaustively (if we are doing research).

- Functions:
Matplotlib Plots
Plots the referenced data frame, by implicitly calling *matplotlib*. It returns a AxesSubplot object 
```python
ax = df.plot(kind='type')
```

> Notice we can save it as a matplotlib axis - `ax =`, where we can make further adjustments/ customizations to it, like `set_xlabel()`... all the matplotlib operations for a subplot.

- Dataframe condition before plot:
	- Feature isolation (e.g., making data frames 2 dimension, by having only 1 feature (x), 1 label (y))
		- ???? IS THIS A REQUIREMENT? HOW DO WE PLOT 3D? Does it only limit to 2D plots?
- Arguments: 
- `kind= {type_of_plot}`
	- `bar` : A bar plot (vertical (vanilla) rectangles)
	- `barh` :  A bar plot (horizontal rectangles)
	- `hist` : A discrete distribution plot
		- `bins= {integer}`: Indicates the range/ class intervals in which data will be grouped, and presented as a single bar. 
		- (if it is a natural data, it will likely be a discrete normal distribution graph)
	- `box` : 
	- `kde` : A continuous distribution plot
		-In statistics, [kernel density estimation](https://en.wikipedia.org/wiki/Kernel_density_estimation) (KDE) is a non-parametric way to estimate the [probability density function](https://www.youtube.com/watch?v=jUFbY5u-DMs) (PDF) of a random variable. 
	- `density` : 
	- `area` : 
	- `scatter` : 
	- `line`: 
	- `hexbin` : 
	- `pie` : sa
- `x= {col_name_in_data_frame}` 
	- We DON'T NEED to refer `df[{col_name}]`!
- `y= {col_name_in_data_frame}`
- `title = '{text}'`: Give the plot a title
			- `bins= {integer}`: Indicates the range/ class intervals in which data will be grouped, and presented as a single bar. 
- Seaborn plots 
- (Described in Features Relationships phase, but can also be used during feature understanding)


### Seaborn
Seaborn plots comes with more functionalities (and hence would be more useful if we want to show more complex relationships like 2D, with markers that uses different hues, that represent different values in the result.)
- **Benefits of Seaborn**: 
	- Succinct syntax 
		- E.g., legend will be automatically generated
	- Works better if you are using Pandas
	- It is just an extension of matplotlib 
		- Hence, matplotlib also should be import,
		- AxesSubplot object is ALSO returned, and can be manipulated using matplotlib functions.
		- we call `plt.show()` to show seaborn plots too.
- **Cons of Seaborn**:
	- Less customizability, But we can always make detailed changes using matplotlib functions.
- Note: **you should always import Matplotlib if you are using Seaborn**. Seaborn is built on top of Matplotlib. It is an extension to it, and not a substitute. It builds on top of Matplotlib, introducing some additional plot types and provides some visual improvements to some plots and graphs. 
