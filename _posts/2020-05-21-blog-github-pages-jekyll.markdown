---
layout: post
title:  "Creating a Blog on GitHub Pages with Jekyll"
tags: github-pages jekyll installation ubuntu
---

There are a number of inaccuracies in GitHub's guide for [setting up GitHub
Pages with
Jekyll](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll).
For those looking to get a Jekyll site running on Ubuntu, these pointers that
supplement and correct the guide should help. I will follow the same headings
and step numbers as on the page above, but won't reproduce that page in its
entirety, so this guide must be used in conjunction with that one.

# Prerequisites
It is pretty ambiguous how to satisfy the dependencies from the GitHub guide.
The concise and complete guide for Ubuntu is instead on Jekyll's page:
<https://jekyllrb.com/docs/installation/ubuntu/>

# Creating a repository for your site
Again, it is not very clear what needs to be done to get a personal page from
this section, especially if you are not using an existing repository for a
project. Skip the paragraphs at the top, and follow the numbered steps. Create
a repository on GitHub, and for the name of the repository use the format
`<github_username>.github.io` (e.g. for my case, `bielsnohr.github.io`).

# Creating your site
2) For my personal website, I chose my `PARENT-FOLDER` to be `~/sites/`.

3) Continuing with my own example `git init bielsnohr.github.io`. Good practice
   to match repository name on local machine with the GitHub one.

4) Use the master branch of your new repository since this is a personal page.

6) Don't need to navigate anywhere because the site source will live at the top
   level of the master branch.

7) This is where the guide is really inaccurate. The new
   jekyll site is initiated simply with the command 
```
jekyll new . 
```
(from within your local repository directory).  The version is then specified
in the `Gemfile` once it is created, so make sure to edit it with the line:
```
gem "jekyll", "~> 3.8.5"
```
To start using this version, do `bundle update`.

8) Once again, the instructions were inaccurate for installing the
   `github-pages` gem. Change the `Gemfile` as instructed, but run `bundle
update` instead of `bundle update github-pages` since github-pages has not been
installed yet and other dependencies need to be updated. 

13) There is a critical step missing before this one! If you are creating a new
repository, then all of the new content needs to be added and committed. From
within the local repository working, execute `git add -A .` and then push to
the remote directory as instructed in this step.

That should be your blog sorted now! The GitHub references for adding content
and viewing your page locally are all accurate from my experience, so consult
those to get blogging.
