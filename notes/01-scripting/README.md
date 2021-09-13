# Scripting

In this section we will go over the general flow of using R projects, scripts, and git.

## Creating an R Project

R projects are helpful in many ways. One of the first benefits is how it takes care of the working directory.

We will use a new R project for each section of this "course"(?)

To do so, click *File* -> *New Project...* -> *Existing Directory* and navigate to the folder 01-scripts in the R_for_research repository and select it.

## RStudio and R

At the bottom left of Rstudio, there should be tabs for both _Console_ and _Terminal_.

_Terminal_ is similar to using gitbash.

_Console_ is an R instance.

There are some similarities between the two, but keep in mind that _Console_ is interpreted by R.

For instance, both _Terminal_ and _Console_ can return the current working directory.

In _Terminal_ you would enter the command

```
$ pwd
```

In _Console_ you would use the R function

```
> getwd()
```

From now on, if not explicitly stated, using the `$` will indicate a command that should be entered at the _Terminal_, while a `>` will indicate a command to be entered at the _Console_.

### Scripts

Since R is scripting language, it is not compiled. In compiled languages, source code must be *compiled* to machine-readable code before running. Non-compiled languages (like R and Python) are interpreted at *run time*.

In some ways, this simplifies development.

To illustrate this, we can create a list called "names" by entering this in the _Console_:

```
> names <- c("John", "Jay", "Rich")
```

*Note*:

* In R, `<-` is the preferred assignment operator. The keyboard shortcut for creating this symbol is `alt` + `-`.

  * However, `=` is also used, but for things like indicating values of keyword arguments, as we will see later.

  * Also, keep in mind that `==` is used for comparisons, like `if (name == "John") {do something}`

* `c()` is simply shorthand notation for the `list()` function


While you can create the `names` list by entering the above command at the _Console_ for most purposes, you will enter code in a script.

This can be done by clicking *File* -> *New File* -> *R Script*, or by clicking the + Button below *File*, or with the shortcut ctrl+shift+n.

In this script, you can type that same command as above. To run that line you can use the shortcut ctrl+enter

You will see that the line is actually run in the _Console_, so effectively, it is identical to typing it into the _Console_, but by placing it in a file, it is much easier to edit.

You can save this file with ctrl+s, and name it "create_names.R"


### Environment

In the top right pane of RStudio, you will now see that your environment has the list variable `names`.

The ability to explore environment variables is extremely useful in RStudio as you work with data.

### Using git

Now that we have a new file in our repository, it is a good chance to add it to git.

At this point, git sees that there is a new file which is not currently being tracked. You can see this by entering

```
$ git status
```

At the _Terminal_ enter

```
$ git add create_names.R
```

This has told git, "Hey, start keeping track of this file". You can see that git now knows the file is being tracked with

```
$ git status
```

Next we will commit this change to our repo (the change being adding the file) with a descriptive `-m`essage such as

```
$ git commit -m 'add create_names.R'
```

Once you have added a file to git and committed that add, when you make changes you will specify the file you are committing changes for. For instance, if you make a change to the file such as adding a new name, you would then enter

```
$ git commit -m 'add a new name' create_names.R
```

You can make as many local commits as you want, but eventually, you will want to push it to your GitHub repository to keep it backed up.

```
$ git push
```

## Summary

* _Console_ in Rstudio is interpreted by R
* Running a script is essentially the same as entering the same code in the _Console_
* Some useful git commands
  * `git status` to see how your working tree is looking
  * `git add` to tell git to track a file
  * `git commit` to commit changes to the working tree
  * `git push` to push local commits to the remote repository
  
## Bonus

It is important to know how to use git from the command line, because it is consistent across any language or project, whether you are using R, Python, or Rust. However, I wanted to note that most IDEs (such as RStudio) have git integration. In Rstudio, you can click the git button next to the `Go to file/function` bar and select commit. This can be useful for seeing how files have changed, commiting and pushing changes.

