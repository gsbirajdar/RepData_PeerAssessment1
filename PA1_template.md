# PA1_templete.Rmd
Ganesh Birajdar  
September 14, 2015  

Following is the r code to load the data necessary for analysis asked for in
question. It assumes that there is a file named 'activity.csv' in your working
directory, which is in following github repository in 'activity.zip' file:
http://github.com/rdpeng/RepData_PeerAssessment1

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
activity <- na.omit(activity)
activity$date <- as.Date(activity$date)
```
Now our dataset is ready to perform some analysis. First of all, we will
calculate **the number of steps taken per day**. We don't want to see it's
output, but rather want to see the histogram created with this output, therefore
we will specify results="hide" in following code which tells it to print only the
code and not the output.

```r
stepsbyday <- sapply(split(activity$steps, activity$date), sum)
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
hist(sapply(split(activity$steps, activity$date), sum), 
     xlab = "Number of steps in a day", ylab = "Frequency (Number of days)",
     main = "Total number steps taken per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 