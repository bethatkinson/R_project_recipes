# Appendix




## Appendix 1: tidyverse package overviews

### dplyr

The package `dplyr` focuses on  transforming and summarizing tabular data with rows and columns. The package contains a set of functions (or “verbs”) that perform common data manipulation operations such as filtering for rows, selecting specific columns, re-ordering rows, adding new columns and summarizing data. In addition, dplyr contains a useful function to perform another common task which is the “split-apply-combine” concept. 

Important dplyr verbs to remember: 

* `select()`: select certain columns (fields/variables) of your dataset
* `filter()`: select specific rows (observations) of your dataset 
* `arrange()`: sort specified columns in ascending (default) or descending order 	
* `mutate()`: add new columns or change existing ones 
* `summarise()`: summarise values
* `group_by()`:	allows for group operations in the “split-apply-combine” concept
* `rename()`: change column names for variables
* `distinct()`: get unique values of specified variable set

Pipe operator: `%>%`

* dplyr imports this operator from another package (magrittr). This operator allows you to pipe the output from one function to the input of another function. Instead of nesting functions (reading from the inside to the outside), the idea of of piping is to read the functions from left to right.

Further examples are found at this [dplyr tutorial](http://genomicsclass.github.io/book/pages/dplyr_tutorial.html).

### tidyr

The package `tidyr` focuses on transposing data, changing from a "wide" format to a "long" format.

Important tidyr verbs to remember:

* `pivot_longer()` takes multiple columns, and gathers them into key-value pairs: it makes “wide” data longer (function used to be called `gather`)
* `pivot_wider()` takes two columns (key & value) and spreads in to multiple columns, it makes “long” data wider (function used to be called `spread`)
* `separate()` splits a single column into multiple columns
* `unite()` combines multiple columns into a single column

Further examples are found at this [data wrangling site](https://rpubs.com/bradleyboehmke/data_wrangling).

### lubridate

Historically dates have been challenging in R.  The package `lubridate` helps with this and includes some basic date manipulation functions.

* `year(), month(), day()`: extract year, month, day
* `hour(), minute(), second()`: extract hour, minute, second from a datetime variable
* `date()`: extract date from datetime variable
* `mdy()`: create date from text string


```r
> library(lubridate)
> mdy("July 4th, 2000")
[1] "2000-07-04"
> mdy("7/4/2000")
[1] "2000-07-04"
```

### ggplot2

The package `ggplot` focuses on displaying data graphically.  It is based on the `grammer of graphics` (Wilkinson, 2005)

What Is The Grammar Of Graphics?

The basic idea: independently specify plot building blocks and combine them to create just about any kind of graphical display you want. Building blocks of a graph include:

* data - where is the data located
* aesthetic mapping - what are your x, y, and grouping variables?  
* geometric object - what type of plot do you want to create
* statistical transformations - log transform (or others)?
* scales
* coordinate system
* position adjustments
* faceting - creating separate figures "by" some value, but using the same scale, variables, labels, etc.
* themes - color schemes used for plots, such as background color, axis defaults
    + `theme_gray()` (default)
    + `theme_bw()`
    + `theme_classc()`

*Geometic Objects* 

Geometric objects are the actual marks we put on a plot. Examples include:

* points (geom_point, for scatter plots, dot plots, etc)
* lines (geom_line, for time series, trend lines, etc)
* boxplot (geom_boxplot, for boxplots)

A plot must have at least one geom; there is no upper limit. You can add a geom to a plot using the + operator

You can get a list of available geometric objects using the code below.  There are also lots of examples of different types of plots available on the web (just include `ggplot` in your search).

```
help.search("geom_", package = "ggplot2")
```

Try working through this [R graphics tutorial](https://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html#putting_it_all_together) to learn more.


## Appendix 2: R for SAS programmers

If you tend to "think SAS", then making the switch to R can be challenging.  A couple book that might help include:

* _SAS and R: Data Management, Statistical Analysis, and Graphics_ by Kleinman and Horton 
* _R for SAS and SPSS Users_ by Robert Muenchen

Below are a few select tasks and the packages/functions that handle those tasks.


Table: (\#tab:unnamed-chunk-2)Reading and Writing files

|task                          |package  |function                                |
|:-----------------------------|:--------|:---------------------------------------|
|read SAS dataset              |haven    |read_sas()                              |
|read csv dataset              |readr    |read_csv()                              |
|read excel file               |readxl   |read_excel()                            |
|read in multiple files        |rlocal   |read.all()                              |
|write csv file                |readr    |write_csv()                             |
|write excel file              |openxlsx |write.xlsx()                            |
|write object to Word/HTML/PDF |arsenal  |write2word(), write2html(), write2pdf() |
|write text to file            |base     |sink()                                  |
|print pretty markdown table   |knitr    |kable()                                 |


Table: (\#tab:unnamed-chunk-3)Manipulating data

|task                                    |package      |function              |
|:---------------------------------------|:------------|:---------------------|
|summarize dataset                       |summarytools |dfSummary()           |
|create data from m, d, y                |arsenal      |mdy.Date()            |
|compare 2 datasets                      |arsenal      |comparedf()           |
|transpose data                          |tidyr        |gather() and spread() |
|create categorical data from continuous |base         |cut()                 |
|X in ('a','b','c')                      |base         |%in%, match()         |
|X NOT in ('a','b','c')                  |arsenal      |%nin%                 |
|concatenate strings                     |base         |paste0()              |



Table: (\#tab:unnamed-chunk-4)Modeling and Statistical Tests

|task                                      |package  |function                 |
|:-----------------------------------------|:--------|:------------------------|
|table 1, unpaired data                    |arsenal  |tableby()                |
|table 1, paired data                      |arsenal  |paired()                 |
|correlations                              |stats    |cor.test()               |
|partial correlations                      |ppcor    |pcor.test()              |
|binomial CI                               |rlocal   |cibinom()                |
|poisson CI                                |survival |cipoisson()              |
|t-tests                                   |stats    |t.test()                 |
|Wilcoxon/Kolmogorov-Smirnov test          |stats    |wilcox.test(), ks.test() |
|linear regression                         |stats    |lm()                     |
|logistic regression                       |stats    |glm(, family=binomial)   |
|poisson regression                        |stats    |glm( , family=poisson)   |
|negative binomial regression              |MASS     |glm.nb()                 |
|cox regression                            |survival |coxph()                  |
|quantile regression                       |quantreg |rq()                     |
|robust regression                         |MASS     |rlm()                    |
|generalized additive regression           |gam      |gam()                    |
|create table from multiple models         |arsenal  |modelsum()               |
|linear mixed effects (random slope) model |nlme     |lme()                    |
|person-years analysis                     |survival |pyears()                 |
|incidence rates                           |rlocal   |poprates()               |
