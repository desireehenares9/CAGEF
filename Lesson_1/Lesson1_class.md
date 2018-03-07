---
title: "Lesson 1 - Intro to R and R-Studio: Becoming Friends with the R Environment and Getting your Data In and Out of R"
output: 
  html_document:
          keep_md: yes
          toc: TRUE
          toc_depth: 3
  html_notebook:
          toc: TRUE
          toc_depth: 3
---
***


![](img/magic.png){width=400px} 


</br>

##A quick intro to the intro to R Lesson Series

</br>

This 'Intro to R Lesson Series' is brought to you by the Centre for the Analysis of Genome Evolution & Function's (CAGEF) bioinformatics training initiative. This course was developed based on feedback on the needs and interests of the Department of Cell & Systems Biology and the Department of Ecology and Evolutionary Biology. 



This lesson is the first in a 6-part series. The idea is that at the end of the series, you will be able to import and manipulate your data, make exploratory plots, perform some basic statistical tests, test a regression model, and make some even prettier plots and documents to share your results. 


![](img/data-science-explore.png)

</br>

How do we get there? Today we are going to be learning about the basic data structures in R, get cozy with the R environment, and learn how to get help when you are stuck. Because everyone gets stuck. A lot. Then you will learn how to get your data in and out of R. Next week we will learn how to tidy our data, subset and merge data and generate descriptive statistics. The next lesson will be data cleaning and string manipulation; this is really the battleground of coding - getting your data into the format where you can analyse it. After that, we will make all sorts of plots - from simple data exploration to interactive plots - this is always a fun lesson. And then lastly, we will learn to write some functions, which really can save you time and help scale up your analyses.


![](img/spotify-howtobuildmvp.gif)

</br>

The structure of the class is a code-along style. It is hands on. The lecture AND code we are going through are available on GitHub for download at https://github.com/eacton/CAGEF __(Note: repo is private until approved)__, so you can spend the time coding and not taking notes. As we go along, there will be some challenge questions and multiple choice questions on Socrative. At the end of the class if you could please fill out a post-lesson survey (https://www.surveymonkey.com/r/GD3KJB9), it will help me further develop this course and would be greatly appreciated. 



__Objective:__ At the end of this session you will be familiar with the R environment, setting your working directory, know about basic data structures in R and how to create them. You will be able to import data into R (tsv, csv, xls(x), googlesheets) and export your data again.


##A quick intro to the R environment##

To paraphrase the CRAN gurus:     
https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf


R is an 'environment' because it has the tools and software for the storage, manipulation, statistical analysis, and graphical display for of data.  It comes with about 25 built-in 'packages' and uses a simple programming language ("S"). Users have been encouraged to make there own packages... there are now over 10,000 packages on CRAN and about 1,500 on Bioconductor.

![](img/cran_pkg.png){width=600px}
</br>

RStudio is an IDE (Integrated Development Environment) for R that provides a more user-friendly experience than using R in a terminal setting. It has 4 main areas or panes, which you can customize to some extent under Tools > Global Options > Pane Layout:

1. Source - The code you are annotating and keeping in your script.
2. Console - Where your code is executed.
3. Environment - What global objects you have created and functions you have written/sourced.
   History -  A record of all the code you have executed in the console.
   Connections - Which data sources you are connecting to. (Not being used in this course.)
4. Files, Plots, Packages, Help, Viewer - self-explanatoryish if you click on their tabs.

(In-class moment for going over these 4 quadrants + Global Options.)


##A quick note on directory structure

This is an image of a possible directory. 

![](img/unix-tree.gif)

</br>

In this hierarchy we will pretend to be sue, and we are hanging out in our subdirectory1 folder. R looks to read in your files from your _working directory_, which in this case would be subdirectory1, so at this moment, R would have access to file1 and file2. If I tried to open file1 under sue, R would tell me there is no such file in my current working directory.

To get your working directory in R you would type:

```

```

R will tell you your _absolute directory_. An absolute directory is a _path_ starting from your root `"/"`. The absolute directory can vary from computer to computer. My home directory and your home directory are not the same; our names are in the path.


To move directories, it is good to know a couple shortcuts. `'.'` is your current directory. `'..'` is up one directory level. `'~'` is your home directory (a shortcut for `"home/sue"`). Therefore, our current location could also be denoted as `"~/subdirectory1"`.

To move to the directory 'sue' we us a function that will set the working directory:

```


```
A _relative directory_ is a path starting from whereever your currently are (your working directory). This path could be the same on your computer and my computer if and only if we have the same directory structure. 

If I wanted to move back to subdirectory1 using the _absolute path_, I would set a new working directory:

```

```

And the _relative path_ would be:

```

```

There is some talk over setting working directories within scripts. Obviously, not everyone has the same absolute path, so if you are setting a directory in your script, _it is best to have a relative path starting from the folder your script is in_. Keep in mind that others you share your script with might not have the same directory structure if you refer to subfolders. 

You can set your working directory by:
1. setwd()
2. Session -> Set Working Directory (3 Options)
3. Files Window -> More (Gear Symbol) -> Set As Working Directory


##Making Life Easier

###Annotate your code

Why???

-Can you rerun this analysis and but change X parameter? (said every PI ever)     
-Can you make this plot, but with dashed lines, a different axis, with error bars? (said every PI ever)     
-Can I borrow your code? (a collaborator or officemate)     
-Your worst collaborator is actually you in 6-months. Do you remember what you had for breakfast last Tuesday? 


<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/real_programmers.jpg)
</div>
 

![](img/why.jpg){width=300px}     
</br>


You can annotate your code for selfish reasons, or altruistic reasons, but annotate your code. 

How do I start?

- A hash-tag `#` will comment your text. A hash-tag in front of code means that code will not be evaluated.
- Put a description of what you are doing near your code (I prefer above) - at every process, decision point, or non-default argument in a function. For example, why you selected k=6, or the Spearman over Pearson option for your correlation matrix, or quantile over median normalization, or why you made the decision to filter out certain samples. 
- Break your code into sections to make it readable.
- Give your objects informative object names __that are not the same as function names__. 

_Key-board shortcuts:_

Comment/Uncomment lines `CTRL + SHIFT + C`     
Reflow Comment (Wrap comments) `CTRL + SHIFT + /`


###Best Practices for Writing Scripts

    Start each script with a description of what it does.

    Then load all required packages.

    Consider what working directory you are in when sourcing a script.

    Use comments to mark off sections of code.

    Put function definitions at the top of your file, or in a separate file if there are many.

    Name and style code consistently. 

    Break code into small, discrete pieces.

    Factor out common operations rather than repeating them.

    Keep all of the source files for a project in one directory and use relative paths to access them.

    Keep track of the memory used by your program.

    Always start with a clean environment instead of saving the workspace.

    Keep track of session information in your project folder.

    Have someone else review your code.

    Use version control.

https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/



###Trouble-shooting basics

- _file does not exist_ - working directory errors  - use getwd() to check where you are working, the Files window to check that your file exists there, and setwd() to change your directory
                         - work inside an _R project_ with your files in the same folder - your working directory will be set automatically when you open the project
- _typos_ - R is case sensitive, check that you've spelled everything right
            - use tab-completion when possible
- _open quotes, parentheses, brackets_
            - R Studio highlights matching brackets, and gives an 'x' on your left sidebar if your final bracket is not closed
- _data type_ - you can't perform a calculation on those 1, and 0's because they are actually characters and not numeric
- _unexpected answers_ - check in the help menu ie. `help("function")` or `?function` to double-check how the function works and its output
- _function is not found_ - make sure the package is installed AND loaded
- _weird error_ you are not sure the meaning of - find answers online (see below)
- sometimes weird things happen - clear your environment and restart your R session
- _the R bomb_!! - congrats, you have completed an R rite of passage.




***

__Beginner Advice__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/beginner.png){width=100px}
</div>

Try to solve a problem yourself, but set a 30 minute cutoff on being stuck. At this level, people have had and solved your problem. Many beginners get frustrated because they get stuck and take hours to solve a problem themselves. Set your limit, stay within it, then go online and get help.
</br>
</br>

***

</br>

_Finding answers online_     

- 99% of the time, someone has already asked your question     
- Google, Stackoverflow, SEQanswers, quora, researchgate, RSeek, twitter, even reddit     
- Including the program, version, error, package and function helps, be specific     
- http://stat545.com/help-general.html      
  
  
_Asking a question_

- Summarize your question in the title.
- Introduce your question, how you ran into the problem, __and how you tried to solve it yourself__. If you haven't done the bolded thing, do the bolded thing.
- Show enough of your code to reproduce the problem.
- Add tags that match your problem.
- Respond to the feedback. People put in their free time to answer you.
- https://stackoverflow.com/help/how-to-ask     
- https://www.r-project.org/posting-guide.html

</br>

![](img/StackOverflow.png)

</br>

_Remember_ - everyone looks for help online ALL THE TIME. It is completely normal. Also, with programming there are multiple ways to come up with an answer. There are different packages that let you do the same thing, but with shortcuts. There are different levels of 'efficiency' and 'redundancy' in coding. You will work on refining these aspects of your code as you go along in this course, and in your coding career.

Last but not least, to make life easier: under Help there is a `Cheatsheet of Keyboard Shortcuts`.




##A quick intro to R data structures


There are 4 types of data structures in R.

1. vectors - 1D - holds one type of data
2. lists - 1D - holds multiple data types
3. matrices - 2D - holds one type of data 
4. data frames - 2D - holds multiple data types
5. arrays - nD - holds one type of data

What do I mean by 'type of data'?     

- character - a#c$E 
- numeric - 7.5
- integer - 1
- logical - TRUE, FALSE

Let's make some data!! 

The assignment operator `"<-"` assigns a value to an object. The equals sign `'='` is also an assignment operator. However, since equals signs are used in logical statements (==, >=, <=, !=) with a different meaning, I prefer to use `<-`. You will see both outside this course.

```

```
(This is for illustrative purposes only and is not code.)

###A quick word on functions.

We are going to use a simple function to create a vector. Functions take arguments. To find out which arguments they take, we can look at the help menu. The help menus in R can be intimidating and hard to read. Don't think it is just because you are new. If you really don't understand the help menu, you are probably not the only one, so look online and there will likely be a simpler explanation.

Let's look up the function `c()`, which combines values into a vector or list. It takes in the argument `'...'`, which is defined as the objects to be concatenated. In the description it says 'all agruments are coerced to a common type, which is the type of the returned value' and in the details it tells you the hierarchy 'NULL < raw < logical < integer < double < complex < character < list < expression' and 'factors are treated only via their internal integer codes'. Now we don't know what all this means yet, but we come back to this as we go along. The output of the function is 'NULL or an expression or a vector'. At the bottom of the help menu, there are usually examples of how to use the function, which are sometimes easier to understand than the documentation. 


###Vectors

Here are what vectors of each 'type' would look like. Note that character items must be in quotations. 



What happens if we try to include more than one type of data?




R will coerce your vector to be of one data type, in this case the type that is most inclusive is a `_______` vector. 
What do you think will happen if 'bacteria' is removed from the vector? Will it be coerced to the same type?



R has forced the vector to be `______`. TRUE and FALSE may be represented by 1 and 0, respectively.




Does it work to change it back into TRUE and FALSE?



What about for our mixed vector?



I am highlighting this for a couple of reasons. Keep your data types in mind. It is good practice to look at your object or the global environment to make sure the object that you just made is what you think it is. Secondly, it can be useful for data analysis to be able to switch from TRUE/FALSE to 1/0, and it is pretty easy, as we have just seen.

You can name the contents of your vectors or specify them upon vector creation.



The number of elements in a vector is its length.




You can grab a specific element by its index, or by its name. 




###Lists

Lists can hold mixed data types of different lengths.



Lists can get complicated. If you forget what is in your list, use the `str()` function to check out its structure. It will tell you the number of items in your list and their data types. You can (and should) call `str()` on any R object. You can also try it on one of our vectors.




To subset for 'virus', I first have to subset for the character element of the list. Kind of like a Russian nested doll or a present, where you have to open the outer layer to get to the next.





###Matrices

Create a demo matrix.  



***

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/pause.jpg){width=100px}

</div>
What has happened here? Look up the rep() function. Why has R not thrown an error? How would I make this same matrix without vector recycling?          
</br>     

***
__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>
Make a 4 x 4 matrix that looks like this, using the seq() function at least once. 

<pre>
2   4   6   8
10  12  3   6
9   12  0   1
0   1   0   1
</pre>

***



A matrix is a 2D object. We can now check out a couple more properties - like the number of rows and columns.


To access a specific row or column we can still use indexing.


Note that when we are subsetting a single row or column, we end up with a vector.


It is common to transform matrices. Note that the set of ones will now be in rows rather than columns.




***

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/pause.jpg){width=100px}
</div>

Now that we have had the opportunity to create a few different objects, let's talk about what an object _class_ is. An object class can be thought of as how an object will behave in a function. Because of this data frames, lists and matrices have their own classes, while vectors inherit from their data type (vectors of characters behave like characters, vectors of numbers behave like numbers).


Some package creaters will have created their own data classes and will require your data to be in the format required of that class. For example in Bioconducter there is an _ExpressionSet_ class. 

![](img/expressionset.jpg)

</br>

This class contains your metadata (information about your samples), your assay data (experiment results), and your feature data (information about genes, probes, whatnot) in different slots. Functions in a package using this class may not work unless your data is in the ExpressionSet class format. This isn't something we will be dealing with a lot in this class, but it is good to be aware of from a trouble-shooting perspective.     

***

###Data Frames

Data frames are lists to the extent that they can hold different types of data. However, they must be of equal length.



Many R packages have been made to work with data in data frames, and this is the class of object where we will spend most of our time. 

Let's use some of the functions we have learned for finding out about the structure of our data frame.



***

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/pause.jpg){width=100px}

</div>

What is a _factor_?

A factor is a _class_ of object used to encode a character vector into categories. This will become clear with a bit more data, so lets make our data frame larger by adding rows. We can only do this if the data we want to add has the same number of columns. How many rows and columns does this new data frame have?


If we look at the structure again, we still have 3 levels. This is because each unique character element has been encoded as a number.
(Note that a column can be subset by index or by its name using the `'$'` operator.)


Note that the first character object in the data frame is 'bacteria', however, the first factor level is archaea. R by default puts factor levels in alphabetical order. This can cause problems if we aren't aware of it. Always check to make sure your factor levels are what you expect. With factors, we can deal with our character levels directly, or their numeric equivalents. Factors are extremely useful for performing group calculations as we will see later in the course.



***
__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>

Look up the factor function. Use it to make 'bacteria' the first level, 'virus' the second level, and 'archaea' the third level. Use functions from the lesson to make sure your answer is correct. 

</br>     
</br>     

***

We can also convert between data types if they are similar enough. For example, I can convert my matrix into a data frame. Since a data frame can hold any type of data, it can hold all of the numeric data in a matrix.


Note that R just made up column names for us. We can provide our own vector of column names.


In contrast, our data frame with multiple data types can not be converted into a matrix, as a matrix can only hold one data type. We could however, transform our new_dat back into a matrix. The matrix will retain our column heading.






###Arrays

Arrays are n dimensional objects that hold numeric data. To create an array, we give a vector of data to fill the array, and then the dimensions of the array. This code will recycle the vector 1:10 and fill 5 arrays that have 2 x 3 dimensions. To visualize the array, we will print it afterwards.


This arrangement makes it more clear how we would subset the number 7 out of array 5.


A 2D array is just a matrix. Unless you specify a 3rd dimension.


Personally, I don't use arrays in my daily genomics life, so if you find this confusing, I wouldn't worry about it too much.

</br>

####Using R for a Calculator

So you can do math...

Addition

Subtraction


Multiplication


Division


Exponents


A logic test ensues.



If x gets updated, what happens to y? This is something you need to be aware of when running code - variables dependent on other variables and where in your program they are created and updated.




So you can do math... on a vector.


So you can do math... on a vector.



So you can do math... on a list.



So you can do math... on a matrix.



So you can do math... on a data frame.



So you can do math... on an array.


These are illustrative examples to see how our different data structures behave. In reality, you will want to do calculations across rows and columns, and not on your entire matrix or data frame. For example, we might have a count table where rows are genes, columns are samples, and we want to know the sum of all the counts for a gene. To do this, we can use the apply function.


The apply function will recognize basic functions.


Public service announcement. Know what logarithm you are using. 


What if I want to know something else? We can create a function.


***
__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>


Create a function to test if ALL of the counts for a gene are greater than 10.     

</br>
</br>     

***

</br>

#A primer on missing data

Sometimes there is missing data in a dataset. For an example, I am going to take the earlier counts table and add a few NAs. If I now try to calculate the mean number of counts, I will get NA as an answer for the rows that had NAs.



How do we find out ahead of time that we are missing data? Knowing is half the battle.
With a vector we can easily see how some basic functions work.


We are returned a logical vector of whether or not a value was NA. We can get the positional index and remove the NAs.



With a large data frame, it may be hard to look at every cell to tell if there are NAs. The function complete.cases looks by row to see whether any row contains an NA. You can then subset out the rows with the NAs.

If you want to keep all of the observations in your data frame and do your calculations anyways, now that you are aware of what is going on in your dataset, some functions specifically allow for this. Let's look up the documentation for the mean function.



Most of the functions used above have this parameter. Although some do not.


In this case na.omit can be useful. 


You can similarly deal with NaNs in R. NaNs (not a number) are NAs (not available), but NAs and NaNs. NaNs appear for imaginary or complex numbers or some numeric values for example 0/0. Some packages may output NAs, NaNs, or Inf/-Inf (rare, use is.finite). 


Depending on your purpose, you may replace NAs with a sample average, or the mode of the data, or a value that is below a threshold.



</br>

#Installing and importing libraries

There are a few different places you can install packages from R. Listed in order of decreasing sketchiness:

- Bioconductor (Bioinformatics focus)
    + Guidelines for submission, reviewed, and must have a vignette.
- CRAN (The Comprehensive R Archive Network)
    + Guidelines for submission, reviewed. Where the majority of packages are.
- GitHub
    + No formal review process, but peers can opens issues to highlight problems or suggest fixes.
    + The is an increasing number of publibacteriaion-related packages.
- Joe's website
    + No review process. Not sure I trust that guy. 
    
</br>

_Readr_ is a package that will help us to read in our files (easily). It is installed from CRAN.



R may give you package installation warnings. Don't panic. In general, your package will either be installed and R will test if the installed package can be loaded, or R will give you a 'non-zero exit status' - which means your package did not install. If you read the entire error message, it will give you a hint as to why the package did not install.

Some packages depend on previously developed packages and can only be installed after said package is installed in your library. Similarly, the previous package may depend on another package... here is the solution to install the package and all of the prior packages it relies on.



You can install more than one package at once.



To load a package (ie. to actually use it):



Likewise, you can install many packages at once:



To install from Bioconductor you can either always use source to use biocLite...



Or you can install the BiocInstaller package. I prefer this as I always forget the url.




Devtools is required to install from GitHub. We don't actually need to load the entire library for devtools if we are only going to use one function.



Libraries from Bioconductor and GitHub load the same as packages from CRAN.




***
__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>

Install and load the package 'DESeq2'.

</br>

</br>


***

</br>

#Reading in data & writing data

###Our Dataset

Metagenomic 16SrRNA sequencing of latrines from Tanzania and Vietnam at different depths (multiples of 20cm). 

We have 2 csv files (change one to tsv or xlsx - maybe both and make an additional files and get a google spreadsheet): 
1. A metadata file (Naming conventions: [Country_LatrineNo_Depth]) with sample names and environmental variables.
2. A table of species abundance.

B Torondel, JHJ Ensink, O Gunvirusdu, UZ Ijaz, J Parkhill, F Abdelahi, V-A Nguyen, S Sudgen, W Gibson, AW Walker, and C Quince.
Assessment of the influence of intrinsic environmental and geographical factors on the bacterial ecology of pit latrines
Microbial Biotechnology, 9(2):209-223, 2016. DOI:10.1111/1751-7915.12334

***

Let's read our metadata file into R. While we do these exercises, we are going to become friends with the help menu.

To see the result, we can either click on meta in the global environment to open it in the viewer, or we can write code to view the variable. `head()` will show us the first 10 rows of our data frame. `tail()` would show the last 10 rows.



This is pretty ugly looking. Why?
In the help file the default `__________________________________________`. We need to use specify a  `___` instead.  



Better. Our columns are now separated appropriately, but what about our column titles?



These samples are not replicates. Each represents a combination of a different country, latrine, and depth. In this case, we might prefer to have Samples as character, not a factor. (Note: TRUE and FALSE can be abbreviated as T and F)



***
__Challenge__ 


<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>

Use a parameter in read.table to read in metadata such that all non-character columns are numeric.

</br>

</br>

***

__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>

Read our data table into R using any function under Usage in the read.table help menu. Save your result in a variable called dat.

</br>
</br>

***

Hopefully this exercise forced you to look at the differences in the default values of the parameters in these different functions. I suggest that you keep these in mind as we look at some functions that were aimed to make a few typing shortcuts. Let's load the readr library.



Use read_csv() to read in your metadata file. What is different from read.csv?


Note that readr tells you exactly how it parsed your file, and how each column is encoded.   

***

But what happens if we have a good, old-fashioned excel file? The _readxl_ package will recognize both xls and xlsx files. It expects tabular data.



This doesn't look like a workbook. Why not? The read_excel function defaults to reading in the first worksheet. You can specify which sheet you want to read in by position or name. Let's see what the name of our sheets are.



Note that the argument to both of these functions was the path to our data sheet. We can save this path into a variable. You can also subset using cell numbers or ranges.






You can also use a list version of the apply function to read in all sheets at once. Each sheet will be stored as a data frame inside of a list object. You can subset the sheet you would like to work with (or work with all sheets at once - see the purrr package for working with list objects).




At this point, you will be able to use your excel worksheet as a normal data frame in R.

***

_Googlesheets_ have a similar structure to excel workbooks, the only tricky thing is getting the name of your googlesheet to input.

If you load googlesheets and ask it to list the googlesheets you have, googlesheets will open a new window and ask if it can have access to your googlesheets. If you say yes, you can return to R and breathe a sigh of relief. Your import of your googlesheets worked.



Register the sheet you are going to use with the sheet title.



How many worksheets are in this spreadsheet and what are their names?





Read in the worksheet you want to access. You can do this using the worksheet number.



The last 2 columns don't hold much information. Specify a subset of this sheet. You can do this by selecting the cell columns, or by using the 'excel-like' cell range.



You can also specify the worksheet by name, and sort by rows. Here are the top recommendations for what to read, when you are no longer in academia.




One nice thing about the googlesheets package is that all of the functions begin with gs_ which is great for finding functions and tab completion.


You 'download' ie. save this file to your computer.


You can upload sheets you've made to googlesheets. This file is now in your google account online.




***
__Challenge__ 

<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/turtle_challenge.jpg){width=100px}
</div>

Read in one of the provided test sheets. Change the column names to something user friendly. How many rows and columns in the dataset? Can you delete the last column? What flavour of variables are there? Write the data to a csv file. 

</br>

</br>

__Bonus:__ 
<div style="float:left;margin:0 10px 10px 0" markdown="1">
![](img/bonus_pow.jpg){width=100px}
</div>

Try reading in one of your own datasets. Write it to a different file format. 

</br>
</br>

***

  
#Resources
https://github.com/eacton/CAGEF
https://github.com/patrickwalls/R-examples/blob/master/LinearAlgebraInR.Rmd     
http://stat545.com/block002_hello-r-workspace-wd-project.html  
http://stat545.com/block026_file-out-in.html     
http://sisbid.github.io/Module1/
https://github.com/tidyverse/readxl
https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf
https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/
http://stat545.com/help-general.html
https://stackoverflow.com/help/how-to-ask     
https://www.r-project.org/posting-guide.html
https://github.com/jennybc/googlesheets


#Post-Lesson Assessment
***

Your feedback is essential to help the next cohort of trainees. Please take a minute to complete the following short survey:
https://www.surveymonkey.com/r/GD3KJB9

</br>

***

</br>

Thanks for coming!!!

![](img/rstudio-bomb.png){width=300px}