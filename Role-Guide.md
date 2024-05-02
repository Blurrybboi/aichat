## Role Structure

Role consists of three parts: `name`, `prompt`, and optional `temperature`

```yaml
- name: shell
  prompt: >
    I want you to act as a linux shell expert.
    I want you to answer only with code.
    Do not write explanations.
  temperature: 0.7
```

## Prompt Type

There are two types of prompt: `embeded` and `system`.

### Embeded Prompt

If prompt contains `__INPUT__`, it's embeded prompt

Here is an example of the embeded prompt:

```yaml
- name: emoji
  prompt: convert __INPUT__  to emoji
```

If we run `aichat -r emoji angry`, aichat will generate messages as follows:
```json
[
  {"role": "user", "content": "convert angry to emoji"}
]
```

The `__INPUT__` in the prompt will be replaced by user input to form one user message.

### System Prompt

If prmopt don't contain `__INPUT__`, it's  system prompt.

Here is an example of the system prompt:

```yaml
- name: emoji
  prompt: convert my words to emoji
```

If we run `aichat -r emoji angry`, aichat aichat will generate messages as follows:

```json
[
  {"role": "system", "content": "convert my words to emoji"}
  {"role": "user", "content": "angry"}
]
```

Prompt will be converted to a `system` message, while user input will become a `user` message.

## Role Args

We can use role args to pass some additional arguments to the prompt.

```
- name: convert:json:yaml
  prompt: convert __ARG1__ below to __ARG2__
```

`:json:yaml` is `role args`. It has two args:

- arg1 `json` will replace `__ARG1__` in prompt
- arg2 `yaml` will replace `__ARG2__` in prompt


If we run `aichat -r convert:json:yaml`, the prompt will be

```
convert json below to yaml
```

If we run `aichat -r convert:yaml:toml`, the prompt will be
```
convert yaml below to toml
```

Different role args will generate different prompts.