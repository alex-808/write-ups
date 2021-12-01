# Portfolio Site Write Up in Markdown

Total Development Time: 146 hours 17 minutes

## Technologies

- React
- Three.js
- Sendgrid API
- Netlify Serverless Functions

## Process

## Takeaways and Lessons

### Netlify CLI and Postman are must haves for serverless functions

### Figma is your friend, not food

### Monkey Patching

### Defining an MVP

## Challenges/Solutions

### Making things super responsive

### Tricky CSS Stuff

### Using configuration objects

This was a solution to a problem that I didn't actually know was a recognized
pattern at the time and actually felt a bit embarassed by. However after reading
how other developers had approached this problem I realized that this was
actually a relatively established pattern.

This portfolio was actually my first React project which I designed myself and
so I hadn't yet encountered certain problems on my own. This site was going to
be my portfolio and because of that it would need to contain a lot of writing.
So when I started initially coding it out I embedded much of the site's copy
into the JSX of different components.

But I had just finished a project which had introduced me to the concept of
modularity or rather what happens when you don't incorporate modularity into a
project and all this embedding of text and copy just didn't feel right. What if
I had to change something? I would have to hunt down the component the text was
contained in and change it there. That sounds miserable.

Using React for a site which could just as easily been completely static like I
did here is absolutely a case of "If all you have is a hammer, every problem
looks like a nail" but it came with an advantage: I could leverage my
understanding of how data is routed through a React app via props to centralize
all my copy data and just let it trickle down to the different props that needed
it.

And that's what I did. The main idea behind a configuration object is generally
to avoid repetitive markup in a given component's return/render by creating an
object that a component can just map through instead but here I took one step
further and created a configuration object for the whole project.

It was much easier to use as editing my content just meant one trip to my
App.jsx and sometimes it felt like I was editing my site in a WYSIWYG web site
maker. The one thing I would change is just to maybe extract out that object to
it's own JSON file. But I'm at a stage where I go back and forth on decisions
like that. It's nice to see the entry point for the data on the one hand but
it's also nice to have a little separation of concerns.

### Adding dynamicism with AOS

### Moving from CSS to JSS

I recently have started working on an open source project which uses JSS for
styling and it has been a game changer. I have always wrestled with organizing
CSS in a React project and have never been super happy with the results. If I do
go back to change the styling of this project at all at some point in the
future, it will be written with JSS.

### Sanitizing User Input

### Environment variables early and often

There is a concept introduced in _The Pragmatic Programmer_ called "tracer
bullets" which is basically the idea of scaffolding out areas of uncertainty in
a project to help you acquire your target. This scaffolding will either succeed
or fail and will either give you an opportunity to build off of something or
rethink your approach.

> Look for the important requirements, the ones that define the system. Look for
> the areas where you have doubts, and where you see the biggest risks. Then
> prioritize your development so that these are the first areas you code.
>
> -The Pragmatic Programmer

In this situation I feel that my tracer bullets did not go as far as they should
have early in the project. The end goal of this project, as with most, was
deployment to a production environment, yet I spent about 90% of the development
time purely running things locally. But getting things ready for a production
environment after most of the project has been built introduces some
inefficiencies and the potential for significant problems down the road.

In particular for the serverless function which handled automated emails fired
via the contact form there were secret API keys which I kept adding and
removing from the file to ensure they wouldn't end up on Github instead of just
creating a new npm build script for production.

### Slow load times

### Creating multiple Three.js Scenes

#writeup
