Лабораторна робота № 1. Завантаження та зчитування даних
================

1. За допомогою download.file() завантажте любий excel файл з порталу http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.

```r
file1 <- download.file('https://data.gov.ua/dataset/6a1df2e2-039c-4769-a32a-adcd6fbb814e/resource/fd874a80-a34b-48a3-bb9e-5924bb9faa99/download/struktura.csv', destfile="lab1_1.csv")
data1 <- read.csv("lab1_1.csv")
head(data1)
```
```                                                 X....з.п...Назва.структурного.підрозділу.
1                                                     "1";"Департамент організації роботи Служби"
2 "2";"Департамент охорони державної таємниці, технічного та криптографічного захисту інформації"
3                        "3";"Департамент матеріального забезпечення та розвитку інфраструктури "
4                                      "4";"Департамент кадрової політики та роботи з персоналом"
5                             "5";"Департамент фінансування, бухгалтерського обліку та звітності"
6                                                          "6";"Департамент внутрішнього аудиту "
```

2. За допомогою download.file() завантажте файл getdata_data_ss06hid.csv за посиланням https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0 Необхідно знайти, скільки property мають value $1000000+

``` r
file2 <- download.file('https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv', destfile="lab1_2.csv")
data2 <- read.csv("lab1_2.csv")
head(data2[1:5])
```
```
  RT SERIALNO DIVISION PUMA REGION
1  H      186        8  700      4
2  H      306        8  700      4
3  H      395        8  100      4
4  H      506        8  700      4
5  H      835        8  800      4
6  H      989        8  700      4
```
``` r
sum(data2$VAL == 24, na.rm = TRUE)
```
```
[1] 53
```

3. Зчитайте xml файл за посиланням http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml Скільки ресторанів мають zipcode 21231?

``` r
library(XML)
file3 <- download.file("http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml", destfile="lab1_3.xml", mode="wb")
data3 <- xmlRoot(xmlTreeParse("lab1_3.xml", useInternalNodes = TRUE))
sum(xpathSApply(data3, "//zipcode", xmlValue) == 21231)
```
```
[1] 127
```
