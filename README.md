# NYPD-Seven-Major-Felonies-dataset-Shiny-Visualization
In this project, we will create a R-shiny and leaflet for an interactive mapping web application. 
We will use the NYPD Seven Major Felonies dataset. 

You would find the the dataset at attached.

Introduction to Shiny and Leaflet

Shiny is an open-source R package for building very quick and powerful web applications using the R syntax. You can get an overview of what can be done using shiny please visit the web site: http://shiny.rstudio.com/gallery/

Leaflet is a popular interactive mapping library written in JavaScript and we will be using the R integration for leaflet. You can find the documentation to the leaflet R package please visit the web site: https://rstudio.github.io/leaflet/

To create our visualization with Shiny, we will be executing related steps;

Step 1: Create a global.R file, install and load the required packages and libraries 

We first need to install and load the required packages. Here are the code that we need to write on global.R file

- package_vector = c("shiny", "leaflet", "tidyverse", "devtools", "dplyr")
- install.packages(package_vector)



To install these R packages, we will be coding the  you can use the install.packages function from the RStudio console. You can also pass a vector of package names to the install.packages function and it’ll do the rest:

In the global.R file, load the following required libraries:

library(shiny)
library(leaflet)
library(dplyr)
