---
layout: post
title: data.table
author: CY
description: "data.table usage"
tags: [R]
categories: [R]
share: false
image:
  background: triangular.png
---

`data.table` provides a high-performance version of base R's `data.frame` with syntax and feature enhancements for ease of use, convenience and programming speed.     

Data analysis using data.table:      
Data manipulation operations such as `subset`, `group`, `update`, `join` etc., are all inherently related. Keeping these related operations together allows for:            

- *concise* and *consistent* syntax irrespective of the set of operations you would like to perform to achieve your end goal.         

- performing analysis *fluidly* without the cognitive burden of having to map each operation to a particular function from a potentially huge set of functions available before performing the analysis.          

- *automatically* optimizing operations internally, and very effectively, by knowing precisely the data required for each operation, leading to very fast and memory efficient code.         


General form of data table:     
```
DT[i, j, by]
Take *DT*, subset/reorder rows using *i*, then calculate *j* grouped by *by*
```
Load the package

```r
#install.packages("data.table") 
library(data.table)
```

## Creat a data table

```r
DT <- data.table(A=c(1L,2L), B=LETTERS[7:9], C=round(rnorm(4),4), D=1:12)

# `fread`: Similar to read.table but faster and more convenient. All controls such as sep, colClasses and nrows are automatically detected.           
# `fread` accepts `http` and `https` URLs directly as well as operating system commands such as `sed` and `awk` output.         
# The value is a data.table by default, otherwise a data.frame when argument data.table=FALSE.
```

## transform between data table and data frame      
`setDF`: Coerce a data.table to data.frame            
`setDT`: Coerce lists and data.frames to data.table     
`as.data.table`: Coerce other structures to data.table         

## Subseting Rows Using i    

```r
DT[3:5];DT[3:5,]    #Select 3rd to 5th row; the ',' is optional
```

```r
DT[B=="G"]    #Select all rows that have value A in column B
```

```r
DT[B %in% c("G","H")] #Select all rows that have value G or H in column B
```

```r
DT[order(-A, D)];DT[order(-A, D), ] #Sort DT first by column A in descending order, and then by D in ascending order; the ',' is optional     
```

```r
DT[!2:4];DT[-(2:4)] #All rows other than 2:4   
```

## Manipulating on Columns in j     

```r
DT[,B] #Return B column as a vector
```

```
##  [1] "G" "H" "I" "G" "H" "I" "G" "H" "I" "G" "H" "I"
```

```r
DT[,.(B,C)];DT[,list(B,C)] #Return B and C columns as data.table; .() is an alias for list()
```

```r
select_cols = c("B","C")
DT[ , ..select_cols] #The same as above. ..prefix should be reminiscent of the “up-one-level” function in linux - the .. signals to DT to look for the select_cols variable “up-one-level”, i.e., in the global environment in this case.   
```

```r
DT[,!c("B","C")];DT[,-c("B","C")] #deselect B and C columns   
```

```r
DT[, A:C] #Select columns from A to C
```

```r
DT[,.(D, D*2)] # return two column data.table
```

```r
DT[,sum(A)]  #Return the sum of all elements of A column in a vector
```

```
## [1] 18
```

```r
DT[,.(sum(A),sd(C))] #Return the sum of all elements of A and the std. dev. of C in a data.table
```

```
##    V1        V2
## 1: 18 0.7448356
```

```r
DT[,.(Aggregate=sum(A),Sd.V3=sd(C))] #The same as the above, with new names
```

```
##    Aggregate     Sd.V3
## 1:        18 0.7448356
```

## Grouping operations - j and by 
`.N` is a special built-in variable that holds the number of observations in the current group. It is particularly useful when combined with `by`. In the absence of group by operations, it simply returns the number of rows in the subset.      

```r
DT[,.N,by=A] #Count number of rows for every group in A
```

```
##    A N
## 1: 1 6
## 2: 2 6
```

```r
DT[,.(C.Mean=mean(C)),by=.(A,B)] #Calculate sum of D for every group in A and B
```

```
##    A B  C.Mean
## 1: 1 G 0.15770
## 2: 2 H 0.61015
## 3: 1 I 0.15770
## 4: 2 G 0.61015
## 5: 1 H 0.15770
## 6: 2 I 0.61015
```

```r
DT[,.(D.Sum=sum(D)),by=sign(A-1)] #Calculate sum of D for every group in sign(A-1)
```

```
##    sign D.Sum
## 1:    0    36
## 2:    1    42
```

```r
DT[,.(D.Sum=sum(D)),by=.(A.01=sign(A-1))] #The same as the above, with new name for the variable you’re grouping by
```

```
##    A.01 D.Sum
## 1:    0    36
## 2:    1    42
```

```r
DT[B=="G",.(D.Sum=sum(D)),by=A] #Calculate sum of D for every group in A afer subseting on the rows equal to G in column B
```

```
##    A D.Sum
## 1: 1     8
## 2: 2    14
```

## Adding/Updating Columns By Reference in j Using `:=`    
The results will saved in DT, but not print on the screen 

```r
DT[,A:=round(exp(A),2)] #A is updated by what is afer :=
DT[,c("A","B"):=list(round(exp(A),2),LETTERS[4:6])] #Columns A and B are updated by what is afer :=
DT[,':='(A=round(exp(A),2),B=LETTERS[4:6])][] #Alternative to the above one. With [], you print the result to the screen
```

```r
DT[,c("A","B"):=NULL] #Remove columns A and B
```

## Indexing And Keys

```r
DT <- data.table(A=c(1L,2L), B=LETTERS[7:9], C=round(rnorm(4),4), D=1:12)

setkey(DT,B) #A key is set on B; output is returned invisibly    
#mult: control which rows are returned, "all" (default), "first" or "last".
DT[c("G","H")] #Return all rows where the key column (set to B) has value G or H
```

```r
DT["G",mult="first"] #Return first row of all rows that match value G in key column B
```

```
##    A B       C D
## 1: 1 G -0.5105 1
```

```r
DT[c("G","J")] #Return all rows where key column B has value G or J
```

```
##     A B       C  D
## 1:  1 G -0.5105  1
## 2:  2 G -0.7310  4
## 3:  1 G -1.6259  7
## 4:  2 G -0.5036 10
## 5: NA J      NA NA
```

```r
DT[c("G","J"),nomatch=0] #Return all rows where key column B has value G or J, not matched will not be returned
```

```
##    A B       C  D
## 1: 1 G -0.5105  1
## 2: 2 G -0.7310  4
## 3: 1 G -1.6259  7
## 4: 2 G -0.5036 10
```

```r
DT[c("G","I"),sum(D)] #Return total sum of D, for rows of key column B that have values G or I
```

```
## [1] 52
```

```r
DT[c("G","I"),sum(D),by=.EACHI] #Return sum of column D for rows of B that have value G, and anohter sum for rows of  B that have value I
```

```
##    B V1
## 1: G 22
## 2: I 30
```

```r
setkey(DT,A,B) #Sort by A and then by B within each group of A (invisible)
DT[.(2,c("G","I"))] #Select rows that have value 2 for the frst key (A) and within those rows the value G or I for the second key (B)
```

```
##    A B       C  D
## 1: 2 G -0.7310  4
## 2: 2 G -0.5036 10
## 3: 2 I -0.5036  6
## 4: 2 I -0.7310 12
```

## Advanced Data Table Operations

```r
DT[.N-1] #Return the penultimate row of the DT
```

```
##    A B       C D
## 1: 2 I -0.5036 6
```

```r
DT[,.N]  #Return the number of rows
```

```
## [1] 12
```

```r
DT[,mean(C),by=.(A,B)] #Return the result grouped by all possible combinations of groups specifed in by
```

```
##    A B      V1
## 1: 1 G -1.0682
## 2: 1 H -1.0682
## 3: 1 I -1.0682
## 4: 2 G -0.6173
## 5: 2 H -0.6173
## 6: 2 I -0.6173
```

## .SD & .SDcols     
`.SD` stands for Subset of Data. It by itself is a data.table that holds the data for the current group defined using `by`.      
`.SD` contains all the columns except the grouping columns by default.It is also generated by preserving the original order.       
`.SDcols` specify just the columns we would like to apply the function on     

```r
DT[,print(.SD),by=B] #Look at what .SD contains
```

```
##    A       C  D
## 1: 1 -0.5105  1
## 2: 1 -1.6259  7
## 3: 2 -0.7310  4
## 4: 2 -0.5036 10
##    A       C  D
## 1: 1 -0.5105  5
## 2: 1 -1.6259 11
## 3: 2 -0.5036  2
## 4: 2 -0.7310  8
##    A       C  D
## 1: 1 -1.6259  3
## 2: 1 -0.5105  9
## 3: 2 -0.5036  6
## 4: 2 -0.7310 12
```

```
## Empty data.table (0 rows) of 1 col: B
```

```r
DT[,.SD[c(1,.N)],by=B] #Select the first and last row grouped by B
```

```
##    B A       C  D
## 1: G 1 -0.5105  1
## 2: G 2 -0.5036 10
## 3: H 1 -0.5105  5
## 4: H 2 -0.7310  8
## 5: I 1 -1.6259  3
## 6: I 2 -0.7310 12
```

```r
DT[,lapply(.SD,sum),by=B,.SDcols=c("C","D")] #Calculate sum of C and D in .SD grouped by B
```

```
##    B      C  D
## 1: G -3.371 22
## 2: H -3.371 26
## 3: I -3.371 30
```

## Chaining   
Queries can be chained together just by adding another one on the end: `DT[...][...]`     

```r
DT[,.(D.Sum=sum(D)),by=A][D.Sum>40] #Calculate sum of D, grouped by A, then select that group of which the sum is >40(chaining)
```

```
##    A D.Sum
## 1: 2    42
```

```r
DT[,.(D.Sum=sum(D)),by=.(A,B)][order(-A, B)] #Calculate sum of D, grouped by A and B, ordered on A and B    
```

```
##    A B D.Sum
## 1: 2 G    14
## 2: 2 H    10
## 3: 2 I    18
## 4: 1 G     8
## 5: 1 H    16
## 6: 1 I    12
```

```r
DT[,.(D.Sum=sum(D)),keyby=A] #keyby automatically orders the result by the grouping variables in increasing order.      
```

```
##    A D.Sum
## 1: 1    36
## 2: 2    42
```

## set()-Family
### set()  
Syntax: `for (i in from:to) set(DT, row, column, new value)`      

```r
#Sequence along the values of rows, and for the values of cols, set the values of those elements equal to NA (invisible)
rows <- list(3:4,5:6)
cols <- 1:2
for(i in seq_along(rows))
  {set(DT,  #multiple expressions included by braces 
    i=rows[[i]], 
    j=cols[i],
    value=NA)}
```

### setcolorder() - re-order variables
Syntax: `setcolorder(DT,"neworder")`          

```r
#Change column ordering to contents of the specifed vector (invisible)
setcolorder(DT,  
            c("B","C","A","D"))   
DT[1]
```

```
##    B       C A D
## 1: G -0.5105 1 1
```

### setnames() - rename variables      
Syntax: `setnames(DT,"old","new")[]`                           

```r
setnames(DT,"B","Rating") #Set column name of B to Rating (invisible)
DT[1]
```

```
##    Rating       C A D
## 1:      G -0.5105 1 1
```

```r
#Change 2 column names (invisible)
setnames(DT, 
         c("C","D"),
         c("C.speed","D.rank"))
DT[1]
```

```
##    Rating C.speed A D.rank
## 1:      G -0.5105 1      1
```
