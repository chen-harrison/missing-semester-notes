# Shell Tools and Scripting

### Variables and Operators

- `foo=bar` for setting variables, access with `$` like `$foo`
    - No space between `=` and variable/expression!
- Strings defined with `''` will not substitute variables, but  `""` will:  
    `echo "$foo"   # bar`  
    `echo '$foo'   # $foo`  
- In addition to program output via `stdout` and `stderr`, programs give a return code - 0 means good, != 0 means an error
- Important variables:
    - `$0` = name of the script
    - `$1` to `$9` = arguments to the script. `$1` is the first argument, etc.
    - `$@` = all arguments
    - `$#` = number of arguments
    - `$?` = return code of the previous command
    - `$$` = process identification number (PID) for the current script (?)
    - `!!` = entire last command, including arguments
        - If a command fails due to missing permissions, quickly re-execute it with sudo by doing `sudo !!`
    - `$_` = last argument from last command. `alt` + `.` does the same thing
- Logical operators: allows exit codes to be used to conditionally run commands
    - `&&` = “and” operator, e.g. `COMMAND_1 && COMMAND_2`
    - `||` = “or” operator, e.g. `COMMAND_1 || COMMAND_2`
    - `;` = same-line command call, no dependency, e.g. `COMMAND_1 ; COMMAND_2`
    - `&&` and `||` are short-circuiting, so not all commands will be run if the outcome is determined partway through. These can be combined with true or false, which are programs that always return 0 and 1, respecively
- `$(COMMAND)`: command substitution, aka output of `COMMAND` is substituted in
    - Allows you to set variables equal to output, e.g. `foo=$(COMMAND)`
- `<(COMMAND)`: process substitution, aka writes command output to temporary file and substitutes file name in, for when a file input is expected

### Scripting

- Shell globbing: using expressions to express multiple values (often command inputs) efficiently
    - `?` = represents any one character, e.g. `foo?` → `foo1 foo2 fool`, but not `foo10`
    - `*` = represents any amount of characters
    - `{}` = `image.{png,jpg}` → `image.png image.jpg`, `{a..e}` → `a b c d e`, `{1..5}` → `1 2 3 4 5`
- Shebang: allows scripts of different types to be run by the shell via `./script{.sh,.py,...}`
    - Bash: `#!/bin/bash`
    - Python: `#!/usr/bin/env python` (superior to `#!/usr/local/bin/python` in terms of portability)
- `shellcheck SCRIPT` helps with debugging
    - `sudo apt install shellcheck`
- Shell functions versus scripts
    - Functions must be in the same language as the shell
    - Functions are loaded once read, scripts are loaded every time they run
    - Functions that are executed will execute the commands in your current shell environment, while running scripts run them in a separate process, i.e. `cd` will not change your working directory in a script, but will in a function
- `./SCRIPT` vs `source SCRIPT`: running a script with `./SCRIPT` will run it in a new instance of bash, so commands like `cd` will not affect the working directory in the session, but `source SCRIPT` will run in the current session
- Bash scripts are good for simple one-off scripts/a series of commands, Python scripts are good for larger/complex processes

### Navigation

- `tldr PROGRAM`: gives succinct documentation with examples (web client: https://tldr.inbrowser.app/)
- `find DIR -name "SEARCH_STRING" -type {d,f}`: searches recursively inside `DIR` for directory/file that matches search string
    - Can also search by size, owner, permissions, modified time, etc.
    - Adding `-exec COMMAND {}` will execute command with `{}` representing the `find` output becoming `COMMAND` input
    - `fd` is an improved alternative: https://github.com/sharkdp/fd#installation
- `locate "SEARCH_STRING"`: faster by using a database, which is updated using `updatedb`
    - Can only search by string, and database is not as fresh
- `grep "SEARCH_STRING" FILES`: search inside files  
    `grep -R "SEARCH_STRING"`: recursive directory search  
    `COMMAND | grep "SEARCH_STRING"`: search lines of output from command  
- `COMMAND | fzf`: from `fzf` package, allows for an interactive, fuzzy search
    - e.g. `find DIR | fzf`
- `rg`: aka “ripgrep” is a `grep` alternative with other options to use
    - `fd`, `ag`, `ack`, are all similar `grep` alternatives
- Previous command search
    - `history NUMBER` = spit out the last `NUMBER` commands in history, can use with `| grep`
    - `ctrl-r` = for history search, made more robust with `fzf`
- Navigation tools
    - `tree`: branched visualization of filesystem
    - `broot`: interactive branched visualization with fuzzy search
    - `nnn`: provides file sytem navigation similar to GUI