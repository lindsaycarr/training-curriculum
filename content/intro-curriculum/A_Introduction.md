---
author: Jeffrey W. Hollister & Luke Winslow
date: 9999-01-10
slug: Introduction
title: A. Introduction to R
image: img/main/intro-icons-300px/r-logo.png
menu:
  main:
    parent: Introduction to R Course
    weight: 1
---
Over the course of the next 2.5 days we are going to walk through a typical data analysis workflow in R. But, with this first lesson we are going to focus on making sure everything is working and getting some basic orientation in R. The real fun will start in the lessons to come.

Quick Links to Exercises and R code
-----------------------------------

My goal is to have this workshop be as hands-on and interactive as possible. I encourage you to get to know the people sitting next to you. Throughout the workshop, I encourage you to ask questions and get help from those around you.

To be hands-on, there are exercises throughout. For each lesson, I will provide a list of links near the top of the post so that you can skip all the prose and jump straight to the lessons. So, here are the links for Lesson 1.

-   [Exercise 1](#exercise-1): RStudio Introduction.
-   [Exercise 2](#exercise-2): Functions, packages, and help

Lesson Goals
------------

-   Understand what R is and what it can be used for
-   Why would you choose R over another tool
-   Troubleshoot software installs (keep your fingers crossed)
-   Gain familiarity with using R from within the RStudio IDE
-   Get to know the basic syntax of R functions
-   Be able to install and load a package into your R library
-   Know how to get help

What is R and why use it
------------------------

R is an open source language and environment for data analysis, statistics, and visualization. This is the typical definition. I would argue that R has evolved a bit and is now, more and more, also a general purpose computing language. It is very widely used in academia and industry for statistics, visualization, data science, and general purpose computation. In short, the answer to the question to, "Can you do that in R" is almost always yes. R may not be the best answer, but it is an excellent one.

The primary reason R is widely used is that it is free, has a large and vibrant community, it is easily extensible, and back to that question, yes you can do that in R! More to the point, in the environmental sciences R is able to handle any task in data management, analysis, or visualization that you would need to accomplish, and it can provide a fully reproducible analysis.

Lastly, R has become the standard for any data analysis or visualization task in many fields. A great site [r4stats.com](http://r4stats.com) has an [article](http://r4stats.com/articles/popularity/) on data analysis software popularity that is kept up to date on the relative popularity of different languages. One striking figure is the comparison of Google Scholar hits for each of the most popular languages:

[![r4stats.com web site link graph](http://i1.wp.com/datasciencepopularity.com/wp-content/uploads/2015/05/fig_2f_scholarlyimpactallstat21.png "popular programming langages")](http://r4stats.com/articles/popularity/)

<caption align="bottom">
source: r4stats.com - The Popularity of Data Analysis Software
</caption>
If you read this article you certainly get the sense that R is one of the top statistical languages and is on track to overtake the two leading proprietary software options (SAS, SPSS) in the next few years.

Getting R and RStudio going
---------------------------

Over the last several years, RStudio has become a very popular IDE (integrated development environment) for R. In addition to interacting with the R Console, RStudio has many extras built in including version control integration, package building, reproducible research, de-bugging, and built-in text editor with smart highlighting and code completion. This is the environment we will be using for the two days and should set you up for continued learning with R.

Exercise 1
----------

This exercise will make sure R and RStudio are working and that you can get around the basics in RStudio.

1.  Start RStudio: To start both R and RStudio only requires firing up RStudio.RStudio should be available from All Programs at the Start Menu. Fire up RStudio.

2.  Take a few minutes to look around RStudio. Find the Console Pane. Find Global and Project Options (hint: look in Tools). Look at the Environment, History Pane. Look at the Files, Plots, Packages ... pane.

3.  Create a new project. Select File | New Project.... Name it "usgs\_r\_workshop". We will use this for the rest of the workshop.

4.  Create a new "R Script" in the Source Pane (click the icon with the green plus symbol below "File"), save that file into your newly created project and name it "lessonA.R".

Using functions
---------------

R is built off of functions and most of everything you do uses a function.

The basic syntax of function follows the form: `function_name(arg1, arg2, ...)`. With the base install, you will gain access to many. Try evaluating the following functions (copy and paste into the command line in the Console pane, then hit enter):

``` r
#Print
print("hello world!")
#A sequence
seq(1, 10)
#Random normal numbers
rnorm(100, mean=10, sd=2)
#Mean
mean(rnorm(100))
#Sum
sum(rnorm(100))
```

A few side notes. The `#` indicates a comment. You can put whatever else you'd like after this, but on the same line as the `#`. R will not evaluate it. When commenting your code, err on the side of too much! Also, you will see `()`, `[]`, and `{}` used in R code. The `()` indicates a function (almost always), the `[]` indicates indexing (grabbing values by the location in a vector, matrix, etc.), and the `{}` groups code that is meant to be run together and is usually used when programming functions in R.

Using packages
--------------

The base install of R is quite powerful, but you will soon have a need or desire to go beyond this. Packages provide this ability. They are a standardized method for extending R with new methods, techniques, and programming functionality. There is a lot to say about packages regarding finding them, using them, etc., but for now let's focus just on the basics.

### CRAN & GRAN

One of the reasons for R's popularity is CRAN, [The Comprehensive R Archive Network](http://cran.r-project.org/). This is where you download R and also where most will gain access to packages (there are other places, but that is for later). For some USGS specific packages that aren't of interest to the public, we have created [GRAN, the Geological survey R Archive Network](http://owi.usgs.gov/R/gran.html). We specify that we want packages from either archive network like this:

``` r
options(repos=c("https://cran.rstudio.com/", "http://owi.usgs.gov/R"))
```

### Installing packages

When a package gets installed, that means the source (or packaged binary for Windows) is downloaded and put into your library. A default library location is set for you so no need to worry about that. In fact on Windows most of this is pretty automatic. Let's give it a shot.

``` r
#Install dataRetrieval and EGRET
install.packages("dataRetrieval")
install.packages("EGRET")

#You can also put more than one in
install.packages(c("dplyr", "ggplot2"))
```

### Loading packages

One source of confusion that many have is when they cannot access functions from a package that they just installed. This is because getting to this point requires an extra step, loading (or attaching) the package.

``` r
#Add libraries to your R Session
library("dataRetrieval")
library("EGRET")

#You can also access functions without loading by using package::function
dataRetrieval::readNWISuv
```

    ## function (siteNumbers, parameterCd, startDate = "", endDate = "", 
    ##     tz = "") 
    ## {
    ##     url <- constructNWISURL(siteNumbers, parameterCd, startDate, 
    ##         endDate, "uv", format = "xml")
    ##     data <- importWaterML1(url, asDateTime = TRUE, tz = tz)
    ##     return(data)
    ## }
    ## <environment: namespace:dataRetrieval>

You will often see people use `require()` to load a package. It is better form to not do this. For a more detailed explanation of why `library()` and not `require()` see [Yihui Xie's post on the subject](http://yihui.name/en/2014/07/library-vs-require/.)

Help!
-----

Being able to find help and interpret that help is probably one of the most important skills for learning a new language. R is no different. Help on functions and packages can be accessed directly from R, can be found on CRAN and other official R resources, searched on Google, found on StackOverflow, or from any number of fantastic online resources. I will cover a few of these here.

### Help from the console

Getting help from the console is straightforward and can be done numerous ways.

``` r
#Using the help command/shortcut
help("print") #Help on the print command
?print #Help on the print command using the `?` shortcut
help(package="dplyr") #Help on the package `dplyr`

#Don't know the exact name or just part of it
apropos("print") #Returns all available functions with "print" in the name
??"print" #Returns fuzzy matches to the text. Also searches demos and vignettes in a formatted page

#Explore what's loaded
ls("package:stats") #Lists all functions in the stats package (which is always loaded)
#'pri'-TAB #press the Tab key as you're typing to see a list of possible word completions
```

One nice way to explore the features of a package is to see a list of all the functions. In the lower right-hand corner, there is a "Packages" tab. From this tab, if you click on the name of a package, you will get a list of all the documentation for that package.

![Package List](../static/img/rstudio_packages.png "list of packages")

This is very helpful if you've forgotten the name of a function or just want to see a quick overview of everything a package has to offer.

![Package List](../static/img/rstudio_dataRetrieval.png "package documentation")

### Official R Resources

In addition to help from within R itself, CRAN and the R-Project have many resources available for support. Two of the most notable are the mailing lists and the [task views](http://cran.r-project.org/web/views/).

-   [R Help Mailing List](https://stat.ethz.ch/mailman/listinfo/r-help): The main mailing list for R help. Can be a bit daunting and some (although not most) senior folks can be, um, curmudgeonly...
-   [R-sig-ecology](https://stat.ethz.ch/mailman/listinfo/r-sig-ecology): A special interest group for use of R in ecology. Less daunting than the main help with participation from some big names in ecological modelling and statistics (e.g., Ben Bolker, Gavin Simpson, and Phil Dixon).
-   [Environmetrics Task View](http://cran.r-project.org/web/views/Environmetrics.html): Task views are great in that they provide an annotated list of packages relevant to a particular field. This one is maintained by Gavin Simpson and has great info on packages relevant to much of the work at EPA.
-   [Spatial Analysis Task View](http://cran.r-project.org/web/views/Spatial.html): One I use a lot that lists all the relevant packages for spatial analysis, GIS, and Remote Sensing in R.

### Google and StackOverflow

While the resources already mentioned are useful, often the quickest way is to just turn to Google. However, a search for "R" is a bit challenging. A few ways around this. Google works great if you search for a given package. You can search for mailing lists directly (i.e. "R-sig-geo"). An R specific search tool, [RSeek.org](http://www.rseek.org/), has been created to facilitate this.

One specific resource that I use quite a bit is [StackOverflow with the 'r' tag](http://stackoverflow.com/questions/tagged/r). StackOverflow is a discussion forum for all things related to programming. You can then use this tag and the search functions in StackOverflow and find answers to almost anything you can think of.

### Other Resources

There are too many resources to mention and everyone has their favorites. Below are just a few that I like.

-   [R For Cats](http://rforcats.net/): Basic introduction site, meant to be a gentle and light-hearted introduction.
-   [Advanced R](http://adv-r.had.co.nz/): Web home of Hadley Wickham's new book. Gets into more advanced topics, but also covers the basics in a great way.
-   [Why R is Hard To Learn](http://r4stats.com/articles/why-r-is-hard-to-learn/): Long and detailed blog post discussing some of the challenges people often face when learning R.
-   [Other Resources](http://scicomp2014.edc.uri.edu/resources.html): A list I helped compile for a URI Class.
-   [CRAN Cheatsheets](http://cran.r-project.org/doc/contrib/Short-refcard.pdf): A good cheat sheet from the official source.
-   [RStudio Cheatsheets](http://www.rstudio.com/resources/cheatsheets/): Additional cheat sheets from RStudio. I am especially fond of the data wrangling one.
-   [R-bloggers](http://www.r-bloggers.com/): Central hub of content collected from bloggers who write about R.

Exercise 2
----------

For this second exercise we are going to get used to using some basic functions, working with scripts and not just the console, and look through some task views and get used to basic navigation around packages.

1.  If it is not already open, open the "lessonA.R" file you created in Exercise 1. Enter your commands into this script. As you go, place your cursor on a line and run that line by pressing Ctrl+Enter (or Cmd+Enter on Macs) or clicking the Run button at the top right of the editor window.
2.  Use the `print` function to print something to the screen.
3.  Combine `mean` and `rnorm` to return the mean value of a set of random numbers.
4.  Open up a [task view](http://cran.r-project.org/web/views/) of your choosing. Select a package and install it.
5.  Load the package into R.
6.  Open the help for the package.
7.  Save all these commands in a script for lesson 1. Comment out any lines that install packages - this only needs to be done once per computer. Run the whole script again using the "Source" button at the top right of the editor. Then run just a few lines at once by highlighting those lines with your mouse, then pressing the Run button or Ctrl+Enter (Cmd+Enter). What's the difference between (1) clicking Source and (2) selecting all lines then clicking Run?
