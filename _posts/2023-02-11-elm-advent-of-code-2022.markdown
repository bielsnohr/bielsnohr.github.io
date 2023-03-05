---
layout: post
title:  "Using the Functional Programming Language Elm for Advent of Code 2022"
tags: AoC AoC22 elm functional-programming
date: 2023-02-18
---

It has been over a month now since the joyful time of Advent of Code 2022 has
ended.[^aoc] In my third year of participation, I decided that I wanted to try
completing the challenges in a functional programming paradigm. Functional
programming is not something that has taken much foothold yet in scientific
computing[^scientific-functional-programming], but I have been hearing about it
more and more through some of the podcasts and blogs that I consume. Some of its
selling points include verifiably correct software (through formal
verification), enhanced testability, and robustness.

[Elm](https://elm-lang.org/) in particular is a purely functional programming
language that boasts "no runtime exceptions in practice" and has come up a few
times as quite approachable for those new to functional programming. Sure, it is
primarily focussed on web applications, which is far outside my domain of
scientific computing, but it is nice to see what other areas of software
engineering look like every now and then.

What I will try to convey is some general reflections of my experience doing
Advent of Code in a functional language in the hopes it might be informative to
both fellow beginners stumbling along and the more experienced experts who shape
learning resources available. Invariably, many of my comments are probably
specific to the Elm language itself, and I would welcome discussion how much
some of the obstacles I approached are endemic to functional programming more
broadly.

If you don't really care about that stuff and just want to see a nice little
website with my solutions to the problems (okay, just up to day 7), then you can
get that [at my deployed web app](https://master--resonant-cannoli-e63c3c.netlify.app/)

## Parsing Input

Something I truly didn't expect to struggle with was parsing input. The Elm
community and functional programming seems pretty sold on something called
[parser
combinators](https://theorangeduck.com/page/you-could-have-invented-parser-combinators).
They live in the esoteric world of language parsing, with things like
context-free grammars, LR parsers, and a whole load of other technical terms I don't
know being someone without a formal computer science training. I'm sure they are
interesting and cool, but my-oh-my they were not easy to use in Elm. Perhaps
this is just because of my inexperience with functional programming and parsing
in general, but it is certainly not something I have run into with other
languages when trying to do what are fairly simple parsing tasks. Take this
`Parser` I wrote for day 5:

```elm
stackParser : Parser (List String)
stackParser =
    loop []
        (\crates ->
            oneOf
                [ succeed (\char -> Loop (char :: crates))
                    |. symbol "["
                    |= getChompedString (chompIf Char.isAlpha)
                    |. symbol "]"
                , succeed (\_ -> Loop ("" :: crates))
                    |= symbol (String.repeat 4 " ")
                , succeed (\_ -> Loop (crates))
                    |= chompIf (\c -> c == ' ')
                , succeed (Done <| List.reverse crates)
                ]
        )
```

The task was pretty simple: take a string like

```text
"[A] [B]    [C]"
```

and extract the letters into the correct indices of an array. So `'A' -> 0, 'B'
-> 1, 'C' -> 3`.  It took absolutely ages to figure out with Parsers in Elm and
is anything but readable. The idea of parser pipelines seems nice in principle.
Something like this from the documentation looks great and understandable:

```elm
type alias Point =
  { x : Float
  , y : Float
  }

point : Parser Point
point =
  succeed Point
    |. symbol "("
    |. spaces
    |= float
    |. spaces
    |. symbol ","
    |. spaces
    |= float
    |. spaces
    |. symbol ")"
```

But my experience was that as soon as you need to do anything slightly more
involved, they get very complicated very quick. I'll acknowledge regular
expressions also aren't the correct tool for this task, but I'm not convinced
this is the best alternative.

## Array Handling

In scientific computing, arrays and operating on them is core to the domain.
Arrays are usually treated in a *mutable* manner (i.e. you can change the values
of an array in place), so I expected to take some time habituating to immutable
arrays, since immutable data is a tenet of functional programming. And yes, it
did take time to get used to, and I was frustrated many a time when I just
wanted to loop through some values changing them as I went along. But once I got
the ethos and hang of what is effectively "map-filter-reduce", I could see both
the clarity and efficiency of treating array data in this manner. This is a
pretty good example from Day 7 which involves a function looking to find the
smallest directory that can be deleted to free up the required amount of space:

```elm
findSmallestDirToFreeSpace : Int -> Int -> T.Tree Int -> Int
findSmallestDirToFreeSpace total_size required_size tree =
    let
        minimum_size =
            required_size - (total_size - T.label tree)
    in
    T.flatten tree
        |> List.filter (\a -> a >= minimum_size)
        |> List.sort
        |> List.head
        |> Maybe.withDefault 0
```

I find this really clean and readable. The array flows through each step of the
pipeline, and each of those steps is quite simple. However, the last line isn't
great because instead of indicating that a directory wasn't found through a
`Maybe` or `Result` type, I am giving up and just returning `0`. In general,
this was something I struggled a bit with: getting the required pipelines for
handling `Maybe` and `Result` types. Coming from the C-based world of scientific
computing, I'm more used to simple return values from functions indicating
failure or success (i.e. 0 or 1) or raising exceptions or errors.

### Recurse, Don't Loop

Related to the immediately preceding point about handling arrays in immutable
pipelines, one could still reasonably observe that it isn't immediately obvious
how this replaces our good friend the loop from imperative programming. Fair
point! In my brief experience of using a purely functional language, loops
tend to be replaced by recursive functions. Perhaps that is obvious to most, but
it was an interesting realisation on my part.

## Debugging

It goes without saying that debugging is an essential technique for any software
developer, and so I was quite surprised to find that Elm does not have any
debugger available for it! One is relegated to the technique of print
statements[^print-statements] with the built-in `Debug` package. But don't
expect these to become visible from the command line. No, you must run the
program in the browser, enable developer mode, and find the debug console.
I imagine this is standard stuff for web developers, but it was a
pain point on my first debugging expedition given I am used to everything
happening in an IDE or from the command line.

## Deployment

Another area where onboarding to Elm falls short is how you actually release
your creations into the wild. Sure, there is the "Elm architecture" guidance on
how to make a web application, but I am talking about how one actually deploys
that application and makes it accessible on the web. For a language that is
focussed on web apps, there is paltry and diffuse information on actually
disseminating an honest-to-goodness _web_ application. Perhaps these steps are
obvious to everyone in the Javascript and front-end world, but for a lowly
scientific software developer like myself, it took far longer to figure this out
than it should have.

An implicit and nearly unspoken assumption is that most Elm applications are
"SPA"s (Single Page Application). These are quite different from the hierarchy
of HTML pages that I am used to when dealing with things like static site
generators. A SPA is basically a single HTML page with some embedded Javascript.
All requests to the web site are routed through this single page which
dynamically serves the correct content based on the request. I don't claim to
understand the internals of how this works, so you will have to settle for this
hand-waving explanation or go try to decipher the Wikipedia page.

For the practicalities of deploying a SPA, it is similar to most web sites: get
a HTTP server running somewhere and put the appropriate mix of HTML and
Javascript in the places it expects. Again, this isn't particularly difficult,
but for someone new to web development it was far from obvious how to get this
off the ground. I had to cobble together the steps below from a variety of
different sources and scratch my head more than a few times along the way. It
shouldn't have been so difficult to get this information!

1. Build an optimised Javascript output from your main Elm program: `elm make
   src/Main.elm --optimize --output=dist/elm.js`. This instruction is available
   from a few different places, and [some][rtfeldman-elm-example] go further
   with things like `uglify`, presumably to get further optimisation. In the
   simple case, my feeling is this isn't necessary and overcomplicates the
   deployment process.
2. Create a simple `index.html` file that will use the Javascript generated
   above. I scavenged something suitable from the [Elm SPA tool][elm-spa-tool]:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
   </head>
   <body>
     <script src="elm.js"></script>
     <script> Elm.Main.init() </script>
   </body>
   </html>
   ```

   Elm Spa along with [Elm Land][elm-land] look appealing because they
   handle most of the behind the scenes practicalities that I am explaining now;
   however, if you haven't started your project using these tools, then they
   provide no information how you can convert a project to use their frameworks.
   Therefore, these were not options for me because I copied my project from
   [someone else who made a nice layout for their Elm advent of code
   solutions][albertdahlin]. But my main question remains: why isn't this simple
   bit of HTML available more readily?!?!
3. Combine the above with an appropriate web deployment solution. Netlify seems
   to be the go-to solution at the moment, so that is what I opted for. Complete
   instructions are available on the [Elm Land guide][elm-land-deploy], and the
   only thing I had to change was the build command in the Netlify configuration
   file, `netlify.toml`:

   ```toml
   # 1️⃣ Tells Netlify how to build your app, and where the files are
   [build]
     command = "npm install --global elm && elm make src/Main.elm --optimize --output=dist/elm.js"
     publish = "dist"
   
   # 2️⃣ Handles SPA redirects so all your pages work
   [[redirects]]
     from = "/*"
     to = "/index.html"
     status = 200
   ```

   The built application goes into the `dist/` subdirectory, so that is also
   where the `index.html` will need to live from step 2.

## Conclusions

Perhaps you can already infer that I was not swept off my feet by Elm. Whilst I
really enjoyed some of the functional elements of the language, it was an
absence of some essential bits like a debugger and deployment guide that
resulted in pain points and will probably deter me from starting any serious
projects with the language. I have also read a few stories on Hacker News lately
how the language is effectively dead and many are not happy with how the core
team has handled some updates, particularly the move from `0.18` to `0.19`.

#### Footnotes

[^aoc]: If you aren't familiar with "Advent of Code (AoC)", it is an annual
    recreational programming challenge where a single problem is released each day
    of advent (December 1 to 25). It's like an advent calendar for computer geeks.
    There has been lots of activity and engagement around the problems that thread a
    whimsical narrative. Find out more at [the official
    website](https://adventofcode.com/).

[^scientific-functional-programming]: [This Computational Science StackExchange
    post](https://scicomp.stackexchange.com/a/8999) nicely summarises some of
    the reasons why functional programming has not found the adoption and attention in
    scientific computing like it has in software engineering communities. It
    also gives some of the relative pros of functional programming as a
    paradigm.

[^print-statements]: There is nothing wrong with using print statements for
    debugging from time to time, but there are many cases where they simply
    won't cut it and a full-featured debugger is indispensible.

[rtfeldman-elm-example]: https://github.com/rtfeldman/elm-spa-example#building
[elm-spa-tool]: https://www.elm-spa.dev/guide
[elm-land]: https://elm.land/
[elm-land-deploy]: https://elm.land/guide/deploying.html
[albertdahlin]: https://github.com/albertdahlin/elm-advent-of-code
