---
layout: post
title: My start in Functional Programming
description: "Know about some nice built-in utils to aid Functional Programming in Python"
categories: fp
tags: [javascript, python, fp, functional, functools, itertools]
---
I had been hearing about Functional Programming for a lot of time. [This](http://paulgraham.com/avg.html) Paul Graham's essay was a good one and piqued my interest. And then I saw this Pete Hunt's talk on React.js at a Meteor dev shop.

<iframe width="560" height="315" src="https://www.youtube.com/embed/qqVbr_LaCIo" frameborder="0" allowfullscreen></iframe>

I could instantly connect that the reason for majority of the bugs is state dependent design. A bug is simply your program entering a state that you didn't predict it to enter. The state is the value of all the variables in your program at any one moment. If you took a series of snapshots of your program's execution, you'd see a progress from one state to the next with each processor cycle. It's a great talk and I recommend you to watch it.

The 'Function' in Functional Programming comes from the mathematical definition of a function.

> A function is a relation between a set of inputs and a set of permissible outputs with the property that each input is related to exactly one output.

The general focus in a functional program is on the **what** not the **how**. The code tries to tell what is the output of a function and generally speaks less about how to get to that output. So, if you were looping over a list, you would generally user `map` function over writing your own `for` loop.

My favorite feature of FP is **Pure functions**. It means that functions should not have any side effect and their behaviour should be completely determined by their inputs. Pause and think about that for a moment. How much predictability that brings to your programs! 

My second favorite feature is actually using the fact that functions are first class objects in these languages. You can pass around a function just like any other variable. So you can make a function compose another function for use in that scope.

The [functools](https://docs.python.org/3.5/library/functools.html), [itertools](https://docs.python.org/3.5/library/itertools.html) and [operator](https://docs.python.org/3.5/library/operator.html) modules provide some great methods to get your program closer to this philosophy.

For example `functools.lru_cache` helps to memoize a function, `functools.partial` takes a function and few of it's arguments and returns a function that takes the remaining arguments. For example:

    def write_to_disk(directory, page, json_object):
        if not os.path.exists(directory):
            os.makedirs(directory)
        filename = directory + "/" + str(page) + ".json"
        with open(filename, "w") as f:
            f.write(json.dumps(json_object)) 

    write_page_to_disk = functools.partial(write_to_disk, "my_directory", 1)


`itertools.map`, `itertools.filter`, etc will help to avoid ugly looping structures like `for` and `while`.

`operator.itemgetter`, `operator.add`, etc also help to avoid some redundant code. Remember that item when you had to get the *[a]* of every *[b]* of every *[c]*? You can write that more elegantly:

    get_a = operator.itemgetter("a")
    get_b = operator.itemgetter("b")
    get_c = operator.itemgetter("c")

    a = get_a(get_b(get_c(input_obj)))

I tried not to duplicate anything that has been written already by other people. Please share your feedback in the comments.

Resources
-----------------

- I wrote a [python crawler](https://github.com/manuganji/fec-api-crawlerd) yesterday and I tried to do it in a more FP way.
- [Alexey Kachayev's talk at PyCon UA, 2012](http://kachayev.github.io/talks/uapycon2012/index.html#/)
- [Mostly adequate guide to FP](https://github.com/DrBoolean/mostly-adequate-guide) (in javascript)
- [ramda.js library](http://ramdajs.com/0.17/index.html)
- [A practical introduction to functional programming](http://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming) by Mary Rose Cook
- [fn.py library](https://github.com/kachayev/fn.py)
