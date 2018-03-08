---
layout: post
title: Extract webpage -- Example one
author: CY
tags: [R]
categories: [R]
share: false
image:
  background: triangular.png 
---


### Extract table from webpage  

```r
# Load the package required to read website
library(XML)

# wegpage address 
url <- "http://www.hmdb.ca/bmi_metabolomics"

# method one: for people who is luckiest (not me, so sad)
df1 <- readHTMLTable(url, header=T, stringsAsFactors = F)
  # Error: failed to load external entity "url"

# method two: use RCurl package, for people who is much luckier (only work on my laptop, not the computer in the office, crying)
library(RCurl)
xmldoc <- getURL(url)
df2 <- readHTMLTable(xmldoc, stringsAsFactors = F)

# method three: use httr package, for people who is not lucky
library(httr)
tabs <- GET(url)
df3 <- readHTMLTable(rawToChar(tabs$content), as.data.frame = T, stringsAsFactors = F)

# The readHTMLTable returns list, we need to extract our data frame. In this example, the first element is our data frame, so we can extract it like this:
df3[[1]]  # extract the first element of list
df3[["NULL"]]  # extract list element based on element names
```

```
##                                                V1 V2       V3    V4
## 1                  Butyrylcarnitine (HMDB0002013)    Increase Blood
## 2         Alpha-ketoisovaleric acid (HMDB0000019)    Increase Blood
## 3    2-Hydroxy-3-methylbutyric acid (HMDB0000407)    Increase Blood
## 4        3-Methyl-2-oxovaleric acid (HMDB0000491)    Increase Blood
## 5                       Ketoleucine (HMDB0000695)    Increase Blood
## 6      (S)-3-Hydroxyisobutyric acid (HMDB0000023)    Increase Blood
## 7                  LysoPC(18:1(9Z)) (HMDB0002815)    Decrease Blood
## 8  2-Linoleoylglycerophosphocholine (HMDB0061700)    Decrease Blood
## 9                      Benzoic acid (HMDB0001870)    Decrease Blood
## 10                        Benzamide (HMDB0004461)    Decrease Blood
## 11                     Benzaldehyde (HMDB0006115)    Decrease Blood
## 12                    Acetylglycine (HMDB0000532)    Decrease Blood
## 13          Palmitoyl sphingomyelin (HMDB0061712)    Decrease Blood
## 14                      L-Histidine (HMDB0000177)    Decrease Blood
## 15                  D-Glutamic acid (HMDB0003339)    Increase Blood
## 16                         L-Valine (HMDB0000883)    Increase Blood
## 17                        D-Mannose (HMDB0000169)    Increase Blood
## 18                     L-Isoleucine (HMDB0000172)    Increase Blood
## 19              Isovalerylcarnitine (HMDB0000688)    Increase Blood
## 20                       L-Tyrosine (HMDB0000158)    Increase Blood
## 21                        L-Leucine (HMDB0000687)    Increase Blood
## 22                      Lathosterol (HMDB0001170)    Increase Blood
## 23                     L-Kynurenine (HMDB0000684)    Increase Blood
## 24                         Glycerol (HMDB0000131)    Increase Blood
## 25                  L-Phenylalanine (HMDB0000159)    Increase Blood
##          V5       V6      V7
## 1  9.95e-10 25254000 details
## 2  2.87e-08 25254000 details
## 3  1.19e-05 25254000 details
## 4  1.68e-05 25254000 details
## 5  6.05e-05 25254000 details
## 6  6.88e-05 25254000 details
## 7   0.00015 25254000 details
## 8  1.36e-05 25254000 details
## 9  3.41e-05 25254000 details
## 10 3.41e-05 25254000 details
## 11 3.41e-05 25254000 details
## 12 1.58e-06 25254000 details
## 13 1.98e-06 25254000 details
## 14 7.61e-11 25254000 details
## 15 2.51e-13 25254000 details
## 16 4.17e-13 25254000 details
## 17 1.43e-06 25254000 details
## 18 8.15e-11 25254000 details
## 19 2.58e-08 25254000 details
## 20 1.97e-11 25254000 details
## 21 2.64e-06 25254000 details
## 22 9.85e-09 25254000 details
## 23 9.42e-08 25254000 details
## 24 8.34e-06 25254000 details
## 25  1.3e-06 25254000 details
```

### Read data from `.xml` file    

```r
# Load the package required to read XML files
library(XML)

# Give the input website or file name to the function
url <- "http://www.w3schools.com/xml/cd_catalog.xml"
# xmldoc <- xmlParse(url) # for webpage 
xmldoc <- xmlParse("cd_catalog.xml") # for downloaded file

# Print the result (be careful when data is too large)
# xmldoc

# Exract the root node from the xml file
rootnode <- xmlRoot(xmldoc)

# Find number of nodes in the root.
rootsize <- xmlSize(rootnode)

# Print the result.
rootsize
```

```
## [1] 26
```

```r
rootnode[1] # details of the first node
```

```
## $CD
## <CD>
##   <TITLE>Empire Burlesque</TITLE>
##   <ARTIST>Bob Dylan</ARTIST>
##   <COUNTRY>USA</COUNTRY>
##   <COMPANY>Columbia</COMPANY>
##   <PRICE>10.90</PRICE>
##   <YEAR>1985</YEAR>
## </CD> 
## 
## attr(,"class")
## [1] "XMLInternalNodeList" "XMLNodeList"
```

```r
rootnode[[1]][[1]] # Get the first element of the first node.
```

```
## <TITLE>Empire Burlesque</TITLE>
```

```r
# convert the inout xml file to a data frame
xmldataframe <- xmlToDataFrame("cd_catalog.xml")
head(xmldataframe)
```

```
##                 TITLE          ARTIST COUNTRY        COMPANY PRICE YEAR
## 1    Empire Burlesque       Bob Dylan     USA       Columbia 10.90 1985
## 2     Hide your heart    Bonnie Tyler      UK    CBS Records  9.90 1988
## 3       Greatest Hits    Dolly Parton     USA            RCA  9.90 1982
## 4 Still got the blues      Gary Moore      UK Virgin records 10.20 1990
## 5                Eros Eros Ramazzotti      EU            BMG  9.90 1997
## 6      One night only        Bee Gees      UK        Polydor 10.90 1998
```



### Extract table from many webpages 

Use loops to extract data for each page     

```r
library(XML)
library(RCurl)

df <- data.frame() # an empty data frame 
for (i in 1:12) {
  url <- paste0("http://www.hmdb.ca/bmi_metabolomics?page=", i)
  xmldoc <- getURL(url)
  xmldoc <- readHTMLTable(xmldoc, stringsAsFactors = F)
  xmldataframe <-  xmldoc[["NULL"]]
  df <- rbind(df, xmldataframe)
  return(df)
}
```



### References 

[R Error using readHTMLTable](https://stackoverflow.com/questions/17045107/r-error-using-readhtmltable)     
