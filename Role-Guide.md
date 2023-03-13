# Role Guide

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

## Role Prompt Type

There are two types of role prompt: `attached` and `unattached`.

### Attached prompt

If prompt contains `__INPUT___`, it's attached prompt

Here is an example of the attached prompt:

```yaml
- name: emoji
  prompt: convert __INPUT__  to emoji
```

If we run `aichat -r emoji angry`, aichat send following messages to gpt internally:

```json
[
  {"role": "user", "content": "convert angry to emoji"}
]
```

The `__INPUT__` in the prompt will be replaced by user input to form one user message.

### Unattached prompt

If prmopt don't contain `__INPUT___`, it's  unattached prompt.

Here is an example of the attached prompt:

```yaml
- name: emoji
  prompt: convert my words to emoji
```

If we run `aichat -r emoji angry`, aichat send following messages to gpt internally:

```json
[
  {"role": "system", "content": "convert my words to emoji"}
  {"role": "user", "content": "angry"}
]
```

Prompt will become a `system` message, user input will become a `user` message.


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