# Portfolio

Total Development Time: 146 hours 17 minutes

## Technologies

- React
- Three.js
- Sendgrid API
- Netlify Serverless Functions

## Process

This site was started a year before it was completed with a lot of time where I
didn't work on it at all in between. It is also my first React project of any
significant size. There are many things about it which I am proud of but also
many things which I would do differently if I were to do it again.

The first step involved a lot of research: What do other web developer portfolios look
like? What should they communicate? What design principles are at play? What
should someone think and feel when they visit my site? I have a Trello board
full of dozens of developer portfolios which did things I liked, some small,
some big.

I decided that, since I was relatively new to design, that I wanted my site to
have a simple but clean aesthetic but would have some key features that would be
unexpected and hopefully impress. With that in mind I started experimenting
with designs in Figma until I was satisfied.

The idea for Three.js/Ammo.js physics simulation just happened to come about
because my previous project had also used Three.js so I knew the library and I
thought that introducing a moving 3D element to the site would make it stand
out. On top of that I thought of a way that it could still match the already
minimal aesthetic.

The large amount of development time which you can see at the top of this
document I attribute to two things: seemingly endless CSS iterations and wrestling with the Netlify serverless function in a stubborn way.

Originally this site was being coded in vanilla HTML/CSS/JS but I had recently
been introduced to React and had also figured out that, in programming, the
absolute best way to learn a new technology was to use it, so I pivoted. The
migration process was

## Takeaways and Lessons

### Figma is your friend, not food

I really don't think I could have made the design for this website without first
creating a prototype in Figma. Actually many prototypes. And that was the real
value. Up until this point I more or less would do my "prototyping" with paper
and then go straight to HTML/CSS which was a rough experience. I couldn't
express the specificities of designs I like I wanted to and so it resulted in a
lot of slow and tedious CSS tweaking.

But Figma allows you to do all that tweaking live with your mouse and makes it
cheap to work iteratively, constantly improving little by little. I find design very challenging but since I've started incorporating Figma into
my project workflow it also has become much more rewarding.

## Challenges/Solutions

### Debugging Serverless Functions

Here I made a huge mistake that wasted a bunch of time: I just kept pushing new
iterations of the serverless function up to production to test them instead of
testing them locally.

Instead, use the Netlify CLI to build and 'serve' your serverless function and
use Postman to test the endpoint. Setting up a serverless function is probably
never going to be a one-shot process so it's better to just set up your
environment locally to do some testing. And the Netlify CLI and Postman are
perfect for this.

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

I have worked on other projects where I have been burned by introducing a new
library into it only to start building around it and find out it is missing some
key features or doesn't play well with the existing code base. Because of this I
have become very hesitant about introducing new npm packages into projects,
especially if they are expected to serve a very central role.

AOS (Animate on Scroll) was very much the opposite. It is a beautiful library which is the closest
thing to drag and drop which I have seen since I've started coding. It might not
have the granularity of some libraries but it does what it does well and I was
very satisfied with using it.

### Moving from CSS to JSS

I recently have started working on an open source project which uses JSS for
styling and it has been a game changer. I have always wrestled with organizing
CSS in a React project and have never been super happy with the results. If I do
go back to change the styling of this project at all at some point in the
future, it will be written with JSS.

### Sanitizing User Input

This was the first project in which I was taking user input and putting it
somewhere potentially dangerous on the serverside. For the contact form, an
object containing the data of each field was going to be passed to the server
following the `onSubmit` form event and from there would be inserted directly
into an email template the serverless function, using the SendGrid API, would
use to fire off an email to my personal email address.

My logic for using this approach was that I did not want to set up a separate
'developer' email, I wanted to keep using the one I always used while also not
just leaving it on the internet for anyone to pick up. I had looked at setting
up captchas and ways of obfuscating the email address to make it more difficult
for site crawlers to pick it up but I didn't like the friction these approaches
could potentially introduce to the contact process.

I also knew that if I was going to take user input I would be opening up the
site to a Cross-Site Scripting attack but I also knew that the solution to the
threat was to make sure the input was sanitized before moving it anywhere
dangerous. This is done by removing elements of the input that may inject
malicious HTML/JavaScript somewhere it doesn't belong such as a `<script>` tag.

I knew Regex was an option for this but for things like this or Auth, things
with significant security implications, I think its best to follow the advice
I've heard and take advantage of a well-known library. So for this site I used
'DOMPurify' to sanitize the input right before it was sent out to the server.

The built-in HTML email validation is also quite good and, from my limited
testing, can prevent some basic XSS attacks if all you need to do is accept a
user email.

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
creating a new npm build script for production. Moving forward I definitely plan
on preparing project for the deployment process earlier on so the transition is
smoother.

### Slow load times

The loading times of the site are definitely still a work in progress but some
of the statistics I was able to improve were:

- Reduce data transferred over network by **51%**
- Reduce `DOMContentLoaded` event time by **21%**
- Reduce `load` event time by **27%**

The most significant activity I did to improve load times was image
optimization. I was able to diagnose the problem when I noticed in Chrome Dev Tools that a specific set of images were
unnecessarily large and significantly slowing the loading of another image that would
need to be available as soon as the page loads.

This was a great problem to have because it ended up teaching me a lot about
optimizing images for the web. These are the three main approaches I used which
got me these results:

- Downscaling images to appropriate size
- Compressing images
- Using appropriate image formats

For me, the biggest problem was that I had been using .png files for images that did not need to be high quality and
converting them to .jpg cut most of their file sizes in half. On top of that
they were much larger than they would ever need to be rendered on any normal
desktop monitor so I applied significant downscaling. Finally I was very
impressed with just how much lossy compression can be applied to images without any
noticeable loss of image quality.

### Creating multiple Three.js Scenes

There are a couple of tricks to this. In my previous project I had solved this
problem in a very non-optimal way: creating separate renderers for each scene.
But here I had to make performance much more of a priority: people might be
willing to put up with a little extra strain on their CPUs while using a music
visualizer but no one wants to put up with that just to see a developer
portfolio.

The way this is done is first to create a canvas element which covers the entirety of
the webpage from top to bottom. This is what the Three.js renderer will render
to. It's z-index is set to -1 so it will remain behind other HTML elements
except in the divs we want to expose it in.

Next, for performance reasons, we will only render a scene if it is currently in
the viewport. This way, although we may have 4 or 5 scenes, each with dozens of
boxes with their own distinct physics, we can save on performance. If I were to
go back I would want to also pause the physics simulation of any scenes not on
screen.

Finally when we set up scenes we associate it an HTML element which it will be
rendered into. When the renderer gets to that scene, it will use the associated
HTML element as a border to render inside of. Although technically the scene
extends beyond that we can limit the renderer to just that element.

#writeup
