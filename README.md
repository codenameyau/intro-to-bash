# intro-to-bash
Intro to bash with real-world examples and command-line tips

### Tips

Spacing is critical in bash. Commands are separated by spaces.
```sh
# Bad. Interprets line as 3 commands. Throws an error.
var = 'lol'

# Good. Will assign 'lol' to var.
var='lol'
```

Always use lowercase variables for local variables and uppercase variables for environment variables.
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
