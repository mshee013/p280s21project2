# Spatial Inequality Dynamics

### *Introduction* 
The focus of interregional income inequality is important to help identify growing gaps between poor and rich regions. These gaps perpetrate political polarization. Thus, creating  social inequalities within different regions. These politically polarized regions become key players in developing policy, and pushing one-sided agendas that then lead to a cycle that perpetuates disparities and inequalities.  

We first begin with a description of the data and why the UK was chosen. We compare the UK to the US. We then go into a description of the analytics measures used. This study uses classical methods used to measure inequality such as, the Gini Index, 20:20 Ratio, and Theil's index to measure such inequalities. We also use geographic tools to identify any special inequalities. Those tools include Time Series, BoxPlot, Map and Scatterplot. 



### *Data: Comparing US and UK* 
Two sets of data were needed for this study, 1) shapefile and 2) populaion income data. UK shapefile data was found on the Database of Global Administrative Areas (GADM). US & UK are appropriate to compare because of similarities in historical economic development. Data from other countries is also lacking. Using Shapefile data has practical applications for spatial analysis. Background data bases do not have the same computing power, data availability and quality check descriptions (Pfister et al. 2020). Shapefile data also enables better accuracy of regional data than other types of analyses (Zhu et al. 2019). This is why Shapefile data is best to use for our project. UK is spilt into Nomencluature of territorial units for statistics (NUTS); a hierarchical systems for dividing up economic territory of the EU and the UK for purposes of: collection, development and EU region statistics as well as socio-economic analyses of the regions. NUTS 1 contains major socio-economic regions, NUTS 2 includes basic regions for the application of regional policies and NUTS 3 focuses on small regions for specific diagnosis. NUTS 1-3 are comparable to 1-US, 2-States and 3-cities. The populatin income data was retrived from the Office for National Statistics. The dataset, Regional Gross Disposable Household Income: All NUTS Level Regions contains a dataset that ranges from 1997-2018, it is divided into 3 levels: NUTS 1-3; NUTS1 containg 12 regions, NUTS2 41 regions and NUTS3 179 regions. This data set has 232 regions in it and is a wide longituinal data set. Each column represents a different period of time, from 1997-2018, and each row contains information on  NUTS Level, NUTS Code, Region and different year (1997-2018). This project specificaly focuses on NUTS 2 level data; this data is most comperabel to US states data. 
 
 

UK Shapefile and UK population were merged to create one data form that contains both polygon and population income data. 

(insert merge table here)

The data is formatted in a wide longitudinal data set; in general wide-format data each displays each column at a different time periods and each row represents a set of measures and as well as any unique identifying information available for the entity (Rey et al., 2020).Be it that we are analyzing trajectories, wide data is the most appropriate format to use.  


### *Analytics: GINI Index*
The first measure of inequality chosen is the GINI Index. The Gini index, also known as the GINI coefficient, measures income inequality by measuring the income distribution across a population (Arribas-Bel, Rey, and Wolf 2020). For our project, this is the United Kingdom. The income distribution is visualized with a Lorenz curve. This is then compared to a “perfectly equal” society, or a straight line. The Gini index is essentially a ratio of the area between the curves. The focus here is on the middle of the society, not the ends. The bigger the coefficient, the more inequality there is. In this project, we calculated the GINI index for all the years in our dataset and the Lorenz curves for all years.

After importing the necessary packages (seaborn, pandas, geopandas, pysal, numpy, mapclassify, matplotlib, inequality), we calculated the lorenz curve for the first year in our dataset, 1997. We then applied this logic to make a Lorenz curve for every year in our data set by specifying the years as a list. The function for lorenz curves gave us a dataframe for all the years with rows as population shares or income shares as lists. After calculating Lorenz curves for every year, we then calculated a function in which the Gini index would be calculated for every year or the ratio for the area between the lorenz curve and the perfect equality curve. 

In 1997, we see the gini index is 0.087922. On average, it increases to 0.1133675 by the end of our dataset in 2017. A higher gini index indicates a greater inequality. Overall inequality has increased in the United Kingdom. When graphing the gini indexes, we see there is a steep increase from 2004 to 2007. It then declines until 2011. From there it increases  until 0.115 in 2015 then decreases to 0.1134 in 2017.

![A test image](Gini_Index.png)

#### The 20:20 Ratio
The second method of measurement in inequality chosen was the 20:20 ratio. The 20:20 ratio is defined as the ratio of the incomes at the 80th percentile over that of the 20th percentile. This measurment helps to uncover some of the challenges that exist between the rich and poor in income inequality distribution in a given region. The United Kingdom data that was given with the years of 1997 to 2017 showed results in which there is increasing periods over the years that income inequality measurements fluctuate at higher and lower levels. However, we still see a pattern of increasing inequality as the years progress.

In order to utilize the 20:20 ratio in Jupyter Lab we use inequality collection from pysal.explore for the given data and import inequality. With this, we take the top 20% and the bottom 20% and divide it starting from the year 1997 “using = merge2[‘1997’]. quantile ([.8, .2])”. This then gives us the top 20 over the bottom 20 which gives us the result of 1.2399614519755862 for the first given year of 1997. To graph the sequence of inequality using the 20:20 ratio, we use the codes: “defineq_20_20(values): top20, bottom20 = values. quantile ([.8, .2]) return top20 / bottom20” to define inequality 20:20 ratio into its values. Then we add the years 1997-2018 by applying these codes and variables to the plot the x and y values. 



### *Visualization: Time Series, Box Plot, Map, Scatterplot*
The Space-Time Analysis of Regional Systems open-source package was designed to analyze data measured at multiple points with different visualization methods. These plots included a time series, box plot, map, and scatterplot. One of the most pressing questions brought up at the beginning of the project was deciding which toolkit would we use to create the maps (Panel, Holoviews, Viola, etc.). We ultimately decided to use hvplots due to its simplicity ("hvplot.scatter" or "hvplot.box"), power, and interactivity  (hovering options, composing plots, etc). To utilize these features, we imported the necessary packages, including 'import hvplot.pandas', 'import holoviews', 'from holoviews import dim and opts', and include the hv.extension('bokeh').

One of the biggest challenges we faced during this process was how slow the system loaded our plots. We decided to create a separate visualization notebook in the hopes that it would address this issue. Thus we had to re-download the data from the first notebook which we saved as 'uk.parquet'. After renaming a time column, we pulled the values we needed to plot our data . Because we are looking at the UK via regions we had to keep all the 'NUTS levels' that were "NUTS2". This also required each region's 'NUTS Code' and 'geometry'. We condensed the individual year columns into a single column, titled 'year', by using 'pandas.melt', and created a new column with their values titled 'per_capita'. Two datasets were created: 'uklong' which included the geometry values, and "uk_long" which dropped this column. 

#### *Time Series*
The first plot we created was the time series, which is featured in the main notebook. Following the methods used by the analytics team, we decided to graph both the "Gini Coefficient" and a "Theil Index" as they both show a significant increase of inequality in their respective coefficients. Between the years of 1997 to 2017 there was a mostly continous rise in per capita income. There were only a few years where the coefficient plateaus or dips, demonstrating how much the UK's level of inequality has grown over the years.  

#### *Boxplot*
The second plot we created was a boxplot. As previously mentioned, we chose 'hvplots' because of the simplified approach to creating interactive plots. We used their code "hv.plot.box" to create an intial boxplot (labeled "box") that mapped out the UK's 'per_capita' range in a given year with an interactive  bar showing the years between 1997-2018. From there we overlaid the boxplot with a scatterplot (['box * hvplot.scatter']) that mapped out the UK's regions on the box plot (labeled "box2"). We added to the scatterplot a hover command which would pop up the name and specific 'per_capita' (hover_cols=['per_capita', 'region']) of each region. 

We noticed that due to the boxplots small size it was difficult to see where each region landed relative to the distribution. Thus we created a third boxplot (labeled "box3") that grouped the points by region and year with an interactive legend that would plot 1 dot at a time (groupby=['region','year']). This displayed where specific regions fell relative to the distribution of a year and tracks how their positions changed over time. The greatest examples we could demostrate are the West Midlands (how they go from fairly poor to the poorest region) and Outer London - West and North West (how they went from a moderately wealthy region to the second richest in the range). Its interesting to see how in 2004 the West Midlands and Outer London W/NW go in opposite directions of one another. 

#### *Map*
The initial dataset we pulled featured each region's geometry which made it easier to create a map given its dimensions ('from [holoviews] import [dim, opt]'). When manipulating the data we created 2 data sets, "uk_long" which featured each region's geometry and "uklong" which removed that column. By simply leaving it in and using a basic hvplot code we were able to create this map. We deliberately chose a divergent color scheme (cmap=["RdYlBu"]) sensitive to variations in per capita income across the UK. In order to make it more interactive, we placed a hover option which displays the name of a region and per_capita values (hover_cols=['region','per_capita']). Sliding the scale to 1997, most regions are in the deep red, indicating many of them were poor but in a similar range. As the years progressed, the colors diverged, representing a growing divide amongst the poorest and richest regions. 

#### *Scatterplot*
The most difficult graph we attempted to make was the scatterplot because of the multiple variables we could have used to create it. We settled on a time series plot because it measured annual data from all  regions with a line indicating the median value. This first plot was created with seaborn and was borrowed from one of the notebooks shared with us. 

We found it rather difficult to replicate this graph using hvplot, but we merged a standard plot with a scatterplot of each year ([uklong.hvplot(x='year', y='per_capita') * uklong.hvplot.scatter...]) and included a hover option to display each region's name and 'per_capita'. Its clear to see across both maps that although the median per_capita rises throughout the years, indicating increasing per capita income, they are within the same area. This is especially true for those beneath the median. Beginning in 2004 however, several regions above the median distance themselves from the rest, highlighting growing inequality across the islands. 



### Challanges/ Academic Limitations* 
Some challenges associated with this project were included in the data portion. The UK was originally not the country of interest to compare with the U.S., but a lack of data from other countries (particuarly Norwegian countries) pushed us to move towards comparing with the United Kingdom. The data was also oriented in a way that was unreadable, and had to be reoriented which caused several time constraints and challenges on our team. 

Another was included in the visualization portion where rendering these plots took time and processing power which caused much fraustration. Although they were eventually polished in a separate notebook they still have a rather long lag time. 




### *Conclusion*
Inequalities has significantly increased in the UK since the beginning of our dataset. Further research provided insight into this and found that these plateaus and dips coincided with times of robubt growth in the GDP and the great recession of the U.S. which impacted the world. The three measures of inequality chosen to represent the U.K. were the Gini Index, the 20:20 Ratio, and Theil's Index. Gini Index measures the gap between a perfectly equal society and reality, 20:20 ratio compares the income to the top 20% and the bottom 20% and Theil's Index measures how evenly distributed income is across the population. 

According to our data the largest increases in inequality came particularly from 2004-2008 and 2012 onward. Research into this showed two themes. The first was that many rich individuals migrated out of regions that were considered "poor" such as West Midlands and congregated in London thus explaining why its such a high outlier in our data. In addition to this, generous tax cuts for the top 10%, 5%, 1%, and .5% led to higher earnings for high ranking officials in companies while the earnings of the median worker remained the same. From 2004 to 2008 the Gini coefficient rose 7.3% in gross income while the Theil index rose nearly 25% in gross income. 




#### Sources
Allison, C., Fleisje, E., Glevey, W. and Johannes, W. L. 2014 ‘Trends and Key Drivers of Income Inequality’, Working Paper, Marshal Society, Cambridge,
http://marshallresearch.co.uk/publications/Oxford_Economics_Trends_and_Key_Drivers_of_Income_Inequality.pdf

Deaton, A. A., &amp; Paxson, C. (2004). Mortality, Income, and Income Inequality over Time in Britain and the United States. In Perspectives on the economics of aging. essay, University of Chicago Press. 

Pfister, S., Oberschelp, C., & Sonderegger, T. (2020). Regionalized LCA in practice: the need for a universal shapefile to match LCI and LCIA. The International Journal of Life Cycle Assessment, 25(10), 1867-1871.

Rey, S., Arribas-Bel, D., & Wolf, L. (2020). Spatial Inequality — Geographic Data Science with Python. Geographic Data Science With Python. https://geographicdata.science/book/notebooks/09_spatial_inequality.html#gini-index

Zhu, J., Wang, X., Wang, P., Wu, Z., & Kim, M. J. (2019). Integration of BIM and GIS: Geometry from IFC to shapefile using open-source technology. Automation in Construction, 102, 105-119.

Hills, J., Brewer, M., Jenkins, S., Lister, R., Lupton, R., et al (2010). An anatomy of economic inequality in the UK: Report of National Equality Panel. Centre for Analysis of Social Exclusion. 
