Завдання 2.(1 бал)
================

Зчитайте xml файл за посиланням http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml

Скільки ресторанів мають zipcode 21231?

```r
library(XML)
file3 <- download.file("http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml", destfile="lab1_3.xml", mode="wb")
data3 <- xmlRoot(xmlTreeParse("lab1_3.xml", useInternalNodes = TRUE))
sum(xpathSApply(data3, "//zipcode", xmlValue) == 21231)
```
```
[1] 127
```