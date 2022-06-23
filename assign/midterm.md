---
id: midterm
layout: default
title: Midterm Project
---

<div class='admonition caution'>
<div class='title'>Caution</div>
<div class='content'>
<ul>
<li>You are expected to work in a team of two or three.</li>
<li><strong>Due: Friday July 1st at 11pm EDT (Baltimore time).</strong></li>
<li><em>This assignment is worth 140 points.</em></li>
<li>No late days are allowed!</li>
</ul>
</div>
</div>

## Introduction

<div class='admonition danger'>
<div class='title'>Danger</div>
<div class='content'>
<p>All programs <strong>must</strong> compile (and run) on the ugrad machines using our standard compiler options.</p>
</div>
</div>

In this project, you will work as a team of two to implement a dynamic ASCII art program that can convert any _word_ (composed of digits and alphabet only) or image to ASCII art _dynamically_. The program will provide instructions on screen so that users can interact with it to select which ASCII art font to use, display the ASCII art font to check, input a word or read an image to convert to ASCII art. 

As a paired project, you should practice pair programming to work synchronously with your partner(s) in driver/navigator roles to design and implement the program. You should frequently work together, in particular when you are testing and debugging your program. Remember, you are both responsible for all the code you submit.

<!--
<div class='admonition info'>
<div class='title'>Note</div>
<div class='content'>
<p>Students who cannot attend class synchronously should find a partner in the same time zone!</p>
</div>
</div>
-->

<div class='admonition tip'>
<div class='title'>Working remotely</div>
<div class='content'>
<p>To work remotely together, you may consider granting access control to your partner during a Zoom session so that both of you can work on a shared screen to code, test and debug the program together.</p>
</div>
</div>

As before, you are required to use the `git` version control system and include a *log file* with your project submission. You should have registered your team [here](https://piazza.com/class/kovkwe85rjy4ec?cid=106) by *Tuesday June 22nd at noon*. Otherwise, we will pair you up with a classmate. A private repository named something like `2021-summer-midterm-<JHED1>-<JHED2>` has been created for your team. You have to use this repository for your midterm project development.

This project is larger and more complex than previous programming assignments. Additionally, since you have now been exposed to most of what C can do, there are no restrictions on what language features you can use (other than the conventions of good style, of course; you still shouldn't use global variables, for example). You’ll want to start early and make steady, incremental progress towards completing the project requirements.

<div class='admonition tip'>
<div class='title'>Tip</div>
<div class='content'>
<p>From this point forward in the semester, your programs will need to not only compile and run cleanly (i.e. with <strong>no warnings, errors, or crashes</strong>), but also not have any <strong>memory leaks</strong> (as reported by valgrind).</p>
</div>
</div>

## Getting started

### Set up your midterm project git repository
- If you have registered your team on time, you will see the private repo (`2021-summer-midterm-<JHED1>-<JHED2>`) under your repositories on GitHub.
- Otherwise, you should receive a private post from us about your assigned partner and repository on Piazza. You must reply to the post to exchange your contact information with your teammate and let us know if there is any problem to kick off the project. **If you have not received the post, reach out to us as soon as possible.**

Once you have access to `2021-summer-midterm-<JHED1>-<JHED2>`, you should clone the repo to your ugrad Unix account (and optionally local machine) the same way you cloned your personal repo in [Ex2 Part 4](https://jhu-ip.github.io/cs220-summer21/docs/exercises/ex2/#part-4---git).

<div class='admonition info'>
<div class='title'>Info</div>
<div class='content'>
<p>If you have opted to use SSH authentication, remember to clone it with the <code>git@</code> link. Otherwise, you should use the <code>https://</code> one.</p>
</div>
</div>

### Get the starter codes from `cs220-public`
1. Use `cd` to move into `cs220-public` on your Unix account, type `git status` and confirm you have not modified any files or accidentally committed to the public repository. Ask for help if you need to undo those accidental changes.

2. Type `git pull` to synchronize your local repository with the remote one.

3. You should see a new directory called `midterm`, which contains the starter code. There will be nine source files: `dialog.[c|h]`, `print_functions.[c|h]`, `project.c`, `structures.[c|h]`, `validation.[c|h]`, and some text files. There will also be some *.ppm image files.

4. Copy the files in `midterm` to your midterm project repository. Assuming both the public and your midterm repositories are under your home directory, you may run `cp ~/cs220-public/midterm/* ~/cs220-public/midterm/.gitignore ~/2021-summer-midterm-<JHED1>-<JHED2>/` to copy the starter codes to your local midterm repository. 

5. Use `cd` to move into your midterm repository (e.g. `cd ~/2021-summer-midterm-<JHED1>-<JHED2>`), type `git status` and confirm you see all the starter files.

6. Do your first commit to add the starter codes to the repository and push them to the remote repository. You can run `git add .`, `git commit -m "Initialized with the starter codes"`, and `git push`.

Your midterm repository is now ready for development!

<div class='admonition tip'>
<div class='title'>Tip</div>
<div class='content'>
<p>Only one of the team members needs to set up the repo when it is the first use. Once it has been set up, the partner can get the starter codes directly by cloning the remote repo or synchronizing their local repositories (<code>pull</code>).</p>
<p>You will now work in a team. You may encounter conflicts more often when you push your code from local to remote. This happens when your teammates have changed the same files and same segments as you have done. If it happens, you will need to resolve the conflicts, compile and test your codes before committing the conflict-resolved version. Typically you will see something like below in the file that has a conflict:</p>
<pre><code>&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD
This is how the file in the current remote (github) repo looks

=======
This is how the file in your local repo looks

&gt;&gt;&gt;&gt;&gt;&gt;&gt; &lt;a commit id&gt;
</code></pre>
<p>To resolve the conflict, you need to decide which version to use or how they should be merged. To minimize the conflicts, you should</p>
<ul>
<li>Communicate with your teammates to avoid editing a file at the same time,</li>
<li>Always sync with the remote before you start working (pull), and</li>
<li>Commit and push often</li>
</ul>
</div>
</div>

## Overview - dynamic ASCII art

Here is a sample run of the program to give you an overview of how the program should look:

```
$ ./project
--------------------------------------------
Usage: ./project <font config file>
--------------------------------------------
$ ./project font_config.txt
--------------------------------------------
Number of fonts loaded: 3
"line", "star", and "contour"
--------------------------------------------
Welcome to the ASCII art generation program!
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 2
--------------------------------------------
Please enter a word: cs220
--------------------------------------------
+--------+--------+--------+--------+--------+
  _/_/_/   _/_/_/    _/_/     _/_/    _/_/_/
 _/    _/ _/    _/  _/  _/   _/  _/  _/    _/
 _/         _/         _/       _/   _/    _/
 _/           _/      _/       _/    _/    _/
 _/    _/ _/    _/   _/       _/     _/    _/
  _/_/_/   _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 1
--------------------------------------------
Please enter a filename: cs220.txt
File saved as "cs220.txt"!
--------------------------------------------
+--------+--------+--------+--------+--------+
  _/_/_/   _/_/_/    _/_/     _/_/    _/_/_/
 _/    _/ _/    _/  _/  _/   _/  _/  _/    _/
 _/         _/         _/       _/   _/    _/
 _/           _/      _/       _/    _/    _/
 _/    _/ _/    _/   _/       _/     _/    _/
  _/_/_/   _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 3
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 3
--------------------------------------------
Please enter an image filename: bluejay.ppm
--------------------------------------------
WWWWWWWWWWWWWW888WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWH*-.---.-UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWH-.*8WWH*.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWW8*.UWWW8--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWU.TW88WU.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWH.TWUHWH.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWH.HWTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWT-WHTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW-H8TTHWH-UUUUHHHHH88WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWW8HUT*--.TWTTTHWU.******---.....--*TUH8WWWWWWWWWWWWWWWWWWWWWWW
WWWWWW8HU*-..-*TUH8U-WUTTT8W*HWWWWWWWWWWWW88HUT*-..-*UHWWWWWWWWWWWWWWWWWW
WW8T-..-*UHWWWWWWWWU-WUTTTTW8*WWWWWWWWWWWWWWWWWWWWWHU*-..-T8WWWWWWWWWWWWW
WT.TH8WWWWWWWWWWWWWU-WUTTTTHWHTWWWWWWWWWWWWWWWWWWWWWWWWW8HT.UWWWWWWWWWWWW
8.8WWWWWWWWWWWWWWWW-TWTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWWW8.8WWWWWWWWWWW
U*WWWWWWWWWWWWWWWHU-W8TTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWW**HWTTTTTTTTHWUTWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
UTWWWWWWWWWWWWWW8.HWHTTTTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWH.WWUTTTTTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WWTTTTTTTTTTTHWH*WWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WHTTTTTTTTTTTT8WTTWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWTUW8TTTTTTTTTTTTTWW*UWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWH*W8TTTTTTTTTTTTTTWW*HWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWW*88TTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWWUTWUTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
H-WWWWWWWWWWWWWWW-TWWTTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWW-HWWWWWWWWWWW
H-WWWWWWWWWW8UT*-.8WW8TTTTTTTTTTTTTTTUWW*UWWWWWWWWWWWWWWWWWW-8WWWWWWWWWWW
8.WWWWWWW8T..*TUHHWWWWWTTTTTTTTTTTTTTTTWWTTWWWWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.WWWWW8*.*HWWWWW8WWWWWWHTTTTTTTTTTTTTTT8WU*8WWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.8WWWT.*8WWHUTTTTT8WWWWWWHTTTTTTTTTTTTTTHW8-HWWWWWWWWWWWWW8-WWWWWWWWWWWW
W-HW8--8WWUTTTTTTTTUWWWWWWWW8HTTTTTTTTTTTTHWW*UWWWWWWWWWWWWH*WWWWWWWWWWWW
W*UH.TWWUTTTTTTTTTUWWWWWWWWWWWWW8UTTTTTTTTTUWWTTWWWWWWWWWWWU*WWWWWWWWWWWW
WT..UW8TTTTTTTTTTTWWWWWWWWWWWWWWWWW8UTTTTTTTTWWTUWWWWWWWWWWTTWWWWWWWWWWWW
WU.HWHTTTTTTTTTTTHWWWWWWWWWWWUU**HWWWHTTTTTTTTWW*UWWWWWWWWW*HWWWWWWWWWWWW
W8.W8TTTTTTTTTTTT8WWWWWWWWWWU*....-HWW8TTTTTTTTWW*8WWWWWWWW.8WWWWWWWWWWWW
WW.88TTTTTTTTTTTTWWWWWWWWWWU-.......TWW8TTTTTTTUWH*WWWWWWW8-WWWWWWWWWWWWW
WW-UWTTTTTTTTTTTTWWWWWWWWWH..........TWWHTTTTTTT8WTHWWWWWWH*WWWWWWWWWWWWW
WWTTWTTTTTTTTTTTUWWWWWWWWWH...........HWWTTTTTTTTW8*WWWWWWTTWWWWWWWWWWWWW
WWH-WUTTTTTTTTTTTWWWWWWWWWW*........T88WWUTTTTTTTHWTHWWWWW-HWWWWWWWWWWWWW
WWW.88TTTTTTTTTTTWWWWWWWWWWWT......UHU8WWWTTTTTTTTWHTWWWWW.WWWWWWWWWWWWWW
WWW-UWTTTTTTTTTTT8WWWWWW8UTTHH-...*HHWW*8W8TTTTTUU8W*WWWWH-WWWWWWWWWWWWWW
WWWT*WUTTTTTTTTTTHWWWWWH-.....--..HUWW8.-WW8TU8W88WWT8WWWTTWWWWWWWWWWWWWW
WWWH.WHTTTTTTTTTTTWWWW8-..........H8WWWUUWWW8WWWWWWWU*8WW.8WWWWWWWWWWWWWW
WWWW.HWTTTTTTTTTTTHWWWH..........-H8WWWWWWWWWWWWH***UH-UH-WWWWWWWWWWWWWWW
WWWWT*WTTTTTTTTTTTTWWWT...........HHWWWWWWWHWWWT.*TT*-8--TWWWWWWWWWWWWWWW
WWWW8.WHTTTTTTTTTTTTWWH...........UUWWWWWWWWW8U.8WWWWWWW--UWWWWWWWWWWWWWW
WWWWW-UWTTTTTTTTTTTTUWWU..........-8T8WWWWW*...HWWWUTUHWW8*.T8WWWWWWWWWWW
WWWWWU-WUTTTTTTTTTTTTT8W8-.......T.-8UUHWW-...*WWW-.....*HW8T.TWWWWWWWWWW
WWWWWW.H8TTTTTTTTTTTTTTHWWH*.....-HUTHWWWT..*UHWWWHTHW8T-.-UW8*.HWWWWWWWW
WWWWWWT*WUTTTTTTTTTTTTTTTHWWWU*-...UWWWWW-*8WWWWWWWWWWWWW8T..UWH-*WWWWWWW
WWWWWW8.88TTTTTTTTTTTTTTTTTTH88WWWWWWWWW8-8WWWWWWWWWWWWWWWWWU.-8WT-8WWWWW
WWWWWWW**WTTTTTTTTTTTTTTTTTTTTTUH8WWWWWWW*WWWW8UUUUH8WWWWWWWWWT.UWU.HWWWW
WWWWWWW8.88TTTTTTTTTTTTTTTTTH8WWHT-..-WWWU8WWWWWWW8HUT*THWWWWWW8-*WH.HWWW
WWWWWWWW**WUTTTTTTTTUTTTTTUWWH-.......HWWWWWWWWWWWWWWWWWHTTUWWWWWU-WH.8WW
WWWWWWWW8.H8TTTTTU8WUTTTTHWU..........*WWWWWWWWWWWWWWWWWWWW8UTHWWWH*WU-WW
WWWWWWWWWT-WUTTT8WWHTTTTHWT..........*WW8WWU*U8WWWWWWWWWWWWWWW8UUWW8TW-UW
WWWWWWWWWW-TWTTWHUWTU8TUWU..........UWH-*--UWHT-*UHWWWWWWWWWWWWWWTUW888.W
WWWWWWWWWWH.888H.8HUW8T8W*.........UWTTWWWWWWWWWWU...-*TUHH88WWWWW8*UWW-H
WWWWWWWWWWWT-WW--W8W8HUWH-........TWTUWWWWWWWWWWW-T8HUTT*--.....-*U8T-HTT
WWWWWWWWWWWW-TH.*WWT8U8WU........-WHTWWWWWWWWWWWT-WWWWWWWWWWWW88HT*..-.-T
WWWWWWWWWWWW8.*.TWH-WUWWU........H8*WWWWWWWWWWWH.8WWWWWWWWWWWWWWWWWWH*..T
WWWWWWWWWWWWWU..*W**WUWWT.......*WTHWWWWWWWWWW8-HWWWWWWWWWWWWWWWWWWWWWWTU
WWWWWWWWWWWWWWT..8-*WHWWT.......H8*WWWWWWWWWWW-TWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWW*.T.-W8WWU......-WUUWWWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWW*...8WWWH......TWT8WWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWW-..*W8WH......HW*WWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWW*..HH88......88TWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW*.-TUW-....-WHUWWWWWWW-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWT..-WU....-WUHWWWWW8-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWU..UWT...-WUHWWWWH.TWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWH..HWU..*WU8WWWT.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWW8-.UW8--WU8WH--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWT.*8W8WUUT.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWW8-.TWWT.*8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWU...-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWHHWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
--------------------------------------------
1) Save it to a file
2) Read another image
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 1
--------------------------------------------
Please enter a filename: bluejay.txt
File saved as "bluejay.txt"!
--------------------------------------------
WWWWWWWWWWWWWW888WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWH*-.---.-UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWH-.*8WWH*.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWW8*.UWWW8--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWU.TW88WU.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWH.TWUHWH.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWH.HWTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWT-WHTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW-H8TTHWH-UUUUHHHHH88WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWW8HUT*--.TWTTTHWU.******---.....--*TUH8WWWWWWWWWWWWWWWWWWWWWWW
WWWWWW8HU*-..-*TUH8U-WUTTT8W*HWWWWWWWWWWWW88HUT*-..-*UHWWWWWWWWWWWWWWWWWW
WW8T-..-*UHWWWWWWWWU-WUTTTTW8*WWWWWWWWWWWWWWWWWWWWWHU*-..-T8WWWWWWWWWWWWW
WT.TH8WWWWWWWWWWWWWU-WUTTTTHWHTWWWWWWWWWWWWWWWWWWWWWWWWW8HT.UWWWWWWWWWWWW
8.8WWWWWWWWWWWWWWWW-TWTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWWW8.8WWWWWWWWWWW
U*WWWWWWWWWWWWWWWHU-W8TTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWW**HWTTTTTTTTHWUTWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
UTWWWWWWWWWWWWWW8.HWHTTTTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWH.WWUTTTTTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WWTTTTTTTTTTTHWH*WWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WHTTTTTTTTTTTT8WTTWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWTUW8TTTTTTTTTTTTTWW*UWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWH*W8TTTTTTTTTTTTTTWW*HWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWW*88TTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWWUTWUTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
H-WWWWWWWWWWWWWWW-TWWTTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWW-HWWWWWWWWWWW
H-WWWWWWWWWW8UT*-.8WW8TTTTTTTTTTTTTTTUWW*UWWWWWWWWWWWWWWWWWW-8WWWWWWWWWWW
8.WWWWWWW8T..*TUHHWWWWWTTTTTTTTTTTTTTTTWWTTWWWWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.WWWWW8*.*HWWWWW8WWWWWWHTTTTTTTTTTTTTTT8WU*8WWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.8WWWT.*8WWHUTTTTT8WWWWWWHTTTTTTTTTTTTTTHW8-HWWWWWWWWWWWWW8-WWWWWWWWWWWW
W-HW8--8WWUTTTTTTTTUWWWWWWWW8HTTTTTTTTTTTTHWW*UWWWWWWWWWWWWH*WWWWWWWWWWWW
W*UH.TWWUTTTTTTTTTUWWWWWWWWWWWWW8UTTTTTTTTTUWWTTWWWWWWWWWWWU*WWWWWWWWWWWW
WT..UW8TTTTTTTTTTTWWWWWWWWWWWWWWWWW8UTTTTTTTTWWTUWWWWWWWWWWTTWWWWWWWWWWWW
WU.HWHTTTTTTTTTTTHWWWWWWWWWWWUU**HWWWHTTTTTTTTWW*UWWWWWWWWW*HWWWWWWWWWWWW
W8.W8TTTTTTTTTTTT8WWWWWWWWWWU*....-HWW8TTTTTTTTWW*8WWWWWWWW.8WWWWWWWWWWWW
WW.88TTTTTTTTTTTTWWWWWWWWWWU-.......TWW8TTTTTTTUWH*WWWWWWW8-WWWWWWWWWWWWW
WW-UWTTTTTTTTTTTTWWWWWWWWWH..........TWWHTTTTTTT8WTHWWWWWWH*WWWWWWWWWWWWW
WWTTWTTTTTTTTTTTUWWWWWWWWWH...........HWWTTTTTTTTW8*WWWWWWTTWWWWWWWWWWWWW
WWH-WUTTTTTTTTTTTWWWWWWWWWW*........T88WWUTTTTTTTHWTHWWWWW-HWWWWWWWWWWWWW
WWW.88TTTTTTTTTTTWWWWWWWWWWWT......UHU8WWWTTTTTTTTWHTWWWWW.WWWWWWWWWWWWWW
WWW-UWTTTTTTTTTTT8WWWWWW8UTTHH-...*HHWW*8W8TTTTTUU8W*WWWWH-WWWWWWWWWWWWWW
WWWT*WUTTTTTTTTTTHWWWWWH-.....--..HUWW8.-WW8TU8W88WWT8WWWTTWWWWWWWWWWWWWW
WWWH.WHTTTTTTTTTTTWWWW8-..........H8WWWUUWWW8WWWWWWWU*8WW.8WWWWWWWWWWWWWW
WWWW.HWTTTTTTTTTTTHWWWH..........-H8WWWWWWWWWWWWH***UH-UH-WWWWWWWWWWWWWWW
WWWWT*WTTTTTTTTTTTTWWWT...........HHWWWWWWWHWWWT.*TT*-8--TWWWWWWWWWWWWWWW
WWWW8.WHTTTTTTTTTTTTWWH...........UUWWWWWWWWW8U.8WWWWWWW--UWWWWWWWWWWWWWW
WWWWW-UWTTTTTTTTTTTTUWWU..........-8T8WWWWW*...HWWWUTUHWW8*.T8WWWWWWWWWWW
WWWWWU-WUTTTTTTTTTTTTT8W8-.......T.-8UUHWW-...*WWW-.....*HW8T.TWWWWWWWWWW
WWWWWW.H8TTTTTTTTTTTTTTHWWH*.....-HUTHWWWT..*UHWWWHTHW8T-.-UW8*.HWWWWWWWW
WWWWWWT*WUTTTTTTTTTTTTTTTHWWWU*-...UWWWWW-*8WWWWWWWWWWWWW8T..UWH-*WWWWWWW
WWWWWW8.88TTTTTTTTTTTTTTTTTTH88WWWWWWWWW8-8WWWWWWWWWWWWWWWWWU.-8WT-8WWWWW
WWWWWWW**WTTTTTTTTTTTTTTTTTTTTTUH8WWWWWWW*WWWW8UUUUH8WWWWWWWWWT.UWU.HWWWW
WWWWWWW8.88TTTTTTTTTTTTTTTTTH8WWHT-..-WWWU8WWWWWWW8HUT*THWWWWWW8-*WH.HWWW
WWWWWWWW**WUTTTTTTTTUTTTTTUWWH-.......HWWWWWWWWWWWWWWWWWHTTUWWWWWU-WH.8WW
WWWWWWWW8.H8TTTTTU8WUTTTTHWU..........*WWWWWWWWWWWWWWWWWWWW8UTHWWWH*WU-WW
WWWWWWWWWT-WUTTT8WWHTTTTHWT..........*WW8WWU*U8WWWWWWWWWWWWWWW8UUWW8TW-UW
WWWWWWWWWW-TWTTWHUWTU8TUWU..........UWH-*--UWHT-*UHWWWWWWWWWWWWWWTUW888.W
WWWWWWWWWWH.888H.8HUW8T8W*.........UWTTWWWWWWWWWWU...-*TUHH88WWWWW8*UWW-H
WWWWWWWWWWWT-WW--W8W8HUWH-........TWTUWWWWWWWWWWW-T8HUTT*--.....-*U8T-HTT
WWWWWWWWWWWW-TH.*WWT8U8WU........-WHTWWWWWWWWWWWT-WWWWWWWWWWWW88HT*..-.-T
WWWWWWWWWWWW8.*.TWH-WUWWU........H8*WWWWWWWWWWWH.8WWWWWWWWWWWWWWWWWWH*..T
WWWWWWWWWWWWWU..*W**WUWWT.......*WTHWWWWWWWWWW8-HWWWWWWWWWWWWWWWWWWWWWWTU
WWWWWWWWWWWWWWT..8-*WHWWT.......H8*WWWWWWWWWWW-TWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWW*.T.-W8WWU......-WUUWWWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWW*...8WWWH......TWT8WWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWW-..*W8WH......HW*WWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWW*..HH88......88TWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW*.-TUW-....-WHUWWWWWWW-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWT..-WU....-WUHWWWWW8-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWU..UWT...-WUHWWWWH.TWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWH..HWU..*WU8WWWT.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWW8-.UW8--WU8WH--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWT.*8W8WUUT.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWW8-.TWWT.*8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWU...-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWHHWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
--------------------------------------------
1) Save it to a file
2) Read another image
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 3
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 4
--------------------------------------------
Thank you for using the ASCII art generation program!
--------------------------------------------
```

This run produced two text files containing ASCII art of the word "CS220" and of the input image "bluejay.ppm": 
- [cs220.txt](cs220.txt) 
- [bluejay.txt](bluejay.txt)


## Program Specification
### Starter code, test program and Makefile

Starter files are provided for you. `git pull` your `cs220-public` repo; you should see the starter code. It contains:
1. `project.c` is the main driver function; it checks the command line arguments, loads the font config and starts the program loop. You don't need to modify it.
2. `dialog.[c|h]` contain functions related to the program control flow. In this project, the skeleton of the control flow is provided for you. You should not need to modify these two files.  However, you should read them carefully to understand the control flow.
3. `structures.[c|h]` contains useful `struct`s that you will use to implement this program. They are `config`, `font`, and `image`. You need to implement functions related to `config` and `font`, while functions related to `image` are provided for you.
4. `print_functions.[c|h]` provide all the print-related functionalities. You are going to implement all the functions declared there.
5. `validation.[c|h]` provide all the input validation-related functionalities. You are going to implement all functions declared there.
6. `font_config.txt`, `line.txt`, `star.txt`, and `contour.txt` are font-related files provided for testing.
7. `bluejay.ppm`, `jhusign.ppm`, and `gilman.ppm` are image files provided for testing.

In short, your task in this project is to implement all functions in `structures.c`, `print_functions.c`, and `validation.c`. In addition, you will need to write your own Makefile and a test program for all validation functions. We recommend you start with the Makefile. Your Makefile should compile each source file into an object file and then link them together into an executable target called `project`.

<div class='admonition info'>
<div class='title'>Info</div>
<div class='content'>
<p>If you are on ugrad (either locally or remotely with X-tunnelling), you can use the program <code>feh</code> to view ppm images. Otherwise, you are welcome to use an image viewer of your choice; <code>feh</code> is easy to install using most linux package managers, but there are other open-source image viewing programs, as well as alternatives for Windows and OSX.</p>
<p><code>feh</code> is a very simple command-line image viewer. It is available on ugrad machines, and you can simply run the program with the name of an image file as a command-line argument, and it will display the image on your screen. e.g.</p>
<div class="sourceCode" id="cb1"><pre class="sourceCode sh"><code class="sourceCode bash"><a class="sourceLine" id="cb1-1" title="1">$ <span class="ex">feh</span> myimage.ppm</a></code></pre></div>
<p><strong>Note:</strong> Before running <code>feh</code>, make sure either Xming or Xquartz is running, and x-tunneling is enabled (i.e. add -Y on mac when you <code>ssh</code> into ugard. On Putty, enable x-11 forwarding option)</p>
</div>
</div>

<div class='admonition tip'>
<div class='title'>Tip</div>
<div class='content'>
<p>Notice that, the program only supports the ppm image format. If you want to test it with your own images, you can convert them to ppm on ugrad using <code>convert</code>. e.g. to convert <code>selfie.jpg</code> to ppm, you could run:</p>
<div class="sourceCode" id="cb1"><pre class="sourceCode sh"><code class="sourceCode bash"><a class="sourceLine" id="cb1-1" title="1">$ <span class="ex">convert</span> selfie.jpg selfie.ppm</a></code></pre></div>
</div>
</div>

### Command line arguments
The program accepts one and only one argument, which is the font config file. If the program is launched with an incorrect number of arguments, a usage message will be displayed as below:
```
--------------------------------------------
Usage: ./project <font config file>
--------------------------------------------
```
and the program should terminate and return an error code `-1`.  You should implement the `isValidArgs` function to complete this logic.

### `structure.h`
#### Font config loading
##### The config information message
If the font config file is provided as its only one argument, the program will first load the config and display the font config information (the `printConfig` function) as below:
```
Number of fonts loaded: n
"font1", "font2", ..., and "fontn"
```
where `n` is the number of fonts loaded, and the next line shows all the font's names in a specific format:
1. font names are enclosed by `"`.
2. they are comma-separated.
3. if there is more than one font, the last one will be concatenated with the word "and".

For example, if there is only one font called "abc", this message should look like:
```
Number of fonts loaded: 1
"abc"
```

If there are three fonts called "abc", "123", and "xyz" loaded, this message should look like this:
```
Number of fonts loaded: 3
"abc", "123", and "xyz"
```

You should implement the `printConfig` function for that.

##### Font config file
The font config file is written in a specific format:
```
n
font_name1 font_filename1
font_name2 font_filename2
...
font_namen font_filenamen
```

where `n` is the number of fonts to load, `font_namex` is the font name of the x'th font, and `font_filenamex` is the font file of the x'th font.

Below is an example of a valid font config:
```
3
line line.txt
star star.txt
contour contour.txt
```

##### Structure `config`
The structure `config` contains the below fields:
1. `num_fonts`: the number of fonts loaded
2. `font_names`: an array of c-string storing the font names (dynamically allocated)
3. `font_filenames`: an array of c-string storing the font filenames (dynamically allocated)

As you can see, the content of a font config file fits tightly into the `config` structure. You need to implement the `initConfig` function to read the file content and fill in the structure `config`. You need to allocate memory dynamically to store the font names and font filenames.  You will also need to implement the `releaseConfig` function to release the allocated memory.

If the program fails to open the config file, the program should display the error message `Cannot open font config file: <config file name>`, terminate and return an error code `-2`.

If the program fails to read the config file, the program should display the error message `Cannot read font config file: <config file name>`, terminate and return an error code `-3`.

If there is no font loaded, the program should display the error message `No font loaded!`, terminate and return an error code `-4`.

You should implement these error messages in the `printErrorMessage` function.

#### Font loading
Upon successfully loading the config, the program will load the first font in the array (i.e. index 0). 

##### Structure `font`
The structure `font` contains the below fields:
1. `num_chars`: the number of characters in a row of a font
2. `num_lines`: the number of lines of the font
3. `font_name`: a pointer to a font name in the config. Note that this is just a pointer. You should not dynamically allocate memory for it. The `font` structure only needs a reference to the memory that you have already allocated in `config` to access its name.
4. `data`: the font data, which is a dynamically allocated array that contains `num_chars` times `num_lines` times 36 (10 digits + 26 alphabets) characters. It is used to draw the font on the console. (Note: depending on your implementation, you may allocate a different size to include null terminator(s).)

You need to implement the `initFont` function to load a font from a font file to this structure, and you also need to implement the `releaseFont` function for releasing the memory.

If the program fails to open the font file, the program should display the error message `Cannot open font file: <font file name>`, terminate and return an error code `-5`.

If the program fails to read the font file, the program should display the error message `Cannot read font file: <font file name>`, terminate and return an error code `-6`.

You should implement these error messages in the `printErrorMessage` function.

##### Font file
A font file is written in a specific way as below:
```
w h
dddddd
dddddd
dddddd
dddddd
...
dddddd
```

It starts with `w` and `h`, which are the number of characters in a row and the number of lines of a font. Each font file contains 36 fonts, for 0 to 9 and A to Z. After `w` and `h`, it contains 36 fonts, each with `h` lines of `w` characters that compose the font. See `line.txt`, `star.txt`, or `contour.txt` provided for reference. Your `initFont` function should read this file and fill in the structure `font`.  You need to allocate memory for `data` dynamically.

By now, you should have implemented all functions in `structures.c`.

### `print_functions.h`
#### Main menu
After loading the font, the program will greet the user, display the main menu options, and ask users for input as below:
```
--------------------------------------------
Welcome to the ASCII art generation program!
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4:
```

You should implement the `printSeparator`, `printGreeting`, and `printMenuOptions` for that. Users can choose to 1) select an ASCII art font, 2) input a word, or 3) quit the program. If users quit the program, your program should terminate, release all allocated memories, and return `0`.

#### Font selection menu
For the 1st option, your program will show the currently selected font by showing the ASCII art of the word "ASCII", display the font selection menu options and ask for input as below:
```
--------------------------------------------
Current font: "line". It looks like:
+--------+--------+--------+--------+--------+
    _/     _/_/_/   _/_/_/   _/_/_/   _/_/_/
   _/_/   _/    _/ _/    _/    _/       _/
  _/  _/    _/     _/          _/       _/
 _/_/_/_/     _/   _/          _/       _/
 _/    _/ _/    _/ _/    _/    _/       _/
 _/    _/  _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Select "line"
2) Select "star"
3) Select "contour"
4) Go back to the main menu
--------------------------------------------
Please select option 1, 2, 3, or 4:
```

Note that this menu is dynamically generated based on how many fonts are loaded.  For example, if there are only two fonts loaded, this page should look like this:
```
--------------------------------------------
Current font: "line". It looks like:
+--------+--------+--------+--------+--------+
    _/     _/_/_/   _/_/_/   _/_/_/   _/_/_/
   _/_/   _/    _/ _/    _/    _/       _/
  _/  _/    _/     _/          _/       _/
 _/_/_/_/     _/   _/          _/       _/
 _/    _/ _/    _/ _/    _/    _/       _/
 _/    _/  _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Select "line"
2) Select "star"
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3:
```

You will need to implement the `printFont` and/or `printWord`, `printRuler`, and `printFontOptions` functions for that.

##### Font display
In the font selection menu, you will show a preview of the ASCII art by converting the word "ASCII" and print it on the screen. You need to implement the `printFont` and/or `printWord`, `printRuler` functions for that.

<div class='admonition tip'>
<div class='title'>Tip</div>
<div class='content'>
<p>Think about what the memory layout of <code>data</code> is. You should be able to deduce which part of the memory you need to access in order to draw the ASCII art.</p>
<p>You may want to reuse <code>printWord</code> in your <code>printFont</code> function.</p>
</div>
</div>

##### Font switching
When switching fonts, your program will release the current `font`'s memory and initialize it with the selected one by calling `releaseFont` and `initFont` functions. This logic has been implemented for you.  However, you need to handle the memory well in your `releaseFont` and `initFont` functions to avoid memory leak problems.

#### Input word menu
For the 2nd option from the main menu, your program will first ask users to input a word, then display the ASCII art of that word, and show the input word menu options for users to select as illustrated below:
```
--------------------------------------------
Please enter a word: aBc
--------------------------------------------
+--------+--------+--------+
    _/     _/_/_/   _/_/_/
   _/_/    _/   _/ _/    _/
  _/  _/   _/   _/ _/
 _/_/_/_/  _/_/_/  _/
 _/    _/  _/   _/ _/    _/
 _/    _/  _/_/_/   _/_/_/
+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3:
```

The `printWordOptions` functions should handle the submenu options display.

Users can choose to enter another word in this submenu or save this ASCII art to a file. The `saveToFileDialog` function is provided for you, in which your `printWord` function will be used to print the word to a file or on screen.

#### Read image menu
The 3rd option is to read an image and convert it to an ASCII art. Your program will first ask users to input an image, then display the ASCII art of that image, and show the read image menu options for users to select:
```
--------------------------------------------
Please enter an image filename: bluejay.ppm
--------------------------------------------
WWWWWWWWWWWWWW888WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWH*-.---.-UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWH-.*8WWH*.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWW8*.UWWW8--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWU.TW88WU.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWH.TWUHWH.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWH.HWTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWT-WHTUWH-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW-H8TTHWH-UUUUHHHHH88WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWW8HUT*--.TWTTTHWU.******---.....--*TUH8WWWWWWWWWWWWWWWWWWWWWWW
WWWWWW8HU*-..-*TUH8U-WUTTT8W*HWWWWWWWWWWWW88HUT*-..-*UHWWWWWWWWWWWWWWWWWW
WW8T-..-*UHWWWWWWWWU-WUTTTTW8*WWWWWWWWWWWWWWWWWWWWWHU*-..-T8WWWWWWWWWWWWW
WT.TH8WWWWWWWWWWWWWU-WUTTTTHWHTWWWWWWWWWWWWWWWWWWWWWWWWW8HT.UWWWWWWWWWWWW
8.8WWWWWWWWWWWWWWWW-TWTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWWW8.8WWWWWWWWWWW
U*WWWWWWWWWWWWWWWHU-W8TTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWW**HWTTTTTTTTHWUTWWWWWWWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
UTWWWWWWWWWWWWWW8.HWHTTTTTTTTT8W*HWWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWH.WWUTTTTTTTTTUW8*WWWWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WWTTTTTTTTTTTHWH*WWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWT*WHTTTTTTTTTTTT8WTTWWWWWWWWWWWWWWWWWWWWWWWWTUWWWWWWWWWWW
UTWWWWWWWWWWWWWWTUW8TTTTTTTTTTTTTWW*UWWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWH*W8TTTTTTTTTTTTTTWW*HWWWWWWWWWWWWWWWWWWWWWW*UWWWWWWWWWWW
U*WWWWWWWWWWWWWWW*88TTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
U*WWWWWWWWWWWWWWWUTWUTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWWW*HWWWWWWWWWWW
H-WWWWWWWWWWWWWWW-TWWTTTTTTTTTTTTTTTUWW*HWWWWWWWWWWWWWWWWWWW-HWWWWWWWWWWW
H-WWWWWWWWWW8UT*-.8WW8TTTTTTTTTTTTTTTUWW*UWWWWWWWWWWWWWWWWWW-8WWWWWWWWWWW
8.WWWWWWW8T..*TUHHWWWWWTTTTTTTTTTTTTTTTWWTTWWWWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.WWWWW8*.*HWWWWW8WWWWWWHTTTTTTTTTTTTTTT8WU*8WWWWWWWWWWWWWWW.WWWWWWWWWWWW
W.8WWWT.*8WWHUTTTTT8WWWWWWHTTTTTTTTTTTTTTHW8-HWWWWWWWWWWWWW8-WWWWWWWWWWWW
W-HW8--8WWUTTTTTTTTUWWWWWWWW8HTTTTTTTTTTTTHWW*UWWWWWWWWWWWWH*WWWWWWWWWWWW
W*UH.TWWUTTTTTTTTTUWWWWWWWWWWWWW8UTTTTTTTTTUWWTTWWWWWWWWWWWU*WWWWWWWWWWWW
WT..UW8TTTTTTTTTTTWWWWWWWWWWWWWWWWW8UTTTTTTTTWWTUWWWWWWWWWWTTWWWWWWWWWWWW
WU.HWHTTTTTTTTTTTHWWWWWWWWWWWUU**HWWWHTTTTTTTTWW*UWWWWWWWWW*HWWWWWWWWWWWW
W8.W8TTTTTTTTTTTT8WWWWWWWWWWU*....-HWW8TTTTTTTTWW*8WWWWWWWW.8WWWWWWWWWWWW
WW.88TTTTTTTTTTTTWWWWWWWWWWU-.......TWW8TTTTTTTUWH*WWWWWWW8-WWWWWWWWWWWWW
WW-UWTTTTTTTTTTTTWWWWWWWWWH..........TWWHTTTTTTT8WTHWWWWWWH*WWWWWWWWWWWWW
WWTTWTTTTTTTTTTTUWWWWWWWWWH...........HWWTTTTTTTTW8*WWWWWWTTWWWWWWWWWWWWW
WWH-WUTTTTTTTTTTTWWWWWWWWWW*........T88WWUTTTTTTTHWTHWWWWW-HWWWWWWWWWWWWW
WWW.88TTTTTTTTTTTWWWWWWWWWWWT......UHU8WWWTTTTTTTTWHTWWWWW.WWWWWWWWWWWWWW
WWW-UWTTTTTTTTTTT8WWWWWW8UTTHH-...*HHWW*8W8TTTTTUU8W*WWWWH-WWWWWWWWWWWWWW
WWWT*WUTTTTTTTTTTHWWWWWH-.....--..HUWW8.-WW8TU8W88WWT8WWWTTWWWWWWWWWWWWWW
WWWH.WHTTTTTTTTTTTWWWW8-..........H8WWWUUWWW8WWWWWWWU*8WW.8WWWWWWWWWWWWWW
WWWW.HWTTTTTTTTTTTHWWWH..........-H8WWWWWWWWWWWWH***UH-UH-WWWWWWWWWWWWWWW
WWWWT*WTTTTTTTTTTTTWWWT...........HHWWWWWWWHWWWT.*TT*-8--TWWWWWWWWWWWWWWW
WWWW8.WHTTTTTTTTTTTTWWH...........UUWWWWWWWWW8U.8WWWWWWW--UWWWWWWWWWWWWWW
WWWWW-UWTTTTTTTTTTTTUWWU..........-8T8WWWWW*...HWWWUTUHWW8*.T8WWWWWWWWWWW
WWWWWU-WUTTTTTTTTTTTTT8W8-.......T.-8UUHWW-...*WWW-.....*HW8T.TWWWWWWWWWW
WWWWWW.H8TTTTTTTTTTTTTTHWWH*.....-HUTHWWWT..*UHWWWHTHW8T-.-UW8*.HWWWWWWWW
WWWWWWT*WUTTTTTTTTTTTTTTTHWWWU*-...UWWWWW-*8WWWWWWWWWWWWW8T..UWH-*WWWWWWW
WWWWWW8.88TTTTTTTTTTTTTTTTTTH88WWWWWWWWW8-8WWWWWWWWWWWWWWWWWU.-8WT-8WWWWW
WWWWWWW**WTTTTTTTTTTTTTTTTTTTTTUH8WWWWWWW*WWWW8UUUUH8WWWWWWWWWT.UWU.HWWWW
WWWWWWW8.88TTTTTTTTTTTTTTTTTH8WWHT-..-WWWU8WWWWWWW8HUT*THWWWWWW8-*WH.HWWW
WWWWWWWW**WUTTTTTTTTUTTTTTUWWH-.......HWWWWWWWWWWWWWWWWWHTTUWWWWWU-WH.8WW
WWWWWWWW8.H8TTTTTU8WUTTTTHWU..........*WWWWWWWWWWWWWWWWWWWW8UTHWWWH*WU-WW
WWWWWWWWWT-WUTTT8WWHTTTTHWT..........*WW8WWU*U8WWWWWWWWWWWWWWW8UUWW8TW-UW
WWWWWWWWWW-TWTTWHUWTU8TUWU..........UWH-*--UWHT-*UHWWWWWWWWWWWWWWTUW888.W
WWWWWWWWWWH.888H.8HUW8T8W*.........UWTTWWWWWWWWWWU...-*TUHH88WWWWW8*UWW-H
WWWWWWWWWWWT-WW--W8W8HUWH-........TWTUWWWWWWWWWWW-T8HUTT*--.....-*U8T-HTT
WWWWWWWWWWWW-TH.*WWT8U8WU........-WHTWWWWWWWWWWWT-WWWWWWWWWWWW88HT*..-.-T
WWWWWWWWWWWW8.*.TWH-WUWWU........H8*WWWWWWWWWWWH.8WWWWWWWWWWWWWWWWWWH*..T
WWWWWWWWWWWWWU..*W**WUWWT.......*WTHWWWWWWWWWW8-HWWWWWWWWWWWWWWWWWWWWWWTU
WWWWWWWWWWWWWWT..8-*WHWWT.......H8*WWWWWWWWWWW-TWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWW*.T.-W8WWU......-WUUWWWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWW*...8WWWH......TWT8WWWWWWWWW**WWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWW-..*W8WH......HW*WWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWW*..HH88......88TWWWWWWWW*-WWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWW*.-TUW-....-WHUWWWWWWW-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWT..-WU....-WUHWWWWW8-*WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWU..UWT...-WUHWWWWH.TWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWH..HWU..*WU8WWWT.HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWW8-.UW8--WU8WH--8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWT.*8W8WUUT.UWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWW8-.TWWT.*8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWU...-HWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWHHWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
--------------------------------------------
1) Save it to a file
2) Read another image
3) Go back to the main menu
```

The `printImageOptions` functions should handle the submenu options display.

Users can choose to read another image in this submenu or save this ASCII art to a file. The `saveImageToFileDialog` function is provided for you, in which your `printImage` function will be used to print the image to a file or on the screen.

##### Convert an image to an ASCII art
To print the image using characters, we need to convert the image colors to characters. In the code, the image will be read as an array of `unsigned char`. Each `unsigned char` value has 8 bits. You are going to map the value to 8 different characters ('W', '8', 'H', 'U', 'T', '*', '-', '.') by considering the 3 high (leftmost) bits. 3 bits can represent values between _0_ and _7_, which can be naturally mapped to the 8 characters, respectively. i.e. `0 -> 'W'`, `1 -> '8'`, etc.

For example, if the `unsigned char` value is _178_, its binary representation is _10110010_, so the value of its 3 highest bits is _101_, which is _5_. We map this value to '*' according to the ordered list of display characters given above. If you implement `printImage` correctly, you should see the exact same bluejay ASCII art as above.

#### Quit the program
If users select to quit the program, it will greet the users again with this message:
```
--------------------------------------------
Thank you for using the ASCII art generation program!
--------------------------------------------
```

This should be implemented in the `printEnding` function.  At this moment, you should have completed all functions in `print_functions.c`. Next, you should work on the input validation.

### `validation.h`
#### Input validation and handling
Your program should validate the user input as specified here. 

When getting an option input from users, you must:
1. first, trim the leading and trailing whitespaces. You should implement the functions `trimLeadingWhitespaces` and `trimTrailingWhitespaces` for that.
2. make sure it is a single character whose value is between the lowest and highest selectable options. It should be handled in the `isValidInputOption` function.
If not, the program will repeatedly ask for input.

When getting a word input from users, the input must:
1. first, trim the leading and trailing whitespaces.
2. make sure it is not an empty input. e.g. "" is not a valid input. (i.e. implement the `isEmptyInput` function)
3. make sure it is the only input. e.g. "abcd" is a valid input, but "0123 abcd" is not. (i.e. implement the `isMultipleInput` function)
4. make sure it only contains digits and alphabet letters. e.g. "o123" is a valid input, but "@123" is not. (i.e. implement the `isContainSpecialChar` function)

You should also implement the helper function `isWhitespace`, which will help you to implement `trimLeadingWhitespaces` and `trimTrailingWhitespaces`.

Besides, there is another helper function that you need to implement, which is `isNullPointer` for checking if a pointer is `NULL`. This should be fairly straightforward to do. Do not overthink the logic. We intended to divide the complex program into manageable small pieces. Each piece contains a simple logic that we can manage to debug and implement.

At this point, you should have implemented all the required functions in `validation.c` as well.

<div class='admonition note'>
<div class='title'>Note</div>
<div class='content'>
<p>When getting an image from users, the code will use <code>isNullPointer</code> function to check if an image is read successfully. Otherwise, it will keep asking for an image file. You do not need to modify this logic or add any additional input validation for image input.</p>
</div>
</div>

## Testing Requirement
In this project, you must also write a test program using `assert` to test each function in `validation.h`. You should create a file called `test_validation.c`. This program will have its own main function and takes no input. It simply runs a series of tests that you have written. Your tests should use assert statements to make sure your functions behave properly. If all tests pass, the program should output a message indicating success.

<div class='admonition tip'>
<div class='title'>Tip</div>
<div class='content'>
<p>It is an extremely, extremely good programming practice to write test cases to test your basic assumptions, try "corner" and extreme cases, test loop invariants, etc. You should write the tests <em>before</em> you write the actual functions you are testing.</p>
<p>It can save you a great deal of frustration and effort down the road. We will look carefully at your tests when grading.</p>
</div>
</div>

You should add a new target in your Makefile called `test` such that the command `make test` will create AND run the test executable. Running the test file should also give a message at the end indicating that all tests have passed (see the example below). Here is an example of `test_validation.c`:

```c
#include <assert.h>
#include <stdio.h>
#include "validation.h"

// ... other test functions

// define test function to test the isNullPointer function in validation.h
void testIsNullPointer() {
  assert(isNullPointer(NULL) == 1);  // isNullPointer should return 1 if input is NULL
  assert(isNullPointer(stdout) == 0); // isNullPointer shoudl return 0 if input is not NULL
}

// ... other test functions

int main() {
  printf("Starting Tests...\n");
  // ... other tests
  testIsNullPointer(); // run the test of isNullPointer;
  // ... other tests
  printf("All tests passed!!!\n");
}

```

## Sample runs
Here is another sample run:
```
$ ./project font_config.txt
--------------------------------------------
Number of fonts loaded: 3
"line", "star", and "contour"
--------------------------------------------
Welcome to the ASCII art generation program!
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 2222
Invalid input option!
Please select option 1, 2, 3, or 4: a
Invalid input option!
Please select option 1, 2, 3, or 4: 2 3
Invalid input option!
Please select option 1, 2, 3, or 4: 2
--------------------------------------------
Please enter a word:
Input is empty
Please enter a word: a!a
"a!a" contains special characters.
Please enter a word: 192 234
"192 234" contains more than one input.
Please enter a word: cs220
--------------------------------------------
+--------+--------+--------+--------+--------+
  _/_/_/   _/_/_/    _/_/     _/_/    _/_/_/
 _/    _/ _/    _/  _/  _/   _/  _/  _/    _/
 _/         _/         _/       _/   _/    _/
 _/           _/      _/       _/    _/    _/
 _/    _/ _/    _/   _/       _/     _/    _/
  _/_/_/   _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 4
Invalid input option!
Please select option 1, 2, or 3: 1 4
Invalid input option!
Please select option 1, 2, or 3: abc
Invalid input option!
Please select option 1, 2, or 3: 1
--------------------------------------------
Please enter a filename: /
Unable to write to "/".
Please enter a filename: cs220.txt
File saved as "cs220.txt"!
--------------------------------------------
+--------+--------+--------+--------+--------+
  _/_/_/   _/_/_/    _/_/     _/_/    _/_/_/
 _/    _/ _/    _/  _/  _/   _/  _/  _/    _/
 _/         _/         _/       _/   _/    _/
 _/           _/      _/       _/    _/    _/
 _/    _/ _/    _/   _/       _/     _/    _/
  _/_/_/   _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 2
--------------------------------------------
Please enter a word: aBc
--------------------------------------------
+--------+--------+--------+
    _/     _/_/_/   _/_/_/
   _/_/    _/   _/ _/    _/
  _/  _/   _/   _/ _/
 _/_/_/_/  _/_/_/  _/
 _/    _/  _/   _/ _/    _/
 _/    _/  _/_/_/   _/_/_/
+--------+--------+--------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 3
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 1
--------------------------------------------
Current font: "line". It looks like:
+--------+--------+--------+--------+--------+
    _/     _/_/_/   _/_/_/   _/_/_/   _/_/_/
   _/_/   _/    _/ _/    _/    _/       _/
  _/  _/    _/     _/          _/       _/
 _/_/_/_/     _/   _/          _/       _/
 _/    _/ _/    _/ _/    _/    _/       _/
 _/    _/  _/_/_/   _/_/_/   _/_/_/   _/_/_/
+--------+--------+--------+--------+--------+
1) Select "line"
2) Select "star"
3) Select "contour"
4) Go back to the main menu
--------------------------------------------
Please select option 1, 2, 3, or 4: 2
--------------------------------------------
Current font: "star". It looks like:
+--------+--------+--------+--------+--------+
    **     ******   ******   ******   ******
   ****   **    ** **    **    **       **
  **  **    **     **          **       **
 ********     **   **          **       **
 **    ** **    ** **    **    **       **
 **    **  ******   ******   ******   ******
+--------+--------+--------+--------+--------+
1) Select "line"
2) Select "star"
3) Select "contour"
4) Go back to the main menu
--------------------------------------------
Please select option 1, 2, 3, or 4: 3
--------------------------------------------
Current font: "contour". It looks like:
+----------+----------+----------+----------+----------+
               _____      _____     ______     ______
     /\       / ____|    / ____|   |_    _|   |_    _|
    /  \     | (___     | |          |  |       |  |
   / /\ \     \___ \    | |          |  |       |  |
  / ____ \    ____) |   | |____     _|  |_     _|  |_
 /_/    \_\  |_____/     \_____|   |______|   |______|
+----------+----------+----------+----------+----------+
1) Select "line"
2) Select "star"
3) Select "contour"
4) Go back to the main menu
--------------------------------------------
Please select option 1, 2, 3, or 4: 4
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 2
--------------------------------------------
Please enter a word: aBc
--------------------------------------------
+----------+----------+----------+
              _____       _____
     /\      |  __ \     / ____|
    /  \     | |__) |   | |
   / /\ \    |  __ <    | |
  / ____ \   | |__) |   | |____
 /_/    \_\  |_____/     \_____|
+----------+----------+----------+
1) Save it to a file
2) Enter another word
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 3
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 3
--------------------------------------------
Please enter an image filename: jhusign.ppp
Please enter an image filename: jhusign.ppm
--------------------------------------------
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWUTHWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWHT--*--U8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWU--*UUUUT*-T8WWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWU--TUUTUUUUUU*-*8WWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWH*-TUTTTTT*UUUUUT*-T8WWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWW8*-TT**TTTTTTUUUUT*TU*-UWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWU-*UT*TTTTTTTTTUUU**UTTT-*8WWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWW8*-TT*T*---TTTTTTUUT-UUTTUT*-UWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWH-*TTT*TTTT*TTT--*TUT*UT*UT-UT-TWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWU-*T-**T*TT*TT--*T--*T***TT**TTT**8WWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWT-TTTT***-*TT--TT*-*T*-*TUU*T*T*TU*-HWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWT-T**TTTTTTT*-*T***TTT*T*-TTTU**TUTTT-HWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWT-TTT**TT*T*-***-UT**TUU-****TU**UT*UUT-HWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWT-T-TTT**TT--*****TT**TUU***T*-TTUT-UU*TT-HWWWWWWWWWWWWWW
WWWWWWWWWWWWWT-TT*TTTT*T--**T*TT****TTT**TT**-*T*TUT*UUT-HWWWWWWWWWWWWW
WWWWWWWWWWWWU-T-*-***T*--**T***-****TT***TT**T-*TUU*TT*TT*HWWWWWWWWWWWW
WWWWWWWWWWWU-TTT--****-***TTT--*UT**TTT*-******T*TU**TUUTT*8WWWWWWWWWWW
WWWWWWWWWWH-T*-*T-*T*-***TT*--*TTT**TTTT*--*TTTTT*TTUUU**T*TWWWWWWWWWWW
WWWWWWWWWW-*****TT**-***TT*--TUUUT**TUTUUT--*TTUU*-TUU**UTT*UWWWWWWWWWW
WWWWWWWWWT-T*-**TT*-T*UU*---UHTUTT**TUTUUHT---THUT**T*TTTUUU*HWWWWWWWWW
WWWWWWWWH-TTT*-***-**TU*---TUUT*T***TTTTTUUT*--TU*T****TTUUTT*WWWWWWWWW
WWWWWWWW-*****UUUUUUUUUUUUUUUUUUUUHHHHHHHHHHHHHHHHHHHHHHUU**T*TWWWWWWWW
WWWWWWWT-T**--HHHHHHHHHHHHHHHHHHHHUUUHHHHH88H88888888888H**UTU*8WWWWWWW
WWWWWW8-T*TTT*HHHTTTTUUTTTUHHHHHUTTTTUUHHHHHTTTTHUTTTH88HU***UTTWWWWWWW
WWWWWW**T**TT*HH**-..**.--*THHHUT*-T*TUUHHH**-.-T-.-**U8HU*UUUU*HWWWWWW
WWWWWH-TTT---*HH**-..*-.--*THHUUUTTUTTUUHHU-*-.-*-.--*U8HTTUU*TT*WWWWWW
WWWWW****TTTT*HH**-..*-.--*THHUTT**T*TUUHHU**-.-*-.--*U8HUTTTTUT*HWWWWW
WWWW8-TT*-**T-HH**-..*-.--*THHHTTTTUUUUUH8U**-.-*-.--*U8HTTTTTUTTTWWWWW
WWWWT*TT*****-HH**-..*-.--*THHHUTUUUUUHHH8H**-.-*-.--*U8H*T**TUUU*8WWWW
WWWW-T-**TTT-*UH***********THHHUUUUHHUHHH8H*****T*****U8H**UTT**T*TWWWW
WWWU-TT*--**-TUH******T****THHHHHHUUHHHH88H*****T*****U8HU-U**TUUT*WWWW
WWW**TTTTTT-T-UHUUUUUTTUUUUUHHHHHHHUHUHH88HUUUUUUTUUUUH8HT*TUUUUTT*HWWW
WW8-TTTTTT*-T*UHHHHHHHHHHHHHHHHHHHH88H888888888888888888H*T*UUUUTTTTWWW
WWU-TTTTTT-**UUHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHH88HHTT*TT**TTU*WWW
WW**TT*TTT-T*UU88888888888888888888HUUUUUUUUUHHHHHHHHHHHHU*T*TUUUTU*HWW
WW-TTTTTT*-TTUU888HH88TTU888HHHHWWWU-------*TTTUHHHHHHHHHH*T*UUUUUU*UWW
W8-UTTTTT***UUU888UTHHTTU888HHHHWWWU-------TUT*THHHHHHHHHUTT*UUUUTTTTWW
WU-TTTTTT-T*TTU888UTTUUUU888HHHHWWWU-------*UT*UHHHHHHHHUTT**TUUTTUU*WW
WT*TTTTTT-T***TUH8UTTH8HU888HHHHWWWU--------TUTHHHHHHHHHU***T*T*TTUU*8W
W*T*T*-*T-T***TUTUUTTH888888HHHHWWWH-------*TUTHHHHHHHHHT***T*UUUUTU*HW
W-T*T-T*******THTTHHUH888H8WHHHHWWWU*TT----*TUTHHHHHUUHHT**TT*UUUUHH*UW
8-T*-TT***-*TTTHUU88HH888HH8HHHHWWWHTUUTTTTUUUTTTUUUTTUUT*TTT*UUUUHHTTW
8-UTTTTT-T-**TTUUU8888888HUHHHHHWWWHTTTTTTTTTUUUUUUUUUUUTTTTT*TUUTUHTTW
H-TTTTTT*****TUUUU8888H88HUU88HHWWWHU**TTUUUTTUUUUUUHHUHTTTT**TUUUHHT*W
H-T***-T****TTUUUU8888UH8HHH8WW8WWWHUUUUUHHHUUU**TTTUUTUTTT***TUHHHHU*W
H-UUT*TT****TTTUHU8888UUH8HH8WWW8WWHUUHHHHHHUUU*TTTTTTUUTTT**TTUUUUUU*W
U-T**TUT-****TUUHU8888UHHW8H8WWWH8WHHHHHHHHHUUUTTTTTTTUUU**TTTTT****U*W
H-T-***T-T**TUUUHH8WW8HHHWWW8WWWHH8HHHHHHHHUTUHUTTTTTTUUU**TTTTTUTUTU*W
H-UUUUTT-TTTTTTTUH8WW8HHHWWW88WWHHHHHHHHHHHUTUHUTTTTTTUTT*TTUTTT****U*W
H-TTTTTT-T*UTTUUUH8888UUH8WWHHH8HHHHHHHHHHHHUUUTTTTTTUUTTTTU*TTUUUUUU*W
H-T*-**T-T-***TUUHHHHHUUUHHHHHHHHHHHHHHHHHHHHHHHHHHHHHUUTT***TTTTUHHU*W
8-UUTTUU-T***TUUUU----****TUTUHHHHHH888H88UUHWW8HH8WWHUU***TT*TUTTTUT*W
8-UTT**T**-**TTTTU*------*TT*THHHHHH88HTUHUUHWW8HH8WWHTT*TTTT*UUTT*TTTW
W-T***TT*-**TUUUTUT------*TT*THHHHHH888TTHHUHWW8HH8W8UTUUTTTU*U*TTUHTTW
W-TUUUTUT*TTUUUUTUU------**UTUHHHHHHH88TTH8HHWW8HH8WHUTUUTTTUTUUHHHH*UW
W*TU****T-TTUUUUUTU*-----**UTUHHHHHHUUHUUH888WW8HH8WUTUUUUUUUTUTUUHH*HW
WT*T*UUTT-T*T*TTT*TT-******UTHHHUUHHUUUHUH8W8H88HH8H**T***UTTTTTTT*U*8W
WH-TUUUTT*T********U*TUUTTTUTUUUTTUHUUH88HWW8HH8HHHU***-***T*UTHHHUU*WW
W8-T*T**UT**TT*****UUUUUUUUUTTTTTTTHHUH8W88W8HH88HHU***-*TT**UTHHHHTTWW
WW*TUTTUUT**UT****TUUT**TTTTHUUUHHUHHUHWW8H88HH8W8HTTT***TT*TUUHHUU*UWW
WWT*UUUT*T******UTT*TUTUHHUTUT*TUUTHHHHWW8HHHHH8WHT*UUT*****TT*TUTU*8WW
WWH-T***T*T**TT*TUT**UHHHHUTHT*TTTTHHHHWW8HH8W888U*TUU******UUUUTTT*WWW
WWW-TTUUTTU**TT**UU**TUHHHUTHTTTTTTHHHHWW8HH8WW8HT*TUT*****TUHHHUU*UWWW
WWWT*UUUUUU***TT**T**TUUHHHTHTTTTTTHHHHWWWHH8WW8U**TU******UTTUHUU*8WWW
WWWH-UUUUUUT-*TT*-****TUHHHTHTTTTTTHHHHWWWHH8WWU***T**TT***UUUT*TTTWWWW
WWWW*TUUUUUU***TU*-****TUHUTHTTTTTTHHH8WWWHH8WHT**T*-T****UTUHHUU*UWWWW
WWWWU*UUUTUUT-T*U**-*TTTUUTTHHTTTTTHHH8WWWHH88T**T*-*TT*T*UUUTUHU*8WWWW
WWWWW*TUUUUUU*T**T**-*TUUUTTHUTTTTTHHH8WWWHHHUTTT*-TUT-T*UU*T**U*UWWWWW
WWWWWU*UUUUUUU*U***T*-*TTUUUUTTTTTTHHH8WWWHHHTTT--T*T-TTTUUUUHHU*8WWWWW
WWWWW8*TUUUUTTT*U***T*--TUUUTTTTTTTHHH8WWWHHHU*-**TT-*U*UUTTTUH*UWWWWWW
WWWWWWU*UUUUUTT*TT**T**--*UUTTTTTTTHHH8WWWHHU*-*UU*-*U*TUUUUTTU*8WWWWWW
WWWWWWW*TUUTTT*U*T***TU---*TUTTTTTTHHH8WWHUT--TT**-*TTTUTT*UHU*UWWWWWWW
WWWWWWWH*UTU**UUT*T****-*T*-*UTTTTTHHH8W8U**TTTT**TTT*UTHHUTHTTWWWWWWWW
WWWWWWWWT*U*TUUUTT*TTT*-TTTT**UTTTTHHHH8U**TTU**T*TUTUHTUHHTU*HWWWWWWWW
WWWWWWWW8*TUUUT*UU*TUUTT**TTTTTUTTTHHHUU*T*T***TTTUTUTUU*TTU*UWWWWWWWWW
WWWWWWWWWH*UUT*THUU*TTTTUT**TU**U*THHUU**TT**UUTTU*THUTUHUUTT8WWWWWWWWW
WWWWWWWWWWT*UTUTT*UU*TTTUTTT*****U*HUU****TT*UTTU*TU*TTTTHU*HWWWWWWWWWW
WWWWWWWWWWWT*UUT*UHHU*TT****TT***TUUU***TT*****U*TUUUTTHTU*UWWWWWWWWWWW
WWWWWWWWWWW8*TTTUHHUTUT*****TTTT*T*U**TT*****TTTUU*UHUTTU*UWWWWWWWWWWWW
WWWWWWWWWWWW8*TUUHU*UHUT*T*TTTUUT****TUUT**TTTTUTUHTUHHH*TWWWWWWWWWWWWW
WWWWWWWWWWWWWH*TTU*UHHHHU*TUTUUTTTTTTTTTUTTUTTUHUHUUTUH*TWWWWWWWWWWWWWW
WWWWWWWWWWWWWWH*TTTHHHHHHU**UT***T**TT*TTTU*THHHHHHHTU*T8WWWWWWWWWWWWWW
WWWWWWWWWWWWWWWH*TTUHHHHHHHT*T**T**TT*TTUT*UHHHHHHUTU*T8WWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWH*THHHHUUHHHUTTTUTTTUUUTTUHHHHUHHHHU*T8WWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWW8**UHHUHHHHHHUT*TTUUT*UHHHHHHUHHHU*UWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWW8T*UHHHHHHHHTUUTTTTTHUTTHHHHHHHT*UWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWU*THHHHHHH*UHUUUHUUTUTUHHHHU**HWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWH**UHHHHTTHTUTUTTUUTUTUHHT*T8WWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWW8U*THHUTHHTTTHHUUHTUTUU**HWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWHT*TTTHTUTHHHUTHHUUT*U8WWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWH**THTUTUHHUTHUT*T8WWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWH**TUUHHHHU**THWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWHT**UUT**T8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW8U**TU8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW8WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW
--------------------------------------------
1) Save it to a file
2) Read another image
3) Go back to the main menu
--------------------------------------------
Please select option 1, 2, or 3: 3
--------------------------------------------
1) Select an ASCII art font
2) Input a word
3) Read an image
4) Quit the program
--------------------------------------------
Please select option 1, 2, 3, or 4: 4
--------------------------------------------
Thank you for using the ASCII art generation program!
--------------------------------------------
```

## Submission Requirement
<div class='admonition danger'>
<div class='title'>Danger</div>
<div class='content'>
<p>Remember that programs that do not compile (with standard compiler flags on the ugrad machines) will not receive credit. Additionally, points will be deducted for any compiler warnings. Points will also be deducted for any warnings, errors, or memory leaks reported by valgrind. All executables should be buildable using a <code>Makefile</code>, and should build and run cleanly.</p>
</div>
</div>

### Gitlog
The requirements for your `git log` requirements are the same as in previous assignments, except that we expect all members of your team to contribute commits to your shared midterm project repository.

### README

You need to submit a file called `README` (not `README.txt` or `README.md`, etc -- just `README`), including information about additional changes you made (besides the program specification) and anything the graders should know about your submission. In your `README` you should:

- Write your names and JHED IDs at the top of the file
- If applicable: Briefly justify the change you made to the structure of your program; why you defined additional functions, etc
- If applicable: Highlight anything you did that was particularly clever
- If applicable: Tell the graders if you couldn’t do everything. Where did you stop? What did you get stuck on? What are parts you already know do not work according to the requirements?

### Makefile
You need to write your own Makefile. Make sure you have defined these two targets properly:
1. `project`: a target to compile your program.
2. `test`: a target to run the test.

We will run `make project` and `make test` to compile your program and run the test. Remember: `make test` should create the test executable **and** run the test file in one command.  Failure to comply with this requirement will result in a **zero** score.

### Code Submission (Team)
Submit your project via Gradescope. Your submission should contain all source code and files necessary to compile your program (including a `Makefile`) as well as a `README` file (which includes both partners' names and JHEDs) and a `git log` file from your midterm project repository. The `log` should indicate that all team members contributed code and pushed their contributions to the repository. Your submission **should not** contain any compiled binaries (executables or object files), or any testing-related files (in particular, please do not submit any image files).

**Only one team member should submit the project on Gradescope [Coding Midterm Project (Team)](https://www.gradescope.com/courses/266485/assignments/1353114), but must also name their partner when submitting.** The same team member should submit all versions of the project in his/her account. **Be sure that source file headers include the names and JHEDs of all team members**, so that each student gets credit for this work.

### Contributions Submission (Individual)
Separately, after your team's code submission is complete, each team member must individually complete the Midterm Contributions assignment on Gradescope [Coding Midterm Project Contributions (Individual)](https://www.gradescope.com/courses/266485/assignments/1354743). This individual submission will give each student an opportunity to comment on the contributions that they and their partner made to the midterm project and provide feedback to the course.

Note that the deadline for this individual submission is 48 hours after the code submission deadline (i.e. Friday 11pm). Each team member must submit their own version of this assignment in order to get credit for their work on the midterm project.
