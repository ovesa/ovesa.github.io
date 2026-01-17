---
title: "IPython Path" 
date: 2021-04-22
tags: ["Note",]
author: ["Oana Vesa"]
description: "This note documents a practical workaround for resolving IPython path conflicts caused by multiple Python installations when running scripts from the terminal."
summary: "The note describes how conflicting Python and IPython installations can cause missing library errors when invoking IPython from the shell. By inspecting all available IPython executables using which -a ipython, the underlying path precedence issue can be identified. Instead of modifying system paths, the solution uses python -m IPython to explicitly launch the IPython instance associated with the desired Python environment, in this case Anaconda. An alias is then added to the shell configuration to enforce this behavior consistently while minimizing the risk of destabilizing existing Python setups."
editPost:
    URL: "https://ovesa.github.io/"
    Text: "GitHub repository"
showToc: true
disableAnchoredHeadings: false

---


Earlier today I tried running a JupyterLab converted executable python script in the terminal using ipython. However, my bash shell kept reading in an incorrect ipython path (that is probably tied to the first time I downloaded python). This meant that all of my regular python libraries could not be found.... I learned that I have several python paths probably due to various user inflicted python installations. Probably should clean that up at some point, but to not upset the python deities I did the next best thing (in my opinion).

To determine the directory of the ipython executable, type in the terminal:
```bash
ovesa:~$ which -a ipython
/usr/local/bin/ipython
/Users/ovesa/opt/anaconda3/bin/ipython
```
This shows all of the paths where this file was downloaded. The first path listed is the one that your bash shell goes to in order to find the command and launch it.

I wanted to use the ipython file associated with anaconda3, so I found this solution online:
```bash
ovesa:~$ python -m IPython
```
It apparently runs the ipython script stored in the directory associated with that python version which in my case is managed by the anaconda3 package.

To ensure that I do not completely self-destruct my precarious python arrangements, I added this into my bash script:
```bash
alias ipython = "python -m IPython"
```
