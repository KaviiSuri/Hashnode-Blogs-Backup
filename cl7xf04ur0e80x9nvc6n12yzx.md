## Going from a VSCode User to a Vim Wizard!

## Intro
Technology comes and goes, and so do text editors and dev tools. But, there are a few that stand the test of time and still remain actively used for more than 30 years. **Vim**, is one of them. In this era of *ram hogging* text editors and IDEs that feel like they were designed to run on supercomputers, **Vim**, a terminal-based text editor, still has [25% of developers as its users](https://insights.stackoverflow.com/survey/2019#technology-_-most-popular-development-environments). 

Tools are important. As devs, we are nothing but craftsmen forging beautiful and useful projects with simple tools at our disposal. As Lincoln said,

> **Give me six hours to chop down a tree and I will spend the first four sharpening the axe**.”
> 
> Abraham Lincoln

It's definitely worth exploring your tools and finding what works for you.

In this article, I'll not only discuss my journey with Vim and why you should use it too, I'll also give you a clear roadmap on how to go from a **VSCode user to Vim Wizard** and leave people around you in awe when you work.

## Why I started Vim?
Vim is cool. Objectively cool. But more than that, it's intriguing how a humble text editor that runs in the terminal competes with the likes of VSCode which huge corporations back.

Other options aren't that performant. It might not be an issue for everyone, but it was for me. VSCode, being made using electron, hogged all my Ram and made my laptop laggy. Vim proved to be very usable on my machine at that time. I started using it and got hooked! I've used it for a year now and it still feels like the best text editor for me!

## Why Vim?
There are many things awesome about vim, here are a few

### Vim is Fast
As I explained above, vim is fast. It's also small. Unlike other IDEs and text editors, it doesn't take multiple GBs on disk or RAM.

### Vim is Fast
No, it isn't a typo. Vim is not only fast, but it also makes you work faster. Like others on the web, I'm not claiming that saving a few keystrokes will bring a boost in productivity. But after using it for a while, vim becomes an extension of your mind, you just think of stuff and do it.

### Vim is everywhere
A random Linux machine, an EC2 instance, an on-premise server, coding prep platforms (like leetcode, hackerrank) vim is everywhere. Heck, even the note-taking app I'm using for writing this has a vim mode (yes, I'm using it!).

You can't rely on VSCode or IntelliJ being everywhere but you'll find knowing vim helps you work almost anywhere easily and productively.

### Vim is Yours
Although all the editors now are immensely customisable with extensions and themes (thanks to the amazing developers behind them), vim is one step forward (for decades). 

Vim provides a complete scripting language to configure your setup. The older, original vim uses Vimscript and the newer (and better IMO) Neovim uses Lua. Lua is a popular scripting language used in many places so you aren't learning a niche thing useful only in one place.

### Muscle Memory is better than Your Memory
People forget stuff, a lot! But while using vim, you build a muscle memory that lasts and makes you even more in the zone while working.


## How do I learn it?
I hope I've convinced you enough to give vim a try. Let's look at a simple roadmap to learning vim

### VimTutor and Learn Vim Extension - VSCode
The vim community has created vimtutor which has simple exercises to introduce vim and build your muscle memory. For VSCode users, this awesome extension called [Learn Vim](https://marketplace.visualstudio.com/items?itemName=vintharas.learn-vim) does the same right in your VSCode.

Try going through this 3 or 4 times to get comfortable and then move forward.

### Vim Mode in VSCode
Learn Vim actually makes you install an extension called [Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim). This extremely useful extension actually brings vim keybindings to your  VSCode. Some people just stop here and use vim bindings with VSCode. 

Before moving forward, try getting comfortable with using this for a week or two in your work.

### Real Vim - Minimal Config 
Once you are comfortable, you can get to the real deal. Download [neovim](https://neovim.io/). Use a minimal config with it. No fancy plugins for now! Get a basic color-theme, switch on syntax highlight, set up tab stops and auto-indentation.

Start using vim for basic editing tasks.

### LunarVim 
You could go crazy with vim and make your own config with handpicked plugins and here's an amazing playlist that does just that:

%[https://youtube.com/playlist?list=PLhoH5vyxr6Qq41NFL4GvhFp-WLd5xzIzZ]

But I won't recommend that. The vim ecosystem, although very awesome, can be overwhelming. Start with something that was handpicked for you. Start with [lunarvim](https://www.lunarvim.org/).

Here's a sneak peek:
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662718626344/6h7_n926i.png align="left") 

## What next?
You are officially now a vim user. You now have the license to act all snobby when someone asks about your dev setup.

Next, start following a few awesome people from the vim community:
- [The Primeagen](https://www.youtube.com/c/ThePrimeagen)
- [TJ DeVries](https://twitter.com/teej_dv)
- [Chris@Machine](https://www.youtube.com/c/ChrisAtMachine)
- And explore more!

## Do Not Delete VSCode!
Although you may not use it anymore, keep VSCode around. Around our magical world, is a muggle world. 
You always need to work in a team. Making an active effort your dev environment accessible to your teammates will go a long way. You will have people who don't know vim, please don't be a jerk and keep VSCode around for them. 

> So Keep it around! Keep it around for the muggles!


## Do you need this?
As much as I want you to join our cult (I mean, club. Ahem!), I'll admit that you don't necessarily need it. A good developer who knows his way around VSCode or WebStorm will be as productive as someone who knows his way around vim. Just make sure you understand your tools and use them to their full potential. 

I've seen many people just googling and fixing their configurations without understanding how it works. I once saw a dev manually run prettier from the terminal because he didn't know how to fix issues in the prettier VSCode extension. That'll slow you down.

We spent almost all our time with our tools and they help us do a lot. It's definitely important to understand them, learn them and explore to find what works for you.

Hope this article helped you, share screenshots of your new vim setup in the comments!