---
layout: post
title:  "Retrospective on Code Review in Research"
tags: code-review RCRC CW22 CW23 RSECon22
---

Code review plays a crucial role in ensuring quality in the software development lifecycle, and it
is a great practice for knowledge transfer within teams. However,
like with most standard software engineering practices, it is much less prevalent in the world of
research software development. It was this observation that led to the creation of the Research Code
Review Community (RCRC) by Hollydawn Murray (Health Data Research UK). I would like to take some
time in this post to reflect on the activities of the RCRC and some of the results for me personally
that came out of my involvement.

## The Research Code Review Community

<div style="float: right;width: 30%;padding-left: 20px">
    <img src="/assets/images/rcrc_square_20_80.svg" width="80%" padding-top="10px"
    padding-left="6px" padding-right="6px">
    <figcaption>© 2021 RCRC</figcaption>
</div>

Hollydawn led a rallying call at the beginning of 2021 to everyone in the research software
community to build consensus and awareness around good practice in code review. I came across it via
[a lightning talk at SORSE](https://sorse.github.io/programme/posters/event-036/). Acknowledging
that fostering this type of culture practice would require change at many levels, the RCRC (then
CRC) set out five working groups:

1. Diversity, equity, and inclusion
1. Code review during development
1. Code review at the time of publication
1. Recommendations for stakeholders
1. Training and education

I was involved with the "Code Review During Development" group, or "dev-review" for short. We made
steady progress towards defining guidelines to implement code review in the research software
development workflow. The final outcome was [a website with
flowcharts](https://dev-review.readthedocs.io/en/latest/index.html) to guide anyone developing
research software towards the practice of code review.

Sadly, like many volunteer-driven projects, the entire RCRC started to fizzle out
after about a year. It is an interesting topic why this happened in our particular case as with lots
of similar projects more broadly, but that is outside the scope of this current post. Personally, it
was a hugely valuable experience to collaborate with people from diverse domains, roles, and
countries, and it was one of my first true introductions into the power of the "open source" model.
However, I was still left with the feeling that our resource needed some further advertisement.

Our dev-review group gave one last kick at the can at CW22, running a workshop to get feedback on
the website and raise awareness about the project. But alas, we weren't able to garner the interest
we needed.

## RSECon22: Making Connections

The story of the RCRC doesn't quite end there. We all know how conferences can be great places to
connect with peers, and RSECon22 is no different. I was lucky enough to bump into another SSI
Fellow, Hannah Williams. In the course of our conversation, Hannah mentioned she had heard about my
work with the RCRC and said she would be interested to have the guidelines about code review
presented at her institution, the UK Health Security Agency (UKHSA).

Thankfully, Hannah followed up on this, and I was invited to give a talk at the UKHSA Code Review
Workshop in December 2022.

## UKHSA Code Review Workshop

I delivered [these
slides](https://doi.org/10.5281/zenodo.7410423) (embedded below) at the
workshop, and they seemed to be generally well received. It was interesting to see some of the other
code review practices happening at UKHSA, which contributed to my own awareness of the state of code
review in UK public sector bodies. Being an employee of a public sector body myself, it is useful to
know about the practices other organisations in similar positions are using.

<iframe src="https://researchcodereviewcommunity.github.io/ukhsa-code-review-workshop-20221207/"
    title="UKHSA Code Review Workshop Slides" width="100%" height="500">
</iframe>

## Conclusion

My journey in the RCRC showcases the transformative power of collaboration but also some of its
limitations when exclusively run by volunteers. I like to think that code review in research has
improved because of the RCRC efforts, but admittedly it is only a small step forward. More
positively, a chance encounter at RSECon22 facilitated by the SSI Fellowship shows how conferences
and fellowships can bridge gaps and extend the impact of community efforts.
