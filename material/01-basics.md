# Intro to Bash - Chapter 1. The Basics

## Table of Contents

- The basics
- Sessions
- Environment variables
- Job control
- Signals
- Scripting

### What is Bash
- String-based scripting language
- Command language

### What can it do
- Start, pause, stop jobs.
- Interact with other programs

### Local variables vs environment variables

```sh
LOL=lol
printenvs
printenvs | grep LOL
```

```sh
export LOL=lol
printenvs
printenvs | grep LOL
```

### Persisting and sourcing environment variables

```sh
echo "export LOL=lol" >> ~/.bashrc
```

```sh
source ~/.bashrc
```

### Job Control
```
1 SIGHUP
Hang up signal. Programs can listen for this signal and act upon it.
This signal is sent to processes running in a terminal when you close the terminal.

2 SIGINT
Interrupt signal. This signal is given to processes to interrupt them.
Programs can process this signal and act upon it.
You can also issue this signal directly by typing Ctrl-c in the terminal window where the program is running.

15 SIGTERM
Termination signal. This signal is given to processes to terminate them.
Again, programs can process this signal and act upon it.
This is the default signal sent by the kill command if no signal is specified.

9 SIGKILL
Kill signal. This signal causes the immediate termination of the process by the Linux kernel.
Programs cannot listen for this signal.
```
