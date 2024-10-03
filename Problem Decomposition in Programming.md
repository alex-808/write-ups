# In Progress

# Article 1

_Better to write something short (500 - 1000 words) of something high quality than write something long (2000+ words) of something low quality._

-   Brainstorming
    Something about design.
    I’d like to include examples, screenshots of things done well or poorly.
    Tricks I’ve been learning:
    -   finding balance with hot/cold (i.e. something is clearly too far or too close, too dark or too light)
    -   looking for inspiration
        Design for programmers
    -   rubber ducking design
    -   knowing the levers to push and pull - balance - unity - separation - cohesiveness
        When we are doing design, we are operating on people’s brains.
        Using AI to generate stylistic content
        Start from somewhere that you don’t pick: take inspiration either from an existing website, dribbble or AI
        Think about tools that serve similar goals. The ultimate purpose behind design is to make your app enjoyable and enticing to use.
        Here you have created this abstract tool capable of doing XYZ
        UX: it’s your job to frame what you have created to reduce friction.
        To some degree UI design is a matter of taste and marketing. But UX is a duty to your user.
        We’ve all had bad user experiences somewhere in our lives even if we haven’t thought of them that way. It could have been a website that took 5 clicks to complete a task that required multiple iterations or just the website being down.
        UX is everyone’s job. It’s how someone builds a relationship with a product.
        A good example of UX differences in design would be Google Podcasts (RIP) vs Podcast Addict. Something accessible and simple.
        I’ll point out that I looked to audible for inspiration because it follows a similar use case.
        Don’t try to reinvent the wheel. Look for ways that people have already solved the problem you have solved. If there is a competitor, look at their solution and try to improve it.
        Key points:
    -   UX is everyone’s job and UI is just one piece
    -   overcoming roadblocks
        -   the hot/cold method
        -   looking for inspiration
    -   don’t reinvent the wheel
    -   the role that UX/UI has in terms of shaping a thing
        I’d like to find a better word than product. Product implies commercialism and I want this to be more open ended.
    -   Tool: because you’ve created a piece of metal you can use to bash nails into wood but now you need to think about how people can use it. Who thought of adding a handle? Who thought about adding rubber to the handle? Who thought about adding a claw? - Hammers have been around for 3.3 million years. Claw hammers have been around for between 500 and 150 years.
        October 1, 2024 11:05 AM
        I’m not actually sure if UI/UX is the thing I want to write about first.
        I also was thinking about writing it as a case study. In many ways I think that may be more useful to others.

## Problem Decomposition in Programming

Finding the Words

Exponentiality of a problem

Key terms:

-   decomposition
-   golden path
-   abstraction
-   subproblems
-   best practice

### Introduction

I am fascinated by the dynamics between the art and the science of software development. There is no doubt that underlying the field is a mantel of physical, replicable scientific facts. For example:

-   Complex data can be stored and operated on via binary operations
-   The algorithmic complexity of linear search, O(n), will result in a slower retrieval time than binary search, O(log n) if all else is held constant
-   (Add one)

But a lot of the problems in the praxis of software development don’t stem from these issues. Many of the scientific facts are abstracted far away in libraries and tools we use every day like Postgres, Redis, React and even the languages themselves.

So what are we doing all day if we aren’t doing hard engineering?

I hypothesize that we are balancing the extremes of physical efficiency and unintelligibility.

There are always nearly infinite solutions to a problem in computer science despite popular discourse. Variations in solutions between developers could be as simple as having different names for the same piece of functionality (differing abstractions) or as complex as completely non-intersecting functional solutions.

As developers we are often trying to reach a consensus on the “best” solution. Best practices are handed down and around often without much thought. As a developer, often we can feel like we don’t need to think critically about these practices because they have already been “vetted” by the consensus of the community.

What I mean to say is that best practices are not scientific, they are social. The idea that React is better than Vue is a social truth, not an objective one. YMMV.

So why does this social truth emerge? Is it just because people like to have opinions and force them on other people? Well, if that’s true, you probably have some opinions on what food is good or bad, why don’t you spend much time trying to convince people that strawberries are yummy? Because it doesn’t matter, it doesn’t affect you if people don’t like strawberries and additionally there is an implicit understanding that an individual and subjective fact, not an objective one.

The reason this social truth arises in software development is because it _does matter_. It matters very deeply. Software development is most often a team sport and so it matters to strangers how you are writing your code because one day they may have to read it. The phenomenon is a form of social control, constraining the number of possible solutions to a problem but in so doing providing increased organizational efficiency at scale, comparable to a standard system design tradeoff.

I think this is one thing that isn’t spoken about enough. When most of us learned to program, we did it in isolation, our projects and assignments weren’t worked on by a team alongside us. They also generally didn’t take an extremely long time and years of iterations like most apps companies run in production. So DRY and KISS didn’t fit into our lived experience.

### Problem Decomposition

All of this is to say that problems are generally expressed in words but these words are not the problem. The words are a signpost to the underlying reality of the problem: the values that are missing from the memory which would be required to accomplish X or the physical machine that must be electronically connected to the overall system to support some functionality. Developers act on this underlying reality, sign posts are just sign posts, the computer’s memory doesn’t care how you describe it.

But on the other hand, where would we be without those signposts? Maybe a PM could give you a table of binary data representing the new state of the code in memory? That sounds like a lot for them to know and more in the scope of the technician responsible for the memory: you.

So we’re back to using signposts but remember, it’s your job to know that the signposts aren’t the problem. They are an abstraction over the problem. This abstraction will need to be held up against examination of the facts where it can be determined as actionable or inactionable. If it is inactionable decomposition maybe be needed.

We start with a problem to solve, a problem I had to solve in a side project recently. The problem is this:

**take a piece of text of arbitrary length and convert it to an audio version**

This problem statement is inactionable because it doesn’t include any tools or methods to accomplish the task. On the face of it, it is the equivalent of saying “do the dishes” without mentioning that doing the dishes requires some way of physically interacting with the dishes (i.e. your hands).

Already we have stumbled into the first step of a decomposition. Our signposts are out of sync with reality. This is a stage that most developers engage with intuitively. We’ll need to delineate our tools to make the statement sensical and actionable again.

### Finding the words

To properly decompose this problem into one or more subproblems, we’ll need to find the words to describe it. A useful mental model that can be used to generate these words is to do the following:

**run through, at a high level, how you would implement the problem statement as it is currently stated**

So let’s break this down:

-   **“take a piece of text of arbitrary length”** - “take” is a pretty overloaded term here. What does it mean to “take”? Where is this piece of text we need to “take”? Is it on a piece of paper? How is it getting to us? Is it already stored in a variable or returned from a function or passed back from a request?
-   **“convert it to an audio version”** - how do we convert it? What do we do with it after conversion, does that even matter? Are we making an mp3 or pressing a vinyl?

These questions can then be condensed into something more concise:

-   How are we going to get the text?
-   How will the text be converted to audio?
-   How will the resulting audio be stored?

There are an almost infinite number of possible solutions to each of these questions but with a combination of experience, intuition and research some solution can be reached for each. Although we are still at a high level in the process of problem decomposition we can make some conclusions:

-   we’ll be taking the input text from users via UI,
-   sending it over to the OpenAI API, wait for it to be converted
-   and then upload the converted audio to our database.

**_Input Text (UI) → OpenAI API → Database_**

### Naive Solution and Further Decomposition

This is our first solution. A simple “A” to “B” that seems straightforward. But this is a still golden path route to implementing the feature. Depending on the scale of a task or the complexity there will be more subproblems due to pieces of information not initially apparent from this still very abstract description of the golden path. What we have right now is a valid solution with the subproblems abstracted away.

Our first was: OpenAI has a limit on the number of characters that can be sent in a single message for audio generation.

This is a big one, but it makes sense. No system can take in a truly arbitrary amount of any data. There must always be constraints. For OpenAI the constraint was 4096 characters per message.

Ok so we’ll need a way to split the text, our path now looks like this:

**_Input Text → Chunk to 4096 chars → OpenAI API → Database_**

If you’re familiar with working with 3rd party APIs you may have already guessed the second subproblem: no only does the OpenAI API limit the size of the messages you can send it but it also has a _rate limit_: 50 messages per minute or more depending on your API tier. In my case it would be 50.

Because of our unique usecase it was inevitable that our users would be likely to submit more than 50 messages per minute:

50 messages \* 4096 characters = 204,800 characters

204,800 characters / 5 (average characters per word in English) = 40,960 words

The average adult fiction book is 70,000 to 120,000 words meaning that if just one user were to submit a book of this length, our app would hit that rate limit instantly.

We have two options:

1. allow the 3rd party API to do the rate limiting for us, i.e. constantly spam the endpoint with requests (maybe with exponential backoff to be a bit less obnoxious)
2. or internally rate limit our requests

OpenAI seem to be pretty good sports with developers and I’m pretty sure there are a lot of junior devs working on apps that absolutely hurang their APIs but in many cases 3rd party APIs are going to expect you to do your part and not push the physical limitations of their rate limiters with constant requests. Additionally, if you are using serverless as we’ll discuss later, all of these failed requests are going to require extra money.

Because this will be a production app we’re going to go with option 2. This protects us from situations that may arise as our user base grows. A few user requests spamming an API may not be a problem but a few thousand will almost inevitably make OpenAI take a second look at our requests.

So we will now need a new piece of infrastructure: a place to store messages until our app has enough rate limit available to process them. From experience on previous projects, I knew this missing piece would be a _queue_.

Queues can be thought of as a crumple zone for apps in system design: any area where the input for a piece of functionality is going to exceed the functionality’s capacity to output is potentially a candidate for a queue.

For example:

Service A (25 msgs per second) → Service B (5 msgs per second)

Here service A is producing more messages per second than service B can process. So what does service B do when it gets those extra messages? Where do those messages go? The messages can’t just disappear.

Well one option would be for service B to store those messages in memory but this is clearly a bad idea. Inevitably service B’s memory would be filled and we can also safely assume that if service B is a node primarily used for processing then that memory isn’t cheap. We will either need to scale service B’s memory in an expensive way or start losing messages and experience degraded performance due to the lack of available memory.

Another option would be to have service B return a “max messages limit reached” message to service A. Now service B doesn’t have to store the messages but service A does. Service A is also a processing node though and scaling it or having it assume this responsibility will cause all the same problems as shifting the responsibility onto service B.

The best option: create a node that is optimized for storage and retrieval between the two processing nodes.

Service A → Queue → Service B

The queue will provide cheaper storage and allow Service A’s input to spike far beyond what is immediately processable by service B and has the capability to retain the order of the messages in the case of a FIFO (first in, first out) queue.

Implementing this solution for our application looks like this:

Text input → Chunk to 4096 characters → FIFO Queue → OpenAI → DB

There is another problem to the rate limiting issue however: a queue generally doesn’t manage rate limiting. In our case we are using SQS which does allow for control over concurrency of the processing of the messages but it doesn’t allow for X number of messages to be processed in Y minutes.

Additionally a queue can’t send a request to OpenAI. When the model was this:

Text input → Chunk to 4096 characters → OpenAI → DB

We could assume that whatever server or serverless function used to chunk the characters could also be used to make the request but that’s no longer true. We’ll need another source of processing added to the chain to make the actual request. In this case I went with an AWS Lambda function:

Text input → Chunk to 4096 characters → Queue → Request Lambda → OpenAI → DB

The reason I went with a Lambda is the same reason people generally choose serverless: my jobs may be very sporadic and distributed unevenly throughout time. I would rather pay for compute as I need it as opposed to all of the time.

??? An additional bonus is that SQS integrates with Lambda very well: you can directly configure an SQS queue to call a Lambda.

So now we have a place to put messages when the 3rd party API doesn’t have available rate to process them but we still haven’t solved rate limiting itself. As it stands, X Lambdas (X being the concurrency we set) will be pulling messages off the queue, sending them to OpenAI and then handling the result but they have no persistent or shared knowledge of how many requests have been sent.

When a Lambda completes and a new message is available on the queue, a new baby Lambda is born. It has no idea how many other Lambdas there are, how many requests have been sent or how many messages are on the queue. All it knows is that it’s been sent a message and it’s the baby Lambda’s job to execute that message. So we need to point this baby Lambda in the right direction.

The key piece of information it needs to know is binary:

```jsx
if (requestsInLastMinute >= rateLimit) {
    // Place message back in queue
} else {
    // Process the message
}
```

Great, so we just need to store somewhere how many requests have been made in the last minute. Any external storage solution could work here: a db or a cache or even a load balancer. Cache is generally considered the gold standard in this case over a db because it is generally cheaper, more scalable and faster since all data is stored in memory instead of on disk.

A load balancer is capable of rate limiting as well but a poor fit for this use case (expand on this)

So we’re settled on a cache but what do we store there? Do we store a simple count of the number of tokens used in the last minute, i.e. 24, 67? When a lambda uses a token, it can just increment this count right? But how do we decrement it? Again, lambdas are babies that know nothing so they have no idea when the tokens were used. So another piece of data is needed: timestamps for when each token was used. With this a lambda can check this list, remove any timestamps used in the last minute and get the length of the updated list.

Awesome, we now have rate limiting: a major subproblem has been solved. But a new subproblem has emerged with how we are handling those messages which can’t be processed immediately and are sent back to the queue: if they are put on the queue they will just be picked up immediately by a different lambda. If the next available token is 60 seconds away, in the mean time lambdas are going to be picking up and putting down that same message ad nauseum wasting compute and driving up cost. We might not be harassing OpenAI anymore with these rate limited requests but we’re definitely spinning our wheels while we wait.

We could just tell the Lambda to sleep until the next available token is ready but this also will eat up compute and drive up costs. To solve this problem we need to look at the queue. Diving into our SQS documentation we can see that using the SQS client we can actually set a message timeout for a given message. This means that the message will essentially become invisible to workers associated with that queue.

In addition, because we are using a FIFO queue, processing will only be able to proceed on subsequent messages when previous messages have been processed. So if we find ourselves in a situation like this:

Message A (no timeout) → Message B (30 sec timeout) → Message C (no timeout)

message B’s timeout essentially rate limits the entire queue and will block all executions of lambdas until it can be processed.

The only thing we need to do is use our lambdas to return messages to the queue _with a timeout until the next available token will be available._ Fortunately we already know when the token that will expire first is since we’ve stored the timestamps of their use in Redis therefore we can just add 60 seconds to that and voila, we have a timeout that will cause a message to be pulled as soon as the next token is available.

Now to finish up we just need to get the data returned from OpenAI back into our database and handle any errors that may occur. For this we can just use the same Request Lambda to do the uploading in our case to a Supabase DB:

Text input → Chunk to 4096 characters function → Queue → Request Lambda → Redis → Request Lambda → OpenAI → Request Lambda → DB

We started with a simple problem and a golden path, remember?

**_Input Text → OpenAI API → Database_**

And now it looks like this:

Text input → Chunk to 4096 characters function → Queue → Request Lambda → Redis → Request Lambda → OpenAI → Request Lambda → DB

There are more underlying problems that can be solved here regarding efficiency but our goal as defined by the problem statement has been achieved.

So what happened here? In the end we didn’t end up writing any binary or machine code or manually switching 1s and 0s in memory. We didn’t interact with any of the fundamental scientific principles of computer science much at all in fact.

Our workflow is still an abstraction, not the table of 1s and 0s to program as described earlier. So what what are we standing on? What is this solution? Why does this iteration work when every other one didn’t?

Abstractions have risen to meet our new abstractions.

The reality underlying the signposts we used never changed. The OpenAI API needed text to be maximum 4096 characters before the signposts said so. What did change was our model of the problem, informed by updated data provided by attempting to apply that model to reality.

-   Notes
    October 1, 2024 6:57 PM
    I guess my inclination is to wrap this into some sort of narrative while not making it ham fisted. I want to elucidate a pattern that I’ve seen in programming which is the evolution of solutions and problems.
    I guess what this doesn’t get at so far is how do you find these problems? How do you find these solutions? I want to refine and share a mental model. It can be represented hierarchically
    October 2, 2024 10:48 AM
    Is evolution of a subproblem an adequate theme to achieve what I’m going for? I think it shows my problem solving process which is what I’m trying to delineate here. But in terms of value to other people I think that the value here would only be between beginner and intermediate.
    Are we maybe trying to do too many things at once? We are describing a problem solving process and it’s evolution and documenting how the solution evolved but the solution that evolved isn’t the point, the way we arrived at it is.
    October 2, 2024 12:46 PM
    It feels sort of gross to superimpose what I’ve already written with some meaning that wasn’t already there. I guess I felt like the point of the article wasn’t to write a technical document about how I implemented a certain feature, it was to explore the exponentiality of a problem.
    Things to add:
    -   using timeouts for efficiency
    -   details of fighting with rate limiting and optimization
