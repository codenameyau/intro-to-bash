# intro-to-bash

Recommended Resources
- Official GNU reference: https://www.gnu.org/software/bash/manual/html_node/index.html
- Bash Guide for Beginners: https://www.tldp.org/LDP/Bash-Beginners-Guide/html/

## Hot Tips

### How to use variables correctly
Spacing is critical in bash since commands are separated by spaces.
Assignments, for example, should be done without spaces.
```sh
# Bad. Interprets line as 3 separate commands.
var = 'lol'

# Good. Will assign 'lol' to var.
var='lol'
```

Always use `lower_case` for local variables and `UPPER_CASE` for environment variables.
```sh
# local variable.
my_local_variable='lol'

# environment variable.
export MY_ENV_VARIABLE='lol'
```

Always use single quotes for string literals and double quotes for interpolated strings.

```sh
cat='sunny'
LOL='hello $cat'
echo "$LOL"
```

```sh
cat='sunny'
LOL="hello $cat"
echo "$LOL"
```

Always double quote variable expansions unless you know what you're doing.
```sh
words="good boy does fine"

# Bad. Execute 4 separate commands with 1 word arg.
ls $words

# Good. Executes a single command with 4 args.
ls "$words"
```
