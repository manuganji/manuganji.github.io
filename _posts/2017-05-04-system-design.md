---
layout: post
title: "Part 3 of Management Series: System Design"
description: "Elements of system design"
categories: management
tags: [technology management, project management, design, systems]
modified: 2017-5-4
---
Good design is half the solution. I'll list down the considerations that make a good design. Obvious things like Redundancy and Availability are omitted as they are sufficiently well discussed by now.

# Scale

In my opinion Scale impacts everything in a project. Knowing the scale at which the system will operate at will really impact good design. Especially in Tech, the default approach is design for extreme scale (biggest, fastest, etc) which results in needless optimisation. In reality however, there are users at all levels of usage.

**Bureaucracy** - Scale changes the level of Bureaucracy. Higher scale means less flexibility to change or to experiment.

**Exponentials** - Not understanding exponentials has caused a lot of suffering. An exponential curve is not at all intuitive to human mind so you must pay special attention to exponential behaviours in system design. For example take a manual process that normally takes 2 hours per day. Now automating that might make process happen in 5 minutes but the impact of mistakes has also gone up exponentially.

Centralised systems (which most tech is) are good for standardisation and benefits of scale but they are always bad at handling diverse conditions. The diseconomies of scale are glaring once you look beneath the surface.

# Interventionist Bias

Its very hard to resist Interventionist bias. But its important to realise that _not doing something_ is also a decision.

**Rules are bad** - I can't remember the last time I saw rule that doesn't break under some condition. As soon as something bad happens we want to create a rule or a policy to make sure that doesn't happen again. But sometimes accepting a small risk is better than creating inflexible rules. This tendency to _do something about it_ is very hard to resist.

**Excessive Automation** - Again interventionists tend to forget the hidden redudancies of manual processes. Everything that can be automated need not be automated.

# Gathering Requirements for the System

I'll list down the order of preference for source of requirements

1. Experienced Practitioners: This is by the far the best source for requirements. They'd have done the processes thousands of times. Often manually or with little automation. They can often tell what they want and more importantly **why** they want it. They can be opinionated sometimes. One good filter is to pick the leader for your desired variable which could be RoI/ Time spent on job/ Least manpower required/ Maximum customer delight, etc.

2. Customer Interviews: Interviewing a bunch of potential users for your tool. This has one advantage - you get to hear multiple perspectives about the same problems. But it is also often that a small minority figures out the secret to success while the majority constantly misses the obvious.

3. Tinkering and Optimisation: You come up with an outsider approach to a problem and put something out there. You react to customer feedback and constantly test your assumptions.

# Transparency

The working of the system must be transparent to end users. Suppose someone made a tool to sum up the values on column A of a table. It may happen that total of values in column A and column B come out to be equal during January though in individual rows column A and B differ. It maybe convenient to implement a sum on column B and demo the correct answer. But that won't stay correct forever. At least after January passes. But I see such code surprisingly often.

**Revealed Systems** invite end users to use them in novel and _correct_ ways and also aid for redundancy in case they stop working for some reason. An opaque system which hides implementation almost always carries bad and complex design because it is closed for verification.

# Immediate Feedback

When things break, are being created or changed users expect immediate feedback. Make loud noise when things break. Users need to know if they are doing a good job. Its best to keep that feedback loop to the shortest possible. Also it should be dead simple to provide feedback to the Administrator.

# Integration into Workflow

Who doesn't remember a fantastic tool that the manager brings in which almost immediately gets orphaned? A good tool integrates smoothly into the workflow. Right from the language. Calling something an _invoice_ does make a difference versus just calling it a _document_. Everyone on the team must know who their end user would be, how their day goes like and how they talk about their work.

# Testing Assumptions

Everything is an assumption until proven. You could make assumptions about scale of usage, about a feature, the distribution channel and any other variable that could affect your team's fate.

# Behavioural Science

People are irrational. Imporant to understand that what looks good on paper is rarely what people do in reality because of their biases or prejudices. So the design you came up with could end up being used in a completely different way. So complement with visual cues and other behavioural science techniques to drive effective usage.

# Simple is better than Complex

There is an urge to look for complex answers. Simple answers are more robust to uncertainty. Complex answers are more specific and more fragile.

# Skin in the Game

Eliminate Agency problem. It happens when stake holders have asymmetric exposures to risk so that decision makers only enjoy the upside while being shielded from the downside. This is again an old idea but Taleb brought it back to focus in _Antifragile_. 

--- 

Resources to understand better.

* _Small Is Beautiful_ by E F Schumacher
* _Thinking Fast and Slow_ by Daniel Kahneman
* _Antifragile_ by Nassim Nicholas Taleb
* _Lean Startup_ by Eric Ries
* [Bret Victor - Inventing on Principle](https://vimeo.com/36579366)
