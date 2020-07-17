---
layout: post
title:  "Performing a Complete Codebase Review with GitHub and Merge Requests"
tags: code-review pull-request github
---
<img align="left" src="/assets/images/Octicons-git-pull-request.png"
width="200px" hspace="20px">

Code reviews should be a regular practice in any collaborative software
project, but there will undoubtedly be scenarios where an entire codebase (or
at least the majority of it) has not been scrutinised by proper review.
Certainly, this is the case for a lot of research software projects where
development by scientists did not follow software-engineering best practices.
Or perhaps it was just a single developer without the luxury of a second set of
eyes on the code.

Whatever the reasons for an unreviewed codebase, there is little value in
playing the blame game. It is more productive to ask how to move forward.
Obviously, code reviews need to be enforced for any new changes to the
codebase, and maintainers should be made aware of the necessity to do so. As
changes are introduced and code reviews performed on them, the portion of the
codebase that has been reviewed will gradually increase. 

However, this leaves a vast amount of code unreviewed for possibly quite some
time. Moreover, there may be structural design problems with the codebase that
require a higher level consideration in a more immediate time frame. It is
important to right the ship before it gets too far off course. For these
reasons, it might be a good idea to perform a more expansive code review that
touches most, if not all, of the current codebase.

On a practical level, this offers some challenges, so let's look how it can be
done. I will assume that all code reviews these days are done through a version
control web interface like GitHub. These web interfaces offer a convenient
layout and process for code reviews when performing merge requests (in GitHub
lingo "pull requests"). But merge requests are fundamentally designed for
small, targeted changes on a separate branch, so one needs to adapt this to get
a merge request of the entire codebase.

By looking at a merge request by the company
[PullRequest](https://www.pullrequest.com/), I was able to reverse engineer the
steps needed to perform a merge request on an entire codebase.

1. From a local copy of the repository for the codebase, create a new
   `delete_code` branch from your `master` or main branch. On the command line:
    ```bash 
    $ git branch delete_code master
    $ git checkout delete_code
    ```
2. Delete all files and commit: 
    ```bash 
    $ rm -rf *
    $ git commit -a
    ```
3. Push this commit and new branch:
    ```bash 
    $ git push -u origin delete_code
    $ git checkout master # for steps ahead
    ```
4. Fork the remote repository.
5. Pull fork to local computer and switch to `delete_code` branch
    ```bash 
    $ cd .. # get out of the original local repo
    $ git clone <fork_remote_url> <new_directory_name>
    $ cd <new_directory_name>
    $ git checkout delete_code
    ```
6. Add all files from `master` in original local repo to this branch, commit,
   and push:
    ```bash 
    $ cp -a ../<original_local_repo> ./
    $ git add -A .
    $ git commit
    $ git push
    ```
7. Make pull request on GitHub from the forked `delete_code` branch to original
   repository's `delete_code` branch.
8. Make comments on the code itself by going to "Files changed" tab of the pull
   request. There is the possibility to make suggestions in these comments as
   well. General comments can be added to the "Conversation" tab.
9. Add a reviewer to look at all of the comments.

