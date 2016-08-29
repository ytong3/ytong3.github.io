---
layout: post
title: Ctags with VIM
---

##Ctags

It wasn't until recently that I still use the very basic search function of VIM to navigate a codebase, which kind of sucks. For example, to find the class definition for `SslServerStream` in [mono](https://www.github.com/mono/mono), I would do something like `find . -name '*.cs' -exec grep -iRHn 'SslServerStream'`. But, the problems were 1) it took a long time to search for it, 2) it gave me every match for the `SslServerStream`, including references, definitions, comments, although the class defintion is all I need. It was no good experience by any means.

Then, I came across *ctags* with vim and wished I had knew it sooner! Without it, I had wasted tons of time navigating a large code base and making myself overwhelmed.

*Ctags* basically goes through your code base, analyzes the code, create tags for classes, functions, and variables and save the tags, and their location in the code base, to a tag file. The tag file then serves as the source of meta information for vim, so that you may navigate the code base easily. It is worth noting that the tag function is builtin with vim. No extra plugin is needed.

[This tutorial](http://courses.cs.washington.edu/courses/cse451/10au/tutorials/tutorial_ctags.html) provides a quite informative description of how to use it.

Briefly, here is how:

1. Create tags
To create tags for your code base: `ctags -R *`, `-R` is for 'recursively'. This will create tags for source files of all programming languages under current folder recursively. You will find ctags creates a file named `tags` under the current directory. *Ctag* also allows to specify languages by `--languages` option followed by a comma delimited list. To generate tags for Java and C++ source file for example, say `ctags -R * --laguages:Java,C++`

2. Use tags
	There are two ways to use tags.
	1. From your shell, say `vim -t tag_name`. This will get you directly to the first tag associated with the specified `tag_name`. For instance, if you say `vim -t Stop`, vim will open a source file with the cursor placed on the definition of the tag `Stop`, which can be a class, function, or a variable.
	2. If you are already inside VIM, here are the relevant commands you may use to play with the tags.

		|Commands   | Function  |
		|:---|:---|
		|**Control+]**   		   |Go the definition of the tag the cursor points to   |
		|**:ts** *mytag*   |Search and list for `mytag`   |
		|**:tn**   |Go to the nexttag definition   |
		|**:tp**   |Go to the previous tag definition   |
		|**:ts**	|List definitions for the last tag|
		|**Control+t** | Get to the last tag in the tag stack


A little more on the last command. Say you are trying to make sense of a class `A`. Sometimes you have to take a detour to understand the `B` which is referenced in the defintion of `A`. So you do `Control+]` on `B` and read the code of `B`, and then you want to get back to where you initiated the search for `B` because you want to end the detour and continue on `A`. `Control+t` will do the trick for you.

That's it. Have fun `VIM`ming!
