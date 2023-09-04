---
title: "You Don't Need to "Learn" Svelte"
seoTitle: "Mastering JavaScript? You Don't Need to Learn Svelte – Here's Why"
seoDescription: "Discover the hidden power of Svelte – the JavaScript framework that feels like déjà vu. Uncover how Svelte simplifies web development, reimagining JS."
datePublished: Mon Sep 04 2023 13:49:32 GMT+0000 (Coordinated Universal Time)
cuid: clm4xuhs8000809mj2ujpepko
slug: you-dont-need-to-learn-svelte
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693294931730/49c9662c-d3a0-4dde-8ec8-34f48da253d2.png
tags: web-development, reactjs, svelte, svelte-vs-react, senior-software-engineer

---

# Introduction

What if I told you, You don't need to learn svelte! Not because svelte is bad, or not worth learning. It's quite the opposite. You don't need to learn it because you already know it! *Dan Dan Daaaannn...*

You've been working with JavaScript, crafting web marvels and wrangling code like a seasoned pro. You've tamed the wild async functions, navigated the treacherous waters of callbacks, and even had a dance-off with the quirky `this` keyword. So, **why on Earth would you need to learn something new**?

### What is this?

In this journey **we uncover a superpower, hidden deep inside you**, buried under mounds of react wrappers and redux sagas. Today, you'll come to realize that Svelte is not some arcane magic potion you need to memorize incantations or syntax for. **It's JavaScript, with a sleek makeover and a secret identity.**

By the end of this article, **you'll find that you don't need to** learn **Svelte—it's practically déjà vu with a futuristic twist!**

Svelte is suprisingly easy to learn, and it's still pretty awesome! So, Let's get to it!

# What is Svelte?

Svelte is a UI framework (we don't shy away from that word here, unlike some other "libraries", ahem ahem...), that's compiled, compact and complete!

It's extremely fast, easy to use and also [the most admired JS Web framework according to Stack Overflow Survey](https://survey.stackoverflow.co/2023/#section-admired-and-desired-web-frameworks-and-technologies).

# Why Svelte, You Ask?

## Compiled

With Svelte, there's no runtime needed. No need to send a few kilobytes of "SvelteJS" runtime on every website you ever built/will build. It's just a compiler with targets to "document.getElementById" instead of machine code.

## Concise

Svelte lets you write beautiful syntax, you know it already! It's HTML CSS and JS (it's like the Avengers of web languages, teaming up to form something magnificent). Svelte compiles it down to extremely fast and optimized JS.

It's like having your cake and eating it too, except it's code, and you're making it run faster than a caffeine-infused squirrel.

## Complete

Svelte comes with a state management solution (one of the best I've seen till now), and component-scoped styling (no styled components needed). It even has motion primitives for those jazzy animations that make users go "oooh" and "ah."

So, while you were busy `npm install`ing the bare essentials for your projects, Svelte was chilling in the corner, whispering, "I've got this, fam."

# It's all Javascript

Love it or hate it, Javascript is a very useful technology, and all the libraries, frameworks, and "meta" frameworks, are nothing but abstractions over JS (mostly leaky ones).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693294080856/65301be7-5198-4b58-bf0b-a64e85edf472.png align="center")

That's where Svelte shines, even though it's another "web framework", It doesn't throw a bunch of alien syntax at you, expecting you to decipher it like an ancient scroll. No, Svelte takes the familiar, battle-tested primitives, syntax, and concepts of JavaScript and weaves them into its fabric.

So, while other frameworks might introduce themselves with an air of mystique, Svelte strides in with a friendly nod, saying, "Hey, it's all JavaScript here. Let's create something amazing together."

# But why though...

Okay, Okay, I see you react lovers (I'm one too!), you might not be convinced yet. Here are a few examples to tip you to the right side...

## Effects/Reactivity

With react, here's what's needed to make something run every time a dependency changes

```js
function Component() {
	useEffect(() => {
		console.log("Count Changed!", count)
	}, [count])

	return /** jsx **/
}
```

Not so bad, is it? Now see what it translates to in svelte

```HTML
<script>
	$: {
		console.log("Count Changed!", count)
	}
</script>

<!-- html -->
```

That's it! Svelte automatically tracks dependencies, and you only need to label a code block as reactive (`$:`). It'll run the code any time those dependencies change.

## Stores/State Management

While in react, you might go with complex setups like zustand, react-query or redux. Svelte gives you an in-built solution. A fascinating, cutting-edge idea called "pub-sub". Yupp, it's that dumb.

```JS
/** store.ts **/
export const counts = writable({
	a: 0,
	b: 0,
})
```

```HTML
<script>
	import counts from './store.ts';
	import {onMount} from 'svelte';
</script>

<button on:click={() => $counts.a += 1}>
	Increment A ({$counts.a})
</button>
```

Here, the component only "subscribes" to `count.a`, unline what react context allows you to do.

> The `$` just before the variable name makes the component handle subscribing and unsubscribing to the store for you!

## Simple Lifecycle

While React uses some implicit behaviors of `useEffect` to do component lifecycles, Svelte is extremely explicit and simple

```xml
<script>
    // ...imports
    onMount(() => {
        // ... on component mount stuff
        return () => { // cleanup stuff 1 }
    })
</script>
<!-- Component Markup -->
<button>click me!</button>
```

If you wanna do something only once, just write it in the script tag! Unlike React Components, the bodies of the script tag of a Svelte Component are only executed when it's created.

## What if I want Redux actions?

To restrict changes to the store, all you need to do is this:

```JS
const _counts = writeable({
	a: 0,
	b: 0,
});

export const counts = {
	subscribe: _counts.subscribe,
	incrementA: () => _counts.update((counts) => {...counts, a: counts.a + 1}),
	...
};
```

A store is an object with a `subscribe` method. You're free to mold it as you please!

## Scoped Styles

```HTML
<script>
// ...
</script>

<div class="container">
	<div class="card">
		<h3>Name</h3>
		<p>Description</p>
	</div>
</div>

<style>
	.container {
		/** .. **/
	}
	.card {
		/** .. **/
	}
</style>
```

All of these classes are scoped to the component by default, "container" means nothing outside of this component.

You get all this, with 0 dependency and no runtime cost.

# But what about the "ecosystem"?

That's the best part, the svelte ecosystem is bigger than React! because it's all of the JS ecosystem.

You see, in the realm of Svelte, there's no need for those wrappers that you might have wrestled with in the past. Say goodbye to deciphering cryptic syntax or quirky APIs just to connect a wrapper to the actual library you want to use. Nope, with Svelte, it's as straightforward as it gets.

> It's like a direct line to JavaScript paradise – no middlemen required! 🚀

## Let's Look at an example

Imagine you're a developer aiming to add some stunning charts to your web app using the renowned "Chart.js" library.

### React: A Web of Wrappers

#### Step 1: Install the Wrapper

First, you'd need to find a React wrapper for Chart.js, install it, and cross your fingers that it behaves as expected. Also remember to use the `2` version.

```jsx
// Terminal
npm install react-chartjs-2 chart.js
```

#### Step 2: Import the Wrapper

Next, you import the wrapper, wrap your component around it, and pray there are no compatibility issues.

```jsx
// Component.jsx
import React from 'react';
import { Bar } from 'react-chartjs-2';

const ChartComponent = () => {
  const data = {/* Chart data here */};
  
  return <Bar data={data} />;
};

export default ChartComponent;
```

#### Step 3: Deal with Wrapper Limitations

You realize that the wrapper doesn't quite support the latest Chart.js features, so you resort to direct manipulation to achieve your goals.

> (I deleted the code here because it got too long 🤕)

### Svelte: The Direct Approach

#### Step 1: Add the Library

In the world of Svelte, you don't need a special wrapper. You just add the Chart.js library directly.

```HTML
<!-- Component.svelte -->
<script>
  import { onMount } from 'svelte';
  import Chart from 'chart.js';

  let chartInstance;
  let canvas
  $: {
	const ctx = canvas.getContext('2d');
    chartInstance = new Chart(ctx, {/* Chart config here */});
  }
</script>

<canvas bind:this={canvas}></canvas>
```

### And... Done!

No wrappers, no compatibility struggles – just plain JavaScript, building upon what you already know. Svelte's direct approach feels like a breath of fresh air, reminding us that sometimes, less is truly more.

# Sold! Sold! Where do I start?

Ah, the enthusiasm! You're ready to jump into the Svelte universe and flex those JavaScript muscles. Here we go!

## Step 1: Embrace The Basics

Good Documentation is a godsend in software, and [Svelte's Intro Tutorial](https://learn.svelte.dev/tutorial/welcome-to-svelte) is especially good. It's like the "Welcome to Svelte" mat laid out for you.

This is where Svelte gives you the first taste of its most-priced quality, its simplicity.

## Step 2: Craft a Mini-Masterpiece

Once you've completed the tutorial and seen how seamlessly Svelte meshes with your JavaScript prowess, it's playtime. Go make a project you've been thinking of building. Don't have one? Here are a few cool ones you can start with:

1. **Virtual Recipe Box -** So you never lose your favourite recipes
    
2. **Snippets Manager** - So you don't ever loose that bash command you keep safely in your bash history (I know you do...)
    
3. **Project Idea Repository** - So you don't need this list again!
    

It's your playground, play around, and you'll realize, how beautiful it is to just use JS and the web platform.

# Conclusion

Svelte is like a breath of fresh air among the syntax-heavy, complexity-mongering tools that exist in the JS ecosystem. You don't need to learn svelte, because it has a learning curve so small, that you won't even realize it when you learn it.

You of course won't become an expert in a day, but Svelte enables you to focus on building stuff rather than learning weird quirks of the framework.

So, whether you're a battle-hardened developer or a curious newcomer, consider giving Svelte a spin. It might just inspire you to view web development through a cybernetically enhanced lens.

> Alright, let's cut to the chase, my friend! You've just uncovered a goldmine of knowledge, and the fun doesn't stop here.
> 
> So, why wait? Dive into the excitement, join our newsletter community, and let's embark on this journey together. Your inbox is about to become the ultimate source of inspiration. Sign up now and stay ahead of the curve!