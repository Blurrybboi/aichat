Use `config.left_prompt`/`config.right_prompt` to custom REPL left/right prompt.

The default configuration:
```yaml
# REPL left prompt
left_prompt: '{color.green}{?session {session}{?role /}}{role}{?session )}{color.cyan}{!session >}{color.reset} '
# REPL right prompt
right_prompt: '{color.purple}{?session {?consume_tokens {consume_tokens}({consume_percent}%)}{!consume_tokens {consume_tokens}}}{color.reset}'
```

## Syntax

The prompt template comprises plain text and `{...}`. 

The syntax of `{...}` is:
- `{var}` - Replace with value of `var`
- `{?var <template>}` - Eval `template` when `var` is evaluated as true
- `{!var <template>}` - Eval `template` when `var` is evaluated as false

## Variables

```yaml
# Model
model: openai:gpt-4
client_name: openai
model_name: gpt-4
max_input_tokens: 4096

# Config
temperature: 1.0
top_p: 0.9
dry_run: true
save: true
wrap: 120
auto_copy: true

role: coder

# Session
session: temp
dirty: false
consume_tokens: 200
consume_percent: 1%
user_messages_len: 0

rag: temp

bot: todo-sh

# ANSI COLORS
color.reset:
color.black:
color.dark_gray:
color.red:
color.light_red:
color.green:
color.light_green:
color.yellow:
color.light_yellow:
color.blue:
color.light_blue:
color.purple:
color.light_purple:
color.magenta:
color.light_magenta:
color.cyan:
color.light_cyan:
color.white:
color.light_gray:
```