---
title: Debugging Ruby command line applications
---

# Debugging Ruby command line applications

I write this mainly as a reminder for when I inevitably set the current side-project on hold and come back to it a few months/years later, but maybe it will help others as well.

In my day to day work, I am primarily a [puts debuggerer](https://tenderlovemaking.com/2016/02/05/i-am-a-puts-debuggerer/). It's fast, it works (almost?) everywhere, and as I switch projects quite often, it dispenses me from having to re-learn the specifics of each setup everytime I do. 
Sometimes, like in my current case, directly outputting debug message to stdout is not an option, so instead I rely on copious logging to a file on which I keep an eye using the loyal `tail -f mylogfile`.
But there are those other times, when the process becomes too involved and being able to step into the code and interogate the system state is simply more efficient, so switching to a debugger is the correct choice for me (this is mainly when I have no idea of what is happening and the debugger is assisting the discovery phase).

The problem is, I'm currently having fun building small TUI-based application in ruby. 
I'm putting together what begins to look like the core of a little Ruby TUI framework, which will probably end up being nothing, but I'm having fun and I'm learning, so that's good enough in my book

The problem is that my go-to debugging solution with Rails (which nowadays consist in dropping a `debugger` statement at a point of interest in the code and refreshing the page in the browser) uses stdin and stdout for user interactions, and tui apps have to get exclusive access to those to work, so when you reach a breakpoint in your code, your UI will be mingled with the debugger output, and input management will stop to work as the debugger has taken possession of it.
To be fair the current default situation in rails is the same as soon as your app needs multiple processes to work correctly, it's just that the impact is less disruptive in this context. 
Indeed, with the current default solution using foreman to manage your various processes, while in a debugging session in one of the processes, if the other one are chatty, their output will come pollute the debugger output. 
This is less disrupting as this is not the UI for the application so you can probably live with it, but this is nevertheless a subpar experience, which is being investigated [here](https://github.com/rails/rails/issues/52459), 
and one which I've worked around years ago by switching from foreman to overmind (or rather one evil-martians worked around many years ago by building overmind, many thanks to them)

But with my small terminal apps, it's not possible, so what's one to do? Remote debugging to the rescue! The modern incarnation of ruby debug is really pleasant to use, and setting this is a whole lot simpler than I remember it to be when I started out working with Ruby.

Running this:

```shell
rdbg --open my_script.rb 2> log/rdbg.log
```

will launch the program as though run with `ruby my_script.rb` and will stop its execution at the first line of the file, waiting for you to run (in another terminal window)

```shell
rdbg -A
```

and TAADAAM, you're back in business! 

The only problem I encountered for now is that I was seeing a flash of debug's own logs before my app screen displays, but this was too fast for me to read it, and when leaving the debugger, it exit output would break the current app screen.
Fortunately, it seems from a cursory look at the code that the gem only log to stderr, and redirecting from it to a file did the trick (This is what the `>2 log/rdbg.log` does).
There are also a lot of options I did not care to dig for now as my current problem is solved, like the ability to disable the "stop-at-startup" behavior, as well as the ability to inject ruby code prior to debugged code loading so I'll make sure to take a look at the docs next time I'm in a context complicating debugging.
