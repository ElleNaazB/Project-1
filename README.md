# Project1
## Info about R Markdown

R Markdown is a simple formatting syntax for authoring HTML, PDF, and MS
Word documents. For more details on using R Markdown see
<http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document.

# Part 3A. Non-spatial Statistics

## Import Data

If your R Markdown is **NOT** in the same folder as your data, please
set your working directory using `setwd()` first. Here is an example
`setwd("\\medusa\StudentWork\(Your UTOR ID)\GGR276\Lab1")`. You will
need to change the code to reflect your personal directory. Otherwise,
you may skip this step and continue to **import data** by reading your
*ElectricPlants.csv* file. You may view the data by clicking the
ElectricPlants in the Environment window or type code `View(DataSet)`.
Click on the little green triangle on the right to **run current
chunk**.

-   **For testing where there is any error in any line of code, you
    should run the script line by line and check how they work
    carefully.**
    -   Any errors in your code will be displayed in the bottom left
        Console window of RStudio, which will help you pinpoint where
        the error lies.
    -   If there is an error, try selecting each line of code
        individually and running the script one by one. This will tell
        you which line of code is causing the error.

<!-- -->

    ElectricPlants <- read.csv("ElectricPlants.csv", sep = ',', header = TRUE)

## Descriptive Statistics of TotalPower

Now that we have data imported, we are ready to calculate median, mean,
range and quantiles of the Total Power Capacity in kilowatts.

    summary(ElectricPlants$TotalPower)

    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ##       0.2       6.9      10.5     125.3      17.4 1872000.0

Next, we will calculate the standard deviation of the Total Power
Capacity in kilowatts. If there are missing values in your dataset,
simply add `na.rm = TRUE` to your code to tell the R to remove NAs in
the calculation. Like this: `sd(ElectricPlants$TotalPower, na.rm=TRUE)`.
Since there isn’t a missing value in this dataset, this line is not
necessary here.

    sd(ElectricPlants$TotalPower)

    ## [1] 7984.225

## Descriptive Statistics of InitialPow

**Question 6**: Now it is your turn to write the code to calculate the
median, mean, range, interquartile range, and standard deviation of the
InitialPow. (2 marks)

    summary(ElectricPlants$InitialPower)

    ##      Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
    ##       0.2       6.8      10.3     123.6      17.0 1872000.0

    sd(ElectricPlants$InitialPower)

    ## [1] 7984.167

## Visualize

Visualize the spread of the TotalPower dataset, and answer **Question
7**: According to the boxplot, would you use median or mean as your
central tendency measure? Explain and justify your choice? (2 marks)

**Type your response here**: According to the boxplot, I would use
median as the central tendency measure. This is because median is more
appropriate to use when there are outliers and skewness in data as it is
not affected by extreme values. In this case, the data shows large
numbers of outliers and significant skewness in data. The median is
close to the bottom of the box which indicates the median is much lower
than the mean (which gets affected by extreme values) would be, given
the right-skewed distribution.

    boxplot(ElectricPlants$TotalPower)

![](GGR276Lab1P3_Starter_2024W_files/figure-markdown_strict/unnamed-chunk-35-1.png)

# Part 3B. Mapping Mean and Weighted Mean Centre

Visualize the locations of the electric production plants and the mean
and weighted mean centres.

    plot(ElectricPlants$easting, ElectricPlants$northing, xlab="easting", ylab="northing", main = "Switherland Electric Production Plants", xlim=c(-10, 4081207), ylim=c(-10, 3094815))
    n<-nrow(ElectricPlants[1])
    mc_x<-sum(ElectricPlants$easting)/n
    mc_y<-sum(ElectricPlants$northing)/n
    points(mc_x,mc_y,'p',pch=15,cex=2,col="blue")
    wmc_x<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$easting))/sum(ElectricPlants$TotalPower)
    wmc_y<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$northing))/sum(ElectricPlants$TotalPower)
    points(wmc_x, wmc_y,'p',pch=15,cex=2,col='red')
    legend("topright", legend = c("Mean centre", "Weighted mean centre"), pch = c(15,15), col = c("blue","red"))

![](GGR276Lab1P3_Starter_2024W_files/figure-markdown_strict/unnamed-chunk-36-1.png)

Notice that after running this script, there are many plants at (0, 0).
These are missing values. Let’s filter out these missing values prior to
plotting the data.

    filtered_ElectricPlants <- subset(ElectricPlants, !(easting == 0 & northing == 0))

Visualize the locations of the electric production plants and the mean
and weighted mean centres on the filtered data. Please adjust the range
of x and y axes as well as the symbols to best represent the data.

-   Code for different colours in R can be found here:
    <http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf>
-   Symbol code in R can be found here:
    <http://www.statmethods.net/advgraphs/parameters.html>
-   Use xlim=c(,) or ylim=c(,) in plot() to change the scale of the
    dataset. Make sure that there isn’t much white space and that the
    legend does not cover the data points. You can also change the
    position of the legend.

<!-- -->

    #TODO
    plot(filtered_ElectricPlants$easting, filtered_ElectricPlants$northing, xlab="easting", ylab="northing", main = "Switherland Electric Production Plants", xlim=c(2468972, 2848456), ylim=c(1064986, 1305759))
    n<-nrow(filtered_ElectricPlants[1])
    mc_x<-sum(filtered_ElectricPlants$easting)/n
    mc_y<-sum(filtered_ElectricPlants$northing)/n
    points(mc_x,mc_y,'p',pch=15,cex=2,col="blue")
    wmc_x<-sum(as.numeric(filtered_ElectricPlants$TotalPower*filtered_ElectricPlants$easting))/sum(filtered_ElectricPlants$TotalPower)
    wmc_y<-sum(as.numeric(filtered_ElectricPlants$TotalPower*filtered_ElectricPlants$northing))/sum(filtered_ElectricPlants$TotalPower)
    points(wmc_x, wmc_y,'p',pch=15,cex=2,col='red')
    legend("topleft", legend = c("Mean centre", "Weighted mean centre"), pch = c(15,15), col = c("blue","red"),cex = 0.75, pt.cex = 0.75)

![](GGR276Lab1P3_Starter_2024W_files/figure-markdown_strict/unnamed-chunk-38-1.png)

**Question 8**: Produce comments (i.e., a detailed explanation for each
parameter in the code) that describes the execution of the statements
given to you in the ElectricPlants example. Make sure you provide a
description for each set of statements and organize your answer in a
manner similar to the following example. (16 marks)

Example: `setwd ("\\medusa\StudentWork\(Your UTOR ID)\GGR276\Lab1")`

The `setwd()` command tells R the current folder to look into when
searching for data, saving outputs etc.

Explain what is occurring in each of the following lines of code:

1.  `ElectricPlants <- read.csv("ElectricPlants.csv", sep = ',', header = TRUE)`
2.  `plot(ElectricPlants$easting, ElectricPlants$northing, xlab="easting", ylab="northing", main = "Switherland Electric Production Plants", xlim=c(-10, 4081207), ylim=c(-10, 3094815))`
3.  `n<-nrow(ElectricPlants[1])`
4.  `mc_x<-sum(ElectricPlants$easting)/n`
    `mc_y<-sum(ElectricPlants$northing)/n`
5.  `points(mc_x,mc_y,'p',pch=15,cex=2,col="blue")`
6.  `wmc_x<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$easting))/sum(ElectricPlants$TotalPower)`
    `wmc_y<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$northing))/sum(ElectricPlants$TotalPower)`
7.  `points(wmc_x, wmc_y,'p',pch=15,cex=2,col='red')`
8.  `legend("topright", legend = c("Mean centre", "Weighted mean centre"), pch = c(15,15), col = c("blue","red"))`

**Type your response here**: a) Example:
`ElectricPlants <- read.csv("ElectricPlants.csv", sep = ',', header = TRUE)`

The `read.csv()` function in R is used to import data from a CSV file
(in this case “ElectricPlants.csv”) and create a data frame. The ‘sep’
parameter defines the delimiter that separates the values in the file.
‘Header’ parameter informs R that the first row of the CSV contains the
header or the column names.

1.  Example:
    `plot(ElectricPlants$easting, ElectricPlants$northing, xlab="easting", ylab="northing", main = "Switherland Electric Production Plants", xlim=c(-10, 4081207), ylim=c(-10, 3094815))`

The `plot()` command in R is used to draw a scatter plot. It takes
several arguments such as x and y coordinates (in this case
ElectricPlants$easting, ElectricPlants$northing, these arguments specify
the data to be plotted, and $easting and $northing are the columns in
the ‘ElectricPlants$easting’) for the plot. Furthermore, ‘xlab’: Used as
the label for x axis, (in this case “easting”). ‘ylab’: Used as the
label for y axis, (in this case “northing”). ‘main’: Used to set the
main title for the plot (in this case “Switherland Electric Production
Plants” ). ‘xlim’: The x limits of the plot (in this case c(-10,
4081207)). ‘ylim’: The y limits of the plot (in this case c(-10,
3094815)).

1.  Example: `n<-nrow(ElectricPlants[1])`

The `nrow()` command in R is used to return the number of rows where the
argument is a vector, array, data frame, or NULL. (In this case it
counts the number of rows in ElectricPlants in column 1).

1.  Example: `mc_x<-sum(ElectricPlants$easting)/n`
    `mc_y<-sum(ElectricPlants$northing)/n` The `sum()` command in R
    returns the sum of all the values present in its argument. In this
    case, mc\_x and mc\_y are variables used to store the mean x
    coordinate(or easting) and mean y coordinate(or northing) in the
    ElectricPlants data frame.

2.  Example: `points(mc_x,mc_y,'p',pch=15,cex=2,col="blue")` This
    `points()`command adds points to an existing plot, using the mean
    center coordinates calculated (mc\_x, mc\_y). The pch=15 argument
    specifies the type of point symbol to use, cex=2 sets the size of
    the point symbol to twice the default size, and col=“blue” sets the
    color of the points to blue.

3.  Example:
    `wmc_x<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$easting))/sum(ElectricPlants$TotalPower)`
    `wmc_y<-sum(as.numeric(ElectricPlants$TotalPower*ElectricPlants$northing))/sum(ElectricPlants$TotalPower)`

The as.numeric() command in R is used to create objects of the type
“numeric”. In this case, the variable wmc\_x calculates and stores the
x-coordinate of the weighted mean center by using easting values and the
variable wmc\_y calculates and stores the y-coordinate of the weighted
mean center by using the northing values.

1.  Example: `points(wmc_x, wmc_y,'p',pch=15,cex=2,col='red')` This
    `points()`command adds points to an existing plot, using the
    weighted mean center coordinates calculated (wmc\_x, wmc\_y).The
    pch=15 argument specifies the type of point symbol to use, cex=2
    sets the size of the point symbol to twice the default size, and
    col=“blue” sets the color of the points to red.

2.  Example:
    `legend("topright", legend = c("Mean centre", "Weighted mean centre"), pch = c(15,15), col = c("blue","red"))`
    The `legend()` command tells R to add legends to the plots. In this
    case, a legend will be added to the top-right corner of the plot.
    The legend argument specifies the text labels for the legend
    entries, pch gives the point symbol types for the legend symbols
    (both are type 15 in this case), and col sets the colors for these
    symbols in the legend.

**Question 9**: What do the mean and weighted mean center tell you about
the distribution of the filtered electric production plant locations and
their total capacity? Please explain. (3 marks)

**Type your response here**:

The mean center represents the geographic center of all the plants
without considering their production capacities.The weighted mean center
accounts for the capacity of each plant, indicating not just the
geographic center but also the ‘weight’ of each plant’s production
capacity. The discrepancy between the mean center and weighted mean
center on the graph suggests that the higher capacity plants are not
uniformly distributed. Instead, they are likely clustered in specific
areas, causing the weighted mean center to shift towards these
locations. This would be expected if, for example, larger plants are
situated close to resources or infrastructure that is not uniformly
available across the region.

## Part 3C. Create and Visualize Subsets

## Create Subsets

There are different sources of energy. Do they have the same mean
centre? Imagine we are interested in how the distribution of electric
production plants with **Photovoltaic** (maincat\_2 and subcat\_2) as
main energy source differ from those with **hydroelectric** (maincat\_1
and subcat\_1). To do this, we will split the ElectricPlants dataset
into two subsets. One subset will only contain power plants using
**Photovoltaic** as the primary source and the other will contain only
those with **hydroelectric** as the primary source.

    Photovoltaic <- subset(filtered_ElectricPlants, (filtered_ElectricPlants$MainCatego == "maincat_2" & filtered_ElectricPlants$SubCategor == "subcat_2"))

    #TODO
    Hydroelectric <- subset(filtered_ElectricPlants, (filtered_ElectricPlants$MainCatego == "maincat_1" & filtered_ElectricPlants$SubCategor == "subcat_1"))

    nrow(Photovoltaic[1])

    ## [1] 190234

    nrow(Hydroelectric)

    ## [1] 1245

Once created, the subset can be viewed in the Console by calling the
object (Photovoltaic) using `View(Photovoltaic)`. If you want to know
the number of Photovoltaic Plants, you can run: `nrow(Photovoltaic[1])`.

## Visualize Subsets

**Question 10**: Show the Switherland Electric Production Plant scatter
plot using the subset data that you created. Remember to overlay the
subsets on the original data to see the distribution of the subset. Use
a different color for the subsets. Also plot the mean centres for the
entire dataset and the subsets. Be sure to include a legend, axis titles
(with units), and a main title. Include your name and student number in
brackets at the end of your main title. Please do not show irrelevant
information on the graph. Please also type your code in the code chunk
below. (10 marks)

    #TODO
    mean_center_photovoltaic <- c(mean(Photovoltaic$easting), mean(Photovoltaic$northing))
    mean_center_hydroelectric <- c(mean(Hydroelectric$easting), mean(Hydroelectric$northing))
    mean_center_total <- c(mean(filtered_ElectricPlants$easting), mean(filtered_ElectricPlants$northing))

    plot(filtered_ElectricPlants$easting, filtered_ElectricPlants$northing, col = "gray", main = "Switzerland Electric Production Plants (Nafisa Khan, 1004409017)", xlab = "easting(m)", ylab = "northing(m)")
    points(Photovoltaic$easting, Photovoltaic$northing, col = "blue", pch = 19)
    points(Hydroelectric$easting, Hydroelectric$northing, col = "green", pch = 19)
    points(mean_center_photovoltaic[1], mean_center_photovoltaic[2], col = "yellow", pch = 4, cex = 2)  
    points(mean_center_hydroelectric[1], mean_center_hydroelectric[2], col = "turquoise1", pch = 4, cex = 2) 
    points(mean_center_total[1], mean_center_total[2], col = "red", pch = 4, cex = 2)  


    legend("topleft", legend = c("Photovoltaic", "Hydroelectric", "Mean Center Photovoltaic", "Mean Center Hydroelectric", "Mean Center"), col = c("blue", "green", "yellow", "turquoise1", "red"), pch = c(19, 19, 4, 4, 4), cex = 0.5, pt.cex = 0.5)

![](GGR276Lab1P3_Starter_2024W_files/figure-markdown_strict/unnamed-chunk-40-1.png)

# Part 3D. Dispersion of Subsets

## Standard Deviation of Subsets

So far, we have measured the central tendency of the spatial data. How
about dispersion? Standard deviation is a measure of dispersion that can
be used to assess the distribution of spatial data. To calculate the
orthogonal dispersion (east-west, north-south) associated with
filtered\_ElectricPlants dataset, we will use sd() command applied on
easting and northing, respectively. Please do the same for the subsets
in Question 11.

    sd(filtered_ElectricPlants$easting)

    ## [1] 72544.4

    sd(filtered_ElectricPlants$northing)

    ## [1] 50633.08

**Question 11**: Please show your code as well as the calculated
standard deviation in your R Markdown. Provide a concise conclusion
regarding the orthogonal dispersion for ElectricPlants dataset and
subsets. These conclusions should include a short description of the
dispersion and a comparison (i.e. ElectricPlants vs. Photovoltaic
vs. Hydroelectric). Remember to include units of measurement in your
response. (6 marks)

    #TODO
    sd(Photovoltaic$easting)

    ## [1] 72525.3

    sd(Photovoltaic$northing)

    ## [1] 50661.54

    sd(Hydroelectric$easting)

    ## [1] 70359.13

    sd(Hydroelectric$northing)

    ## [1] 44444.7

**Type your response here**:

We observe that the Photovoltaic subset has a slightly higher standard
deviation in both easting and northing compared to the Hydroelectric
subset. This indicates that Photovoltaic plants are more dispersed
across the geographic landscape, both in the east-west and north-south
directions, than Hydroelectric plants. When comparing the subsets to the
entire ElectricPlants dataset, we see that the standard deviations for
the full dataset are quite similar to those for the Photovoltaic subset.
This suggests that the overall dispersion of electric production plants
is influenced heavily by the Photovoltaic plants, assuming that they
make up a significant proportion of the dataset. The Hydroelectric
plants have a narrower dispersion in both directions, indicating a more
clustered distribution.
