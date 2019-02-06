url<- "ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn-v2.5-stations.txt"
download.file(url = url, destfile = "weatherdata.txt" )
wdata<-read_table("weatherdata.txt")


###you can try this code to import data and creat the plots

Part 2: Weather Station

```{r}
library(readr)
weather <- read_fwf("ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn-v2.5-stations.txt",col_positions = fwf_widths(c(2,1,2,6,9,10,7,3,31,7,7,7,3),col_names = c("COUNTRY CODE ", "NETWORK CODE","ID PLACEHOLDERS (\"00\")","COOP ID", "LATITUDE", "LONGITUDE", "ELEVATION","STATE", "NAME", "COMPONENT 1 (COOP ID)","COMPONENT 2 (COOP ID)","COMPONENT 3 (COOP ID)", "UTC OFFSET")))
```

Creat the plot
```{r}
library(ggplot2)
library(RColorBrewer)
p<-ggplot()+geom_point(data=weather,aes(y=LATITUDE,x=LONGITUDE,colour=ELEVATION))+scale_color_gradientn( colours = brewer.pal( 11, "RdYlBu" ))
p
```
Include the state information and time zone information
```{r}
library(ggmap)
library(maps)
library(mapdata)
states <- map_data("state")
p + geom_path(data = states,aes(x = long, y = lat, group = group), color = "black") +   coord_fixed(1.3) +  guides(fill=FALSE) 

```

```{r}
download.file("ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn.tavg.latest.raw.tar.gz", destfile = "/Users/ganghan/Desktop/585/STAT585_Lab1/average_temperature.tar.gz")
untar('average_temperature.tar.gz')
```


### the code for download and untar etc..

download .gz file and open with tools available in R.
```{r}
download.file("ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn.tavg.latest.raw.tar.gz",destfile = "ushcn.tavg.latest.raw.tar.gz")
untar("ushcn.tavg.latest.raw.tar.gz")
```

Check the number of files inside the file ushcn.tavg.latest.raw.tar.gz and the name of the file containing the temperature data of your hometowns or Fort Dodge, IA (please specify).

```{r}
library(dplyr)
files <- list.files("ushcn.v2.5.5.20190206")
cat('total number of files is', length(files))

weather %>% filter(grepl("FORT DODGE", weather$NAME)) %>% select(`COUNTRY CODE `,`NETWORK CODE`,"ID PLACEHOLDERS (\"00\")","COOP ID" ) %>% paste(collapse = "") %>% grep(files) -> index
files[index]
```