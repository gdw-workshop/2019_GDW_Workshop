## Command-line clinic, continued 

### Paths: absolute, relative, and the $PATH

This morning, Bob introduced you to the concept of a path in unix, and explained how paths relate to the heirarchical filesystem.  Let's briefly revisit that topicby discussing absolute paths, relative paths, and the $PATH.  

#### absolute paths

Absolute paths start at the root of the filesystem.  In other words, absolute paths start with `/`.  `/Users/gdw/Desktop` is an absolute path. 

**Absolute paths always refer to the same place, no matter what your present working directory is**

#### relative paths

Relative paths don't start with an `/`.   `./Desktop` and `Desktop` and `../Desktop`  are all relative paths.  What they refer to depends on where you are. 

**A relative path's meaning depends on your present working directory**

#### $PATH

The $PATH has a special meaning in unix environments.  The $PATH is a list of directories where the shell will look for commands.  If you didn't have the $PATH, you'd always have to type the full path (absolute or relative) of a command to run it.

What is your $PATH?   The $ at the beginning of $PATH is a hint: in the bash shell, names that begin with $ are variables, and $PATH is what's called an [environmental variable](https://en.wikipedia.org/wiki/Environment_variable).  Here are two ways to find your $PATH:

- Run the `env` command in the terminal.  Do you see your $PATH?
- Run `echo $PATH` in your terminal.  

Can you recognize what other environmental variables mean?

#### The $PATH and the `which` command

The which command will you tell you where in the filesystem a command is, or more specically whether a command exists in your $PATH.  To see a description of this command, run:

```
man which
```

Not to be confused with a [manwich](https://manwich.com/) ![manwich](./manwich.jpg)

The `man` (manual) command is a great way to get more information about built-in linux commands.  You can page through a manual page using the up and down arrows or the space bar.  Press q to exit.  

OK, back to which.  All of the commands you run, even really basic ones like `ls` and `cd`, are just a file somewhere in your path.  To find out where they are, try typing:

```
which ls
which cd
```

The $PATH is a convience, so that instead of always typing:

```
/bin/ls
```

You can just type `ls`.  

Other software that you might install can also be found by which:

```
which blastn
which bowtie2
```

Note that all these commands are in your $PATH.   Let's try something.  Let's change your path:

```
cd
export PATH=/Users/gdw
```

What do you think the impact of this change will be?  Try this:

```
env
```

How about these two commands?

```
ls
/bin/ls
../../bin/ls
../bin/ls
```

What's going on?  Why do all these commands work or not work?


### Aliases

Creating command aliases can be a convenient shortcut.  This allows you to define a new command or to redine the meaning of a command, for instance:

```
alias 'ls=ls -G'
ls
alias 'll=ls -l'
ll
```

Want to know what the `-G` and `-l` options do for `ls`?  See `man ls`.

Now, with these aliases, when you type `ls`, the shell will replace `ls` with `ls -G`.  And when you type `ll`, it will replace `ll` with `ls -l`, which will in turn be expanded to `ls -G -l`


### Installing software from the command line

Installing software in a linux command-line environment can be a roadblock to beginners.  Let's practice installing a bioinformatics tool from the command line.

We'll install jellyfish, a tool for counting [k-mers](https://en.wikipedia.org/wiki/K-mer).  The main webpage for Jellyfish can be found [here](https://github.com/gmarcais/Jellyfish).  If you scroll down that page, you will find installation instructions that direct you to the [releases page](https://github.com/gmarcais/Jellyfish/releases).

Here you find there are two options:

1. You can download a so-called pre-compiled binary.  Pre-compiled binaries are ready to go, but you must download a file that is matched to your operating system.  Since we are working on mac laptops, you want to download the jellyfish-macosx file from github

2. You can download the source code for the software and compile it to create a binary program file yourself. Sometimes this is the only option, for example for [minimap2](https://github.com/lh3/minimap2/releases), a program we'll use later this week.  


Let's first try downloading the pre-compiled binary.  Download the file named jellyfish-macosx
``` 
cd
curl -OL https://github.com/gmarcais/Jellyfish/releases/download/v1.1.12/jellyfish-macosx
```

Type `ls -l` (or `ll`) to confirm that you have a file named jellyfish-macosx that has a size of 434 kb.  Note that you can also type `ls -lh` or `ll -h`.  The -h option to `ls` outputs file sizes in a **h**uman readable format.

Now that we have the file, let's try to run it.  That was the point of downloading it, after all.  Try typing:

```
jellyfish-macosx
```

