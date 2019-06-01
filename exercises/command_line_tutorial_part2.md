## Command-line clinic, continued 

### Paths: absolute, relative, and the $PATH

This morning, Bob introduced you to the concept of a path in unix, and explained how paths relate to the heirarchical filesystem.  Let's briefly revisit that topicby discussing absolute paths, relative paths, and the $PATH.  

#### absolute paths

Absolute paths start at the root of the filesystem.  In other words, absolute paths start with `/`.  `/Users/gdw/Desktop` is an absolute path. 

**Absolute paths always refer to the same place, no matter your present working directory**

#### relative paths

Relative paths don't start with an `/`.   `./Desktop` and `Desktop` and `../Desktop`  are all relative paths.  What they refer to depends on where you are. 

**A relative path's meaning depends on your present working directory**

#### PATH

The PATH has a special meaning in unix environments.  The PATH is a list of directories where the shell will look for commands.  If you didn't have the PATH, you'd always have to type the full path (absolute or relative) of a command to run it, which would be annoying.

PATH is what's called an [environmental variable](https://en.wikipedia.org/wiki/Environment_variable).  Here are two ways to find your PATH:

- Run the `env` command in the terminal.  Do you see your $PATH?
- Run `echo $PATH` in your terminal.  

Can you recognize what other environmental variables mean?

#### The PATH and the `which` command

The which command will you tell you where in the filesystem a command is, or more specically whether a command exists in your PATH.  To see a description of this command, run:

```
man which
```

Not to be confused with [manwich](https://manwich.com/) ![manwich](./manwich.jpg)

The `man` (manual) command is a great way to get more information about built-in linux commands.  You can page through a manual page using the up and down arrows or the space bar.  Press q to exit.  

OK, back to `which`.  All of the commands you run, even basic ones like `ls` and `cd`, are just a file somewhere in your path.  To find out where they are, run:

```
which ls
which cd
```

The PATH is a convience, so that instead of always typing:

```
/bin/ls
```

You can just type `ls`.  

Other software that's not a core part of the operating system, for instance the blastn and bowtie2 aligners, can also be found by `which`:

```
which blastn
which bowtie2
```

Note that all these commands are in your PATH.   Let's try something.  Let's change your PATH:

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

What's going on?  Why do these commands work or not work?

### Installing software from the command line

Installing software in a linux command-line environment can be a roadblock to beginners.  Let's practice installing a bioinformatics tool from the command line.

We'll install jellyfish, a tool for counting [k-mers](https://en.wikipedia.org/wiki/K-mer).  The main webpage for Jellyfish can be found [here](https://github.com/gmarcais/Jellyfish).  If you read that page, you will find installation instructions that direct you to the [releases page](https://github.com/gmarcais/Jellyfish/releases).

Here you find there are two options:

1. You can download a so-called pre-compiled binary.  Pre-compiled binaries are ready to go, but you must download a file that is matched to your operating system.  Since we are working on mac laptops, you'd want to download the jellyfish-macosx file from github

2. You can download the source code for the software and compile it to create a binary program file yourself. Sometimes this is the only option, for example for [minimap2](https://github.com/lh3/minimap2/releases), a program we'll use later this week.  


Let's first try downloading the pre-compiled binary.  Download the file named jellyfish-macosx
``` 
cd
curl -OL https://github.com/gmarcais/Jellyfish/releases/download/v1.1.12/jellyfish-macosx
```

`curl` is a program that will download files from the internet.

Type `ls -lh` to confirm that you have downloaded a file to the pwd named jellyfish-macosx that has a size of 434 kb.  The `-h` option to `ls` outputs file sizes in a **h**uman readable format and the `-l` option outputs a more detailed "**l**ong" listing.

Now that we have the file, let's try to run it.  That was the point of downloading it, after all.  Try typing:

```
jellyfish-macosx
```

You should have gotten an error like this:

```
-bash: jellyfish-macosx: command not found
```

What do you think is going on?

<br><br><br><br> <br><br><br><br> <br><br><br><br> <br><br><br><br> 

One issue is that the file jellyfish-macosx is not in your $PATH.  Or more accurately, jellyfish-macosx _is_ in your home directory, and your home directory is not in your $PATH.  Let's confirm this by using the which command again:

```
which jellyfish-macosx
```

To fix this situation, we could either move the jellyfish file into a directory in your PATH, or could add your home directory to your $PATH.  The first option would manifest as:

```
# option 1: move jellyfish to a directory already in your $PATH
sudo mv jellyfish-macosx /usr/local/bin
```

Note that you had to use the sudo (**s**uper **u**ser **do**) command to move jellyfish to /usr/local/bin.  This is because you lacked the necessary permissions to move a file into that directory.  Running commands prepended by sudo is the same as doing something with Administrator priveleges (so be careful!).

The second option would be:
```
# option 2: add ~ to your $PATH
export PATH=$PATH:/Users/gdw
```

Here, you are changing the $PATH the way you are supposed to, by appending a new directory to the $PATH instead of overwriting it as we did above.  So bash interprets `PATH=$PATH:/Users/gdw` as "assign to the variable named PATH the current value of the variable PATH plus ":/Users/gdw" 

After either (or both) of these, jellyfish-macosx should now be in your $PATH.  let's see what happens:

```
which jellyfish-macosx
jellyfish-macosx
```

You should see an error like this:

```
-bash: /usr/local/bin/jellyfish-macosx: Permission denied
```

Arrgh!  This is why people get frustrated with the command line.  Let's power through!

#### Permissions

This gets us to another common pitfall for linux beginners: [file permissions](http://linuxcommand.org/lc3_lts0090.php).

Every file and every directory in linux has a set of permissions that tell whether the file or directory can be read, written, or executed.  

Your user lacked write permissions for `/usr/local/bin`, which is why you couldn't move a file into that directory, and had to use the `sudo` command, which gives you super privileges.  

Similarly, the jellyfish-macosx file that you downloaded did not arrive with executable permissions. And in order to be run as a command, a file needs executable permissions.  

Let's check the permissions on jellyfish:

```
ls -l /usr/local/bin/
```

When you list a file using the `-l` option, the first part of the output for each file is the permissions, which look like this:

```
-rw-r--r--
```

These permissions have this meaning: ![permissions](./file_permissions.png)

You can see that this file indeed lacks e**x**ecutable permissions.  We can change that by running:

```
chmod +x /usr/local/bin/jellyfish-macosx
```

Now try running:

```
jellyfish-macosx
```

Phrew.  

Jellyfish got a little mad because you didn't supply enough arguments, but at least it ran!  That's a good sign.  You may also note that it outputs usage information about how to actually run it, which most well-written software should do.  You can also see that it has a `--help` option, which is another common feature of good software (sometimes the option is `-h` or `-help`).  


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
