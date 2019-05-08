bookish-octo-succotash
======================

> Tic-tac-toe implemented in Vue.

Features Implemented
--------------------

This implements all of the given product requirements:

* The game should have some kind of interface for user(s) to interact. (e.g. in the browser or on the command line)
  * It presents a web interface upon running `npm start` and can be utilized with any modern web browser.
* It should enforce the basic rules and determine the end result of a game.
  * Players 'X' and 'O' take turns until one gets a 3-in-a-row, at which point the board locks and the winner is declared until the Reset button is pressed (or the page is reloaded).
* The user should be able to start the game
  * A new game begins upon page load or when the Reset button is pressed.
* The user should be able to take alternate turns to play the game
  * 'X' goes first, followed by 'O' until a winner or draw is declared.
* The logic should be able to evaluate the winner
  * A player can win by getting 3-in-a-row either in a row, column, or diagonal.
* The user should be able to stop an ongoing game at any point
  * If a draw becomes inevitable or a player loses interest, they can press Reset to stop the current game and begin a new one.
* There should be proper messaging when the game changes the state
  * The current player's turn is announced at the top of the board as turns are taken, and a winner is declared as soon as the conditions are met. When the board has filled up with no winner, it is declared a draw.

Decisions Made
--------------

I've been enjoying using Vue, with its Web Components-adjacent philosophy, for a few of my one-off side projects. I've been accustomed to bringing it in for small single-page/single-file apps, but decided this time to try a full-blown project initialized with Vue CLI. I'm pleased with the results, and I like how each component is organized, with separate `<template>`, `<script>`, and `<style>` sections.

Under normal circumstances, I would have taken the time to learn how to property perform automated tests on the components and business logic, particularly that which is at the heart of the game, and proceeded about developing it under a TDD approach. Instead, I decided to use my limited time to focus on designing the state management and delivering a fully-functional app, and left that exploration for another day.

At several points while designing the state management for the game, I thought to myself that Vuex, Vue's official state manager, would be a natural solution. However, every time I had that thought and again visited the [documentation site](https://vuex.vuejs.org/), I decided that, while that may be a logical long-term step, the upfront cost of building that in could no justify it for a project of this scope.

Although the UI works exactly as designed, I admit I'm somewhat out-of-practice when it comes to CSS Grid layouts. I would expect a more regular CSS engineer to recognize at least a few places where refactoring would be warranted.

How to run the game
-------------------

If you haven't already, install the latest version of Node (currently 11.14.0), or use `nvm` to install and use the correct version:

```console
nvm install
```

Once we're on the same page Node-wise (and npm-wise), install the npm packages:

```console
npm install
```

Start up the development server with the canonical `npm start`:

```console
npm start
```
