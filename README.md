# NYPD-Seven-Major-Felonies-dataset-Shiny-Visualization
In this project, we will create a R-shiny and leaflet for an interactive mapping web application. 
We will use the NYPD Seven Major Felonies dataset. 

You would find the the dataset at attached.

Introduction to Shiny and Leaflet

Shiny is an open-source R package for building very quick and powerful web applications using the R syntax. You can get an overview of what can be done using shiny please visit the web site: http://shiny.rstudio.com/gallery/

Leaflet is a popular interactive mapping library written in JavaScript and we will be using the R integration for leaflet. You can find the documentation to the leaflet R package please visit the web site: https://rstudio.github.io/leaflet/

To create our visualization with Shiny, we will be executing related steps;

Step 1: Create a global.R file, install and load the required packages and libraries: 

We first need to install and load the required packages. Here are the code that we need to write on global.R file

```html
package_vector = c("shiny", "leaflet", "tidyverse", "devtools", "dplyr")
install.packages(package_vector)

library(shiny)
library(leaflet)
library(tidyverse)
library(devtolls)
library(dplyr)
```

Step 2: Load the dataset from .rds file on global.R file and prepare it for mapping:

And continue to write the code below to read the dataset

```html
df <- readRDS("./sample_data.rds")
```

In the dataset, we can see that we have a Location.1 column that contains the crucial Latitude-Longitude information for mapping. But now this column is in string format and combined. To map the data in leaflef we need columns named as latitude and longitude.

First, we will split the column and create two separate columns named Latitude and Longitude as below;

```html
df <- tidyr::separate(data=df,
                      col=Location.1,
                      into=c("Latitude", "Longitude"),
                      sep=",",
                      remove=FALSE)
```

Also, we don’t need the “(” or “)” so we will remove them;

```html
df$Latitude <- stringr::str_replace_all(df$Latitude, "[(]", "")
df$Longitude <- stringr::str_replace_all(df$Longitude, "[)]", "")
```

We now have clean Latitude and Longitude columns but their data type is still string. We need to convert them to numeric so that they can be interpreted as coordinates;

```html
df$Latitude <- as.numeric(df$Latitude)
df$Longitude <- as.numeric(df$Longitude)
```

Step 3: Create a server.R file and code the structure of the map: 

In the server.R file, we will be creating our server function which will be called once for each session. For more detailed information about server.R function, please refer to Shiny Documentation: https://shiny.rstudio.com/articles/scoping.html

```html
server <- function(input,output, session){

 data <- reactive({
   x <- df
 })

 output$NYmap <- renderLeaflet({
   df <- data()

   m <- leaflet(data = df) %>%
          addTiles() %>%
          addMarkers(lng = ~Longitude,
                     lat = ~Latitude,
                     popup = paste("Offense", df$Offense, "<br>",
                                   "Jurisdiction", df$Jurisdiction, "<br>",
                                   "Year:", df$CompStat.Year))
   m
 })
}
```

Step 4: Create a ui.R file and code the ux design of the web application:

```html
ui <- fluidPage(
  leafletOutput("NYmap",height = 1000)
)
```

Step 5: runApp() from the RStudio console: 

Now, we have our web application ready, you can do runApp() from the RStudio console. You would find a preview of the web applicaion at attached. 
