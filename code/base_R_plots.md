# Base `R` plotting
Chris Hamm  
`r format(Sys.Date())`  



## Introduction

Base `R` refers to the default suite of tools that come with a standard `R` installation. There are many packages that allow the user to plot in different ways. For example, the package `ggplot2` is particularly popular. However, these alternative packages require learning a new language (the **gg** in `ggplot2` stands for **g**rammer of **g**raphics) and you may not feel inclined to learn another language. Whether you prefer `ggplot2` or base `R` is besides the point. If you are making reproducible figures in `R` you are already winning. For the record, I use both base `R` and `ggplot2`. Both have their own strengths and weaknesses.

We will be working with the`iris` data set, which comes with `R` when you install the software. 

### `iris` data set 

The history of the [`iris` flower dataset](https://en.wikipedia.org/wiki/Iris_flower_data_set) is very interesting. In short, the data were collected by E. Anderson and introduced by one of the founders of statistics, R.A. Fisher, in the [paper](http://onlinelibrary.wiley.com/doi/10.1111/j.1469-1809.1936.tb02137.x/abstract;jsessionid=872BB90F822BC6CED8F4696E544EF6F5.f03t04) that described [`linear discriminant analysis`](https://en.wikipedia.org/wiki/Linear_discriminant_analysis). But enough about that, let's load the data and generate some plots. 

To load the `iris` data set:

```r
data(iris)
```

Nothing appears to have happened but in fact we did load the data set into `R`'s memory. Let's look at the dimensions of the data set and the first 6 rows of data:


```r
dim(iris)
```

```
## [1] 150   5
```

```r
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

We can see there are 150 rows and 5 columns of data. Those 5 columns are: 

1. `Sepal.Length`
1. `Sepal.Width`
1. `Petal.Length`
1. `Petal.Width`
1. `Species`

It looks like the first four columns of data should be continuous numbers and the last column should be a factor. Let's make sure that `R` is treating the data accordingly:


```r
str(iris)
```

```
## 'data.frame':	150 obs. of  5 variables:
##  $ Sepal.Length: num  5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
##  $ Sepal.Width : num  3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
##  $ Petal.Length: num  1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
##  $ Petal.Width : num  0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
##  $ Species     : Factor w/ 3 levels "setosa","versicolor",..: 1 1 1 1 1 1 1 1 1 1 ...
```

We are good to go. Let's make some plots.

## Plots

### Histogram

The basic command to create a histogram is `hist()`. We need to specify which of the columns we want to plot in our histogram. Let's plot a histogram of `Sepal.Length`.


```r
hist(iris$Sepal.Length)
```

<img src="base_R_plots_files/figure-html/hist_1-1.png" style="display: block; margin: auto;" />

Yay!

Wait. This is kind of boring to me. 

The real power of plotting in `R` comes from the ability to customize graphics. We plotted with the default parameters for the `hist()` function.

To see the default parameters of a function, and all of the other arguments that can be passed through a function, we use the `?` in front of the function name.


```r
?hist
```

This will open the `Help` window on your computer and show you the arguments and defaults for a function. The `Help` page for a function is the first place I go to troubleshoot an issue.

Let's make the histogram look a little bit nicer. The first thing I want to do is color in the bars of the histogram so they stand out more. The `col` argument takes a color inside of `""`.


```r
hist(iris$Sepal.Length, col = "grey")
```

<img src="base_R_plots_files/figure-html/hist_2-1.png" style="display: block; margin: auto;" />

A few things to mention here: 

* Note that I am building on the previous code. Right now it is OK to copy and paste and then add to the code with `col = "grey"`. There are a lot of colors in base `R` that you can spell out. Try changing `col = ""` to something else.
* I am spelling out the name of the color. You can also specify color using `rgb` values of `#hex` codes. More on that later. 
* from here on out I will be changing plots incrementally and tweak one thing at a time. You don't need to do it this way but it is convenient when starting out because if your code doesn't work you know exactly where it broke.

Now I am going to make the title easier to read my changing the `main` argument:


```r
hist(iris$Sepal.Length, col = "grey", main = "Sepal length")
```

<img src="base_R_plots_files/figure-html/hist_3-1.png" style="display: block; margin: auto;" />

Or I could make it go away entirely with by telling `R` not to plot anything in the title by leaving the `""` empty:


```r
hist(iris$Sepal.Length, col = "grey", main = "")
```

<img src="base_R_plots_files/figure-html/hist_4-1.png" style="display: block; margin: auto;" />

The x-axis label looks pretty bad with the name of the vector. Let's change it using the `xlab` (short for x label) argument:


```r
hist(iris$Sepal.Length, col = "grey", main = "", xlab = "Sepal length (cm)")
```

<img src="base_R_plots_files/figure-html/hist_5-1.png" style="display: block; margin: auto;" />

The next thing I want to change is the orientation of the numbers on the y-axis. I want them facing the same way as the labels on the x axis to make it easier for people to read. I will adjust this using the `las`, which will accept a value between `0` and 3.

* `las = 0` - Label is parallel to the axis (default).
* `las = 1` - Label is horizontal to the axis (awesome).
* `las = 2` - Label is perpendicular to the axis (why?).
* `las = 3` - Label is placed vertically (really, why?).


```r
hist(iris$Sepal.Length, col = "grey", main = "", xlab = "Sepal length (cm)", las = 1)
```

<img src="base_R_plots_files/figure-html/hist_6-1.png" style="display: block; margin: auto;" />

Play with the different `las =` and see how label orientation changes. 
