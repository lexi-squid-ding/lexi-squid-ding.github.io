---
title: "Vim Tricks: For when you don't have a mouse"
date: 2022-01-09
categories:
  - blog
tags:
  - env
---

_Why do people use vim?_

<figure>
    <a href="/assets/images/banana-slug-question.jpeg"><img src="/assets/images/banana-slug-question.jpeg"></a>
    <figcaption>This banana slug must have a question.</figcaption>
</figure>

[Hackernoon](https://hackernoon.com/why-vim-8m1r3z1k) has a more complete answer, but there are many benefits aside from not having to shell out for a new Apple mouse after you accidentally left it at the bottom of your backpack and squashed it in the TSA line. As someone who lives "in the cloud" during a lot of the workweek, vi/vim are installable on basically every machine- unlike modern GUI-based IDEs. In case you're daunted by the learning curve, fret not, because there are [games](https://vim-adventures.com/) and tutorials to help with the basics.

Here are a few life pro tips I've come across

### Add something to the end/beginning of each line
Have you ever needed to create a comma-delimited list from a text input like this?
```
# input
squid
octopus
whale
cuttlefish

# output
'squid',
'octopus',
'whale',
'cuttlefish',
```

Add a quote to the beginning of the line and a quote + comma to the end of the line.

End: `:%norm A',` & Beginning: `:%norm I'`

Explanation:
```

 %       # for every line
 norm    # type the following commands
 A*      # append '*' to the end of current line
 I*      # append '*' to the beginning of current line
```

### Find and replace
You've renamed a class and now need to change all occurrences of it in your file (oh no). Rather than using your IDE like a normal person (or perhaps you don't have one) try the following (from the [vim docs](https://vim.fandom.com/wiki/Search_and_replace))

```
:s/foo/bar/g # Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'.
:%s/foo/bar/g # Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.
```

Whatever you do, leave with `:wq`.[^1]


[^1]: unless you want to discard your changes, then it's `:q!`
