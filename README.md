# single-branch-test
This repository is created in order to answer the following question:
- Will the ``git clone`` command with the ``-b <branch-name> --single-branch`` options download the entirity of the files from the repo onto the local, or not?

The experiment exhibited will answer the question and help the user better understand essential internal git architecture, so, follow along for best results.

# The Experiment
The following steps describe an experiment that you, as a user, can conduct, in order to solve this mystery.

- On your local machine pick a directory where you will clone 2 versions of this repository.
- For the first version use the following command: 

```console
git clone https://github.com/iwannabeacookie/single-branch-test/ <path>
```

This command, naturally, clones the repo onto your local machine.
Pay attention to the verbose response of the command: the amount of objects copied and the size of the created directory.
Inside the repo you can see two branches - `main` and `single`. They both contain the markdown file and one of them - an image of one of the greatest works of humankind\*.

- Navigate back up the directory and execute the following command:

```console
git clone https://github.com/iwannabeacookie/single-branch-test/ -b main --single-branch <other-path>
```

Unlike the previous command, this contains options that exclusively clone the ``main`` branch from the remote.
Once again, pay attention to the output and compare it to the output of the previously executed command.

- Finally, one can compare the sizes of the two created directories in the file browser or the console to further conclude the expreriment.

# Explanation
One of the most important things to understand about git is that it stores **commits**, not files.

A **commit** is a git object. Git also implements other objects, but the most essential ones (or at least the ones we would ever care about) are **commits**, **trees** and **blobs**.

We already know what commits are, but what are **trees** and **blobs**?

**Trees** are somewhat of hashmaps, associating objects together. Trees compose and describe the hierarchy of directories and files of your repository in a specific point of time, called a **commit**.

Finally, **blobs** contain data and files, compressed and done some other horrible things to.

**Blobs** and **trees** are the reason we could clone the repository without downloading an ioootgwohk\*. You see, the commits that we downloaded do not contain any references to ioootgwohk™ , therefore, git did not load unreferenced objects, saving us a mb. 
