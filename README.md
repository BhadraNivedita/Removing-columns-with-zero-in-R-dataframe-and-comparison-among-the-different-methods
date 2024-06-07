


```
#install.packages('rbenchmark') 
library(rbenchmark) # for benchmarking
library(readr) # for reading CSVs
```


```

removeZeroVar1 <- function(df){
  df[, sapply(df, var) != 0]
}
```


```
removeZeroVar2 <- function(df){
  df[, sapply(df, function(x) length(unique(x)) > 1)]
}
```


```
removeZeroVar3 <- function(df){
  df[, !sapply(df, function(x) min(x) == max(x))]
}

```


```
# Create a dataframe with some columns containing only zeros

# Sample data
id <- 1:10
age <- c(23, 45, 34, 28, 67, 54, 31, 40, 52, 29)
zeros1 <- rep(0, 10)
zeros2 <- rep(0, 10)
score <- c(89, 76, 91, 85, 88, 77, 92, 84, 79, 80)

# Combine into a dataframe
df <- data.frame(id, age, zeros1, zeros2, score)

# Print the dataframe
print(df)

```


```
benchmark(
  'Variance Method' = removeZeroVar1(df),
  'Unique Values Method' = removeZeroVar2(df),
  'Min-Max Method' = removeZeroVar3(df),
  columns = c("test", "replications", "elapsed", "relative"), 
  order = "elapsed",
  replications = 100
)



```


Reference: https://www.ttested.com/removing-zero-variance-columns/
