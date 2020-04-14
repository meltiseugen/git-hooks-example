# Git Hooks Example

If you are using Git as a Version Control System, then Git Hooks can surely 
improve your work.
This repository aims to showcase what are the most useful hooks, how to use them,
and what you can add to them.

### 1. What are Git Hooks?

Hooks are programs you can place in a hooks directory to trigger actions 
at certain points in git’s execution. 

By default the hooks directory is `.git/hooks` in every local repository.

### 2. What Git Hooks are there?
| Hook name          	| Description                                                                                                                                                                                                                                                                                                                                                                 	|
|--------------------	|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| applypatch-msg     	| This hook is invoked by `git-am`. It takes a single parameter, the name of  the file that holds the proposed commit log message. Exiting with a non-zero  status causes `git am` to abort before applying the patch.                                                                                                                                                        	|
| pre-applypatch     	| This hook is invoked by `git-am`. It takes no parameter, and is invoked after  the patch is applied, but before a commit is made. If it exits with non-zero  status, then the working tree will not be committed after applying the patch. It can be used to inspect the current working tree and refuse to make a commit  if it does not pass certain test.                	|
| post-applypatch    	| This hook is invoked by `git-am`. It takes no parameter, and is invoked after  the patch is applied and a commit is made.This hook is meant primarily for  notification, and cannot affect the outcome of `git am`                                                                                                                                                          	|
| pre-commit         	| This hook is invoked by `git-commit`, and can be bypassed with the `--no-verify option`.  It takes no parameters, and is invoked before obtaining the proposed commit log  message and making a commit. Exiting with a non-zero status from this script  causes the `git commit` command to abort before creating a commit.                                                 	|
| pre-merge-commit   	| This hook is invoked by `git-merge`, and can be bypassed with the `--no-verify option`.  It takes no parameters, and is invoked after the merge has been carried out  successfully and before obtaining the proposed commit log message to make a commit.  Exiting with a non-zero status from this script causes the `git merge` command to abort  before creating a commit. 	|
| prepare-commit-msg 	| This hook is invoked by `git-commit` right after preparing the default log message,  and before the editor is started.                                                                                                                                                                                                                                                      	|
| commit-msg         	| This hook is invoked by `git-commit` and `git-merge`, and can be bypassed with the  `--no-verify option`. It takes a single parameter, the name of the file that  holds the proposed commit log message. Exiting with a non-zero status causes  the command to abort.                                                                                                       	|
| post-commit        	| This hook is invoked by `git-commit`. It takes no parameters, and is invoked  after a commit is made.                                                                                                                                                                                                                                                                       	|
| pre-rebase         	| This hook is called by `git-rebase` and can be used to prevent a branch from  getting rebased. The hook may be called with one or two parameters. The first  parameter is the upstream from which the series was forked. The second parameter  is the branch being rebased, and is not set when rebasing the current branch.                                                	|
| pre-push           	| This hook is called by `git-push` and can be used to prevent a push from taking  place. The hook is called with two parameters which provide the name and location  of the destination remote, if a named remote is not being used both values will  be the same.                                                                                                           	|
| pre-receive        	| This hook is invoked by `git-receive-pack` when it reacts to `git push` and updates  reference(s) in its repository. Just before starting to update refs on the remote  repository, the pre-receive hook is invoked. Its exit status determines the success  or failure of the update.                                                                                      	|

### 3. Real world examples of hooks usage

The two most common hooks are `pre-commit` and `pre-push`.
Below you can see what I am using them for:

### 3.1 Pre-commit

Here you can add everything you want to perform before a commit is made
For example:
  * Linter checks
  * Reagange code
  * Reformat code
  * Optimze imports

```shell
#!/bin/sh

pylint
```

### 3.2 Pre-push

Here you can add what you woulf like to happen before pushing.
For example:
  * Make a merge or a rebase from the develop branch
  * Run the tests before making a push
  
```shell
#!/bin/sh

git fetch
git merge origin/develop
pytest
```