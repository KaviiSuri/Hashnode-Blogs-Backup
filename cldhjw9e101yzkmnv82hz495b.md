# Keeping it together with NX Monorepos: What are they?

So, you've been hearing a lot about monorepos. Maybe a little bit of turborepo, blaze, or nx. Or maybe you haven't! Anyway, in this blog, I'll explain what monorepos are, how I prefer to use them personally, and help you form an informed decision about them.

Traditionally, we always try to stick to the **one-project one-repo** principle, which works fine, but also has a few issues and needs some manual operations to keep in check. Monorepos give you an alternative to that approach.

## What are Monorepos?

> A monorepo is a single repository containing multiple distinct projects, with well-defined relationships.

This quote is from [monorepo.tools](http://monorepo.tools), and describes how nrwl thinks about them! So it's right from the source!

## Why though?

![[Pasted image 20230128163214.png]](https://monorepo.tools/images/monorepo-polyrepo.svg align="left")

So we generally have this approach of **polyrepos** that we follow, and they are fantastic! They prioritize team autonomy and each team can ship in isolation, without worrying about the other teams! It's incredible, it's magic! Let's not even think about Monorepos!

But wait, the user gets the app as a single version right? So, how is it possible that teams work in isolation and ship features, without actually collaborating? And that's where the poly-repo approach falls short.

> Polyrepos are good at isolation, but bad at collaboration.

Monorepos solve this, you have one repo. If you make a change, it's your job to make sure it works across the product. So your teams are divided by features/apps rather than on the basis of the tech they use.

### Version Management

Teams often need to maintain older versions to prevent breaking changes in projects where there are multiple repos, worked on in parallel. All these rituals and processes can take the developers' time, and they move away from actually shipping stuff.

Monorepos have 1 version, that's it! If you deploy a new version, it'll work, there's no older version to maintain, at least for internal APIs.

### Developer Productivity

In a monorepo, developers can not only confidently contribute to different projects, and use a consistent way of writing, building, and testing applications but also learn from various other projects and verify that their changes are safe.

### Atomic Commits & Rollbacks

As devs, we make mistakes, and sometimes it's so bad that we might need to roll back our changes. Well, monorepos allow for **Atomic Commits** that let you roll back the whole stack in one step instead of cherrypicking commits and hacking around.

### Shared Types

This is one of my favorite things about monorepos. If you use something like typescript on the backend or at least swagger to document your API. You can basically generate the API calls and the integration layer. This will not only make your integration layer less error-prone but also make the lives of your devs a lot easier.

## So is it a one size fits all?

Sadly, no. Although monorepos are awesome and I honestly think a very good for companies of all sizes (yes especially startups). There are a few things one might need to think about before going to the monorepo route.

### Tooling

Monorepos need good tools. You don't want to build without a cache, you don't want to build unnecessarily and you don't want to develop without constraints. It's often worth it to invest in good toolings like [**nx.dev**](http://nx.dev) or turborepo but it's an effort you need to think about.

### Learning Curve

Every new technology you bring to your stack will add to the stuff your devs need to learn to work effectively. Although good tooling can make this very easy to handle!

### Git

Git was not designed with monorepos in mind. So it might become an issue for very large codebases to manage a monorepo. But this is not an issue for most organs, and at the scale of google where you do face this, some tools help you manage it.

## FAQ

### Is it just keeping the code together?

No! A monorepo has code co-location, but the projects must have **well-defined** relationships to be called a **monorepo**.

### Won't it make my app a monolith?

![[Pasted image 20230128163231.png]](https://monorepo.tools/images/monolith-modular.svg align="left")

Not at all! Monorepos is just as much about **well-defined** relationships as they are about **single repositories**

### We are a startup, does it help me?

Yes, monorepos are amazing for startups. Utilizing opensource tooling will help you create the best possible DX for your team and help them ship faster without having to worry about the tedious procedures and rituals that polyrepos entail.

This also helps you do faster refactors, pivots, and stack-wide changes.

## What is Nx?

[Nx](nx.dev) is my tool of choice when it comes to monorepos. It's definitely not the only one, but I like it. It has excellent tooling, remote caching, vs code integrations, code generation, and a lot more!

At its core, it's a build tool that builds all your apps in parallel, adds a layer of caching, and makes sure to avoid unnecessary work. It's also awesome at developer experience and reduces the repetitive work devs do, to a minimum.

### Why Nx?

Nx provides you with tools that help you run tasks concurrently, and manage dependencies between projects. But so do almost all monorepo tools. How is it different?

#### Never Rebuild the Same Code

Nx is really smart about this. It can figure out whether the same computation has run before, and can restore files and the terminal output from its cache.

#### Remote Caching

Nx allows you to share your nx cache with your teammates and the CI system, thus maximizing efficiency.

#### Only Run What's Affected

> Nothing is faster than not running a task

Nx analyzes your project graph and can diff it against a baseline to determine which projects changed and what tasks need to be re-run. So on every PR, you can rest assured that there will be no unnecessary computation.

#### Amazing CLI

The nx cli is powerful and mostly runs on metadata. You can run targets in parallel for many projects, use distributed caching, and a lot more.

Doing `nx build` is enough to build all your projects in parallel.

#### Plugins

NX not only has an extensive suite of plugins both supported and community-built, but also has excellent libraries and APIs that enable you to write your own plugins.

You can make custom plugins, in the same monorepo, and use it then and there!

#### IDE / Editor Support

Nx has excellent IDE Support, you can see it for VSCode, Neovim, or Webstorm. Here's an example of what it might look like in VSCode.

![[Pasted image 20230128164603.png]](https://nx.dev/_next/image?url=%2Fimages%2Fnx-console%2Fvscode-dark.webp&w=1920&q=75 align="left")

#### Migrations

Migrations are boring, and hard but necessary. NX loves code-gen! They even have `nx migrate` command, that migrates your monorepo for you.

#### Interactive Graph

NX Gives you an interactive graph. You can visualize what projects depend on each other and what tasks depend on each other.

#### Distributed Computation

On CI Pipelines, NX enables you to run stuff in parallel. That's how it speeds up CI pipelines. It even provides templates for most major CI solutions in it's docs to get you started.

### The Mental Model

For any piece of software tooling, there are certain mental models developers need to adopt and learn.

In NX, there are a few concepts on which the whole tooling works. These are easy to understand and very powerful. An NX Monorepos is built of **projects** and **associated tasks/targets**. Projects depend on each other and these dependencies dictate how tasks are run.

#### Projects

Projects are modules of code that are decoupled from each other. They can be of 2 types:

1. **Apps** - In NX, apps are shells around libraries. They are individual applications that combine multiple libraries to do one single thing and do it well. Nx is very flexible in terms of how you can use it.
    
2. **Libraries** - Libraries are reusable code that may or may not depend on other libraries. You can choose to divide up your code into libraries however you want.
    

Projects depend on each other and that's how the whole monorepo dependency graph gets formed. These dependencies dictate how different tasks are run.

#### Associated Tasks / Targets

In a monorepo there are not just dependencies among packages, but also among their tasks. For example, whenever we build an app, we need to ensure all it's libraries are also built if changed or a "build" task might depend on "lint" task. They are specified in the `nx.json` file

```json
{
  ...
  "targetDefaults": {
    "build": {
      "dependsOn": ["^build"],
      ...
    },
    ...
  },
  ...
}
```

With these concepts, NX enables you to do a lot of stuff. It enables building projects faster, caching builds, saving time and more!

## Okay, I'm sold! How do I use it?

Monorepos are awesome! And so is NX. I hope you are sold on both of them at this point. This article feels already very long. So, in the interest of my sanity and yours, I've decided to break it up into a series!

> In the next post, I'll be demoing a fullstack setup, with 2 frontends, a backend and a few libraries, all powered by NX.
> 
> **Make sure you subscribe to my newsletter to get notified when it comes out next!**