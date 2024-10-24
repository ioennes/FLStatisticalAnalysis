install.packages("farff")
install.packages("zoo")
library(zoo)

library(farff)
library(ggplot2)

data <- readARFF("./french_load.arff")
data <- data[ , !(names(data) %in% c("id"))]
View(data)

data$tempAvg <- (data$tempMin + data$tempMax) / 2
data$date <- as.POSIXct(data$date, format="%Y-%m-%dT%H:%M:%SZ")

data$tempMin_smooth <- rollmean(data$tempMin, k = 5000, fill = NA, align = "right")
data$tempMax_smooth <- rollmean(data$tempMax, k = 5000, fill = NA, align = "right")
data$tempAvg_smooth <- rollmean(data$tempAvg, k = 5000, fill = NA, align = "right")
data$sun_smooth <- rollmean(data$sun, k = 5000, fill = NA, align = "right")

# Plot the smoothed data using geom_line()
ggplot(data, aes(x = sun, y = Load)) +
  geom_point(size=0.1) +
  geom_smooth(method=lm, se=FALSE)
