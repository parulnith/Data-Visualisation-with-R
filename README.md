


# Data Visualisation with R

The world today is filled with data and it becomes imperative that we analyse it properly to gain meaningful insights.  



*Our goal as Data Analysts is to arrange the insights of our data in such a way that everybody who sees them is able to clearly understand their implications, or their truths and how to act on them.

*### The need to understand plots
There are several reasons why it is important to be able to produce and interpret plots of data.
_Visualize your data_. Plots are essential for visualizing and exploring your data. Plotting a histogram gives a sense of the range, center, and shape of the data. It shows if the data is symmetric, skewed, bimodal, or uniform. Box plots and plots of means, medians, and measures of variation visually indicate the difference in means or medians among groups. Scatter plots show the relationship between two measured variables.
_Communicate your results to others_. Being able to choose and produce appropriate plots is important for summarizing your data for professional or extension presentations and journal articles. Plots can be very effective for summarizing data in a visual manner and can show statistical results with impact.*



In this tutorial, we will learn how to analyze and display data using R. We will begin with basic plots and move on to more advanced stuff.


## Pre-requisites
Since this is a tutorial about visualisation in R, basic knowledge and working in R would come in handy.

## Table of Contents

 1.   #### [Introduction to R](#introduction-to-r)
 -  Overview
 -   Installation
 -  Loadng the Data
  - Data Exploration
 2.   #### [Getting Started with Basic Plots](#getting-started)
		
- Plot() command
- Barplot
- Histogram
- Boxplot

3. #### [Visualisation Packages in R](#visualisation-libraries)
- R Graphics
- Lattice
- plotrix
- ggplot2
- 
5. #### [Visualising Geographical data in R](#geographic-data)

6. #### Conclusion


# <a name="introduction-to-r"></a>1.Introduction to R

## Overview

[R](https://www.r-project.org/about.html) is a language and environment for statistical computing and graphics. It was developed by Ross Ihaka and Robert gentleman at the University of Auckland. It is freely available under GNU General Public License.
R provides a wide variety of statistical and graphical techniques, and is highly extensible. R is also extremely flexible and easy to use when it comes to creating visualisations. One of its capabilities is to produce good quality plots with minimum codes.

## Installation

We shall briefly go over the steps required to install R ont he system incase you haven't done it till now.

 1.   Go to the [R homepage](https://www.r-project.org/) and select **CRAN**
 **CRAN** is an acronym for -  Comprehensive R Archive Network. It’s the collection of sites which carry R Distributions, collection of R packages and documentation.
 
 2. Select the location which is nearest to you.
 3. Download and Install R depending upon your OS.
 
 *Alternatively, you can use [RStudio](http://www.rstudio.com/) over the base R GUI.*
 

### Startup
After R is downloaded and installed, simply find and launch R from your Applications folder(MacOS) or from Desktop Icon(Windows).

R is a command line driven program. The user enters commands at the prompt **>** and each command is executed one at a time.

    > 1
    1
    > 'hello World'
    hello world

###  The Workspace

Workspace in R refers to the current working environment . 


## Loading the Data

We will be working with a dataset to demonstrate the visualisation capabilities of R. this will help us to know how to create plots on a real data set. For this task we shall be utilising an built-in  dataset  from R.
* **Builit-in datasets**

We will be working with the airquality dataset. The dataset pertains to the Daily air quality measurements in New York, May to September 1973. This dataset consists of more than 100 observations on 6 variables i.e **Ozone**(mean parts per billion), **Solar.R**(Solar Radiation), **Wind**(Average wind speed), **Temp**(maximum daily temperture in Fahrenheit), **Month**(month of observation) and **Day**(Day of the month)

To load the built in dataset into the R  type the following command in the console:

    > data(airquality)
* **External data**
Data can also be loaded from external data sources like csv,excel, text, html and many more. But to be able to do that , the **working  directory** in R needs to be changed to where you saved the source files. You can easily do that with the **setwd()** command.

`> setwd(path of the folder where the file is located) `
    
Next step is to load the file. In this case it is an csv file named **airquality.csv**. You can download the source from here and place it in the current working directory.

`data = read.csv('airquality.csv',header=TRUE, sep=",")`
The above code reads the file **airquality.csv** into a data frame that it creates called data. **Header=TRUE** specifies that the data includes a header  and **sep=”,”** specifies that the values in data  are separated by commas. 

##  Data Exploration
Once the data has been loaded in the workspace, it is time to explore it to get an idea about its structure. Few commands which can be used are:

* **str(data)**
It displays the internal structue of an R object and gives a quick overview about regardign the rows and columns of the dataset.

  ```  > str(data)
    'data.frame':	111 obs. of  6 variables:
     $ Ozone  : int  41 36 12 18 23 19 8 16 11 14 ...
     $ Solar.R: int  190 118 149 313 299 99 19 256 290 274 ...
     $ Wind   : num  7.4 8 12.6 11.5 8.6 13.8 20.1 9.7 9.2 10.9 ...
     $ Temp   : int  67 72 74 62 65 59 61 69 66 68 ...
     $ Month  : int  5 5 5 5 5 5 5 5 5 5 ...
     $ Day    : int  1 2 3 4 7 8 9 12 13 14 ... `

 

* **head(data,n)** and **tail(data,n)**
The head outputs the top **n** elements in the dataset while the tail method outputs the bottom **n**. 
```
> head(data, n=3)
Ozone Solar.R Wind Temp Month Day
1    41     190  7.4   67     5   1
2    36     118  8.0   72     5   2
3    12     149 12.6   74     5   3

> tail(data)
   Ozone Solar.R Wind Temp Month Day
109    14     191 14.3   75     9  28
110    18     131  8.0   76     9  29
111    20     223 11.5   68     9  30
```
* **summary(data)**
The summary method displays descriptive statistics for every variable in the dataset, depending upon the  type of the variable. 
```
> summary(data)
    
    Ozone          Solar.R           Wind            Temp           Month            Day       
 Min.   :  1.0   Min.   :  7.0   Min.   : 2.30   Min.   :57.00   Min.   :5.000   Min.   : 1.00  
 1st Qu.: 18.0   1st Qu.:113.5   1st Qu.: 7.40   1st Qu.:71.00   1st Qu.:6.000   1st Qu.: 9.00  
 Median : 31.0   Median :207.0   Median : 9.70   Median :79.00   Median :7.000   Median :16.00  
 Mean   : 42.1   Mean   :184.8   Mean   : 9.94   Mean   :77.79   Mean   :7.216   Mean   :15.95  
 3rd Qu.: 62.0   3rd Qu.:255.5   3rd Qu.:11.50   3rd Qu.:84.50   3rd Qu.:9.000   3rd Qu.:22.50  
 Max.   :168.0   Max.   :334.0   Max.   :20.70   Max.   :97.00   Max.   :9.000   Max.   :31.00 
 ```

We can see at a glance the **mean**, **median**, **max** and the **quartile values** of the variables.

# <a name="getting-started"></a>2. Getting Started with Basic Plots

##  **plot()** function

R comes equipped with a  `plot()` function that is a kind of generic function for plotting of **R** objects.
*Please note that we use the $ sign to select a particular column in a dataset*

`> plot(airquality$Ozone)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Basic%20Plot.png)

We get a **scatter/dot**  plot here wherin each dot represents the value of the **Ozone** in **mean parts per billion**.

* Plotting a graph between the Ozone and Wind values.

` > plot(airquality$Ozone, airquality$Wind)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Ozone%20vs%20Wind.png)

The plot shows that wind and Ozone values have a somewhat negative correlation.


* Let us now see what happens when we use plot command the with the entire dataset without selecting any columns.

`> plot(airquality)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/All%20variables.png)

We get a matrix of scatterplots which is kind of a correlation matrix of all the columns. The plot shows that
 * The level of Ozone and Temperature is correlated positively.
 * Wind speed is negatively correlated to both Temperature and Ozone level.

###  Using arguments with the plot() function

Different capabilities of the plots can be unearthed by playing with the arguments in the function. In this section we will see how exactly does this happen.
### type argument

The plot function has an argument `type` which can have the following values.

-   `"p"`  for  **p**oints,
    
-   `"l"`  for  **l**ines,
    
-   `"b"`  for  **b**oth,
    
-   `"c"`  for the lines part alone of  `"b"`,
    
-   `"o"`  for both ‘**o**verplotted’,
    
-   `"h"`  for ‘**h**istogram’ like (or ‘high-density’) vertical lines,
    
-   `"s"`  for stair  **s**teps,
    
-   `"S"`  for other  **s**teps, see ‘Details’ below,
    
-   `"n"`  for no plotting.

Let us try few of the options 

     # points and lines 
     > plot(airquality$Ozone, type= "b") 

 ![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/line%20and%20point%20plot.png)
 

     # high density vertical lines.
     > plot(airquality$Ozone, type= "h")
![enter image description here](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/high%20density.png)

### Lables and Titles
The plot() function also gives the capabilities to label the X and Y axis and also the Title.You also have a option of giving a color to the plot.

> plot(airquality$Ozone, xlab = 'ozone Concenteration', ylab = 'No of Instances', main = 'Ozone levels in NY city', col = 'green')

![enter image description here](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/lables%20and%20titles.png)

Please feel free to experiment with the other options too.

## Other Basic Charts

Other types of charts available in R are:

### Barplot
In bar plot, data is represented in form of rectangular bars and the length of each bar is proportional to the value of the variable or column in the dataset. Both horizontal as well as veritcal bar chart can be generated by tweaking with the **horiz** parameter. 

    # Horizontal bar plot
    > barplot(airquality$Ozone, main = 'Ozone Concenteration in air',xlab = 'ozozne levels', col='green',horiz = TRUE)
![]()

    # Vertical bar plot
    >  barplot(airquality$Ozone, main = 'Ozone Concenteration in air',xlab = 'ozozne levels', col='red',horiz = FALSE)
    
### Histogram

A histogram is similar to a bar chart except that it groups values into continuous ranges. A histogram represents the frequencies of values of a variable bucketed into ranges. 


### Boxplot



### Multiple Boxplots

### Grid of Charts

# <a name="visualisation-libraries"></a>3. Visualisation libraries in R 

R comes equipped with sophisticated visualisation libraries. Let us have a closer look at some of the commonly used ones.





## Lattice Graphs
Lattice is a package which is essentially an improvement upon the R Graphics package and is used to visualize multi-variate data. lattice enables the use of *trellis graphs*. Trellis graphs exhibit the relationship betwen variables which are dependent on one or more variables.
We will use the built-in [mtcars dataset](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html) which was extracted from the 1974 _Motor Trend_ US magazine.

    # Loading the package
    library(lattice)  
    
    #Loading the dataset
    attach(mtcars)

    # Exploring the dataset
    head(mtcars)
                           mpg cyl disp  hp drat    wt  qsec vs am gear carb
    Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
    Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
    Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
        


    # Creating factors
    
       gear_factor<-factor(gear,levels=c(3,4,5),
               labels=c("3gears","4gears","5gears")) 
        cyl_factor <-factor(cyl,levels=c(4,6,8),
                labels=c("4cyl","6cyl","8cyl")) 

 

####  Kernel density plots

    densityplot(~mpg,  
    main="Density Plot",  
    xlab="Miles per Gallon")

####  scatterplot matrix  

        scatterplot matrix  
    splom(mtcars[c(1,3,4,5,6)],  
    main="MTCARS Data")

####  scatterplots depicting combination of two factors  

    xyplot(mpg~wt|cyl_factor*gear_factor,  
    main="Scatterplots : Cylinders and Gears",  
    ylab="Miles/Gallon", xlab="Weight of Car")

# <a name="geographic-data"></a>4. Visualising Geographical data in R

Geographic data (**Geo data**) relates to the  location based data. It primarily deals with describing objects with respect to their replationship in space. The data is usually stored in form of co-ordinates so that it be mapped. It makes more sense to be able to see the state or country in form of a map as it gives a more realistic overview. In the sections below, we will briefly ouline the capabilities of R in terms of geographical data visualisation. 

## Plotting basic geographical maps

Working on a real dataset will make much more sense int his section. We will be working with a sample superstore dataset of ABC company. the dataset has locations of their stores in the US. Let's load in the data.

    data <- read.csv('ABC_locations.csv', sep=",")

    head(data)
                        Address       City   State   Zip.Code Latitude  Longitude
    1  1205 N. Memorial Parkway Huntsville Alabama 35801-5930 34.74309  -86.60096
    2      3650 Galleria Circle     Hoover Alabama 35244-2346 33.37765  -86.81242
    3    8251 Eastchase Parkway Montgomery Alabama      36117 32.36389  -86.15088
    4 5225 Commercial Boulevard     Juneau  Alaska 99801-7210 58.35920 -134.48300
    5      330 West Dimond Blvd  Anchorage  Alaska 99515-1950 61.14327 -149.88422
    6          4125 DeBarr Road  Anchorage  Alaska 99508-3115 61.21081 -149.80434

###  Using  plot() function
by using the Latitude and the Longitude column, we will create a crude plot.

    plot(data$Longitude,data$Latitude)

The output isn't an exact map but gives a faint outline of the US map.
![]()

###  Using  map() function
maps package is very useful and straightforward too when it comes to plotting geographical data. But it needs to be installed before using it.

    # Install package 
    install.packages("maps", dependencies=TRUE)
    
    # Load maps package
    library(maps)
    

**Using the map() function to plot a base map**

     map(database="state")
![]()


**Building a point map on top of the base map using symbols() function**

    symbols(data$Longitude, data$Latitude, squares =rep(1, length(data$Longitude)), inches=0.03, add=TRUE)
![]()

**Giving the symbols a color**

    symbols(data$Longitude, data$Latitude,bg = 'red', fg = 'red', squares =rep(1, length(data$Longitude)), inches=0.03, add=TRUE)

![]()

> ?map() gives more details into the functioning of map command.




