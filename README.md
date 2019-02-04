url<- "ftp://ftp.ncdc.noaa.gov/pub/data/ushcn/v2.5/ushcn-v2.5-stations.txt"
download.file(url = url, destfile = "weatherdata.txt" )
wdata<-read_table("weatherdata.txt")
