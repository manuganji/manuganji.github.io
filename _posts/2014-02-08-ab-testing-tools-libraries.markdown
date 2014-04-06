---
title: Tools and libraries for A/B testing
layout: post
author: manu
categories: A/B testing
---

We were looking for some good A/B testing tools and libraries for our internal products. These are some good projects we came across useful for production level deployments with commercially friendly licenses.

- [Six pack](https://github.com/seatgeek/sixpack) by [SeatGeek](http://seatgeek.com). I'm especially awed by the elegance of their approach. I was cracking my head about how to setup the infrastructure to run so many experiments for my startup. Here they are with such a dead simple approach to all of that big problems. It's cross platform. Requires very minimal setup and a lot of clients are already available in a language of your choice.
- [A/Bingo](http://www.bingocardcreator.com/abingo) by  [Bingo Card Creator](http://www.bingocardcreator.com). They also have a nice [comparison](http://www.bingocardcreator.com/abingo/compare) with other tools that take a more front end approach to A/B testing. You should definitely check their site even if you don't use it as the author explains some points about the importance of statistical significance in A/B testing.
- [Vanity](http://vanity.labnotes.org/) for Rails people
- [Optimizely](https://www.optimizely.com) is a commercial alternative. This one also takes a more front end approach leading to ease of configuration but limited in the functionality.
- Facebook released [PlanOut](http://facebook.github.io/planout/) which was their internal tool for Online Experiments. It also has an elegant straight forward approach.

I'll follow this up with a short tutorial on how to implement one of these for your project. In a few days. ;)

There will also be another post on why A/B testing is so important for organizations of all sizes.
