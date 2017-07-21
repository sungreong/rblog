# rblog
R 예제들

# as.Date() 년 월 일이 다 필요해서 일이 없어서 사용할수가 없다.  
myData <- data.frame(Year = c(floor(time(AirPassengers) + .01)),
                     Month = c(cycle(AirPassengers)),
                     Value = c(AirPassengers),
                     Date =paste(c(floor(time(AirPassengers) + .01)), c(cycle(AirPassengers)),sep="_"))
myData$Date<- as.character(myData$Date)
myData$Date <- as.Date(myData$Date,"%Y")

ggplot(myData, aes(Month,Value)) + geom_line()+ xlab("") + ylab("Daily Views")
myData$Month <- factor(myData$Month)
levels(myData$Month) <- month.abb
referenceLines <- myData
colnames(referenceLines)
colnames(referenceLines)[2] <- "groupVar"
zp <- ggplot(myData,
              aes(x = Year, y = Value))
zp <- zp + geom_line(data = referenceLines,  # Plotting the "underlayer"
                       aes(x = Year, y = Value, group = groupVar),
                       colour = "steelblue", alpha = 1/2, size = 1/2)
zp <- zp + geom_line(size = 1)  # Drawing the "overlayer"
zp <- zp + facet_wrap(~ Month)
zp <- zp + theme_bw()
library(plotly)
ggplotly()
