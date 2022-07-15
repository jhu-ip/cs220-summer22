---
id: final
layout: mathjax
title: "Final Project"
---

<div class='admonition caution'>
<div class='title'>Caution</div>
<div class='content'>
<ul>
<li>You are expected to work in a team of two or three.</li>
<li><strong>Due: Thursday July 28th at 11pm EDT (Baltimore time).</strong></li>
</ul>
</div>
</div>


## Learning Objectives

<div class='admonition success'>
<div class='title'>Objectives</div>
<div class='content'>
<p>To practice with:</p>
<ul>
<li>Reading and writing file data</li>
<li>Classes and objects</li>
<li>Constructors, destructors, assignment operators, and the rule of 3</li>
<li>Object-oriented design</li>
<li>Operator overloading</li>
<li>Trees (dynamic linked structures)</li>
<li>Recursion</li>
</ul>
</div>
</div>

## Overview

*Note: this is preliminary content. It should not be considered official
unless it is announced in class and posted to the course website.*

In this project, you will implement a program to render images based on
plotting mathematical functions.

### An example plot

Here is an example plot input file. (This is available as `input/example04.txt` in
the starter files.)

```
Plot 0 -2.5 40 2.5 640 480
Function fn1 ( sin x )
Function fn2 ( * 1.6 ( cos x ) )
Color fn1 100 100 255
Color fn2 100 255 100
FillBetween fn1 fn2 0.4 128 0 200
```

This plot produces the following image (click for full size):

<a href="img/final/example04.png"><img class="keep_original_size" style="width:480px;" alt="plot image from the example04.txt input" src="img/final/example04.png"></a>

Here is a quick overview of the meaning of the example plot input file:

* The `Plot` directive indicates that the plot will show the region
  of the x/y coordinate plane where $$0 \le x \le 40$$ and $$-2.5 \le y \le 2.5$$,
  and the generated image will have the dimensions 640x480
* The first `Function` directive indicates that the function called
  `fn1` will plot the function $$y=\sin x$$
* The second `Function` directive indicates that the function called
  `fn2` will plot the function $$y=1.6 (\cos x)$$
* The first `Color` directive indicates that the plot of `fn1` will use
  the color $$(100,100,255)$$ (colors are RGB triples, with color component
  values in the range 0–255)
* The second `Color` directive indicates that the function called `fn2`
  will use the color $$(100,255,100)$$
* The `FillBetween` directive indicates that the area between `fn1` and
  `fn2` should be filled with the color $$(128,0,200)$$ at an opacity
  of $$0.4$$

The detailed semantics of the various directives are described below.

## Getting started

To get started on the project, use `git clone` to clone the final project
repository we have created for you. Also, use `git pull` to make sure that
your clone of the `cs220-summer22-public` repository is up to date.
Then, copy the starter files into your final project repository.
Assuming your current directory is your clone of your team's final project
repository, you could use the following commands to copy the files:

```
cp -r ~/cs220-summer22-public/projects/final/* .
cp ~/cs220-summer22-public/projects/final/.gitignore .
```

Once you have copied the starter files, use `git add`, `git commit`,
and `git push` to incorporate them into your team's repository.
