


# Reproducible Research: Peer Assessment 1
library(knitr)  
Author: erinosb  
Date:   August 16th, 2014  


## Loading and preprocessing the data
 


```r
setwd("~/Dropbox/Courses/Coursera/ReproducibleResearch")  
repdata.df <- read.csv("activity.csv")  
```

## Basic EDA  

```r
dim(repdata.df)  
```

```
## [1] 17568     3
```

```r
head(repdata.df) 
```

```
##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
## 6    NA 2012-10-01       25
```

```r
str(repdata.df)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```
  

## What is mean total number of steps taken per day?  

```r
##Make a histogram of the total number of steps taken each day
attach(repdata.df)
hist(by(repdata.df$steps, date, function(x) mean(x)))
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

```r
##Calculate and report the mean and median total number of steps taken per day
mean(as.vector(by(repdata.df$steps, date, function(x) mean(x))), na.rm = TRUE)
```

```
## [1] 37.38
```

```r
median(as.vector(by(repdata.df$steps, date, function(x) mean(x))), na.rm = TRUE)
```

```
## [1] 37.38
```

```r
help(mean)
```


## What is the average daily activity pattern?  

```r
##Make a time series plot
intervalmeans <- sapply(split(repdata.df$steps, interval), function(x) mean(x, na.rm=TRUE))
plot(names(intervalmeans), intervalmeans, type = "l",
     main = "Steps per interval, averaged over days",
     xlab = "interval",
     ylab = "mean steps", 
     las = 1)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

```r
#Which 5 minute interval contains the maximum number of steps?
names(which(intervalmeans == max(intervalmeans)))
```

```
## [1] "835"
```



## Imputing missing values  



## Are there differences in activity patterns between weekdays and weekends?  
