
Reproducibe Research Week 2 Assignment

Loading and preprocessing the data

>activity<-read.csv("activity.csv")

>head(activy)

Error in head(act) : object 'acttivy' not found

>head(activity)

output

steps date interval

1 NA 2012-10-01 0
2 NA 2012-10-01 5
3 NA 2012-10-01 10
4 NA 2012-10-01 15
5 NA 2012-10-01 20
6 NA 2012-10-01 25

Now we have to remove the NA values from our data. For that

>Clean_activity<-activity[complete.cases(activity),]

>dim(clean_activity)

Error: object 'clean_activity' not found

>dim(Clean_activity)

[1] 15264 3

What is mean total number of steps taken per day?

steps_per_day <- aggregate(steps ~ date, Clean_activity, sum)


head(steps_per_day)


    date steps
1 2012-10-02 126 2 2012-10-03 11352 3 2012-10-04 12116 4 2012-10-05 13294 5 2012-10-06 15420 6 2012-10-07 11015

hist(steps_per_day$steps, main="Total Number of Steps per day", xlab = "Steps per Day")

Calculate and report the mean and median total number of steps taken per day

summary(steps_per_day)

     date        steps      
2012-10-02: 1 Min. : 41

2012-10-03: 1 1st Qu.: 8841

2012-10-04: 1 Median :10765

2012-10-05: 1 Mean :10766

2012-10-06: 1 3rd Qu.:13294

2012-10-07: 1 Max. :21194

(Other) :47

What is the average daily activity pattern?

steps_per_interval <- aggregate(steps ~ interval, Clean_activity, mean)

head(steps_per_interval)
  interval     steps
  
1        0 1.7169811

2        5 0.3396226

3       10 0.1320755

4       15 0.1509434

5       20 0.0754717

6       25 2.0943396

> plot(steps_per_interval$interval, steps_per_interval$steps, type='l',main="Average number of steps per interval across all days", xlab="Interval", ylab="Average number of steps")

TOTAL NUMBER OF MISSING VALUES IN THE DATASET

> sum(is.na(activity))

[1] 2304

> new_activity<-activity

>  for (i in 1:nrow(activity)) {
+       if (is.na(activity$steps[i])) {
+         new_activity$steps[i] <- steps_per_interval[steps_per_interval$interval ==     activity$interval[i], ]$steps
+       }
+     }

> head(new_activity, 10)

       steps       date interval
       
1  1.7169811 2012-10-01        0

2  0.3396226 2012-10-01        5

3  0.1320755 2012-10-01       10

4  0.1509434 2012-10-01       15

5  0.0754717 2012-10-01       20

6  2.0943396 2012-10-01       25

7  0.5283019 2012-10-01       30

8  0.8679245 2012-10-01       35

9  0.0000000 2012-10-01       40

10 1.4716981 2012-10-01       45
