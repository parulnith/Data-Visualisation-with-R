

# Getting started with Data Visualisation in R

The world today is filled with data and it becomes imperative that we analyse it properly to gain meaningful insights.  Data Visualisation is a vital tool that can unearth possible crucial insights from data. If the results of an analysis are not visualised properly, it will not be communicated effectively to the desired audience.

In this tutorial, we will learn how to analyze and display data using R statistical language. We will begin with basic plots and move on to more advanced ones later int he article.

## Pre-requisites
Since this is a tutorial about visualisation in R, a basic knowledge and working in R would come in handy.

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
- lattice
- plotly
- ggplot2
- tidyverse

5. #### [Visualising Geographical data in R](#geographic-data)

6. #### [Conclusion](#conclusion)


# <a name="introduction-to-r"></a>1.Introduction to R

## Overview

[R](https://www.r-project.org/about.html) is a language and environment for statistical computing and graphics. R provides a wide variety of statistical and graphical techniques, and is highly extensible. R is also extremely flexible and easy to use when it comes to creating visualisations. One of its capabilities is to produce good quality plots with minimum codes.

## Installation

We shall briefly go over the steps required to install R ont he system incase you haven't done it till now.

 1.   Go to the [R homepage](https://www.r-project.org/) and select **CRAN**.
 **CRAN** is an acronym for -  Comprehensive R Archive Network. It’s the collection of sites which carry R Distributions, Packages and documentation.
  2. Select the location which is nearest to you.
 3. Download and Install R depending upon your OS.
 
 *Alternatively, you can use [RStudio](http://www.rstudio.com/) over the base R GUI.*
 

### Startup
After R is downloaded and installed, simply find and launch it from your Applications folder(MacOS) or from Desktop Icon(Windows). R is a command line driven program. The user enters commands at the prompt **>** and each command is executed one at a time.

    > 1
    1
    > 'hello World'
    hello world

## Loading in the Data

Datasets can either be built in or external. 
* **Builit-in datasets** refers to the datasets already provided with R and we shall be using one such dataset to explore its visualisation capabilities. We will be working with the **airquality** dataset. The dataset pertains to the Daily air quality measurements in New York, May to September 1973. This dataset consists of more than 100 observations on 6 variables i.e **Ozone**(mean parts per billion), **Solar.R**(Solar Radiation), **Wind**(Average wind speed), **Temp**(maximum daily temperture in Fahrenheit), **Month**(month of observation) and **Day**(Day of the month)

To load the built- in dataset into the R  type the following command in the console:

    data(airquality)
* In case of an **External data** source (csv,excel, text, html file etc), simply set the folder containing the data as the   the **working  directory** with the **setwd()** command.

`setwd(path of the folder where the file is located) `
    
Now, load the file with the help of **read** command. In this case data is inform of a csv file named **airquality.csv** and can be downloaded from [here]()

`airquality = read.csv('airquality.csv',header=TRUE, sep=",")`

The above code reads the file **airquality.csv** into a data frame  **airquality**. **Header=TRUE** specifies that the data includes a header  and **sep=”,”** specifies that the values in data  are separated by commas. 

##  Data Exploration
Once the data has been loaded into the workspace, it is time to explore it to get an idea about its structure. Few commands which can be used are:

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

> tail(data, n=3)
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

The [graphics](https://stat.ethz.ch/R-manual/R-devel/library/graphics/html/graphics-package.html) package is used for plotting **base** graphs like scatter plot, box plot etc.For a complete list of functions with individual help pages, use  `library(help = "graphics")`.

##  **The plot()** function

* The  `plot()` function that is a kind of generic function for plotting of **R** objects. If we plot the ozone column of a dataset , we get a plot like this:

`> plot(airquality$Ozone)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Basic%20Plot.png)

We get a **scatter/dot**  plot here wherin each dot represents the value of the **Ozone** in **mean parts per billion**.

* Let us now plot a graph between the Ozone and Wind values to study the relationship between the two values.

` > plot(airquality$Ozone, airquality$Wind)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Ozone%20vs%20Wind.png)

The plot shows that wind and Ozone values have a somewhat negative correlation.

*  What happens when we use plot command the with the entire dataset without selecting any particular columns?

`> plot(airquality)`

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/All%20variables.png)

We get a matrix of scatterplots which is kind of a correlation matrix of all the columns. The plot shows instantly shows that: 
 * The level of Ozone and Temperature is correlated positively.
 * Wind speed is negatively correlated to both Temperature and Ozone level.
 
***Thus, we can easily discover the relationship  between variables by simply looking at the plots drawn between them. This is the power of visualisation.***

###  Using arguments with the plot() function

The plot() function has many arguments and by playing with the values , we can easily style the charts .
### type argument

The plot function has an argument called `type` which can take in values like **p : points**, **l:lines**,**b: both** etc. This basically decides the shape of the output graph. 


     # points and lines 
     > plot(airquality$Ozone, type= "b") 

 ![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/line%20and%20point%20plot.png)
 

     # high density vertical lines.
     > plot(airquality$Ozone, type= "h")
![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/high%20density.png)

*You can read more about the plot() command by typing `?plot()` in the console.*


### Lables and Titles
We can also label the X and the Y axis and also give a title to our plot . Additionally, we  also have an option of giving a color to the plot.

> plot(airquality$Ozone, xlab = 'ozone Concenteration', ylab = 'No of Instances', main = 'Ozone levels in NY city', col = 'green')

![enter image description here](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/lables%20and%20titles.png)


## Barplot

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

R comes equipped with sophisticated visualisation libraries having great capabilities.  Let us have a closer look at some of the commonly used ones.


## Lattice Graphs
[Lattice](https://stat.ethz.ch/R-manual/R-devel/library/lattice/html/Lattice.html) is a package which is essentially an improvement upon the R Graphics package and is used to visualize multi-variate data. Lattice enables the use of *trellis graphs*. Trellis graphs exhibit the relationship betwen variables which are dependent on one or more variables.
We will use the built-in [mtcars dataset](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html) which was extracted from the 1974 _Motor Trend_ US magazine.

    # Installing & Loading the package
    install.package("lattice")
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

 Now let us see how we can use the the **lattice** package to create some basic plots in R.

####  Kernel density plots

    densityplot(~mpg,  
    main="Density Plot",  
    xlab="Miles per Gallon")

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Lattice/kde.png)

It is very straightforward to use the lattice library. One simply needs to plug in the columns for which the plot is desired.

####  scatterplot matrix  

        scatterplot matrix  
    splom(mtcars[c(1,3,4,5,6)],  
    main="MTCARS Data")

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Lattice/scatterplot%20matrix.png)

####  scatterplots depicting combination of two factors  

    xyplot(mpg~wt|cyl_factor*gear_factor,  
    main="Scatterplots : Cylinders and Gears",  
    ylab="Miles/Gallon", xlab="Weight of Car")
    
![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Lattice/scatterplot%2B2%20factors.png)
  
    
    
## Plotly

[Plotly](https://github.com/ropensci/plotly#readme) is a R package that creates interactive web-based graphs via the open source JavaScript graphing library [plotly.js](http://plot.ly/javascript). It can easily translate the ‘ggplot2’ graphs to web-based versions also.

    #Installing & Loading the package 
     
     install.package(“plotly”)  
     library(plotly)

Let us now see how we can utilise plotly to create interactive visualisations. We will be working with the same mtcars dataset that  used in the lattice graphs demonstration.

#### Basic Scatter Plot

    p <- plot_ly(data = mtcars, x = ~hp, y = ~wt)
    p

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Plotly/Plotly_scatter.png)

we obtain a scatter plot as follows. The plot can also be exported in form of a web page to keep its interactiveness intact.

#### Styled Scatter Plot

The scatter plot can be styled by giving in the appropriate color codes.

    > p <- plot_ly(data = mtcars, x = ~hp, y = ~wt, marker = list(size = 10, color = ‘rgba(255, 182, 193, .9)’, line = list(color = ‘rgba(152, 0, 0, .8)’, width = 2)))
    
    > p
![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Plotly/Plotly_style_scatterplot.png)


#### Markers and Lines

It is also possible to plot markers and lines in the same plot. let’s create a data frame named data consisting of markers and lines and plot it.

    data1 <- rnorm(100, mean = 10)   
    data2 <- rnorm(100, mean = 0)   
    data3 <- rnorm(100, mean = -10)   
    x <- c(1:100)
    
    data <- data.frame(x, data1, data2, data3)
    
    p <- plot_ly(data, x = ~x)%>%   
        
    add_trace(y = ~data1, name = ‘data1’,mode = ‘lines’)%>%             
    add_trace(y = ~data2, name = ‘data2’, mode = ‘lines+markers’)%>% 
    add_trace(y = ~data3, name = ‘data3’, mode = ‘markers’)

 ![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Plotly/Plotly_markers.png) 

####  Adding Color and Size Mapping

    p <- plot_ly(data = mtcars, x = ~hp, y = ~wt,color = ~hp, size = ~hp )
    p
    
 ![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Packages/Plotly/Plotly_color_size.png)     


# <a name="geographic-data"></a>4. Visualising Geographical data in R

Geographic data (**Geo data**) relates to the  location based data. It primarily deals with describing objects with respect to their replationship in space. The data is usually stored in the form of co-ordinates so that it be mapped. It makes more sense to be able to see a  state or a country in the form of a map as it gives a more realistic overview. In the section below, we will briefly ouline the capabilities of R in terms of geographical data visualisation. 

###  Geographical maps

We will be working with a sample superstore dataset of the [ABC company](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/ABC_locations.csv). The dataset consists of locations of their stores in the US. Let's load in the data and check out its columns.

    data <- read.csv('ABC_locations.csv', sep=",")

    head(data)
                        Address       City   State   Zip.Code Latitude  Longitude
    1  1205 N. Memorial Parkway Huntsville Alabama 35801-5930 34.74309  -86.60096
    2      3650 Galleria Circle     Hoover Alabama 35244-2346 33.37765  -86.81242
    3    8251 Eastchase Parkway Montgomery Alabama      36117 32.36389  -86.15088
    4 5225 Commercial Boulevard     Juneau  Alaska 99801-7210 58.35920 -134.48300
    5      330 West Dimond Blvd  Anchorage  Alaska 99515-1950 61.14327 -149.88422
    6          4125 DeBarr Road  Anchorage  Alaska 99508-3115 61.21081 -149.80434

###  plot() function 
We will create a crude map by simply using the Latitude and the Longitude column.

    plot(data$Longitude,data$Latitude)

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/Basic%20geog%20plot.png)

The output isn't an exact map but it does give a faint outline of the the US structure .


###  map() function
**maps package** is very useful and straightforward  when it comes to plotting geographical data. Let us see how we can use it for our purpose. 

    # Install package 
    install.packages("maps", dependencies=TRUE)
    
    # Loading the installed maps package
    library(maps)
    

**Using the map() function to plot a base map of the US**

     map(database="state")
![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/base%20map.png)


**Building a point map on top of the base map using symbols() function**

    symbols(data$Longitude, data$Latitude, squares =rep(1, length(data$Longitude)), inches=0.03, add=TRUE)
![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/top%20of%20base%20map.png)

**Giving the symbols a color**

    symbols(data$Longitude, data$Latitude,bg = 'red', fg = 'red', squares =rep(1, length(data$Longitude)), inches=0.03, add=TRUE)

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/styling%20map.png)

The commands used with the map function are kind of self explanatory. You can read more about it at their [documentation page](https://cran.r-project.org/web/packages/maps/maps.pdf).

Thus, geographical data visualisation holds a lot of importance where the data consists of locations. One can easily visualise the exact places and areas and convey a better picture.


# <a name="conclusion"></a>5. Conclusion

We have seen how simple and easy to start visualisation using R. One can either opt to create visualisations from scratch or use the pre built packages. Whatever you choose, it is clear that visualisations capabilities of R are endless.



