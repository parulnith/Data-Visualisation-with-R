

We will create a crude map by simply using the Latitude and the Longitude column.

    plot(data$Longitude,data$Latitude)

![](https://github.com/parulnith/Data-Visualisation-with-R/blob/master/Visualisation%20geographical%20data/Basic%20geog%20plot.png)
The output isn't an exact map but it does give a faint outline of the US map.


###  map() function
**maps package** is very useful and straightforward  when it comes to plotting geographical data. Let see how we can use it for our purpose. 

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

The commands used with the map function are kind of self explanatory. You can read more about it by typing `?maps()` at the R console.

Thus, geographical data visualisation holds a lot of importance where the data consists of locations. One can easily visualise the exact places and areas and convey a better picture.


# <a name="conclusion"></a>5. Conclusion

We have seen how simple and easy to start visualisation using R. One can either opt to create visualisations from scratch or use the pre built packages. Whatever you choose, it is clear that visualisations capabilities of R are endless.
