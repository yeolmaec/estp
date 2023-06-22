# making an inflation map

## install necessary packages
install.packages("sf")
install.packages("tmap")
install.packages("terra")
install.packages("tidyverse")
library(sf)
library(terra)
library(tmap)
library(tidyverse)
data(World)

##import inflation data and merge it to the 'World' data
inflation <- read.csv("inflation.csv")
inflation <-
  inflation %>% 
  rename(iso_a3=Country.Code,inflation=X222..YR222. )

World2<- merge(World,inflation, by="iso_a3")

##draw a map
tm_shape(World2)+
  tm_polygons("inflation", breaks=c(0,2,6,10,20,80))

tm_shape(World2)+
  tm_polygons("inflation", style = "fisher")    #==> fisher or equal

tm_shape(World2)+
  tm_polygons("inflation", style = "fisher") +   
  tm_facets(by="continent")

