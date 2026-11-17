
**1. Leap year**
y <- as.integer(readline("Enter year to be checked: "))
leap <- (y %% 4 == 0 && y %% 100 != 0) || y %% 400 == 0
cat(y, ifelse(leap, "is a leap year.", "is not a leap year."))
   
**2. Sum of natural numbers (if-else + while)**
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

**3. Student grade**
m <- sum(c(57, 98, 59, 89, 78, 90, 57, 96, 45, 75))
g <- if (m >= 800) "A+" else
     if (m >= 700) "A"  else
     if (m >= 500) "B+" else
     if (m >= 400) "B"  else
     if (m >= 150) "C"  else "D"
cat(m, "is the total marks scored\n")
cat(g, "is the grade secured by the student")


**4. Calculator (switch + function)**
calc <- function(x, y, ch) switch(ch, x + y, x - y, x * y, x / y)
ch <- as.integer(readline("Enter choice [1/2/3/4]: "))
a  <- as.integer(readline("Enter first number: "))
b  <- as.integer(readline("Enter second number: "))
op <- switch(ch, "+", "-", "*", "/")
cat(a, op, b, "=", calc(a, b, ch))


**5. Matrix with rbind() and row names**
x <- rbind(c("C#", "Java", "COBOL", ".Net"),
           c("JavaScript", "Node.js", "R", "Azure"),
           c("Power BI", "ASP.Net", "Unity", "Block Chain"))
rownames(x) <- c("Lang1", "Lang2", "Lang3")
print(x)
cat("The third element in the second row is", x["Lang2", 3])


**6. Excel to CSV and data viewer functions**
library(readxl)
library(writexl)
d <- data.frame(
  AGE = c(25, 35, 42, 28, 51),
  NAME = c("John", "Mary", "John Smith", "David", "Anna"),
  order = 1:5
)
write_xlsx(d, "dataset.xlsx")
write.csv(
  read_excel("dataset.xlsx"),
  "dataset.csv",
  row.names = FALSE
)
d <- read.csv("dataset.csv")

print(dim(d))                        # Dimensions
print(head(d, 5))                     # First 5 rows
print(tail(d, 5))                     # Last 5 rows
d[order(d$AGE), ][1:5, ]       # Sort by age, ascending
d[order(-d$AGE), ][1:5, ]      # Sort by age, descending
subset(d, AGE > 30)            # Filter rows where age is over 30
d[grep("John", d$NAME, ignore.case = TRUE), ]  # Search names
rm(d)                          # Remove object


**7. CSV of 10 students - mean and median**
d <- data.frame(
  Name  = c("Amit", "Bhavna", "Chetan", "Divya", "Esha",
            "Farhan", "Gita", "Hari", "Isha", "Jay"),
  Marks = c(85, 92, 78, 88, 95, 67, 84, 90, 73, 89))
write.csv(d, "students_marks.csv", row.names = FALSE)
d <- read.csv("students_marks.csv")
print(d)
cat("Mean Marks:", mean(d$Marks), "\n")
cat("Median Marks:", median(d$Marks))


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


**9. K-Means clustering (2 clusters)**
data(iris)
set.seed(123) # For reproducible results
iris_data <- iris[, 1:2]
kmeans_result <- kmeans(iris_data, centers = 2, nstart = 20)
print(kmeans_result)
plot(iris_data, col = kmeans_result$cluster, main = "K-Means Clustering (2 Clusters)")
points(kmeans_result$centers, col = 1:2, pch = 8, cex = 2)


**10. Histogram**
d <- c(19, 23, 11, 5, 16, 21, 32, 14, 19, 27, 39)
print(d)
hist(d, main = "Histogram of Given Data",
     xlab = "Data Values", ylab = "Frequency",
     col = "skyblue", border = "black")


**11.** bar chart of monthly sales
d <- data.frame(months = c("Jan", "Feb", "Mar", "Apr", "May"),
                Profit = c(72, 80, 87, 90, 89))
write.csv(d, "monthlysales.csv", row.names = FALSE)
d <- read.csv("monthlysales.csv")
barplot(d$Profit, names.arg = d$months,
        col = "pink", border = "red", ylim = c(0, 100),
        main = "Monthly Sales Profit",
        xlab = "Months", ylab = "Profit (in thousands)")

    
**12.**linear regression 
data(cars)
model <- lm(dist ~ speed, data = cars)
summary(model)



**13.**
SparkR - faithful dataset
library(SparkR)
sparkR.session(appName = "SparkR Faithful Example")
df <- createDataFrame(faithful)
head(df)
sparkR.session.stop()


**14****.Sales prediction with linear regression**
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
  

**15.PCA on mtcars (first four columns)**
p <- prcomp(mtcars[1:4], scale = TRUE)
summary(p)
