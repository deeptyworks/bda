Big Data R Programs - Short Versions
Outputs for 1-7 are from the record. Outputs for 8-15 were not in the record, so they are worked out from the code.
1. Leap year
y <- as.integer(readline("Enter year to be checked: "))
leap <- (y %% 4 == 0 && y %% 100 != 0) || y %% 400 == 0
cat(y, ifelse(leap, "is a leap year.", "is not a leap year."))
Output:
Enter year to be checked: 2024
2024 is a leap year.
Enter year to be checked: 2025
2025 is not a leap year.
2. Sum of natural numbers (if-else + while)
n <- as.integer(readline("Enter a number: "))
if (n < 0) {
  print("Enter a positive number.")
} else {
  s <- 0
  while (n > 0) {
    s <- s + n
    n <- n - 1
  }
  cat("The sum of numbers up to the given limit is", s)
}
Output:
Enter a number: 15
The sum of numbers up to the given limit is 120
3. Student grade
m <- sum(c(57, 98, 59, 89, 78, 90, 57, 96, 45, 75))
g <- if (m >= 800) "A+" else
     if (m >= 700) "A"  else
     if (m >= 500) "B+" else
     if (m >= 400) "B"  else
     if (m >= 150) "C"  else "D"
cat(m, "is the total marks scored\n")
cat(g, "is the grade secured by the student")
Output:
744 is the total marks scored
A is the grade secured by the student
4. Calculator (switch + function)
calc <- function(x, y, ch) switch(ch, x + y, x - y, x * y, x / y)
ch <- as.integer(readline("Enter choice [1/2/3/4]: "))
a  <- as.integer(readline("Enter first number: "))
b  <- as.integer(readline("Enter second number: "))
op <- switch(ch, "+", "-", "*", "/")
cat(a, op, b, "=", calc(a, b, ch))
Output:
Enter choice [1/2/3/4]: 1
Enter first number: 5
Enter second number: 10
5 + 10 = 15
Choice 2 (50, 25):  50 - 25 = 25
Choice 3 (5, 5):    5 * 5 = 25
Choice 4 (50, 5):   50 / 5 = 10
1
5. Matrix with rbind() and row names
x <- rbind(c("C#", "Java", "COBOL", ".Net"),
           c("JavaScript", "Node.js", "R", "Azure"),
           c("Power BI", "ASP.Net", "Unity", "Block Chain"))
rownames(x) <- c("Lang1", "Lang2", "Lang3")
print(x)
cat("The third element in the second row is", x["Lang2", 3])
Output:
      [,1]         [,2]      [,3]    [,4]
Lang1 "C#"         "Java"    "COBOL" ".Net"
Lang2 "JavaScript" "Node.js" "R"     "Azure"
Lang3 "Power BI"   "ASP.Net" "Unity" "Block Chain"
The third element in the second row is R
6. Excel to CSV and data viewer functions
library(readxl)
write.csv(read_excel("dataset.xlsx"), "dataset.csv", row.names = FALSE)
d <- read.csv("dataset.csv")
dim(d)                                        # dimensions
head(d, 5)                                    # first 5 rows
tail(d, 5)                                    # last 5 rows
head(d[order(d$AGE), ], 5)                    # sorted by age
head(d[order(-d$AGE), ], 5)                   # sorted descending
subset(d, AGE > 30)                           # filtering
d[grep("John", d$NAME, ignore.case = TRUE), ] # searching
rm(d)                                         # remove object
Output:
[1] 20  3
  SL.NO    NAME AGE        (head)
1     1    ABEL  29
2     2 HARSHIN  20
3     3 ANANDHU  30
4     4   ARJUN  30
5     5   ASEEM  23
   SL.NO    NAME AGE       (tail)
16    16   IMRAN  26
17    17  DEEPTY  29
18    18  JISHNU  21
19    19  HARFAS  29
20    20   LAYAS  29
   SL.NO     NAME AGE      (sorted by age)
2      2  HARSHIN  20
18    18   JISHNU  21
6      6 NIRANJAN  22
10    10  DRUPATH  22
5      5    ASEEM  23
   SL.NO      NAME AGE     (sorted descending)
14    14      JOHN  31
3      3   ANANDHU  30
4      4     ARJUN  30
11    11 AISHWARYA  30
1      1      ABEL  29
   SL.NO NAME AGE          (filter and search)
14    14 JOHN  31
2
7. CSV of 10 students - mean and median
d <- data.frame(
  Name  = c("Amit", "Bhavna", "Chetan", "Divya", "Esha",
            "Farhan", "Gita", "Hari", "Isha", "Jay"),
  Marks = c(85, 92, 78, 88, 95, 67, 84, 90, 73, 89))
write.csv(d, "students_marks.csv", row.names = FALSE)
d <- read.csv("students_marks.csv")
print(d)
cat("Mean Marks:", mean(d$Marks), "\n")
cat("Median Marks:", median(d$Marks))
Output:
     Name Marks
1    Amit    85
2  Bhavna    92
3  Chetan    78
4   Divya    88
5    Esha    95
6  Farhan    67
7    Gita    84
8    Hari    90
9    Isha    73
10    Jay    89
Mean Marks: 84.1
Median Marks: 86.5
8. Pie chart of product sales
d <- data.frame(
  Product = c("Laptops", "Smartphones", "Tablets",
              "Headphones", "Smartwatches", "Monitors"),
  Units   = c(120, 250, 90, 180, 150, 60))
write.csv(d, "product_sales.csv", row.names = FALSE)
d   <- read.csv("product_sales.csv")
pct <- round(100 * d$Units / sum(d$Units), 1)
pie(d$Units,
    labels = paste0(d$Product, " - ", pct, "%"),
    col    = rainbow(6),
    main   = "Product Sales Distribution (Units Sold)")
Output: a pie chart with 6 slices labelled
Laptops - 14.1%        Headphones - 21.2%
Smartphones - 29.4%    Smartwatches - 17.6%
Tablets - 10.6%        Monitors - 7.1%
9. K-Means clustering (2 clusters)
d <- data.frame(X = c(1, 2, 3, 4, 5, 8, 9, 10, 11, 12),
                Y = c(2, 3, 2, 4, 3, 9, 8, 10, 9, 11))
set.seed(123)
k <- kmeans(d, centers = 2)
print(k$cluster)
print(k$centers)
print(k$tot.withinss)
plot(d, col = k$cluster, pch = 19, main = "K-Means Clustering (K=2)")
points(k$centers, col = 1:2, pch = 8, cex = 2)
Output (cluster numbers 1 and 2 may come out swapped):
 [1] 1 1 1 1 1 2 2 2 2 2
   X   Y
1  3 2.8
2 10 9.4
[1] 28
Plot: 5 points bottom-left in one colour, 5 points top-right in another, with a star at each centre.
3
4
10. Histogram
d <- c(19, 23, 11, 5, 16, 21, 32, 14, 19, 27, 39)
print(d)
hist(d, main = "Histogram of Given Data",
     xlab = "Data Values", ylab = "Frequency",
     col = "skyblue", border = "black")
Output:
 [1] 19 23 11  5 16 21 32 14 19 27 39
Plot: sky-blue bars of width 5 from 5 to 40, with heights
5-10  10-15  15-20  20-25  25-30  30-35  35-40
 1      2      3      2      1      1      1
11. Bar chart of monthly sales
d <- data.frame(months = c("Jan", "Feb", "Mar", "Apr", "May"),
                Profit = c(72, 80, 87, 90, 89))
write.csv(d, "monthlysales.csv", row.names = FALSE)
d <- read.csv("monthlysales.csv")
barplot(d$Profit, names.arg = d$months,
        col = "pink", border = "red", ylim = c(0, 100),
        main = "Monthly Sales Profit",
        xlab = "Months", ylab = "Profit (in thousands)")
Output: a bar chart with 5 pink bars
Jan  Feb  Mar  Apr  May
 72   80   87   90   89
12. Linear regression (Hours vs Marks)
d <- data.frame(Hours = 1:10,
                Marks = seq(35, 80, by = 5))
m <- lm(Marks ~ Hours, data = d)
summary(m)
print(coef(m))
plot(d, pch = 19, main = "Linear Regression")
abline(m)
Output (the data is an exact straight line, so R also warns "essentially perfect fit"):
Coefficients:
            Estimate
(Intercept)       30
Hours              5
Multiple R-squared: 1
(Intercept)       Hours
         30           5
So Marks = 30 + 5 x Hours. Plot: 10 points lying exactly on the fitted line.
13. SparkR - faithful dataset
library(SparkR)
sparkR.session(appName = "SparkR Faithful Example")
df <- createDataFrame(faithful)
head(df)
sparkR.session.stop()
Output:
  eruptions waiting
1     3.600      79
2     1.800      54
3     3.333      74
4     2.283      62
5
5     4.533      85
6     2.283      55
14. Sales prediction with linear regression
d <- data.frame(Month = 1:5,
                Sales = c(120, 150, 170, 210, 250))
m <- lm(Sales ~ Month, data = d)
print(summary(m))
new  <- data.frame(Month = 6:8)
pred <- predict(m, new)
print(data.frame(Month = 6:8, Predicted_Sales = pred))
plot(d, col = "blue", pch = 16, xlim = c(1, 9), ylim = c(100, 350),
     main = "Sales Prediction using Linear Regression")
abline(m, col = "red", lwd = 2)
points(new$Month, pred, col = "darkgreen", pch = 17)
Output:
Coefficients:
            Estimate Std. Error t value Pr(>|t|)
(Intercept)   84.000      7.659   10.97 0.001623 **
Month         32.000      2.309   13.86 0.000814 ***
Residual standard error: 7.303 on 3 degrees of freedom
Multiple R-squared: 0.9846, Adjusted R-squared: 0.9795
F-statistic: 192 on 1 and 3 DF, p-value: 0.0008136
  Month Predicted_Sales
1     6             276
2     7             308
3     8             340
Plot: 5 blue points, a red regression line, and 3 green triangles for months 6-8.
15. PCA on mtcars (first four columns)
p <- prcomp(mtcars[1:4], scale = TRUE)
summary(p)
Output:
Importance of components:
                          PC1     PC2     PC3     PC4
Standard deviation     1.8714 0.48934 0.40652 0.30517
Proportion of Variance 0.8755 0.05986 0.04132 0.02328
Cumulative Proportion  0.8755 0.93540 0.97672 1.00000
