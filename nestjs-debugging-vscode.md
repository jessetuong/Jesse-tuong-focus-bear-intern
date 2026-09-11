# How do breakpoints help compared to console logs?
A console log only shows what you thought to print, at one point in time, and
requires editing code and restarting to add more. A breakpoint pauses real
execution: you can inspect every variable in scope, step
line by line, and even evaluate new expressions on the spot - without touching
the code or guessing in advance what you'll need to see.

# What is the purpose of launch.json, and how does it configure debugging?
launch.json tells VS Code how to start or connect to a debug session: which
runtime/command to run,  which port to attach to, the working directory,
environment, and which files to skip. It
turns "run this app under a debugger" into a one-click, repeatable action
instead of manual `node --inspect` flags every time.

# How can you inspect request parameters and responses while debugging?
Set a breakpoint inside a controller method. When a real HTTP request hits it,
execution pauses there and the Variables pane shows the method's parameters. 
Stepping forward into the service shows how that data transforms before the response is built.

# How can you debug background jobs outside the request-response cycle?
The debugger is attached to the whole app, not just the main modules, so it can be used with BullMQ. It pauses whenever that code runs, triggered by a job being picked off the queue instead of an
HTTP request. You just need to trigger the job while the debugger is attached and waiting.