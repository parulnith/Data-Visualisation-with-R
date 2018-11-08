
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



