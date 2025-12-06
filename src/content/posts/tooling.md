---
title: 'Developer tooling and engineering philosophy'
published: 2025-12-06
#update:
draft: false
description: 'A brief history of how I arrived at my preferred tools of the trade, and how they shaped my approach to software engineering.'
#tags: ['javascript']
#series:
#author:
#coverImage:
#toc:
---

## Origin story

When I started my first "real" job in 2013, I was asked "vim or emacs"? No, not as in which I preferred, but which one I wanted to use to start a development task. I had never even heard of them. I was hired as an applied mathematician, and I didn't even know how much I would be writing code, if at all.

I was working in an odd environment - it was air-gapped from the broader internet. Hence, whatever the hot new "modern" tools of the time were, they were certainly not available to me. But one can always count on the old reliables to be available, which is why I was asked pick between two text editors that have been around (in some form) for nearly 50 years at the time of this writing.

I picked vim. I had no real rationale, other than some of the coworkers I worked more closely with used it, and I figured they could show me the ropes. What I didn't know at the time was that that choice was one of the defining choices of my professional career, and ended up completely shaping how I work up to the present day.

:::note
I am by no means a vim-elitist. I fully recognize the randomness inherent in this origin story - if someone offered me VS Code, hell I probably would have chosen that ... and _it_ would have shaped my philosophy on how I write software over the coming decade. Truthfully, I probably would be an equivalent engineer to what I am today, too. Just following a different mentality.
:::

## An approach to engineering

One of the positives about working in a constrained, air-gapped environment is that it really forces you to learn the tools you use. You can't just download plugins. You can't even lookup tutorials or guides online. All you really have is `man`. And believe it or not, I've also read the entirety of vim's `:help` pages.

> As an aside, two of the most mind-blowing moments of my vim journey was learning how to compose commands with text objects (like `ciw`), and piping text out to external utilities for transformation (like `:!sort`). And turns out, it's also surprising how well you can make the built-in `netrw` work 😎.

Once you're working in these kinds of environments, before you know it you start to get a good grasp on what tools you can reliably count on to be available on a given system. And you then start to appreciate the UNIX philosophy of tools that "do one thing and do it well", which naturally lead you to develop an appreciation of simplicity. No complex software or architectures that try to do too much, or have too many dependencies.

I've brought this mentality to how I think as an engineer. To me, good engineering is about _managing complexity_ (an idea reinforced by [one of my favorite books on software](https://openlibrary.org/books/OL28736729M/A_Philosophy_of_Software_Design)). And complexity can take many forms. For example, is there a high cognitive load required to make contributions to the software? Does a simple feature or change require making modifications to several disparate areas of the codebase? Or, to steal a line from [a favorite website of mine](https://wthhyb.sacha.house/), _"can you explain to a junior developer what your system does without drawing a diagram that looks like a bowl of spaghetti"_?

Had my start in writing software been different, I don't know if I would be thinking this way. Sure, I'd have _some_ philosophy around software engineering, but I don't know if I'd be thinking about complexity the same way I do now.

## Now back to tooling...

The above approach has shaped how I think about developer tooling for a long time. For example, I would restrict myself to tools that could be found in standard Debian package repositories (commonly mirrored in offline environments). This allowed me to be agile - I didn't need to spend hours setting up a development environment to be "just right". I could get by with `grep` (thankfully `ripgrep` was typically available in Debian package repos) and ... _gulp_ ... `ctags`. I feel like a dinosaur just mentioning `ctags`.

It took me awhile to shed some of these extreme restrictions, but I'm glad I experienced life as an engineer this way early in my career. Even when I had the internet available to me, it took me a _long_ time to feel OK about using my first vim plugin, and _even longer_ to move to neovim (and btw, I'm never going back).

These days, I'm definitely using more modern tooling (at least by my standards), though I am still selective about what tooling I adopt. The standouts include `neovim`, `fzf`, `tmux` (which I could write a whole post about...), `ripgrep`, `zoxide`, and more recently `zsh` and `ghostty`. I'm also loving the renaissance of TUI software like `k9s` and `opencode`.

I'll end this post with an obligatory [link to my dotfiles](https://github.com/groundboi/dotfiles), though they're about due for a little tidying up!
