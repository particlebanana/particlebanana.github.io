---
layout: post
title: The Containerization of Functions
---

For years the phrase *"software is eating the world"* has been a rallying cry to get more people writing code. As software begins to seep into increasingly new areas we are left in a world where the only growth industry is code, and even in today’s startup-fueled frenzy we can’t crank out developers fast enough to fill the void.

Unfortunately this leaves a large part of the world in a place where they are unable to contribute or participate, because the sheer breadth of knowledge needed to build a modern web application is staggering.

Today's developers must navigate a sea of constantly changing technologies and still manage to stay productive. To solve this we have begun moving more and more to an SOA (service oriented architecture) where large complex systems can be orchestrated by small independent and reusable components.

Technologies like [Docker](https://www.docker.com/) have made constructing and deploying these systems easier than ever before. Package managers such as [npm](https://npmjs.org/) have made it simple to share code and logic between systems. These things allow small teams to move faster and give less experienced developers the tools needed to create more complex systems.

The problem arises when we need to actually construct the pieces that make up these SOA components. We are stuck implementing the same boilerplate code over and over again and stringing together various modules with no standard interface. When you **require('my-cool-module')** you have no idea what you will get back. This is the major issue with module based development today.

What's needed is what I would call the containerization of functions. We need to focus on making it easier to get new developers on board and make it easier to maintain complex code bases so that we can focus on what's important: shipping code. We are working on a project for this now in the node community called [Node-Machine](http://node-machine.org/) which we hope will be a step forward in solving some of these issues.

By creating a wrapper around your logic that ensures you have a clear way of knowing exactly what a function takes as an input and what it returns, you make it easier for developers to quickly piece together complex pieces of logic and know that it will work. Machines allow your applications to be built in a tree like structure based on what we are calling *outcome oriented programming*. You can think of it as the *"if this then that"* of backend development. Machines take a set of declarative inputs and return a set of exits that represent outcomes in the processing of the function. By chaining more machines onto the exits of a parent machine you begin to create a structure that resembles a decision tree.

It turns out humans are really great at understanding linear processes. So when thinking about going to the store for milk for instance, we can quickly and easily break down the steps needed in the process. Get in my car, drive to the store, find the milk, checkout, drive home. What we often fail to do however is handle the edge cases in these processes. What happens if the store is out of milk? What if my card gets declined and I don’t have any cash? What if my car won’t start? And on and on. These edge cases are where software bugs come from. Outcome oriented programming and machines highlight these edge cases and give us a way to branch our decision tree logic.

![flow chart](/public/2013-02-13-the-containerization-of-functions/medium_chart.jpg "Chart")

Machines ensure that errors are handled and instead of returning error codes we have declarative outcomes. They also handle common issues like type checking and input validation to make sure what you are getting is actually what it says it will be. They have the benefit of being able to be packaged up and dropped into any application with a guaranteed fit. Similar to stacking shipping containers on a cargo ship you can stack machines together without worrying about the logic for connecting the pieces together. When you bring in a machine from the Twilio pack you know exactly how it fits into your application and what it returns.

You can start to imagine an interface that allows you to connect various machines together, similar to building out a breadboard. As you begin placing these machines together you begin to see the outcomes of the "circuit".

So leveraging the best pieces of the current application development process you have machines for building app code, npm for sharing these modules across systems and Docker for building and deploying the various pieces of the application. Combined these allow for developers to move faster and to create more maintainable infrastructure. It also lowers the barrier to entry, allowing more people to participate in the process.

The hardest part of taking an idea and turning it into a product is getting started. The more tools we can create to open up that process the better off we will be. Our tools are currently undergoing a new found renaissance as development is being moved to higher level abstractions. Instead of focusing on the lower level pieces we are free to experiment and solve problems quicker and easier than ever before. Hopefully tools like [Sails](http://sailsjs.org/), [Waterline](http://github.com/balderdashy/waterline) and [Node-Machine](Node-Machine) are helping to lower that barrier and provide a way to create cleaner and more maintainable code.
