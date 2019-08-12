# Intro to Bash - Chapter 1. Sessions and Jobs

## Table of Contents
- Sessions
- Variables (local vs environment)
- Job control (process (fg) vs daemon (bg))
- Signals

### What is Bash
- String-based command language.
- Each command is delimited by whitespace.

### What can you do with bash
- Start, stop, and kill jobs.
- Run jobs in foreground and background.

## Sessions
Every time you login to your machine, open a new terminal window or tab, it will begin a new
terminal session. That session will end when you log out or close the terminal.

These files are sourced (or run) in this order.

```sh
# Load system-wide profile.
source /etc/profile

# Load user setting profile.
source ~/.bash_profile
```

Sidenote:
- `/etc/profile` is where you should specify system-wide startup commands for all users.
- `~/.bash_profile` is where you should define your aliases.

## Variables

Why this doesn't work.
```sh
LOL = lol
```

Local variables
```sh
LOL=lol
printenvs
printenvs | grep LOL
```

Environment variables
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

## Job Control
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

Example commands
```sh
# Run sleep in foreground.
sleep 1000

# Run sleep in background.
sleep 2000 &

# Send interrupt signal (2 SIGINT)
$ ctrl-c

# Send suspend signal (17 SIGSTP)
$ ctrl-z

# Job control
$ jobs

# run suspended job in foreground (default is pop last stack)
$ fg
$ fg 1

# run suspended job in background (default is pop last stack)
$ bg
$ bg 1
```

## Signals
Send a signal to a process. SIGTERM (least dangerous) is sent by default.

```sh
kill -9 <process-id>
kill -SIGKILL <process-id>

# Send SIGTERM.
killall sleep

# Send SIGKILL.
killall -9 sleep
killall -SIGKILL sleep
```

List of common signals
```
2 SIGINT
Interrupt signal. This signal is given to processes to interrupt them.
Programs can process this signal and act upon it.
You can also issue this signal directly by typing Ctrl-c in the terminal window where the program is running.

15 SIGTERM (DEFAULT)
Termination signal. This signal is given to processes to terminate them.
Again, programs can process this signal and act upon it.
This is the default signal sent by the kill command if no signal is specified.

9 SIGKILL
Kill signal. This signal causes the immediate termination of the process by the Linux kernel.
Programs cannot listen for this signal.

17 SIGSTOP
Stop signal. Suspends the current running process.
```
