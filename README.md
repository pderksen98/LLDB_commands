# LLDB

LLDB stands for low-level debugger and is a debugger that runs in the terminal. The following are some basic commands that I use when I use LLDB. A comma in the code means that both commands work.

## How to run

* Compile your code with the -g flag      
* Run lldb without arguments:
```bash
lldb a.out
```
* Run lldb with arguments:
```bash
lldb -- a.out arg1 arg2 ...
```
* (Before you run the program you can set breakpoints and more. Do this before you run the program.)
* Now run the program in lldb:
```bash
run, r
```
* Exit the debugger
```bash
quit, q, exit, CTRL-D
```
* Kill the current process
```bash
kill
```

## Breakpoints

### Setting Breakpoints

* on a function:
```bash
b main
b square(int)
```

* at a location in a specific file:
```bash
breakpoint set -file <file_name> -line <line_number>
br s -f <file_name> -l <line_number>
b <file_name> : <line_number>
```
* on a class method:
```bash
b Demo::demo()
```

* inside a namespace:
```bash
b LLDBDemo::add(int,int)
```

### Manipulation Breakpoints

* list all breakpoints:
```bash
br list
```

* delete all breakpoints:
```bash
br del
```

* delete a specific breakpoint:
```bash
br del <breakpoint_number>
```


## Steps

* stepping over. Ignore any functions that are called in the next step and continue in the current function:
```bash
next, n
```
* stepping into. Step into any subfunction that gets called in the next step:
```bash
step, s
```
* coninue to next breakpoint:
```bash
continue, c
```

## Frames and variables

* Show the current position in the code:
```bash
frame select
fr s
```

* switch frames
```bash
frame select <frame_number>
f <frame_number>
```

* Show all local variables in the current frame:
```bash
frame variables
fr v
```

* print variable:
```bash
print <variable_name>
p <variable_name>
```
* print a pointer:
```bash
p <pointer_name>
```

* print content of a pointer:
```bash
p *<pointer_name>
```

* print class/struct member variable:
```bash
p person.age
```

* print current class/struct (if this pointer is shown in fr v) :
```bash
p *this
```

## Watchpoints

* Watchpoints are used to inspect whenever a variable changes or is accessed
* Program must be running in order to set watchpoinst, otherwise you get the error message "invalid process". set breakpoint at main 'b main' then 'run'.
* Global variable:
```bash
watchpoint set variable <glob_var_name>
watchpoint set variable - w <var>
watchpoint set variable - write <var>
watchpoint set variable - read_write <var>
w s v (shortcut)
```

* Member variable:
```bash
w s v <person.age>
```

* Ex : You want to see whenere the global varibale 'person' is being read:
```bash
(start lldb)
b main
run
w s v -w read person
continue, continue, ... etc
```





## Other

* TIP : You can repeat the last command by just typing enter
* TIP : if your programme crashes, just run lldb without breakpoints. It will stop where the program crashed. Then you can use 'bt', 'fr s', 'fr v' etc to inspect the call stack.
* To see the backtrace (calling stack of the breakpoint that you hit)
```bash
bt
```
* Before typing 'run', if you type 'help' you will see al options (sort of a manual)
* To have a basic graphical interface of the debugger type:
```bash
gui
```

