# Curso R - Introdução
Ítalo Cegatta  
3 de junho de 2016  



# Sobre o R

O R é um software open-source mantido por um grupo de voluntários de vários países, o R-core team. No site oficial do [projeto](https://www.r-project.org/) a primeira descrição sobre ele é a seguinte:

> O R é uma linguagem e ambiente para computação estatística e gráficos.

Esse grupo mantem o sistema base que possibilita a interação com a linguagem R para computação numérica, manipulação de dados, gráficos e uma variedade de outras tarefas. No R, tudo o que acontece é o resultado de uma função. Eu, você e tantos outros usuários podemos desenvolver funções para facilitar a nossa vida e posteriormente organizá-las em pacotes (ou *packages*) e disponibilizar para todo o mundo.

O projeto do R teve início com Ross Ihaka e Robert Gentleman nos anos 90 a partir de uma implementação da linguagem S, que foi desenvolvida anos antes por um grupo de pesquisadores liderados por John Chambers no Bell Laboratories. Desde então, o R tem crescido em um ritmo absurdo e pode ser considerado o principal software livre para programação estatística e um dos mais usados no mundo. Não vou listar todas potencialidades do R aqui neste post, em primeiro lugar por que eu não domino todas elas, e segundo por que com certeza o post ficaria muito grande :P. Com o tempo vou apresentar nos posts algumas aplicações pontuais do R com relação aos problemas que precisei resolver. Mas já adianto, é comum dizermos que a pergunta certa sobre uma tarefa no R não é *se podemos fazer*, mas sim *como* podemos fazer.

# Estrutura dos dados

Como em qualquer outra linguagem de programação, o R tem em sua concepção tipos e estruturas de dados que determinam como será o comportamento durante os processos. Os tipos de dados são estes: 

|    | Homogêneo     | Heterogêneo   |
|----|---------------|---------------|
| 1d | Atomic vector | List          |
| 2d | Matrix        | Data frame    |
| nd | Array         |               |

É importante entender a diferença entre estes tipo de objetos pois cada um dele tem um comportamento diferente e exigem tipos específicos de elementos.

## Atomic Vectors

Um vetor aceita 4 tipos de elementos: integer, double, character e logical. Teste o código abaixo atribuindo elementos aos objetos.


```r
x <- 1
typeof(x)
```

```
## [1] "double"
```

```r
x <- 1L
typeof(x)
```

```
## [1] "integer"
```

```r
x <- 2.333
typeof(x)
```

```
## [1] "double"
```

```r
x <- "a"
typeof(x)
```

```
## [1] "character"
```

```r
x <- TRUE
typeof(x)
```

```
## [1] "logical"
```

```r
x <- c("a", "b", "c", "d")
typeof(x)
```

```
## [1] "character"
```

Por que isso é importante? Cada função é desenhada para trabalhar com um certo tipo de objeto e elementos. Veja os exemplos abaixo.


```r
x <- c(1, 5, 10, 15)
x
```

```
## [1]  1  5 10 15
```

```r
mean(x)
```

```
## [1] 7.75
```

```r
x <- c(1, 5, 10, "15")
x
```

```
## [1] "1"  "5"  "10" "15"
```

```r
mean(x)
```

```
## [1] NA
```

```r
x <- as.numeric(c(1, 5, 10, "15"))
x
```

```
## [1]  1  5 10 15
```

```r
mean(x)
```

```
## [1] 7.75
```

## Lists

As listas são vetores com flexibilidade quanto ao tipo do elemento. Para criá-la basta usar `list()` ao invés de `c()`.


```r
x <- list(1:3, "a", c(TRUE, FALSE, TRUE), c(2.3, 5.9))
x
```

```
## [[1]]
## [1] 1 2 3
## 
## [[2]]
## [1] "a"
## 
## [[3]]
## [1]  TRUE FALSE  TRUE
## 
## [[4]]
## [1] 2.3 5.9
```

```r
str(x)
```

```
## List of 4
##  $ : int [1:3] 1 2 3
##  $ : chr "a"
##  $ : logi [1:3] TRUE FALSE TRUE
##  $ : num [1:2] 2.3 5.9
```

## Matrices and arrays

Se acrescentarmos mais dimensões aos vetores teremos matrizes (2d) e arrays (ou arranjos) para várias dimensões.


```r
x <- matrix(1:6, ncol = 3, nrow = 2)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

```r
typeof(x)
```

```
## [1] "integer"
```

```r
class(x)
```

```
## [1] "matrix"
```

```r
x <- array(1:18, c(2, 3, 3))
x
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
## 
## , , 3
## 
##      [,1] [,2] [,3]
## [1,]   13   15   17
## [2,]   14   16   18
```

```r
typeof(x)
```

```
## [1] "integer"
```

```r
class(x)
```

```
## [1] "array"
```

```r
x <- list(1:3, "a", TRUE, 1.0, matrix(1:6, ncol = 3, nrow = 2))
x
```

```
## [[1]]
## [1] 1 2 3
## 
## [[2]]
## [1] "a"
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] 1
## 
## [[5]]
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

```r
typeof(x)
```

```
## [1] "list"
```

```r
class(x)
```

```
## [1] "list"
```

## Data frames

Objetos do tipo Data frame são os mais comuns quando estamos trabalhando no R. Você pode entender um data frame como um conjunto de vetores, ou como uma matriz com maior flexibilidade.


```r
x <- 1:10
y <- c("a", "b")

df <- data.frame(x, y)
df
```

```
##     x y
## 1   1 a
## 2   2 b
## 3   3 a
## 4   4 b
## 5   5 a
## 6   6 b
## 7   7 a
## 8   8 b
## 9   9 a
## 10 10 b
```

```r
str(df)
```

```
## 'data.frame':	10 obs. of  2 variables:
##  $ x: int  1 2 3 4 5 6 7 8 9 10
##  $ y: Factor w/ 2 levels "a","b": 1 2 1 2 1 2 1 2 1 2
```

```r
df2 <- cbind(df, z = 21:30)

df3 <- rbind(df2, c(100, "a", 200))
df3
```

```
##      x y   z
## 1    1 a  21
## 2    2 b  22
## 3    3 a  23
## 4    4 b  24
## 5    5 a  25
## 6    6 b  26
## 7    7 a  27
## 8    8 b  28
## 9    9 a  29
## 10  10 b  30
## 11 100 a 200
```

# Subsetting

O acesso ao elemento armazenado em um objeto pode ser feito com 3 operadores: `$`, `[` e `[[`.

## Vetores


```r
## Número interiro positivo

x <- c(5.4, 6.2, 7.1, 4.8)

x[2]
```

```
## [1] 6.2
```

```r
x[c(2,3)]
```

```
## [1] 6.2 7.1
```

```r
x[c(2,2)]
```

```
## [1] 6.2 6.2
```

```r
## Número inteiro negativo

x[-1]
```

```
## [1] 6.2 7.1 4.8
```

```r
x[-c(1, 2, 3)]
```

```
## [1] 4.8
```

```r
## Operador lógico

x[c(TRUE, TRUE, FALSE, FALSE)]
```

```
## [1] 5.4 6.2
```

```r
x[x > 6]
```

```
## [1] 6.2 7.1
```

## Listas


```r
x <- list(vetor = 1:3, letra = "a", logico = c(TRUE, FALSE, TRUE))
x
```

```
## $vetor
## [1] 1 2 3
## 
## $letra
## [1] "a"
## 
## $logico
## [1]  TRUE FALSE  TRUE
```

```r
x$vetor
```

```
## [1] 1 2 3
```

```r
x[1]
```

```
## $vetor
## [1] 1 2 3
```

```r
x[[1]]
```

```
## [1] 1 2 3
```

## Matrizes


```r
x <- matrix(1:6, ncol = 3, nrow = 2)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

```r
colnames(x) <- c("A", "B", "C")
x
```

```
##      A B C
## [1,] 1 3 5
## [2,] 2 4 6
```

```r
x[ ,3]
```

```
## [1] 5 6
```

```r
x[1, ]
```

```
## A B C 
## 1 3 5
```

```r
x[ , "A"]
```

```
## [1] 1 2
```

```r
x[c(TRUE, FALSE), ]
```

```
## A B C 
## 1 3 5
```

```r
x[, -2]
```

```
##      A C
## [1,] 1 5
## [2,] 2 6
```

## Data frames


```r
df <- data.frame(x = 1:3, y = 3:1, z = letters[1:3])

df$x
```

```
## [1] 1 2 3
```

```r
df[ , 2]
```

```
## [1] 3 2 1
```

```r
df[ , "y"]
```

```
## [1] 3 2 1
```

```r
df[c(1,2), ]
```

```
##   x y z
## 1 1 3 a
## 2 2 2 b
```

```r
df[df$x == 2, ]
```

```
##   x y z
## 2 2 2 b
```
