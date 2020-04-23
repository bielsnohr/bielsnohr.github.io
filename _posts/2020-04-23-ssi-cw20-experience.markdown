---
layout: post
title:  "SSI Collaboration Workshop 2020: Remote Unconference Experience and Notes"
tags: workshops unconference ssi cw20
---

## Introduction

All of us will doubtless have attended many online meetings over the past month
and a bit as a result of the Covid-19 crisis and lock down. Small group
meetings are quite manageable with today's technology, but most conferences and
events have not been able to adjust and have been cancelled. However, there are
some adventurous organisers at the Software Sustainability Institute (SSI) who
decided to attempt to run their Collaboration Workshop 2020 (CW20) completely
remotely. The purpose of the workshop was to bring together an
interdisciplinary group "to explore best practices and the future of research
software", with themes of Open Research, Data Privacy, and Software
Sustainability. It used an *un*conference style, and had about 70 participants.

I was lucky enough to sneak in at the last minute, and I want to share some of
my experience about what worked for running a remote *un*conference.


## What Worked for Remote Conferencing?

Three technologies were used to facilitate the workshop.  Everyone is sure to
be well acquainted with Zoom, and it was certainly up to the task of hosting a
remote conference of this size. An essential feature was Zoom's ability to
generate small breakout rooms on-the-fly from an existing larger video
conference. The *un*conference style would not have worked without this---see
below.

Second, a set of Google Docs and Spreadsheets, accessible and editable by all
participants, were used to both disseminate workshop information and record a
collaborative set of notes for all sessions. This was really clever and well
orchestrated. With minimal individual effort, I now have a set of documents
providing a nice summary of the workshop, including parallel sessions that I
couldn't attend, and a list of all workshop participants with their contact
details. Interestingly, these were also used as an avenue to ask questions of
speakers. As someone who can be quite timid asking questions IRL, this turned
out to be quite a useful feature that maintained anonymity.

Third, a Slack group was used to catch any general questions and conversation
outside of Zoom and Google Docs. The "Pets at CW20" channel was a personal
favourite, lending that lighter social touch which one would not expect from
a remote conference.


## What I Enjoyed from the *UN*conference?

This was the first event I have attended in the
[unconference](https://en.wikipedia.org/wiki/Unconference) style, not to
mention my first completely remote workshop. The main strategy of an
*un*conference is to organically have sessions evolve from the interests and
input of participants rather than a preset "top-down" organisation, which is
common to scientific research and academia more broadly. Even though it wasn't
in person, I felt it had many advantages over the traditional conferences that
I have attended in the past.

My personal favourite were the *knowledge cafés* (i.e. small breakout discussion
sessions of around 5 people). Using a Google Spreadsheet, participants were
able to suggest topics and then put their names against the topic they would
like to discuss. This facilitated conversation in a manageable group size on a
topic of interest that may not have otherwise been raised. Moreover, the direct
engagement and interaction with other participants was incredibly fruitful and
rewarding.  I find that this aspect all too frequently gets lost in traditional
conferences with a presentation followed by Q&As. Why not bake participant
interaction into the very fabric of the conference/workshop design? Genius.

That being said, free ranging discussions can have their downsides, so these
sessions also had a requirement of producing a small blog post. As a result, the
discussion had an objective, which prevented too many off-topic tangents. Watch
the [SSI blog](https://www.software.ac.uk/) for our group's contribution over
the next few weeks. We tackled the topic of "Improving the Maintainability of
Legacy Code".

There was a second knowledge cafe where participants were randomly split into
groups and given the task of coming up with a collaborative idea for the
Hackathon. Again, a great way to engage.

The other major part of the conference were the mini-workshops and demos. Three
or four short sessions of about 45 minutes were run in parallel, and this was
repeated in four blocks. Of course, the leaders of these sessions prepared
their material in advance. Participants had the freedom to choose the session
in each block that most interested them, giving a "Choose Your Own Adventure"
feel. I opted for sessions in the Software Sustainability Theme, but
participants could be as narrow or broad in their selection as they desired.
That liberty is again something sorely lacking in most conferences. My one
criticism would be that these sessions weren't long enough in some cases!

Another interesting *un*conference feature were the lightning talks: 15
participants had two minutes and one slide for any topic they wanted to
advertise. And I mean anything: there was one about mindful cross-stitching!
This format struck me as a nice way to encourage networking and collaboration
for later in the conference, although I think it would probably work better in
person.

There were keynote presentations that all participants attended, the
one vestige of a traditional conference. My belief is these were important to
give a sense of unity to the conference so that participants could have a
shared experience of at least some parts. 


## Other Highlights and Resources

- **Keynote on Open Research by Andrew Stuart**
  - slides: <https://drive.google.com/file/d/1sN8xdUYD9flusHxR0SfTFy7EpLaGiDAK/view?usp=sharing>
  - on the history and problem of p-hacking in psychology
    - e.g. Power Posing and Stanford Prision Experiment aren't real effects
  - Big concern: PhD student might try to reproduce a "definitive" effect and
    fail because the effect isn't powerful enough
  - Turing Institute has a handbook for reproducible data science

- **Speed Blog Breakout Session**
  - the Covid-19 crisis has acutely shown the importance of legacy codebases
  - the Imperial College modelling is based on undocumented C code that started
    development 13 years ago; that's 13 years of undocumented features and
    models that have been added! 
  - must be a maintenance nightmare, which impacts the trust we can have in the
    results even if they have been rigourously tested
  - we focussed on how to make legacy code more maintainable in this context

- **Demo Session: FAIR Software**
  - <https://fair-software.nl>: website that gives five actions that can be
    taken to make software more FAIR (findable, accessible, interoperable,
    reproducible)
  - my breakout session focussed on software quality checklists
  - it was quite a rabbit hole to get the Core Infrastructure Initiative ones: <https://github.com/coreinfrastructure/best-practices-badge/blob/master/doc/criteria.md>
  - we agreed a better one is probably from EURISE: <https://github.com/eurise-network/technical-reference/blob/v0.1/quality/software-checklist.rst>

- **Talk by Simon Hettrick on history of RSE**
  - <https://slides.com/simonhettrick/rse-professionalisation-cw20>
