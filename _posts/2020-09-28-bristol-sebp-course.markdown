---
layout: post
title:  "Review of Matt Williams' Best Practices in Software Engineering Course"
tags: courses software-engineering
---


Following on from my [previous review of the Google Tech Dev
Guide](/2020/06/19/google-tech-dev-guide.html), I have completed
another course related to software engineering and am posting a review in the
hopes it will help others direct their own learning journey. This time, it is a
course by a fellow RSE at the University of Bristol, Matt Williams. It came to
me by recommendation on the UK RSE Slack. You can find the course material
online: <https://milliams.com/courses/software_engineering_best_practices/>

### Learning objectives

To round out my proficiency in _good_ (not necessarily _best_) practices of
software engineering. I would like practical steps and techniques I can apply
to my daily work to improve the code that I write.

### Brief summary of the course

The course is based on the use of Python, and the value of attempting to
complete it in another language is dubious. But the topics covered have
applicability outside of this particular language. It is broken into three main
teaching sections, accessible through a web browser:

1. Documentation (using Sphinx)
2. Licensing
3. Testing (using pytest)

Practical examples are employed throughout to introduce and explain the topics,
and then related exercises are given to help the student put this into
practice. At the end, a series of exercises tie all of the learning sections
together and reinforce them nicely.

### How would you evaluate you skill level in the material covered by the course?

Novice to Intermediate. I have fairly good awareness of documentation,
licensing, and testing, but my practical experience is usually working within
larger projects where the tool and standards have already been decided. I have
less experience starting from scratch and getting the tools and practices set
up in a project.

### Was the course too easy or too difficult?

For an intermediate level software engineer, this course will
be quite straightforward, and most would probably say easy. For a novice, this
course is spot on for difficulty, and I think that is probably the objective of
the course author anyway. Being somewhere between those levels, I found this
course easy at times but exactly appropriate at others. Personally, I would
have liked the course to reach just a bit further in terms of seeing how these
practices can be fully exploited and automated in a proper software project.
However, there are resources at the end of the course that likely do just this.

### Was the course useful to you? 

Notwithstanding my comments above, this course was very useful to me. For
documentation, it has made me realise that I need to get serious about sticking
to a consistent documentation standard in whatever language I use, and it gave
me a very nice introduction to how to get Sphinx up and running. I had also
usually hacked my way through reStructuredText, and this gave me the
opportunity to get more seriously acquainted. The licensing
section had no practical work attached to it, and I did have awareness of most
of what it said. However, now I know exactly where to go if I am trying to
decide what license I need for a project: <https://choosealicense.com/>.

Lastly, and certainly not least, the sections on testing were undoubtedly the
most useful to me. It fully convinced me that _pytest_ is a really powerful yet
intuitive tool for testing in Python. It will certainly be my default moving
forward as opposed to _unittest_ which feels really clunky in comparison.
Getting some experience, even toy examples, of Test-Driven Development (TDD)
and how easy it can be makes a convincing case for its use more broadly. In
fact, I actually found a minor inconsistency in the exercises related to the
`word_count()` routine, and used the tests to update the function so that it
produces results that match `grep`'s use of word boundaries instead of the
simpler implementation supplied in the course.

### What did you like?

The layout and teaching style is impeccable, and it is obvious a great deal of
thought and care has gone into it. Getting small, manageable bits of
information and then putting them into practice is a great way to learn,
especially content like this.

I particularly liked the final exercises since they really tied the entire
course together, reinforcing the points and techniques made earlier. 

### What did you not like?

It is very hard to pick any bone with this course. My one criticism would be
that it doesn't mention where testing data and parameters should come from. For
the initial toy examples, it is easy to verify what the correct answers should
be, but once one gets to the word count problems, it is impractical to do
manually, and this is a better reflection of what happens in the real world. I
have raised an issue about this on the course repository, and it seems like it
will be addressed shortly.

### How would you rate the course overall?

A solid 8.5/10

### Other comments?

This course certainly aligned with my learning objectives and has given me
practical techniques to apply in my daily work. I see it being of great value
to others on the spectrum of novice to intermediate in software
engineering proficiency.
