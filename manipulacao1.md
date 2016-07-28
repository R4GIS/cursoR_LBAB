# Curso R - Manipulação de dados 1
Ítalo Cegatta  
3 de junho de 2016  



# Manipulação de data frame


```r
#install.packages("pacman")
library(pacman)
p_load(readxl, dplyr, tidyr, nycflights13)

#?flights

flights
```

```
## Source: local data frame [336,776 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

# Filter

Com a função `filter()` é possível selecionar linhas específicas, de acordo com o fator que deseja. Podem ser usados um ou vários fatores de seleção.


```r
filter(flights, month == 1, day == 1)
```

```
## Source: local data frame [842 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

```r
filter(flights, month == 11 | month == 12)
```

```
## Source: local data frame [55,403 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013    11     1        5           2359         6      352
## 2   2013    11     1       35           2250       105      123
## 3   2013    11     1      455            500        -5      641
## 4   2013    11     1      539            545        -6      856
## 5   2013    11     1      542            545        -3      831
## 6   2013    11     1      549            600       -11      912
## 7   2013    11     1      550            600       -10      705
## 8   2013    11     1      554            600        -6      659
## 9   2013    11     1      554            600        -6      826
## 10  2013    11     1      554            600        -6      749
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

```r
filter(flights, month %in% c(11, 12))
```

```
## Source: local data frame [55,403 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013    11     1        5           2359         6      352
## 2   2013    11     1       35           2250       105      123
## 3   2013    11     1      455            500        -5      641
## 4   2013    11     1      539            545        -6      856
## 5   2013    11     1      542            545        -3      831
## 6   2013    11     1      549            600       -11      912
## 7   2013    11     1      550            600       -10      705
## 8   2013    11     1      554            600        -6      659
## 9   2013    11     1      554            600        -6      826
## 10  2013    11     1      554            600        -6      749
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

# Arrange

Para ordenar as colunas, podemos usar a função `arrange()`. A hierarquia é dada pela sequência dos fatores que são adicionados como argumentos da função.


```r
arrange(flights, year, month, day)
```

```
## Source: local data frame [336,776 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

```r
arrange(flights, desc(arr_delay))
```

```
## Source: local data frame [336,776 x 19]
## 
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    (int) (int) (int)    (int)          (int)     (dbl)    (int)
## 1   2013     1     9      641            900      1301     1242
## 2   2013     6    15     1432           1935      1137     1607
## 3   2013     1    10     1121           1635      1126     1239
## 4   2013     9    20     1139           1845      1014     1457
## 5   2013     7    22      845           1600      1005     1044
## 6   2013     4    10     1100           1900       960     1342
## 7   2013     3    17     2321            810       911      135
## 8   2013     7    22     2257            759       898      121
## 9   2013    12     5      756           1700       896     1058
## 10  2013     5     3     1133           2055       878     1250
## ..   ...   ...   ...      ...            ...       ...      ...
## Variables not shown: sched_arr_time (int), arr_delay (dbl), carrier (chr),
##   flight (int), tailnum (chr), origin (chr), dest (chr), air_time (dbl),
##   distance (dbl), hour (dbl), minute (dbl), time_hour (time)
```

# Select

A função `select()` auxilia-nos na seleção de variáveis (colunas). A sintaxe é muito ao usado com o operador ´[´.


```r
select(flights, year, month, day)
```

```
## Source: local data frame [336,776 x 3]
## 
##     year month   day
##    (int) (int) (int)
## 1   2013     1     1
## 2   2013     1     1
## 3   2013     1     1
## 4   2013     1     1
## 5   2013     1     1
## 6   2013     1     1
## 7   2013     1     1
## 8   2013     1     1
## 9   2013     1     1
## 10  2013     1     1
## ..   ...   ...   ...
```

```r
select(flights, year:day)
```

```
## Source: local data frame [336,776 x 3]
## 
##     year month   day
##    (int) (int) (int)
## 1   2013     1     1
## 2   2013     1     1
## 3   2013     1     1
## 4   2013     1     1
## 5   2013     1     1
## 6   2013     1     1
## 7   2013     1     1
## 8   2013     1     1
## 9   2013     1     1
## 10  2013     1     1
## ..   ...   ...   ...
```

```r
select(flights, -(year:day))
```

```
## Source: local data frame [336,776 x 16]
## 
##    dep_time sched_dep_time dep_delay arr_time sched_arr_time arr_delay
##       (int)          (int)     (dbl)    (int)          (int)     (dbl)
## 1       517            515         2      830            819        11
## 2       533            529         4      850            830        20
## 3       542            540         2      923            850        33
## 4       544            545        -1     1004           1022       -18
## 5       554            600        -6      812            837       -25
## 6       554            558        -4      740            728        12
## 7       555            600        -5      913            854        19
## 8       557            600        -3      709            723       -14
## 9       557            600        -3      838            846        -8
## 10      558            600        -2      753            745         8
## ..      ...            ...       ...      ...            ...       ...
## Variables not shown: carrier (chr), flight (int), tailnum (chr), origin
##   (chr), dest (chr), air_time (dbl), distance (dbl), hour (dbl), minute
##   (dbl), time_hour (time)
```

# Mutate

Para criar novas variáveis, podemos usar a função `mutate()`. Um diferencial dessa função é que podemos utilizar variáveis criadas dentro do próprio comando. Se quisermos mostrar apenas as novas variáveis, podemos usar a função `transmute`.


```r
flights_sml <- select(flights, 
  year:day, 
  ends_with("delay"), 
  distance, 
  air_time)

mutate(flights_sml,
  speed = distance / air_time * 60,
  hours = air_time / 60)
```

```
## Source: local data frame [336,776 x 9]
## 
##     year month   day dep_delay arr_delay distance air_time    speed
##    (int) (int) (int)     (dbl)     (dbl)    (dbl)    (dbl)    (dbl)
## 1   2013     1     1         2        11     1400      227 370.0441
## 2   2013     1     1         4        20     1416      227 374.2731
## 3   2013     1     1         2        33     1089      160 408.3750
## 4   2013     1     1        -1       -18     1576      183 516.7213
## 5   2013     1     1        -6       -25      762      116 394.1379
## 6   2013     1     1        -4        12      719      150 287.6000
## 7   2013     1     1        -5        19     1065      158 404.4304
## 8   2013     1     1        -3       -14      229       53 259.2453
## 9   2013     1     1        -3        -8      944      140 404.5714
## 10  2013     1     1        -2         8      733      138 318.6957
## ..   ...   ...   ...       ...       ...      ...      ...      ...
## Variables not shown: hours (dbl)
```

```r
mutate(flights_sml,
  gain = arr_delay - dep_delay,
  hours = air_time / 60,
  gain_per_hour = gain / hours
)
```

```
## Source: local data frame [336,776 x 10]
## 
##     year month   day dep_delay arr_delay distance air_time  gain     hours
##    (int) (int) (int)     (dbl)     (dbl)    (dbl)    (dbl) (dbl)     (dbl)
## 1   2013     1     1         2        11     1400      227     9 3.7833333
## 2   2013     1     1         4        20     1416      227    16 3.7833333
## 3   2013     1     1         2        33     1089      160    31 2.6666667
## 4   2013     1     1        -1       -18     1576      183   -17 3.0500000
## 5   2013     1     1        -6       -25      762      116   -19 1.9333333
## 6   2013     1     1        -4        12      719      150    16 2.5000000
## 7   2013     1     1        -5        19     1065      158    24 2.6333333
## 8   2013     1     1        -3       -14      229       53   -11 0.8833333
## 9   2013     1     1        -3        -8      944      140    -5 2.3333333
## 10  2013     1     1        -2         8      733      138    10 2.3000000
## ..   ...   ...   ...       ...       ...      ...      ...   ...       ...
## Variables not shown: gain_per_hour (dbl)
```

```r
transmute(flights,
  gain = arr_delay - dep_delay,
  hours = air_time / 60,
  gain_per_hour = gain / hours
)
```

```
## Source: local data frame [336,776 x 3]
## 
##     gain     hours gain_per_hour
##    (dbl)     (dbl)         (dbl)
## 1      9 3.7833333      2.378855
## 2     16 3.7833333      4.229075
## 3     31 2.6666667     11.625000
## 4    -17 3.0500000     -5.573770
## 5    -19 1.9333333     -9.827586
## 6     16 2.5000000      6.400000
## 7     24 2.6333333      9.113924
## 8    -11 0.8833333    -12.452830
## 9     -5 2.3333333     -2.142857
## 10    10 2.3000000      4.347826
## ..   ...       ...           ...
```

# Summarise 

A função `summarise` nos permite resumir dados. Também é possível resumir dados em função de vários fatores com o `group_by`.


```r
summarise(flights, delay = mean(dep_delay, na.rm = TRUE))
```

```
## Source: local data frame [1 x 1]
## 
##      delay
##      (dbl)
## 1 12.63907
```

```r
by_day <- group_by(flights, year, month, day)
summarise(by_day, delay = mean(dep_delay, na.rm = TRUE))
```

```
## Source: local data frame [365 x 4]
## Groups: year, month [?]
## 
##     year month   day     delay
##    (int) (int) (int)     (dbl)
## 1   2013     1     1 11.548926
## 2   2013     1     2 13.858824
## 3   2013     1     3 10.987832
## 4   2013     1     4  8.951595
## 5   2013     1     5  5.732218
## 6   2013     1     6  7.148014
## 7   2013     1     7  5.417204
## 8   2013     1     8  2.553073
## 9   2013     1     9  2.276477
## 10  2013     1    10  2.844995
## ..   ...   ...   ...       ...
```

```r
by_dest <- group_by(flights, dest)
delay <- summarise(by_dest,
  count = n(),
  dist = mean(distance, na.rm = TRUE),
  delay = mean(arr_delay, na.rm = TRUE))
delay <- filter(delay, count > 20, dest != "HNL")
delay
```

```
## Source: local data frame [96 x 4]
## 
##     dest count      dist     delay
##    (chr) (int)     (dbl)     (dbl)
## 1    ABQ   254 1826.0000  4.381890
## 2    ACK   265  199.0000  4.852273
## 3    ALB   439  143.0000 14.397129
## 4    ATL 17215  757.1082 11.300113
## 5    AUS  2439 1514.2530  6.019909
## 6    AVL   275  583.5818  8.003831
## 7    BDL   443  116.0000  7.048544
## 8    BGR   375  378.0000  8.027933
## 9    BHM   297  865.9966 16.877323
## 10   BNA  6333  758.2135 11.812459
## ..   ...   ...       ...       ...
```

# Operador %>% 
O pacote `dplyr` foi desenhado para trabalhar em conjunto que o operador em cadeia `%>%`. O que esse operador faz é aplicar o que está no LHS no primeiro parâmetro da função do RHS. Podemos também direcionar o local onde o conteúdo do LHS será aplicado informando um ´.´ como argumento.


```r
flights %>% 
  group_by(dest) %>% 
  summarise(count = n(),
    dist = mean(distance, na.rm = TRUE),
    delay = mean(arr_delay, na.rm = TRUE)) %>% 
  filter(count > 20, dest != "HNL")
```

```
## Source: local data frame [96 x 4]
## 
##     dest count      dist     delay
##    (chr) (int)     (dbl)     (dbl)
## 1    ABQ   254 1826.0000  4.381890
## 2    ACK   265  199.0000  4.852273
## 3    ALB   439  143.0000 14.397129
## 4    ATL 17215  757.1082 11.300113
## 5    AUS  2439 1514.2530  6.019909
## 6    AVL   275  583.5818  8.003831
## 7    BDL   443  116.0000  7.048544
## 8    BGR   375  378.0000  8.027933
## 9    BHM   297  865.9966 16.877323
## 10   BNA  6333  758.2135 11.812459
## ..   ...   ...       ...       ...
```

```r
flights %>% 
  group_by(year, month, day) %>% 
  summarise(mean = mean(dep_delay))
```

```
## Source: local data frame [365 x 4]
## Groups: year, month [?]
## 
##     year month   day  mean
##    (int) (int) (int) (dbl)
## 1   2013     1     1    NA
## 2   2013     1     2    NA
## 3   2013     1     3    NA
## 4   2013     1     4    NA
## 5   2013     1     5    NA
## 6   2013     1     6    NA
## 7   2013     1     7    NA
## 8   2013     1     8    NA
## 9   2013     1     9    NA
## 10  2013     1    10    NA
## ..   ...   ...   ...   ...
```

```r
flights %>% 
  group_by(year, month, day) %>% 
  summarise(mean = mean(dep_delay, na.rm = TRUE))
```

```
## Source: local data frame [365 x 4]
## Groups: year, month [?]
## 
##     year month   day      mean
##    (int) (int) (int)     (dbl)
## 1   2013     1     1 11.548926
## 2   2013     1     2 13.858824
## 3   2013     1     3 10.987832
## 4   2013     1     4  8.951595
## 5   2013     1     5  5.732218
## 6   2013     1     6  7.148014
## 7   2013     1     7  5.417204
## 8   2013     1     8  2.553073
## 9   2013     1     9  2.276477
## 10  2013     1    10  2.844995
## ..   ...   ...   ...       ...
```

# Tidy data

O conceito tidy data está muito bem descrito no [artigo de Hadley Wickham](https://www.jstatsoft.org/article/view/v059i10), onde ela apresenta o pacote [tidyr](https://cran.r-project.org/web/packages/tidyr/index.html) que contém uma gama de funções muito úteis para esse fim. Wickham também dedicou um capítulo específico sobre esse conceito em seu novo [livro](http://r4ds.had.co.nz/). Por tidy data, entendemos que:
  
* Variáveis estão dispostas em colunas.
* Observações estão dispostas em linhas.
* Os valores atribuídos às variáveis em cada observação formam a tabela.

Agora vamos aplicar esse conceito neste [banco de dados]().


```r
#getwd()

dados <- read_excel("base_vespa.xlsx")
dados
```

```
## Source: local data frame [140 x 17]
## 
##    Tratamento Individuo 1-Peciolo 1-Nervura 1-Caule 2-Peciolo 2-Nervura
##         (chr)     (dbl)     (dbl)     (dbl)   (dbl)     (dbl)     (dbl)
## 1   Actara d1         1         1        NA      NA         1         1
## 2   Actara d1         2        NA        NA      NA        NA        NA
## 3   Actara d1         3        NA        NA      NA        NA        NA
## 4   Actara d1         4        NA        NA      NA        NA        NA
## 5   Actara d1         5        NA        NA      NA        NA        NA
## 6   Actara d1         6        NA        NA      NA        NA        NA
## 7   Actara d1         7        NA        NA      NA         2        NA
## 8   Actara d1         8        NA        NA      NA        NA        NA
## 9   Actara d1         9        NA        NA      NA        NA        NA
## 10  Actara d1        10        NA        NA      NA        NA        NA
## ..        ...       ...       ...       ...     ...       ...       ...
## Variables not shown: 2-Caule (dbl), 3-Peciolo (dbl), 3-Nervura (dbl),
##   3-Caule (dbl), 4-Peciolo (dbl), 4-Nervura (dbl), 4-Caule (dbl),
##   5-Peciolo (dbl), 5-Nervura (dbl), 5-Caule (dbl)
```

```r
#dim(dados2)[2]
dados <- gather(dados, "Local", "Galhas", 3:17)
dados
```

```
## Source: local data frame [2,100 x 4]
## 
##    Tratamento Individuo     Local Galhas
##         (chr)     (dbl)     (chr)  (dbl)
## 1   Actara d1         1 1-Peciolo      1
## 2   Actara d1         2 1-Peciolo     NA
## 3   Actara d1         3 1-Peciolo     NA
## 4   Actara d1         4 1-Peciolo     NA
## 5   Actara d1         5 1-Peciolo     NA
## 6   Actara d1         6 1-Peciolo     NA
## 7   Actara d1         7 1-Peciolo     NA
## 8   Actara d1         8 1-Peciolo     NA
## 9   Actara d1         9 1-Peciolo     NA
## 10  Actara d1        10 1-Peciolo     NA
## ..        ...       ...       ...    ...
```

```r
dados <- separate(dados, Local, c("Coleta", "Local"))
dados
```

```
## Source: local data frame [2,100 x 5]
## 
##    Tratamento Individuo Coleta   Local Galhas
##         (chr)     (dbl)  (chr)   (chr)  (dbl)
## 1   Actara d1         1      1 Peciolo      1
## 2   Actara d1         2      1 Peciolo     NA
## 3   Actara d1         3      1 Peciolo     NA
## 4   Actara d1         4      1 Peciolo     NA
## 5   Actara d1         5      1 Peciolo     NA
## 6   Actara d1         6      1 Peciolo     NA
## 7   Actara d1         7      1 Peciolo     NA
## 8   Actara d1         8      1 Peciolo     NA
## 9   Actara d1         9      1 Peciolo     NA
## 10  Actara d1        10      1 Peciolo     NA
## ..        ...       ...    ...     ...    ...
```

```r
dados <- read_excel("base_vespa.xlsx") %>% 
  gather("Local", "Galhas", 3:17) %>% 
  separate(Local, c("Coleta", "Local"))
```
