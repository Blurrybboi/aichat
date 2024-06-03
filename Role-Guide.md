## Role Definition

Roles in AIChat define how the LLM will respond to your input. Each role consists of four fields:

- **`name`:** A unique identifier for the role (e.g., "shell", "translator").
- **`prompt`:** Instructions and context provided to the LLM.
- **`temperature`:**  (Optional) Controls the creativity and randomness of the LLM's response.
- **`top_p`:** (Optional) Alternative way to control LLM's output diversity, affecting the probability distribution of tokens.

Here's a basic example:

```yaml
- name: shell
  prompt: >
    I want you to act as a linux shell expert.
    I want you to answer only with code.
    Do not write explanations.
```

## Types of Prompts

There are three types of prompts in AIChat:

### Embedded Prompt:

- Contains `__INPUT__` placeholder, which gets replaced with your input.
- Ideal for concise, input-driven replies.

```yaml
- name: emoji
  prompt: convert __INPUT__ to emoji
```

Running `aichat -r emoji angry` would generate messages:
```json
[
  {"role": "user", "content": "convert angry to emoji"}
]
```

### System Prompt

- Does not include `__INPUT__`.
- Sets a general context for the LLM's behavior.

```yaml
- name: emoji
  prompt: convert my words to emoji
```

Running `aichat -r emoji angry` would generate messages:

```json
[
  {"role": "system", "content": "convert my words to emoji"},
  {"role": "user", "content": "angry"}
]
```

### Structured Prompt

- An extension of the system prompt, offering more precise instructions.
- Uses `### INPUT:` and `### OUTPUT:` to denote user and assistant messages.

```yaml
- name: code
  prompt: |-
    Provide only code without comments or explanations.
    ### INPUT:
    async sleep in js
    ### OUTPUT:
    ```javascript
    async function timeout(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
```

Running `aichat -r code echo server in node.js` would generate messages:

```json
[
  {"role": "system", "content": "Provide only code without comments or explanations."},
  {"role": "user", "content": "async sleep in js"},
  {"role": "assistant", "content": "```javascript\nasync function timeout(ms) {\n  return new Promise(resolve => setTimeout(resolve, ms));\n}\n```"},
  {"role": "user", "content": "echo server in node.js"}
]
```

## Role Arguments

ole arguments can be employed to supply extra parameters to the prompt.

```yaml
- name: convert:json:yaml
  prompt: convert __ARG1__ below to __ARG2__
```

`:json:yaml` represents `role args`. It contains two arguments:

- arg1 `json` will replace `__ARG1__` in the prompt
- arg2 `yaml` will replace `__ARG2__` in the prompt

If we run `aichat -r convert:json:yaml`, the prompt will be

```
convert json below to yaml
```

If we run `aichat -r convert:yaml:toml`, the prompt will be
```
convert yaml below to toml
```

Different role args will generate different prompts.