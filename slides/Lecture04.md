--- 
title       : Microbial Informatics
subtitle    : Lecture 04
date        : September 12, 2014
author      : Patrick D. Schloss, PhD (microbialinformatics.github.io)
job         : Department of Microbiology & Immunology
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : standalone    # {selfcontained, standalone, draft}
knit        : slidify::knit2slides
--- 

## Announcements
* No class on Thursday (9/18) or Friday (9/19).

--- 

## Review
> * Comments
 * Use your varible names as comments
 * Comment your code with # (console) or ## (knitr)
> * Variables hold information
 * **Numeric/double/integer:** counts of things, measurements
 * **Characters/strings:** DNA sequence, amino acids, names
 * **Logical:** is something true or not
 * **Functions:** more complex...

---

## Learning objectives
* Review different data types
* Learn how to create and manipulate vectors

---

## Numerical varaibles


```r
x <- pi
y <- 2
z <- -3
```

---

## String variables


```r
office <- "1520A MSRB I"
grade <- "A"
genome <- "ATGCATCGTCCCGT"
```

* **Note:** the the grade value is in quotes. What happens if it is not in quotes?

---

##	Logical values as inputs (T/F; 1/0)


```r
x <- TRUE
y <- FALSE

!x              # NOT operator
x && y          # AND operator
x & y           # bitwise AND operator (vectors)
x || y          # OR operator
x | y			# bitwise OR operator (vectors)
x == y          # is equal operator
x != y          # is not equal operator
```

* Logical variables will be very useful when selecting subsets of data to work with

---

## Logical values as outptus on numbers


```r
x <- 5
y <- 3

x > y          # greater than operator
x >= y         # greater than or equal to operator
x < y          # less than operator
x <= y         # less than  or equal tooperator
x == y         # is equal to operator
x != y         # is not equal to operator
```

---

## Logical values as outptus on strings


```r
x <- "ATG"
y <- "CCC"

x > y          # greater than operator
x >= y         # greater than or equal to operator
x < y          # less than operator
x <= y         # less than  or equal tooperator
x == y         # is equal to operator
x != y         # is not equal to operator
```

---

##	Converting


```r
as.numeric(x)
as.logical(x)
as.character(x)
```

* There are other conversions that can be done. How would you figure out which converters are out there?
* Be sure to understand the "side effects" of the conversions

---

## Types of containers
* Vectors
* List
* Matrix
* Table
* Data table
* Factors
*	We will go through these more in detail throughout the course and especially in second half of the course

---

##	Vectors

* One-dimensional sets of values of the same type
* Everything in R is some form of a vector
* You can read in vectors from a file or create them on the fly.  Four common ways of creating a vector include using `c()`, `:`, `rep()`, `seq()`.  Here are several examples:


```r
19:55                   # list the values from 19 to 55 by ones
c(1,2,3,4)              # concatenate 1, 2, 3, 4, 5 into a vector
rep("red", 5)           # repeat "red" five times
seq(1,10,by=3)          # list the values from 1 to 10 by 3's
seq(1,10,length.out=20) # list 20 evenly spaced elements from 1 to 10
seq(1,10,len=20)        # same thing; arguments of any function can be 
c(rep("red", 5), rep("white", 5), rep("blue", 5))
rep(c(0,1), 10)
countToTen <- 1:10
```


---

## Operations act on vectors


```r
countToTen <- 1:10
length(countToTen)
countToTen
countToTen^2
countToTen > 5
typeof(countToTen)
is.vector(countToTen)  
```

---

## Indexing into vectors
* Note that in contrast to many programming languages, vectors in R are indexed such that the first value is 1 NOT 0.

	

```r
code <- c("A", "T", "G", "C")

code[2]				# get the second element
code[0]				# errr...
code[-1]			# remove the first element
code[c(1,2)]		# get the first and second elements
code[code > "M"]	# get any element greater than "M"
```

* What does this do?


```r
code[length(code)]
```

---

## Defining a vector


```r
z <- numeric(5)			#	This creates a numerical vector with 5 zeros
z[3] <- 10
z
z[1:3] <- 5
z
z[10] <- pi				#	NA's are inserted between 5 and 9
z[4] <- "R rocks!"		#	everything changes to a character

t <- character(5)
t[4] <- "DNA rocks!"
```

---

## Indexing by characters

* You can also create vectors that are indexed by character strings
* In some programming languages these are called hash-maps or look-up tables.


```r
v <- numeric(0)
v["A"] <- 1.23498
v["T"] <- 2.2342
v["C"] <- 3
v["G"] <- 4
v["A"]
v[["A"]]      # strips the name associated with value 1

v2 <- c(A=1.23498,T=2.2342,C=3,G=4)
```

---

## Naming cells in your vectors


```r
names(v)
names(v) <- c("A", "B", "C", "D")
names(v) <- NULL  # this removes names attribute
```

---

## matrices
* multidimensional data structure of the same data type
* we'll see a lot of overlap with tables and data.frames

---

## Create and access a matrix...


```r
m <- matrix(seq(1:96), nrow=8, ncol=12)	#create a 8 x 12 matrix
colnames(m)<-1:12
rownames(m)<-c("A", "B", "C", "D", "E", "F", "G", "H")

dim(m)
nrow(m)
ncol(m)
m[1:5,1:5]
m[1:5,]
m[,1:5]
```

---

## Numerous operations that can be performed on a matrix	


```r
t(m)             # transpose the matrix
1/m              # take each value of m and find it's reciprocal
m * m            # calculate the square of each value in m
m %*% t(m)       # performs matrix multiplication
crossprod(m,m)   # performs the cross product
rowSums(m)       # calculate the sum for each row
colSums(m)       # calculate the sum for each column
lower.tri(m)     # find the indices that are below the diagonal
m[lower.tri(m)]  # give the lower triangle of m
diag(m)          # the values on the diagonal of m
det(m[1:8,1:8])  # the determinent of m
```

---

## Apply functions to matrices


```r
apply(m, 1, sum)	# get the sum for each row - same as rowSums(m)
apply(m, 2, sum)	# get the sum for each column - same as colSums(m)
```

---

## Data frames
* multidimensional data structure that allows for multiple data types across columns
* think of gene statistics in a genome annotation

gene | start | end   | strand  | length | annotation
-----|-------|-------|---------|--------|-------------
rbcA | num   | num   | logic   | num    | character 
rbcB |       |       |         |        | 
rbcC |       |       |         |        | 
rbcD |       |       |         |        | 
etc. |       |       |         |        | 

* important point is that the data is linked across the rows

---

## Let's get some data
* Want to work with metadata from a study looking at the gut microbiota of wild populations of *Peromyscus leucopis* and *P. maniculatis*
* [Download data](https://raw.githubusercontent.com/SchlossLab/wild_mice/master/wild.metadata.txt)
* Take a look at the data
* Save folder to your Desktop
* Set your working directory to the Desktop

---

## Working with data frames

> * Be sure to set correct working directory in RStudio
>```{r, eval=FALSE}
metadata <- read.table(file="wild.metadata.txt", header=T)
head(metadata)		# look at the first lines of table
dim(metadata)
nrow(metadata)
ncol(metadata)
colnames(metadata)
rownames(metadata)  # notice a problem here?
summary(metadata)	# output a summary of each column in table
```
> * Check out the Data section of the Environment tab of RStudio
> * What problems can you see with this output?

---

## Accessing values from data frames


```r
metadata$Age			# output column named "Age"
metadata[,"Age"]		# output column named "Age"
metadata[,7]			# output 4th column ("end")
metadata[,-7]			# output everything but the 4th column ("end")

metadata["23", ]		# output row with Group 6_16m33
metadata[23, ]			# output 23rd row (aka Group 6_16m33)
metadata[-23,]			# output everything but the 23rd row
```

---

## Let's use these functions to clean up the data

* We'd like to use the "Group"" column as the rowname
 * Group names must be unique
 * Case sensitive - "group" will not work


```r
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
head(metadata)
```

--- &twocol

## More complicated stuff

> * What do these commands do?  
>```{r, eval=FALSE}
metadata$Weight[1:5]
metadata[1:5,"Weight"]
metadata["5_31m2",]
```		

> * What's the difference between these commands?  
> ```{r, eval=FALSE}
metadata[-23,]
metadata <- metadata[-23,]
```

> * Can make new columns  
> ```{r, eval=FALSE}
metadata[,"sequences"] <- rep(NA, nrow(metadata))
```

---

## Incorporating logic

* Define criteria to set rows you want to keep
* Let's get all of the *P. leucopis* samples


```r
metadata[metadata$SP=="PL",]
```

* Let's get all of the *P. leucopis* samples from males


```r
metadata[metadata$SP=="PL" & metadata$Sex=="M",]
```

---

## Factors
* Defining categorical variables
* In a genome we might think of the forward/reverse orientation, reading frame, dna/protein sequence designation, or annotation category as categorical variables.  	
* Create factors


```r
factor(metadata$ET)
metadata$ET <-factor(metadata$ET)
summary(metadata)
levels(metadata$polymer)
```

* What other variables here would be a factor?

---

##	Lists
* Similar to data fames, but not necessarily read across rows and not all variables have the same length
* Could hold a genome's data within a list:
 * name: Character with organism name
 * genome.size: Number with number of bases
 * start.pos: Vector of start positions for each gene
 * end.pos: Vector of end positions for each gene
 * gene.name: Name of each gene
 * hydrolases: Names of genes that are hydrolases
* Allow one to create complex data structures
* We'll use these only in passing

---

## An example of where we'll use lists...
* Let's get the mean weight for each sex of mouse

```r
aggregate(metadata$Weight, by=metadata$Sex, mean)
aggregate(metadata$Weight, by=list(metadata$Sex), mean)
sex.weight <- aggregate(metadata$Weight, by=list(metadata$Sex), mean)
sex.weight$x
```

* Let's get the mean weight for each sex and species of mouse

```r
aggregate(metadata$Weight, by=list(metadata$Sex, metadata$SP), mean)
```

---

## For Tuesday
* Start working on new assignment that will be posted this weekend
* Read ***Introduction to Statistics with R*** (Chapters 1 and 2)


--- .segue .dark

## Questions?

