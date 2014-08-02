---
layout: post
title: Debugging snippet for code igniter
description: "Use this snippet to profile/debug a code igniter from any point in the app"
categories: debug
tags: [debug, code igniter, snippet, profiler]
---
Use this snippet to profile/debug a code igniter from any point in the app.
The ideal place for this is in the controller right after you enter it.

{% highlight php %}

$this->db->save_queries = TRUE;
$this->output->enable_profiler(TRUE);

{% endhighlight %}
