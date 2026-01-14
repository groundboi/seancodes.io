---
title: 'Using devcontainers for easy cross-compilation'
published: 2025-01-14
#update:
draft: false
description: 'How I handled needing to build for Linux x86_64 from an ARM Mac.'
#tags: ['javascript']
#series:
#author:
#coverImage:
#toc:
---

## The problem

I've recently found myself in need of building very Linux-specific (i.e. interfacing with X11 and Wayland) software in C/C++. I'm very comfortable working in Linux, and for a long time it was my OS (I know, I know, it's _not_ an OS) of choice...though recently I've become partial to macOS. So naturally, as any software engineer does, my first question wasn't "how do I get this build done as fast as possible", but rather "how can I develop and build this with my existing tools/config/etc" 😎. I want to use all the dev tooling that I already have setup on my mac!

For me, that meant building on my ARM mac. I also had a strong preference to not build in a full-blown VM, since I don't want something that resource intensive always running, and I also don't want to have to maintain the VM state and install dupes of all the tools on my host machine in there.

I'm also aware that it is possible to cross-compile directly on a mac, in the same sense that it's technically possible to cross-compile from anywhere to anywhere, so long as you have the right toolchain. I didn't want to mess with this approach, since cross-compilation toolchains are always in varying states of maintenance and reliability. I also wanted to be able to do _the same build_ as any other folks who might be contributing, for consistency and reproducibility.

## The solution

So I thought...it's ~~2025~~ 2026. There _has_ to be some container solution for this. And sure enough, there is - [devcontainers](https://containers.dev/), the same thing that powers GitHub Codespaces. And so I began experimenting.

Using devcontainers turned out to be super simple. I essentially get to specify my own Dockerfile with any base image and system dependencies I want, build that image and run a container based on it, volume mount my current project in that container, and build right in there! Not fighting with sysroots, toolchains, etc. I can develop on my host machine with whatever tooling I want, and then build in the container.

### Why I love this

- You can target any platform and architecture, and use libraries specifically for those platforms
- It's an easily reproducible build environment, so team members can be confident that we aren't have "builds on my machine" issues, and new team members can get up and running fast
- By that same logic, _we can use that exact build environment in CI_. Knowing that your local builds and CI builds are exactly the same is incredibly powerful
- You don't have to manage any state of your build environment. Do whatever you want in it, wipe it away, and rebuild the environment!
- No more worrying about global/system packages interfering with the project's expected environment
- Develop using whatever tools you want on your host system! VS Code has native support for devcontainers, though for vim/neovim we'll take a more script-based approach
- The [devcontainer-cli](https://github.com/devcontainers/cli) abstracts away raw Docker commands, making it easy to work with devcontainers

### LSP setup for neovim

If you're a vim/neovim user, by this point you probably already had this thought:

> If I'm using the neovim on my host, but want to use LSP (in this case, the `clangd` language server), the language server on my host won't understand the Linux-specific libraries and where they come from! It won't be able to link or compile, so I'll get red diagnostic errors all over.

But guess what? It turns out it's not difficult at all to tell your host system neovim to use a language server running in the build container. It's essentially a one-liner in your neovim config to change, where you say "instead of running `clangd` for the language server, run `docker exec ...`".

Once I got that working, I had full LSP capabilities as if I was natively developing on Linux, despite developing directly on my host mac. It felt like magic.

## Just show me the code

Ok, ok...it's [on GitHub here](https://github.com/groundboi/devcontainers-cross-compilation/tree/main).

You can pull it down and try yourself to see how it easy it is. Or, see how simple it was to build in CI.

Oh and if that previous section on LSP config in neovim was relevant to you, check out `just nvim-lsp-config`.
