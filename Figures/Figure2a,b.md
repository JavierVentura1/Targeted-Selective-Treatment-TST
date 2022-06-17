# Targeted-Selective-Treatment-TST-
library(dplyr)
library(readr)
library(lubridate)
Climatemal <- read_csv("Climatemal.csv")
Climatemal$Date <-dmy(Climatemal$Date)
Climatemal$month <- month(ymd(Climatemal$Date))
Climatemal$year <- year(ymd(Climatemal$Date))
month.abb[Climatemal$month]
Climatemal$month <-month.abb[Climatemal$month]
Climatemal$Time <- paste(Climatemal$month,Climatemal$year)
Climatemal$Time <-factor(Climatemal$Time, levels = c("Jan-20", "Feb-20", "Mar-20", "Apr-20","May-20", "Jun-20","Jul-20","Aug-20","Sep-20","Oct-20","Nov-20","Dec-20", "Jan-21", "Feb-21", "Mar-21"))
climalmean <- read_csv("climalmean.csv")
climalmean$Time <-factor(climalmean$Time, levels = c("Jan-20", "Feb-20", "Mar-20", "Apr-20","May-20", "Jun-20","Jul-20","Aug-20","Sep-20","Oct-20","Nov-20","Dec-20", "Jan-21", "Feb-21", "Mar-21"))
ggplot(data=climalmean, aes(x=Time, y=Mean, group=Climate, color = Climate)) +
  geom_errorbar(aes(ymin=Mean-SD, ymax=Mean+SD), width=.1)+
  geom_line(aes(color = Climate))+
  geom_point(aes(colour = Climate)) +
  ThemeEM_XY+
  labs(fill="Climatic conditions")+
  theme(legend.position="top")+
  facet_wrap(~Climate, ncol = 1)
