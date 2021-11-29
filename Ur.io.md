# Ur.io Write Up in Markdown
## Technologies
Socket.io
TypeScript
SCSS/Sass
React
Node.js/Express

## Process
This project was created as an improvement on a previous project I had done which implemented the same game in just vanilla JavaScript. That was actually my first JS project I ever made. It has since been refactored and is relatively clean but digging through the git history you would find vast amounts of global variables, massive complex functions, poor variable naming technique and hardcoded constants left and right.

My intention with this new iteration was to leverage my existing knowledge of the game logic and build upon it. The primary goals for this version were
* To write a cleaner version
* To make it capable of online multiplayer
* To use this project as an opportunity to learn two new topics which fascinated me: TypeScript and Socket.io.
* To implement this version in React, using what I had learned from the mistakes of my previous React projects

## Takeaways

### Sometimes code splitting can get excessive

I was an am pretty happy with how my code is organized in this project. Especially in terms of encapsulation and writing modular code and React components with relatively simple APIs I think I was successful. 

However there is a moment that I still think about which I think has been really formative. Toward then end of writing the server side Socket.io code I decided to extract all the socket event handlers to a new ‘controller’ file. I had seen this done before in other projects and I personally favor smaller files as a general rule so I thought I would try out the pattern. But as soon as it was done I realized I had made the code more difficult to work with. Sure it _looked_ cleaner but now all these event listeners which had a closure on the data passed to the Socket.io server had to accept one or even two additional parameters. 

React is not great for everything
Socket.io is awesome but was maybe unnecessary
TypeScript is awesome

## Challenges/Solutions
Organizing SCSS
Getting used to compiling TS
Sharing types between server and client

## Lessons
@types is your friend
npm scripts are your friend 
Environment variables early and often


The project was built client side first which forced me to encapsulate server side code well so it would be easy to pull out when it was time to work on the server. This method worked well, transferring the game’s data structures and converting client side events into Socket.io API requests was a relatively simple process.

#writeup
