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
- https://bash.cyberciti.biz/guide/Sending_signal_to_Processes
- https://www.tldp.org/LDP/abs/html/x9644.html

List all processes run by user.
```
$ ps u
```

List all basic and elevated processes by user.
```
$ ps au
```

Send a signal to a process. SIGTERM (least dangerous) is sent by default.

```sh
kill -9 <process-id>
kill -SIGKILL <process-id>

# Send SIGTERM to firefox.
killall firefox

# Send SIGKILL to firefox.
killall -9 firefox
killall -SIGKILL firefox
```

List of common signals
```
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

17 SIGSTOP
Stop signal. Suspends the current running process.
```

Send job to the background (run as daemon).
```sh
$ firefox
$ firefox &

# Send suspend signal (SIGSTP)
$ ctrl-z

# Send interrupt signal (SIGINT)
$ ctrl-c

# Job control
$ jobs
$ fg
$ bg
```
