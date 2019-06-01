# An Introduction to R and R Studio!
R is a programming language and free software environment for statistical computing and visualizations (i.e. making graphs). R is widely used among statisticians and data miners for developing statistical software, but has also become the workshorse for scientists across disciplines for its flexibility, speed, and cost (open source). R is written primarily in C, Fortran and R itself and is freely available under the GNU General Public License.

You can download R here:
[The R Project for Statistical Computing](https://www.r-project.org)

R is already installed on your Macbook Pro computers, and you can open an R environment easily in the terminal by simply typing the command:
```
R
```

However, for this introduction we are going to use a tool called ___R Studio___ as our R environment. ___R Studio___ should already be installed on your computers as well.  You can open ___R Studio___ by searching for it on your computers (click on the magnifying glass in the upper right-hand corner and type "R Studio" and hit \<ENTER\>).

If ___R Studio___ is not available, you can download it at this link: [R Studio](https://download1.rstudio.org/desktop/macos/RStudio-1.2.1335.dmg)

Once open, ___R Studio___ should look something like this:
![Rstudio1](../images/rstudio1.png)

___R Studio___ combines a graphical user interface with R's terminal-like interface called the "console".  
Let's start by writing a new R script:
1.  Click on the "+" icon in the upper left
2.  Select "R script"

The ___R Studio___ interface should now have 4 windows.
- R script - upper left - where you build your script/code by combining commands and comments.
  - comment lines start with an "#" and are ignored by R
  - commands are interpreted or run by R in the console.
- R console - lower left - the R console, or command line interface where R commands are run
- Environment - upper right - list of the various objects (e.g., vectors, variables, data frames, etc) currently present
- Explorer - lower right - an explorer of the folders and files available in the current working directory.

# Now let's learn some R!!!
## Part 1:  Basic Math
R can easily perform basic math. For example, type in the console (the spaces are optional, I think it looks easier to read):
```R
6 + 5
```
Then try:
```R
1 + 120 - 6 * 2
```

*Note: R follows the standard order of operations.  Remember:* "**P**lease **E**xcuse **M**y **D**ear **A**unt **S**ally?"

```R
1 + (120 - 6) * 2
```

Here is a table of the various standard operators:

| Operator | Type | Description |
| :---: | :---: | :---: |
| + | arithmetic | addition |
| - | arithmetic | subtraction |
| / | arithmetic | division |
| * | arithmetic | multiplication |
| ^ | arithmetic | exponentiation |
| > | logical | greater than |
| < | logical | less than |
| >= | logical | greater than or equal to |
| <= | logical | less than or equal to |
| == | logical | equals (compare two objects) |

Some logical operation examples:
```R
5 < 7
124 >= 124
56 < 10
6 == 6
9 == 8
```

## Part 2: R variables/objects and data types
So yes, R can do all sorts of math for you, but so can a slide rule.  Let's start learning some more basics about the types of data R can understand and how to perform operations on those data.

First, in our 'R Script' (upper left), type a comment line to describe what we will be doing:
```R
# R Practice Session: Basic Variables
```
It is good practice to actually build your commands and scripts in the 'R Script' box, then run these commands in the console separately.  This allows you to add comments to supplement your commands, such as with notes or descriptions, make changes when there is an error, and to save the script.  This can thought of as your 'R notebook'.  Next, let's make some variables.  In your R script, on a new line, enter the following:
```R
a <- 5
b <- 7
a + b
```
The `<-` is the assignment operator that assigns values to a new variable. Now highlight your R script with the cursor and click on the 'Run' button. What happened?  You should notice that these lines were run in the R console below.  Does the result `12` make sense?

The most common types of data stored in R variables are:
- **vectors** - one dimensional list of items
  - numeric (e.g. 1,2,3,4,5)
  - character (e.g. "a", "B", "c", "D")
  - logical (e.g., TRUE, FALSE, FALSE, TRUE)
- **data frames** - two dimensional list of items (i.e., a table)

| day | count |
| :---: | :---: |
| Monday | 2 |
| Tuesday | 3 |
| Wednesday | 9 |
| Thursday | 1 |
| Friday | 6.7 |

- **matrices** - a special type of numeric, two-dimensional table for performing matrix operations
- **lists** - a combination of variables, such as one or more vectors, data frames, or matrices.

In your R script, make a new comment:
```R
# Vectors
``` 

Now let's build two vectors, one character and one numeric:
```R
day <- c("Monday", "Tuesday", "Wednesday", "Thurday", "Friday")
count <- c(2, 3, 9, 1, 6.7)
```
Notice that when using strings (or text), you must use quotations or else R expects them to be variables.  Also, the `c` means to combine the elements into a vector).  Highlight these lines and click on the `Run` icon. What do you notice?  _HINT: Look in the "Environment" box in the upper right_.

With a numeric vector, you can perform arithmetic operations on each element simultaneously. Type the following into your R script then execute the command.
```R
count + 1
``` 
Repeat with `day`:
```R
day + 1
```
Did you get an error?  Yeah, it's hard to do math on a string.  There are many other operations we can do to text strings, but we don't have time to learn them today.

You can also access individual elements of a vector if needed.  Enter the following commands into your R script then `Run` them:
```R
# Get the second item in the 'day' vector:
day[2]

# Get the third and fourth elements of the 'count' vector:
count[3:4]

# Combine the first element from 'day' and 'count' into a new variable called 'day1'
day1 <- c(day[1], count[1])
```
_Got complicated pretty quickly, huh?  We will talk about this one as a class._


Now data frames.  We can combine our two vectors into a data frame.  Enter these commands and `Run` them.
```R
# Build a data frame
data <- data.frame(day, count)
```

Similar to a vector, you can access specific elements by refering to their row and column indices:
```R
# Get the item in the 3rd row and 2nd column
data[3,2]

# Get all of column 1
col1 <- data[,1]

# Get all of row 5
row5 <- data[5,]
```

# Part 3: Functions
R naturally has numerous functions built-in to speed up your analyses. For example, how many rows and columns are in the `data` variable?  Use the `dim()` function:
```R
# Get the dimensions of a table (rows, columns)
dim(data)
```

Notice that the syntax for a function is the name of a function, then some object or variable inside of parentheses. Here is another example to get the mean and standard deviation of the `count` vector:
```R
# Get the mean
mean(count)

# Get the standard deviation
sd(count)
```
Some functions can also do creative things with strings.  For example, in the vector `day`, replace the text "day" with "is fun":
```R
# Modify the 'day' vector
sub("day", " is fun", day)

# Not sure of all the arguments to 'sub'? Read the manual.
help(sub)
```

Existing functions are great (we will learn more about this at the end), but one of the core features of R is the ability to build and customize _your own_ functions! As an example, we are going to build our own custom function to calculate the mean of a vector.  We will talk about this as a class:
```R
# Custom function to calculate the mean
mean.custom <- function(x) {
   total <- sum(x)
       n <- length(x)
     avg <- total / n
   return(avg)
}
```
Enter the function above into your R script, highlight it, then load it using the `Run` icon.
Now you can run the function `mean.custom` just like any other function in R!
```R
# Calculate the mean of 'count'
mean.custom(count)
```
Did it work?

## Part 4: Loading data
Generally, you will not be manually entering your data into R like we have done above.  It is much more common to load in an existing file, like a spreadsheet from Microsoft Excel or a simple delimited text file (tab or comma delimited). The CSV, or "comma separated values" format is perhaps one of the most common, so we will use that here as an example. First, let's download a practice CSV file from the internet. Click in the link [Here](https://people.sc.fsu.edu/~jburkardt/data/csv/biostats.csv) to download a CSV file called `biostats.csv`.  Don't worry, there are no viruses!

---

I have included a quick reference guide to common R functions [Here](./Rcard.pdf).  If you are ever unsure of how to use a function, try searching the internet (there are TONS of resources) or use the help menu:
```R
# Get the help manual for a function
help(mean)
```

