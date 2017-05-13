---
title: "Better Python Debugging With IPDB"
category: ["Python", "Productivity"]
tags: ["Python", "Productivity"]
desc: "I have been using Python extensively for past few months in my projects and like any other programming project I spend most of my time debugging and optimizing my code"
---

## Introduction

I have been using Python extensively for past few months in my projects and like any other programming project I spend most of my time debugging and optimizing my code. Initially, I had been using `print` statements to understand my code flow, rectify bugs, profiling my code and other tasks but later realized how inefficient and time consuming this approach is. Searching for a better approach to debug code, there is always something better available out there, I came across [pdb][1] and [ipdb][2]. 

[pdb][1], the Python Debugger, is an interactive debugger that is part of the Python standard library. It allows you to jump into a shell at arbitrary breakpoints in your code, where you can inspect the code and runtime, walkthrough the code line by line, change the values of objects, and more.

[ipdb][2], the IPython-enabled Python Debugger, is a third party interative debugger with all pdb's functionality and adds [IPython][3] support for the interactive shell, like tab completion, color support, magic functions and much more. You use ipdb just as you use pdb but with an enhanced user experience.

Please not that all the code snippets provided are for Python2.7

## Essential Commands

Some of the essential and common ipdb commands which you are going to use, these are issued in `ipdb>` shell. Most of commands are same as in `pdb` and can this section can be skipped if you are acquainted with them.

* __n[ext]__ : `n`  simply continues program execution to the next line in the current method
	
* __s[tep]__ : `s`  steps to the very next line of executable code, whether it is inside a called method or just on the next line


On a line where a method is being called, `n` will "step over" the method execution code while `s` will "step into" the method execution code allowing you to introspect the method code.

* __w[here]__ : `w` prints a stack trace, with the most recent frame at the bottom. An arrow indicates the "current frame", which determines the context of most commonds.

* __b[reak]__ *\(\[filename:\]lineno\|function\)* :
	`b` ddds breakpoints to the specified locations. Example usage:
	
	- `b sample-filename.py:<line no>`
	- `b <function>`
	- `b <lineno>` (for the current file)
	
* __c[ontinue]__ : `c` continues program execution until another breakpoint is hit or the program execution completes

* __a[rgs]__ : `a` prints out all the arguments the current function received

* __r[eturn]__ : `r` continues execution until the current function returns

In case you are already using variables with names such as `c`, `a` use complete command `continue`, `args` to get desired operation.

For more advanced usage of these commands refer to [pdb's documentation][4]

## IPython Magic

Reason I preferred `ipdb` over Python's native debugger is the support of seamless integeration with IPython Shell which support [magic functions][5].

Once in ipdb shell execute the follow code snippet to get IPython Interactive Shell.

```python
ipdb> from IPython import embed
ipdb> embed() # drop into an IPython session.
        # Any variables you define or modify here
        # will not affect program execution
```

Executing this will open an ipython iteractive shell with all the variables and objects loaded from the calling frame. Exiting from the shell will return to ipdb shell. Changes done in ipython shell will not affect objects and variables in ipdb shell.

## Usage

After installing ipdb via `pip install ipdb` or one of the other installation method as mentioned [here][2]. You can use one of the apporaches given to get started with code debugging. 

All the approaches break into an interactive shell on execution, allowing you to introspect objects at runtime, use IPython features - Read previous section to know how, walkthrought line by line and more.

* 	```python
	import ipdb
	ipdb.set_trace()
	```
	Add this code snippet at an arbitrary location in your code, and you iteractive shell will start from that location.

* 	To start an interactive shell from shell itself execute:
	
	```$ python -m ipdb Run-Script.py```
	
	In case of multifile python project `Run-Script.py` should be the driver script.
	
If you know other cool ipdb features which I missed please comment.

[1]: https://docs.python.org/2/library/pdb.html
[2]: https://github.com/gotcha/ipdb
[3]: https://github.com/ipython/ipython
[4]: https://docs.python.org/2/library/pdb.html#debugger-commands
[5]: http://ipython.readthedocs.io/en/stable/interactive/magics.html