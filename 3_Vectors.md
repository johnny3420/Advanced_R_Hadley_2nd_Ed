---
title: "3_Vectors"
output: 
  html_document: 
    keep_md: yes
date: "2022-09-12"
---



# 3. Vectors
## 3.1 Introduction
## 3.2 Atomic Vectors
### 3.2.1 Scalars
### 3.2.2 Making longer vectors with c()


```r
lgl_var <- c(TRUE, FALSE)
int_var <- c(1L, 6L, 10L)
dbl_var <- c(1, 2.5, 4.5)
chr_var <- c("these are", "some strings")
```


```r
c(c(1, 2), c(3, 4))
```

```
## [1] 1 2 3 4
```


```r
typeof(lgl_var)
```

```
## [1] "logical"
```

```r
#> [1] "logical"
typeof(int_var)
```

```
## [1] "integer"
```

```r
#> [1] "integer"
typeof(dbl_var)
```

```
## [1] "double"
```

```r
#> [1] "double"
typeof(chr_var)
```

```
## [1] "character"
```

```r
#> [1] "character"
```

### 3.2.3 Missing Values

```r
NA > 5
```

```
## [1] NA
```

```r
#> [1] NA
10 * NA
```

```
## [1] NA
```

```r
#> [1] NA
!NA
```

```
## [1] NA
```

```r
#> [1] NA
```

```r
NA ^ 0
```

```
## [1] 1
```

```r
#> [1] 1
NA | TRUE
```

```
## [1] TRUE
```

```r
#> [1] TRUE
NA & FALSE
```

```
## [1] FALSE
```

```r
#> [1] FALSE
```


```r
x <- c(NA, 5, NA, 10)
x == NA
```

```
## [1] NA NA NA NA
```

```r
#> [1] NA NA NA NA
```


```r
is.na(x)
```

```
## [1]  TRUE FALSE  TRUE FALSE
```

```r
#> [1]  TRUE FALSE  TRUE FALSE
```

### 3.2.4 Testing and coercion

```r
str(c("a", 1))
```

```
##  chr [1:2] "a" "1"
```

```r
#>  chr [1:2] "a" "1"
```


```r
x <- c(FALSE, FALSE, TRUE)
as.numeric(x)
```

```
## [1] 0 0 1
```

```r
#> [1] 0 0 1

# Total number of TRUEs
sum(x)
```

```
## [1] 1
```

```r
#> [1] 1

# Proportion that are TRUE
mean(x)
```

```
## [1] 0.3333333
```

```r
#> [1] 0.333
```


```r
as.integer(c("1", "1.5", "a"))
```

```
## Warning: NAs introduced by coercion
```

```
## [1]  1  1 NA
```

```r
#> Warning: NAs introduced by coercion
#> [1]  1  1 NA
```

### 3.2.5 Exercises

### 1. How do you create raw and complex scalars? (See ?raw and ?complex.)


```r
#?raw
raw(length = 0)
```

```
## raw(0)
```

```r
#?complex
complex(length.out = 0, real = numeric(), imaginary = numeric(), modulus = 1, argument = 0)
```

```
## [1] 1+0i
```

#### 2. Test your knowledge of the vector coercion rules by predicting the output of the following uses of c():


```r
c(1, FALSE)
```

```
## [1] 1 0
```

```r
# Numeric/Double
c("a", 1)
```

```
## [1] "a" "1"
```

```r
# Character
c(TRUE, 1L)
```

```
## [1] 1 1
```

```r
# Integer
```
#### 3. Why is 1 == "1" true? Why is -1 < FALSE true? Why is "one" < 2 false?


```r
1 == "1"
```

```
## [1] TRUE
```

```r
# "1" is equal to 1
-1 < FALSE
```

```
## [1] TRUE
```

```r
# FALSE is 0
"one" < 2
```

```
## [1] FALSE
```

```r
# "one is greater"
```
#### 4. Why is the default missing value, NA, a logical vector? What’s special about logical vectors? (Hint: think about c(FALSE, NA_character_).)

It's a binary vector either yes or no. so applicable or not

#### 5. Precisely what do is.atomic(), is.numeric(), and is.vector() test for?

Check the type of the vector

## 3.3 Attributes
### 3.3.1 Getting and setting


```r
a <- 1:3
attr(a, "x") <- "abcdef"
attr(a, "x")
```

```
## [1] "abcdef"
```

```r
#> [1] "abcdef"

attr(a, "y") <- 4:6
str(attributes(a))
```

```
## List of 2
##  $ x: chr "abcdef"
##  $ y: int [1:3] 4 5 6
```

```r
#> List of 2
#>  $ x: chr "abcdef"
#>  $ y: int [1:3] 4 5 6

# Or equivalently
a <- structure(
  1:3, 
  x = "abcdef",
  y = 4:6
)
str(attributes(a))
```

```
## List of 2
##  $ x: chr "abcdef"
##  $ y: int [1:3] 4 5 6
```

```r
#> List of 2
#>  $ x: chr "abcdef"
#>  $ y: int [1:3] 4 5 6
```


```r
attributes(a[1])
```

```
## NULL
```

```r
#> NULL
attributes(sum(a))
```

```
## NULL
```

```r
#> NULL
```

### 3.3.2 Names


```r
# When creating it: 
x <- c(a = 1, b = 2, c = 3)

# By assigning a character vector to names()
x <- 1:3
names(x) <- c("a", "b", "c")

# Inline, with setNames():
x <- setNames(1:3, c("a", "b", "c"))
```

### 3.3.3 Dimensions

```r
# Two scalar arguments specify row and column sizes
x <- matrix(1:6, nrow = 2, ncol = 3)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

```r
#>      [,1] [,2] [,3]
#> [1,]    1    3    5
#> [2,]    2    4    6

# One vector argument to describe all dimensions
y <- array(1:12, c(2, 3, 2))
y
```

```
## , , 1
## 
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
## 
## , , 2
## 
##      [,1] [,2] [,3]
## [1,]    7    9   11
## [2,]    8   10   12
```

```r
#> , , 1
#> 
#>      [,1] [,2] [,3]
#> [1,]    1    3    5
#> [2,]    2    4    6
#> 
#> , , 2
#> 
#>      [,1] [,2] [,3]
#> [1,]    7    9   11
#> [2,]    8   10   12

# You can also modify an object in place by setting dim()
z <- 1:6
dim(z) <- c(3, 2)
z
```

```
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
```

```r
#>      [,1] [,2]
#> [1,]    1    4
#> [2,]    2    5
#> [3,]    3    6
```


```r
str(1:3)                   # 1d vector
```

```
##  int [1:3] 1 2 3
```

```r
#>  int [1:3] 1 2 3
str(matrix(1:3, ncol = 1)) # column vector
```

```
##  int [1:3, 1] 1 2 3
```

```r
#>  int [1:3, 1] 1 2 3
str(matrix(1:3, nrow = 1)) # row vector
```

```
##  int [1, 1:3] 1 2 3
```

```r
#>  int [1, 1:3] 1 2 3
str(array(1:3, 3))         # "array" vector
```

```
##  int [1:3(1d)] 1 2 3
```

```r
#>  int [1:3(1d)] 1 2 3
```

### 3.3.4 Exercises
#### 1. How is setNames() implemented? How is unname() implemented? Read the source code.

Creates a new object as assigns names. removes the name attribute

#### 2. What does dim() return when applied to a 1-dimensional vector? When might you use NROW() or NCOL()?


```r
a <- 1:4
dim(a)
```

```
## NULL
```

```r
# NULL. may use when combining or scaling data
```

#### 3. How would you describe the following three objects? What makes them different from 1:5?


```r
x1 <- array(1:5, c(1, 1, 5))
x1
```

```
## , , 1
## 
##      [,1]
## [1,]    1
## 
## , , 2
## 
##      [,1]
## [1,]    2
## 
## , , 3
## 
##      [,1]
## [1,]    3
## 
## , , 4
## 
##      [,1]
## [1,]    4
## 
## , , 5
## 
##      [,1]
## [1,]    5
```

```r
x2 <- array(1:5, c(1, 5, 1))
x2
```

```
## , , 1
## 
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    2    3    4    5
```

```r
x3 <- array(1:5, c(5, 1, 1))
x3
```

```
## , , 1
## 
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
## [4,]    4
## [5,]    5
```

5 1x1 matrices counting up, 1 1x5 matrix counting up, and 1 5x1 matrix counting up

#### 4. An early draft used this code to illustrate structure():


```r
structure(1:5, comment = "my attribute")
```

```
## [1] 1 2 3 4 5
```

```r
#> [1] 1 2 3 4 5
```
Doesn't print by default

## 3.4 S3 atomic vectors
### 3.4.1 Factors


```r
x <- factor(c("a", "b", "b", "a"))
x
```

```
## [1] a b b a
## Levels: a b
```

```r
#> [1] a b b a
#> Levels: a b

typeof(x)
```

```
## [1] "integer"
```

```r
#> [1] "integer"
attributes(x)
```

```
## $levels
## [1] "a" "b"
## 
## $class
## [1] "factor"
```

```r
#> $levels
#> [1] "a" "b"
#> 
#> $class
#> [1] "factor"
```


```r
sex_char <- c("m", "m", "m")
sex_factor <- factor(sex_char, levels = c("m", "f"))

table(sex_char)
```

```
## sex_char
## m 
## 3
```

```r
#> sex_char
#> m 
#> 3
table(sex_factor)
```

```
## sex_factor
## m f 
## 3 0
```

```r
#> sex_factor
#> m f 
#> 3 0
```


```r
grade <- ordered(c("b", "b", "a", "c"), levels = c("c", "b", "a"))
grade
```

```
## [1] b b a c
## Levels: c < b < a
```

```r
#> [1] b b a c
#> Levels: c < b < a
```

### 3.4.2 Dates


```r
today <- Sys.Date()

typeof(today)
```

```
## [1] "double"
```

```r
#> [1] "double"
attributes(today)
```

```
## $class
## [1] "Date"
```

```r
#> $class
#> [1] "Date"
```


```r
date <- as.Date("1970-02-01")
unclass(date)
```

```
## [1] 31
```

```r
#> [1] 31
```

### 3.4.3 Date-times


```r
now_ct <- as.POSIXct("2018-08-01 22:00", tz = "UTC")
now_ct
```

```
## [1] "2018-08-01 22:00:00 UTC"
```

```r
#> [1] "2018-08-01 22:00:00 UTC"

typeof(now_ct)
```

```
## [1] "double"
```

```r
#> [1] "double"
attributes(now_ct)
```

```
## $class
## [1] "POSIXct" "POSIXt" 
## 
## $tzone
## [1] "UTC"
```

```r
#> $class
#> [1] "POSIXct" "POSIXt" 
#> 
#> $tzone
#> [1] "UTC"
```


```r
structure(now_ct, tzone = "Asia/Tokyo")
```

```
## [1] "2018-08-02 07:00:00 JST"
```

```r
#> [1] "2018-08-02 07:00:00 JST"
structure(now_ct, tzone = "America/New_York")
```

```
## [1] "2018-08-01 18:00:00 EDT"
```

```r
#> [1] "2018-08-01 18:00:00 EDT"
structure(now_ct, tzone = "Australia/Lord_Howe")
```

```
## [1] "2018-08-02 08:30:00 +1030"
```

```r
#> [1] "2018-08-02 08:30:00 +1030"
structure(now_ct, tzone = "Europe/Paris")
```

```
## [1] "2018-08-02 CEST"
```

```r
#> [1] "2018-08-02 CEST"
```

### 3.4.4 Durations

```r
one_week_1 <- as.difftime(1, units = "weeks")
one_week_1
```

```
## Time difference of 1 weeks
```

```r
#> Time difference of 1 weeks

typeof(one_week_1)
```

```
## [1] "double"
```

```r
#> [1] "double"
attributes(one_week_1)
```

```
## $class
## [1] "difftime"
## 
## $units
## [1] "weeks"
```

```r
#> $class
#> [1] "difftime"
#> 
#> $units
#> [1] "weeks"

one_week_2 <- as.difftime(7, units = "days")
one_week_2
```

```
## Time difference of 7 days
```

```r
#> Time difference of 7 days

typeof(one_week_2)
```

```
## [1] "double"
```

```r
#> [1] "double"
attributes(one_week_2)
```

```
## $class
## [1] "difftime"
## 
## $units
## [1] "days"
```

```r
#> $class
#> [1] "difftime"
#> 
#> $units
#> [1] "days"
```

### 3.4.5 Exercises

#### 1. What sort of object does table() return? What is its type? What attributes does it have? How does the dimensionality change as you tabulate more variables?


```r
sex_char <- c("m", "f", "m")
sex_factor <- factor(sex_char, levels = c("m", "f"))

typeof(table(sex_factor)) 
```

```
## [1] "integer"
```

Factors are integers under the hood


```r
structure(table(sex_factor))
```

```
## sex_factor
## m f 
## 2 1
```

```r
attributes(table(sex_factor))
```

```
## $dim
## [1] 2
## 
## $dimnames
## $dimnames$sex_factor
## [1] "m" "f"
## 
## 
## $class
## [1] "table"
```

#### 2. What happens to a factor when you modify its levels?


```r
f1 <- factor(letters)
structure(f1)
```

```
##  [1] a b c d e f g h i j k l m n o p q r s t u v w x y z
## Levels: a b c d e f g h i j k l m n o p q r s t u v w x y z
```

```r
levels(f1) <- rev(levels(f1))
structure(f1)
```

```
##  [1] z y x w v u t s r q p o n m l k j i h g f e d c b a
## Levels: z y x w v u t s r q p o n m l k j i h g f e d c b a
```
Vector also changed order

#### 3. What does this code do? How do f2 and f3 differ from f1?


```r
f2 <- rev(factor(letters))
f2
```

```
##  [1] z y x w v u t s r q p o n m l k j i h g f e d c b a
## Levels: a b c d e f g h i j k l m n o p q r s t u v w x y z
```

```r
f3 <- factor(letters, levels = rev(letters))
f3
```

```
##  [1] a b c d e f g h i j k l m n o p q r s t u v w x y z
## Levels: z y x w v u t s r q p o n m l k j i h g f e d c b a
```
Levels and order aren't the same as in f1

## 3.5 Lists
### 3.5.1 Creating


