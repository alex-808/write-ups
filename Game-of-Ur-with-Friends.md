# Ur.io Write Up in Markdown

Total Development Time: 93 hours 6 minutes

## Technologies

- Socket.io
- TypeScript
- SCSS/Sass
- React
- Node.js/Express

## Process

This project was created as an improvement on a previous project I had done
which implemented the same game in just vanilla JavaScript. That was actually my
first JS project I ever made. It has since been refactored and is relatively
clean but digging through the git history you would find vast amounts of global
variables, massive complex functions, poor variable naming technique and
hardcoded constants left and right.

My intention with this new iteration was to leverage my existing knowledge of
the game logic and build upon it. The primary goals for this version were

- To write a cleaner version
- To make it capable of online multiplayer
- To use this project as an opportunity to learn two new topics which fascinated
  me: TypeScript and Socket.io.
- To implement this version in React, using what I had learned from the mistakes
  of my previous React projects

The project was built client side first which forced me to encapsulate server
side code well so it would be easy to pull out when it was time to work on the
server. This method worked well, transferring the game’s data structures and
converting client side events into Socket.io API requests was a relatively
simple process.

Initially the game logic was scaffolded out feature by feature until the game
could run successfully as a local multiplayer game. Then parts of the code which
belonged on the server such as event handlers, the Game class and game state
were extracted to a Node environment and reconnected.

The next step took some delving into the Socket.io docs where I became familiar
with the concept of 'rooms' and ids for them which I ended up associating with a
game state. On top of this I built out some logic for special cases that now
existed as the game transitioned to a client-server architecture. For example I introduced logic to initialize games only when
a second player joined, logic to prevent too many players joining and logic to
delete the game state once both players had disconnected.

From there there were a few bugs to fix such as unhandled errors causing the
server to crash but then I moved on to design and coding out the CSS. I made
some graphical improvements over the previous iteration and ensured that the app
was 100% responsive.

Finally I added some quality of life features such as a notification system for
players and an improved game start/join flow and finally the project was ready
for deployment.

## Takeaways and Lessons

### Sometimes refactoring can get excessive

I was an am pretty happy with how my code is organized in this project.
Especially in terms of encapsulation and writing modular code and React
components with relatively simple APIs I think I was successful.

However there is a moment that I still think about which I think has been really
formative. Toward the end of writing the server side Socket.io code I decided
to extract all the socket event handlers to a new `controllers.js` file. I had seen
this done before in other projects and I personally favor smaller files as a
general rule so I thought I would try out the pattern. But as soon as it was
done I realized I had made the code more difficult to work with. Sure it
_looked_ cleaner but now all these event listeners which had had a closure on the
data passed to the Socket.io server had to accept one or even two additional
parameters.

Since then I have been introduced to a new one of those punchy three-letter
acronyms programmers love so much which fits the circumstance perfectly:

> AHA: "Avoid Hasty Abstractions."

Just because an abstraction _can_ be created doesn't
mean it should. Abstractions should meet certain criteria and in particular they
should be _useful_ and _appropriate_. Although one could argue that this
specific abstraction was appropriate, it wasn't actually useful because it made the
code harder to grok.

### React is not meant for everything

I have been using React for a bit over a year now and have misused it left and
right. I know this because with every new project I understand it a little
better and in particular understand what it is good at and what it is not. React
is presented as "A JavaScript library for building user interfaces" and this is
what it does best. JSX, components, state, lifecycle all good stuff in my very
humble opinion. Especially when you are building a medium to large complex app
with a large amount of reuseable components.

However I was really able to compare and contrast my experience in building it
in React with the experience of building the original version in vanilla JS. I
will admit that the comparision isn't exactly apples to apples, there was
certain non-trivial functionality added to this version. However the beginning
stages of this project were very similar to the other. Server side and client
side code were originally written together and extracted from each other later
meaning that implementing the core functionality of the game itself was
comparable, just Reactified.

All that being said, this implementation took a good amount more time to
implement in comparision to the version I had made a few years ago with
significantly less experience. The code quality was certainly higher but there is
just a certain level of boilerplate and prop wrangling involved in using React that
only really starts to pay off when a project is of a bit larger scale.

In this project I had very few components that were actually reused which really
meant that there wasn't much payoff.

I still love React, it's changed the way I think about my code. However I think
the moral here is the same as the one above: "Avoid Hasty Abstractions". Just
because you can introduce an abstraction doesn't mean you should. Abstractions
need to be both appropriate and useful. React
is full of opinionated abstractions which are generally useful for guiding larger, more
complex projects. But if you don't need them, they will probably just end up getting in
your way.

### React ❤️ TypeScript

From my experience the TypeScript support in React was excellent. I loved being
able to add type checking to things like state and props. There is such a peace
of mind that comes from declaring a interface for a component. But also, at
least for me I think it helps to mentally model a component and how it should
interact with its neighbors.

While I was
working on this project I was also starting to make my way through _Head First
Design Patterns_ which was written primarily with Java developers in mind and,
other than an _Intro to Computer Science_ course I had taken which predominately
used C, TypeScript is the only other statically typed language I had used to
this point. But working on this project gave me an appreciation for statically
typed language I didn't have before. It changed my conception of Object
Oriented Programming. It made me want to write every new project in TypeScript
because it made me feel as though I had been writing essays without
punctuation my whole life.

TypeScript works so well with React because TypeScript lets you reify what React
essentially implies. React is a framework with opinions but when you apply
TypeScript to it, it gives things like components a life of their own. You can
make components that aren't just theoretically reusable but actually reuseable
because the guard rails are on. You can say explicitly and exactly how you want a
component to behave and TypeScript will enforce that.

So yes, React loves TypeScript not only in the fact that it supports it well but
I think also from a recognition that TypeScript loves React back. It likes the
encapsulation components provide. It likes that React tunnels all this data around as
props. And it wants to protect that and make it better, more reliable and
easier.

### Socket.io is awesome but was maybe unnecessary

Essentially I used Socket.io as a glorified event handler on the server side. I
could imagine a version of this project where things like player movements were
just passed to different express API endpoints which would update the state on
the server and pass back the result to both players. And that probably would
have been fine.

Socket.io is more or less a wrapper around the Web Sockets API which allows for
low-latency, persistent, two-way communication between client and server.
What excited me
about using this library was this idea of rapid, low-latency communication which
I thought would allow for seamless and exciting gameplay. But
in retrospect, I made a board game. Board games just don't need low-latency to the
level which Web Sockets offer. Delays of even a full second or two would have
been acceptable in a game where someone may spent a minute or two pondering
their next move.

All that being said I am actually glad I used it. It made creating events and
event handlers a real pleasure and actually allowed for some nice quality of
life features for players such as a near instant notification system for
important things like if your opponent has connected/disconnected.

Although including Socket.io added some knowledge overhead and in strict terms
was unnecessary, I believe it's low-latency offered headroom to build out a
higher quality product.

### TypeScript is awesome but not stupid simple

This was my first project of a decent size using TypeScript and it definitely
gave me an appreciation for the depth and power of the language. At this point
there is still a lot I don't know. However I also think I am able to use most of
the most powerful features of TypeScript which for me is mission accomplished.

For anyone who is trying to pick up the language and has heard the phrase "All
JavaScript is valid TypeScript" as a argument for its supposed ease-of-use, I'd
like to warn you that it is not that simple. That statement is generally used to
imply that you can just start sprinkling a little bit of TypeScript in your code
and you can control the learning curve. However in my opinion TypeScript
deserves
the respect you would assign to learning any other new language. It is deep and
powerful and you will get out of it what you put into it. Your mileage my vary
but for me, taking a nose dive into the water gave me a better return than wading
in the kiddie pool.

### @types is your friend

The fact that any time I have ever needed to reach for the type definitions of a
dependency I'm using it's just been there is nothing short of magical. It took
me some poking around to actually believe that it wasn't just some automated npm thing and
was actually some amazing crowdsourced TypeScript support.

From what I can tell, the DefinitelyTyped organization which manages the type
definitions is completely distinct from the TypeScript organization but I wish a
reference to
@types would be included in the TS handbook. It may smooth some of the hurdles
to adoption. At least for new people like me.

### npm scripts are your friends

I have used npm scripts to a very limited level in other projects for simple
build or start commands but in working with TypeScript I think it is especially
valuable. For example at one point in this project I was directly executing my TypeScript
with a package called 'ts-node' but later on I had split the code between client
and server and I wanted to build them separately. After that, when it was time
to start deploying to a production server I had to start introducing new build
commands which would interpolate my environment variables into a build as well.

I'm sure you could organize all these tasks with bash scripts or something but
npm scripts are just a joy to use. They are nestled in with all of your
package's other most important data and it's all grouped in easy to understand
key-value pairs.

### In many cases conditional rendering is fine

In other projects when I have multiple 'pages' or 'views' in a React project I
would reach for React Router. After all it provides a layer of abstraction that
makes someone new to React feel like they are coding something more like vanilla
HTML/CSS/JS. And I do believe that layer of abstraction can be useful if not
essential in some cases. But for this project I decided to fight my instinct and
see what I could do with just raw conditional rendering. And it turns out that
the answer is: pretty much everything.

To simplify some of the complexity that can come with substantial use of
conditional rendering I just extracted all of that logic to a single "View"
component which pretty much just took in two props to determine which view to
render: the gamestate and the room code.

No room code? You need one to start or
join a game so let's render the `LandingPage` component. Room code but no game state? It
sounds like you have started a game but the server is waiting for another player
to join before sending you the initial game state so let's render the `WaitingRoom` component.

I think the key to embracing this approach is extracting this logic to a similar
`View` or `ViewController` component. There is a lot you can do with such a
component and some high-level state to simulate typical navigation.

## Challenges/Solutions

### Organizing SCSS

I have struggled with conventions around styling in React since I have picked up
the framework. Initially I was introduced to the 'one CSS file per component all
contained in one directory'
paradigm. Up until this point I had been working in monolithic CSS files so this
was a breath of fresh air for me. Finding things in these massive CSS files can
add a lot of friction to the development process.

But developing in this modular, isolated way also had it's drawbacks. Generally
in my work flow if I'm working with CSS, that's all I'm doing in the current
stage of development and I do not want to spend a lot of time flipping through
potentially nested directories to find a specific component's CSS file.

For this project I had decided to use Sass which I love as a practical, clean extension of CSS and because of this I was able to implement a pattern I had seen while poking around Github.
The project [takenote](https://github.com/taniarascia/takenote) also uses SCSS
and leverages it's `@import` method (now `@use`) to gather all the specific code
of individual components as well as globals such as variables and mixins and
create a single insertion point into the app via the index.scss file as seen
[here](https://github.com/taniarascia/takenote/tree/master/src/client/styles).
Using this method gives you the best of both worlds in my opinion, allowing you
to write your SCSS in a modular way while also centralizing it and making easy
to navigate. You can even keep that one-to-one relationship between stylesheet
and component while avoiding potentially brittle import statements in the component itself.

### Getting used to compiling TS

Although it worked fine for this project, I would recommend against using
`ts-node` as a sort of TypeScript stand-in for `nodemon`. You should get used to
compiling your TypeScript because it is ultimately meant to be compiled. In
addition at a certain point in my project it became very confusing what was
the source for what was being served in my local environment. Was it `ts-node`
directly executing the TS via JIT or was it the files in my `build` directory?
When was the last time I built them? This became a real problem.

Instead I propose a single source of truth: your built files. Use the `--watch`
flag with `tsc` to get compiling occuring on save and if you were writing server
code like I was with this project, just direct a `nodemon` instance toward the
`build` folder. Debugging problems like this can be very time-consuming so even
if you don't follow this exact advice, at least try to use a single source of
truth.
