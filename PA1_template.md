# Peer assessment1_Repdata-032
Ganesh Birajdar  
September 14, 2015  

Following is the r code to load the data necessary for analysis asked for in
question of peer assessment 1 of the course repdata-032 on coursera. It assumes 
that there is a file named 'activity.csv' in your working
directory, which is in following github repository in 'activity.zip' file:
http://github.com/rdpeng/RepData_PeerAssessment1
We will first read the given dataset and then answer the 4 question asked one by
one, which are:  
**_What is mean total number of steps taken per day?_**  
**_What is the average daily activity pattern?_**  
**_Imputing missing values_**  
**_Are there differences in activity patterns between weekdays and weekends?_**  


```r
activity <- read.csv("activity.csv")
```
Now that we have loaded the data into workspace, we will remove NAs in order to
make it is for us to perform operations like 'sum' or 'mean' on this data. Also 
following code will change the class of date variable in dataset to date format
using as.Date function.
Before that it is useful to check how our data looks like, using functions like
str() or head().

```r
activity2 <- na.omit(activity)
activity2$date <- as.Date(activity2$date)
```
Now our dataset is ready to perform some analysis. Starting with first question:  
**_What is mean total number of steps taken per day?_**
First of all, we will calculate **the number of steps taken per day**. We don't 
want to see it's output, but rather want to see the histogram created with this 
output, therefore we will specify results="hide" in following code which tells 
it to print only the code and not the output.

```r
stepsbyday <- sapply(split(activity2$steps, activity2$date), sum)
```
We will now plot this daily count to a histogram which will allow us how it is
distributed.

```r
require(knitr)
```

```
## Loading required package: knitr
```

```r
opts_chunk$set(fig.path = "./figures/")
hist(stepsbyday, 
     xlab = "Number of steps in a day", ylab = "Frequency (Number of days)",
     main = "Total number steps taken per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 

```r
print(meansteps <- mean(stepsbyday))
```

```
## [1] 10766.19
```

```r
print(mediansteps <- median(stepsbyday))
```

```
## [1] 10765
```
So we see that the mean steps taken in a day were 10766.15 and median were
10765.  
Now coming to our second question:  
**_What is the average daily activity pattern?_**  
For this, first we will creat average out number of steps taken in each time
interval averaged over all days (e.g., number of steps taken in time 
interval 5, everyday)

```r
stepsmeanbyinterval <- sapply(split(activity2$steps, activity2$interval), mean)
```
