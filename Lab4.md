Лабораторна робота № 4. Зчитування даних з реляційних баз даних.
================

```r
library(DBI)
library(RSQLite)
```

1. Назва статті (Title), тип виступу (EventType). Необхідно вибрати тільки статті с типом виступу Spotlight. Сортування по назві статті.
```r
conn <- dbConnect(RSQLite::SQLite(), 'db.sqlite')
res1 <- dbSendQuery(conn, "SELECT Title, EventType FROM Papers WHERE EventType='Spotlight' ORDER BY Title")
data1 <- dbFetch(res1, n=10)
dbClearResult(res1)
data1
```
```
                                                                                          Title EventType
1  A Tractable Approximation to Optimal Point Process Filtering: Application to Neural Encoding Spotlight
2                                    Accelerated Mirror Descent in Continuous and Discrete Time Spotlight
3                        Action-Conditional Video Prediction using Deep Networks in Atari Games Spotlight
4                                                                      Adaptive Online Learning Spotlight
5                          Asynchronous Parallel Stochastic Gradient for Nonconvex Optimization Spotlight
6                                                 Attention-Based Models for Speech Recognition Spotlight
7                                                       Automatic Variational Inference in Stan Spotlight
8                                   Backpropagation for Energy-Efficient Neuromorphic Computing Spotlight
9                       Bandit Smooth Convex Optimization: Improving the Bias-Variance Tradeoff Spotlight
10                         Biologically Inspired Dynamic Textures for Probing Motion Perception Spotlight
```

2. Ім’я автора (Name), Назва статті (Title). Необхідно вивести всі назви статей для автора «Josh Tenenbaum». Сортування по назві статті.
```r
res2 <- dbSendQuery(conn, "SELECT Authors.Name, Papers.Title FROM Papers JOIN PaperAuthors ON Papers.Id=PaperAuthors.PaperId JOIN Authors ON Authors.Id=PaperAuthors.AuthorId WHERE Authors.Name='Josh Tenenbaum' ORDER BY Papers.Title")
data2 <- dbFetch(res2, n=10)
dbClearResult(res2)
data2
```
```
            Name
1 Josh Tenenbaum
2 Josh Tenenbaum
3 Josh Tenenbaum
4 Josh Tenenbaum
                                                                                              Title
1                                                       Deep Convolutional Inverse Graphics Network
2 Galileo: Perceiving Physical Object Properties by Integrating a Physics Engine with Deep Learning
3                                                Softstar: Heuristic-Guided Probabilistic Inference
4                                                        Unsupervised Learning by Program Synthesis
```

3. Вибрати всі назви статей (Title), в яких є слово «statistical». Сортування по назві статті.
```r
res3 <- dbSendQuery(conn, "SELECT Title FROM Papers WHERE Title LIKE '%statistical%' ORDER BY Title")
data3 <- dbFetch(res3, n=10)
dbClearResult(res3)
data3
```
```
                                                                                 Title
1 Adaptive Primal-Dual Splitting Methods for Statistical Learning and Image Processing
2                                Evaluating the statistical significance of biclusters
3                  Fast Randomized Kernel Ridge Regression with Statistical Guarantees
4     High Dimensional EM Algorithm: Statistical Optimization and Asymptotic Normality
5                Non-convex Statistical Optimization for Sparse Tensor Graphical Model
6            Regularized EM Algorithms: A Unified Framework and Statistical Guarantees
7                            Statistical Model Criticism using Kernel Two Sample Tests
8                         Statistical Topological Data Analysis - A Kernel Perspective
```

4. Ім’я автору (Name), кількість статей по кожному автору (NumPapers). Сортування по кількості статей від більшої кількості до меньшої.
```r
res4 <- dbSendQuery(conn, "SELECT Authors.Name, COUNT(Authors.Id) as NumPapers FROM Authors JOIN PaperAuthors ON Authors.Id=PaperAuthors.AuthorId JOIN Papers ON Papers.Id=PaperAuthors.PaperId GROUP BY Authors.Id ORDER BY COUNT(Authors.Id) DESC")
data4 <- dbFetch(res4, n=20)
dbClearResult(res4)
data4
```
```
                      Name NumPapers
1     Pradeep K. Ravikumar         7
2                  Han Liu         6
3           Lawrence Carin         6
4      Inderjit S. Dhillon         5
5                  Le Song         5
6        Zoubin Ghahramani         5
7           Christopher Re         4
8     Simon Lacoste-Julien         4
9             Zhaoran Wang         4
10        Csaba Szepesvari         4
11       Michael I. Jordan         4
12          Josh Tenenbaum         4
13            Prateek Jain         4
14           Ryan P. Adams         4
15          Percy S. Liang         4
16             Honglak Lee         4
17             Shie Mannor         4
18           Yoshua Bengio         4
19 Dimitris Papailiopoulos         3
20            Zoltan Szabo         3
```
