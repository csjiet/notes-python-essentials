Analysing and visualizing the data frame - with a focus of the relationship between 
- Feature understanding vs feature relationships?: Feature relationship analyses the relationship between 2 features ($x_{1}, x_{2}$) and its result ($y$), which can be either represented by 
	1) 3D plots, or 
	2) 2D plots, with each axis being a feature, but using different plot markers/ colors (`hue` parameter in `Seaborn` plot functions) to identity the different results. 
		- E.g., if we decide to plot feature relationship between 2 features and 1 result, Seaborn is then useful to bring about color (`hue`) to the marker of our plots, where each hue/ color difference, may represent the different values in the result.
- Functions
	- `df.corr(method= '{method_type}')` :
		- Computes pairwise correlation of columns in the data frame using the 'Pearson' method by default, excluding NA/null values in columns.
		- Gives a coefficient value score between -1 to 1, where 1 being perfect correlation (e.g., increasing together, and at the same rate), with -1  being NO remote correlation. (The correlation of a column with itself is always 1)
		- Arguments:
		- `method={method_type}`: 
			- `pearson` (Standard correlation coefficient): Plots a matrix, which matches all combination of columns in the data frame, with their associated 'correlation' coefficient value.
			- `kendall` (Kendall Tau correlation coefficient)
			- `spearman`(Spearman rank correlation)
		- `sns.heatmap(df.corr(...), annot=True)`:  Heatmap plots rectangular data (2D dataset) as a color-encoded matrix. If a Pandas DataFrame is provided the column information will be used to label the columns and rows. Where the increasing gradient of hue "heat", show the magnitude of a continuous value on a range of values. A legend of the associated gradient and its true value scale is also provided.
			- Arguments:
				- `annot=True` : Annotate the real value on top of the color_encoded matrix.
- Seaborn plots (`import seaborn as sns`)
	- [Difference between seaborn vs matplotlib](https://codesolid.com/matplotlib-vs-seaborn/#:~:text=Matplotlib%20is%20highly%20customized%20and,and%20Pandas%20to%20plot%20graphs.)
	- [Full tutorial of seaborn](https://seaborn.pydata.org/tutorial/function_overview.html)
	- relational plots
		- `sns.scatterplot()` 
			- Arguments:
				- `x = {col_name1} `
				- `y = {col_name2} `
				- `hue = {col_name8} `: Use different hue to represent different values in the column.
				- `data = {data_frame_variable} `
		- `sns.lineplot()` 
	- distribution plots
		- `sns.histplot()` 
		- `sns.kdeplot()` 
		- `sns.ecdplot()` 
		- `sns.rugplot()` 
	- categorical plots
		- `sns.stripplot()` 
		- `sns.swarmplot()` 
		- `sns.boxplot()` 
		- `sns.violinplot()` 
		- `sns.pointplot()` 
		- `sns.barplot()` 
	- >2 feature 2D plots by making multiple 2D plots 
		- Problem: We want to compare **>=3 features** (e.g., 3, 4, 5, ...,n_col-1 features), with 1 result, we can represent data using 
			1) ***4D - nD*** (which is not possible) OR  
			2) ***3D***, (possible to compare a maximum of 3 features ONLY) each axis (x,y,z) being features ($x_{1}, x_{2},x_{3}$), and marker color/ symbol as result ($y$).
			3) ***Multiple 2D***, BUT however: `Find the all combination of the subsets of 2 feature relationships in n features`. (aka. ploting multiple 2 feature relationship graph with xy axis for each of the 2 feature, with marker color/ symbol/ size as result. 
				1) This can be done by comparing 2 features: feature 1 (at the x-axis) to n-1 separate features (at each n-1 plot's y-axis) for each n-1 features, and repeat the plot for all n features.) This results in a **nxn graphs plot**, where 'n' is the number of features in the data frame.
				2) We do this by using multiple pair plots - `sns.pairplot(df, {args})` 
		- Functions:
		- `sns.pairplot(df, {args})` 
			- Arguments:
				- `vars = [{a list of features/ columns in data frames to compare}]`
					- Compares each feature in a set of n features, to all other n-1 features, and repeats for all n features. To generate nxn number of plots, presented as a nxn matrix.
					- Example of the result generated: [Youtube](https://www.youtube.com/watch?v=xi0vhXFPegw&t=1913s)
				- `hue = {col_name1}`
					- It allocates different hue for each unique item in the column.