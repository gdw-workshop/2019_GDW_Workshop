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

_Note: R follows the standard order of operations.  Remember:_ "__P__lease __E__xcuse __M__y __D__ear __A__unt __S__ally?"

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

## Part Two: R variables/objects and data types
So yes, R can do all sorts of math for you, but so can a slide rule.  Let's start learning some more basics about the types of data R can understand and how to perform operations on those data.

First, in our 'R Script' (upper left), type a comment line to describe what we will be doing:
```R
# R Practice Session: Basic Math
```
It is good practice to actually build your commands and scripts in the 'R Script' box, then run these commands in the console separately.  This allows you to add comments to supplement your commands, such as with notes or descriptions, make changes when there is an error, and to save the script.  This can thought of as your 'R notebook'








