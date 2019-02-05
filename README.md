url<- "ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn-v2.5-stations.txt"
download.file(url = url, destfile = "weatherdata.txt" )
wdata<-read_table("weatherdata.txt")


###you can try this code to import data

library(readr)
weather <- read_fwf("ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn-v2.5-stations.txt",col_positions = fwf_widths(c(2,1,2,6,9,10,7,3,31,7,7,7,3),col_names = c("COUNTRY CODE ", "NETWORK CODE","ID PLACEHOLDERS (\"00\")","COOP ID", "LATITUDE", "LONGITUDE", "ELEVATION","STATE", "NAME", "COMPONENT 1 (COOP ID)","COMPONENT 2 (COOP ID)","COMPONENT 3 (COOP ID)", "UTC OFFSET")))
