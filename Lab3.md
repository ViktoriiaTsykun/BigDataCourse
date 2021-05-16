Лабораторна робота № 3. Зчитування даних з WEB.
================

В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі
100 фільмами 2017 року виходу за посиланням
«http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_ty
pe=feature». Необхідно створити data.frame «movies» з наступними даними:
номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data).
Для виконання лабораторної рекомендується використати бібліотеку «rvest».
CSS селектори для зчитування необхідних даних: rank_data: «.text-primary»,
title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для
зчитування url використовується функція read_html, для зчитування даних по CSS
селектору – html_nodes і для перетворення зчитаних html даних в текст -
html_text. Рекомендується перетворити rank_data та runtime_data з тексту в числові значення. При формуванні дата фрейму функцією data.frame рекомендується використати параметр «stringsAsFactors = FALSE».
```r
library(rvest)
file <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")
rank_data <- html_text(html_nodes(file,'.text-primary'))
num_rank_data <- as.numeric(rank_data)
title_data <- html_text(html_nodes(file,'.lister-item-header a'))
runtime_data <- html_text(html_nodes(file,'.text-muted .runtime'))
num_runtime_data = as.numeric(gsub(" min", "", runtime_data))
movies <- data.frame(Rank = num_rank_data, Title = title_data, Runtime = num_runtime_data, stringsAsFactors = FALSE)
```

1. Виведіть перші 6 назв фільмів дата фрейму.
```r
head(movies$Title)
```
```
[1] "Тор: Раґнарок"                "Ліга справедливості"          "Той, хто біжить по лезу 2049"
[4] "Тюльпанова лихоманка"         "Вартові Галактики 2"          "Дюнкерк"        
```

2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
```r
movies[movies$Runtime > 120, 'Title']
```
```
 [1] "Тор: Раґнарок"                            "Той, хто біжить по лезу 2049"            
 [3] "Вартові Галактики 2"                      "Людина-павук: Повернення додому"         
 [5] "Диво-жінка"                               "Воно"                                    
 [7] "Зоряні війни: Епізод 8 - Останні Джедаї"  "Назви мене своїм ім'ям"                  
 [9] "Форма води"                               "Чужий: Заповіт"                          
[11] "Логан: Росомаха"                          "Kingsman: Золоте кільце"                 
[13] "Король Артур: Легенда меча"               "Красуня і Чудовисько"                    
[15] "Дружина доглядача зоопарку"               "Пірати Карибського моря: Помста Салазара"
[17] "Форсаж 8"                                 "Метелик"                                 
[19] "Темні часи"                               "Джон Вік 2"                              
[21] "Трансформери: Останній лицар"             "Валеріан і місто тисячі планет"          
[23] "Мати!"                                    "Гра Моллі"                               
[25] "Вбивство священного оленя"                "Примарна нитка"                          
[27] "Постріл в безодню"                        "Saban's Могутні рейнджери"               
[29] "Сім сестер"                               "Війна за планету мавп"                   
[31] "Вороги"                                   "1+1: Нова історія"                       
[33] "Усі гроші світу"  
```

3. Скільки фільмів мають тривалість менше 100 хв.
```r
nrow(movies[movies$Runtime < 100, ])
```
```
[1] 12
```
