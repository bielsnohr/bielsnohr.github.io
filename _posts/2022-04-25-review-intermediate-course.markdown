---
layout: post
title:  "Review of Piloting a New Course: Intermediate Research Software Development in Python"
tags: training research-software RSE intermediate-level python
---

At the end of January and beginning of February this year (2022), I piloted a
new course at my institution which sought to teach _intermediate_-level software
development skills to researchers. In the immediate aftermath, I posted a short
thread of tweets on Twitter to share some of the experience of running the course.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Last Wednesday, I finished delivering a pilot of a new course at <a href="https://twitter.com/UKAEAofficial?ref_src=twsrc%5Etfw">@UKAEAOfficial</a> with the help of two colleagues from <a href="https://twitter.com/RSECulham?ref_src=twsrc%5Etfw">@RSECulham</a> (Kristian Zarebski and Sam Mason). Some initial impressions and further details... 🧵</p>&mdash; Matthew (@mattasdata) <a href="https://twitter.com/mattasdata/status/1490649293497196557?ref_src=twsrc%5Etfw">February 7, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

Understandably, this thread conveyed my initial impressions of how the course
went, but a further and more in-depth analysis was always planned. So, here I am
to make good on that intention and pick apart the course delivery, successes,
and challenges in more detail. I'll be quoting the content from the thread below
because it introduces much of what I want to discuss. The target audience for
this post is other people who want run this course at their institution.

The course is titled "Intermediate Research Software Development in Python" and
you can find [all of the material freely
online](https://carpentries-incubator.github.io/python-intermediate-development/).
It is important to clarify that this is a course about software engineering
practices and not more advanced features of Python. Python is merely the sandbox
in which to demonstrate and learn the intermediate-level skills relevant to
_most_ forms of research software development in all languages.

## Context and Motivation

> ❓Why? This was hatched as part of my SSI fellowship proposal. I identified a gap
> between what is taught by the essential, introductory @SoftwareCarpentry courses
> and the skills that researchers at my lab require day-to-day. Things like IDE
> use, automated testing, virtual environments, project structure and design, etc.
> The material developed by the SSI overlapped almost perfectly with these
> needs.

There isn't much to add to this, except my own personal journey of learning the
necessary software development practices for being a researcher. A Software
Carpentry workshop at the beginning of my PhD gave me a solid foundation to work
from, but I quickly found that the code for my research would require more than
a novice understanding of version control, the Unix shell, and Python. Although
I enjoyed independently learning about software engineering during my PhD, I often felt
uncertain about where to find authoritative content on how researchers should be
developing their code at an intermediate-to-advanced level. Sure, StackOverflow
is great, but it doesn't provide development path for someone follow. What is
important to learn, and what should be the order of those topics? The
shortcomings were obvious: I completed my PhD having never done, let alone heard,
about automated software testing, and my approach to design and architecture was
_ad hoc_ and completely shaped by the code within my research group. Given how
important I think testing is for software and the fact I was developing library
codes, that was simply not acceptable—but certainly not all my fault!!!

A direct consequence of this personal shortcoming was my desire to rectify it
for other present and future researchers, and hence, when I moved into an RSE
role, I finally had the time and resources to direct towards achieving that
through the delivery of training courses. This culminated in my SSI Fellowship
2021 and the formalisation of a plan to delivery an _intermediate_-level course
at UKAEA.

Now you know why, so let's get down to the practicalities of the course.

## Scheduling

> 📅 Scheduling? The course was run over four separate, half-day sessions in the
> afternoon, split equally across two weeks (Tuesdays and Wednesdays). This was by
> far the preferred format from the post-workshop survey.  It gave learners the
> time blocks they needed to focus on the material, while allowing flexible time
> between sessions to digest material and catch-up if needed.

These comments still hold true, but it is nice to see the other options that
learners were choosing from, and how they ranked them following the course:

![](/assets/images/scheduling_rank.png)

The second choice is "4 afternoon sessions, 1 session per week". I can see this
being suited to advanced learners who simply want a quick introduction at the
beginning and then just sit in breakout rooms with some helpers as they read
through the material and do the exercises. These are also the learners who tend
to have busier schedules, likely being higher up the seniority ladder, and
therefore a single session per week is much less of a time commitment. Although
I see the potential value of this scheduling, it is unlikely we will shift to it
unless it is clear more learners want it.

The third option is "4 afternoon sessions, all in the same week". My main
criticism of this is that it would make for quite an intense week, and the
likelihood of scheduling conflicts increases greatly: someone is going to have a
weekly meeting that clashes with one of the slots. While it isn't fatal to step
out of one of the sessions for a meeting, the process of catching up puts a
strain on both learners and helpers/instructors.

It is quite interesting that both of the "full day" options came in at the
bottom. Combined with the long form comments in the feedback, it is obvious that
learners appreciated having the morning half of the day to use as they pleased,
whether that be for usual work, or catching up on course content from the
previous day. The same can be said about having the course split across two
weeks: the interim time could be used for catch-up.

However, it is important to acknowledge the potential bias in the answers to
these questions. Participants have only directly experienced one of the
schedule formats, so they will undoubtedly tend to prefer that scheduling.
Regardless, it is fair to conclude that they did not _dislike_ the format nor
was it inconvenient.

## Teaching Format

> 📑 Format? A previous pilot of the course I helped with used longer breakout
> rooms for entire sections of the course with learners reading through the
> material. While this worked well, I wanted to see if a bit more instructor-led
> content might improve things further. So, I created a set of Jupyter-notebook
> slides to accompany the course website content:
> <https://github.com/ukaea-rse-training/python-intermediate-development/tree/ukaea-instructor-led/slides>
> Free for anyone to use. These give some guidance for introducing individual
> episodes, when to send learners into breakout rooms, and what material they
> should cover.

What I critically failed to mention was that in both cases the courses were run
completely remotely via Zoom, and also in both cases breakout rooms played an
essential role in the delivery of the course. It is important to clarify some
terminology as well: a section is the top level division of the course, and each
section is composed of episodes.

Therefore, the two key difference in the format of delivery was first the use of
slides to introduce each episode and in some cases eliminate the need for
learners to read content, and second the length and number of breakout room
sessions. I like to think of the main difference being in terms of the frequency
of "synchronisation" points. In the case of the UKAEA course that I instructed,
the synchronisation between breakout rooms tended to happen at the beginning and
end of each _episode_, whereas the SSI delivered courses are synchronised at the
beginning and end of each _section_. Again, these are both equally valid
approaches that I think have their respective merits and drawbacks.

What I like about the more frequent and shorter breakout rooms is that it
contributes to a cohesive and collective feel to the course. If the
breakout rooms are long, then it is effectively like each breakout room
has their own unique experience of the course that isn't shared with the other
groups. By returning to the main room more frequently to go over some high-level
concepts and share discussions from the breakout rooms, there is more collective
experience of the material.

On the other hand, more frequent synchronisation means that advanced learners
will more often be kept waiting in breakout rooms with dead time, even though
the total amount of time they might wait is the same in either case. In the
single breakout session per section format, advanced learners have a single
block of time during which they might wait, and they can more effectively put
that time to good use rather than the salami slicing that happens in the other format.

Moreover, whilst there was a lot of valuable discussion from the "report out" at
the end of breakout sessions, it did throw off the timing of the course, so
there will need to be some further reflection about whether it will be possible
to continue to do this in future iterations or how it might be fit in better.

Overall, the feedback supports that the teaching style with slides was
effective. The graph below shows the level of agreement with the statement "The
mix of instructor-led tuition and independent study and exercises was
effective", with 1 = completely disagree and 5 = completely agree.

![](/assets/images/int_course_feedback_tuition_mix_likert.png){:style="display:block; margin-left:auto; margin-right:auto"}

Asking a slightly different question showed similar results: "If the current
delivery of the course was said to represent a "5" on the scale below, where do
you think the balance of instructor-led to independent study should be for the
course? (0 - more instructor led, 10 - more independent study)"

![](/assets/images/int_course_feedback_more_instructor_led_likert.png){:style="display:block; margin-left:auto; margin-right:auto"}

This figures suggests there might be a slight preference for their being
more instructor-led components for the course, but likely the sample size is not
large enough to firmly conclude this. Based on written feedback, it seems the
main reason for why the instructor-led components were valuable was because they
eliminated some of the reading required from the main course pages. Reading
fatigue is one common point of feedback from the few iterations of this course
I have helped with.

Another important component of the course was a shared Markdown document. This
is fairly standard practice for Carpentries courses, but it is worth remembering
that even more advanced learners can still find this tool useful. I am hoping to
include a markdown template in the course materials at some point in the future.

Finally, a comment about what is to come. Moving to in-person learning will
require some adaptation. Zoom breakout rooms are actually somewhat difficult to
recreate in real life. Having seating arrangements that allow participants to be
in small groups but then also access the slides delivered by the instructor is
non-trivial. So, there needs to be thought about which venue is being booked for
the training.

## Feedback

> 💬 Feedback? We collected daily feedback from learners, and from initial
> inspection it is overwhelmingly positive. The breakout rooms with helpers was a
> consistent feature that learners found helpful. Some preferred a verbal delivery
> of the contents (i.e. using the slides) while others were quite impressed with
> the website content and happy to read through themselves whilst asking questions
> in breakout rooms. It is likely we will alternate between both formats in the
> future.

Having reviewed the full feedback, it is likely we will stick solely with the
slide-based delivery of this course. To accommodate different learner pace, we
will instead try to get some "additional exercises" into the course content that
advanced learners can do while they wait. This feature has come up in other
sessions of the course I have helped with, so it is likely to happen.

Universally, the content was seen to be useful and appropriately targeted.
However, Section 3 (Software Architecture and Design) of the course does deserve
some special mention. This is undoubtedly one of the more content dense
sections, with modules on programming paradigms like Object-Oriented (OO) and
Functional Programming. The figures show that this was perceived to be too much detail,
slightly more difficult, and probably not quite what learners where expecting.

![](/assets/images/int_course_feedback_sections_likert.png){:style="display:block; margin-left:auto; margin-right:auto"}

The lesson developers are aware of this from other runs of the session, so I am
certain this will get ironed out in the long run. The main way that I will seek
to mitigate this in the short term is to give more time for this section, whilst
perhaps starting to make an attempt at unifying the exercises from the
functional and OO episodes with the main "inflammation" project that is used in
the rest of the content.

## Improvements

> 📈 Improvements? VSCode seems to be a more popular editor at our institution, so
> we want to adapt the material to that.  Keeping to time was difficult. It is
> likely the course needs one or two extra half-day sessions when delivered like
> this.

There is certainly still the desire to get the lesson material compatible with
VSCode users. I am hoping to address this prior to the next iteration of the
course in May.

For this next run, I have added an additional half-day session (5 half-day
sessions in total), to ease the time constraints slightly. This is also more in
line with how the course authors are now running the course.

## Acknowledgements

It imperative that I thank some important people who made
this possible. First, the original authors of the course material, Aleks
Nenadic, Steve Crouch, and James Graham from the [Software Sustainability
Institute (SSI)](https://software.ac.uk/) deserve huge credit for developing
this incredible resource and making it freely available for all to use. Second,
my two colleagues from the UKAEA RSE Team, Kristian Zarebski and Sam Mason, have
my gratitude for being helpers of the course and ensuring the breakout rooms
were such a valuable learning environment.
