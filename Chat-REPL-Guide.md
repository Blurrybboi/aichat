The core of AIChat is Chat-REPL.

## Common REPL Features

- **Tab Autocompletion:** All REPL commands have tab completions.
    > Type `.<tab>` to complete REPL commands.
    > Type `.set <tab>` to complete config keys.
    > Type `.set key <tab>` to complete config values.
    > ...
- **Multi-line Support:** Input multi-line text in the following ways:
    > Press `ctrl+o` to edit buffer with an external editor (recommend).
    > Paste multi-line text (requires terminal support for bracketed paste).
    > Type `:::` to start multi-line editing, type `:::` to finish it.
    > Use hotkey `{ctrl,shift,alt}+enter` to insert a newline directly.
- **History Search:** Press `ctrl+r` to search the history.
    > The history only includes text entered after the REPL starts.
- **Configurable  Keybinding:** Emacs-style bindings and basic VI-style
    > The default keybindings are Emacs.
    > Switch to VI keybindings by adding `keybindings: vi` to the `config.yaml` file.
- **[Custom REPL Prompt](https://github.com/sigoden/aichat/wiki/Custom-REPL-Prompt):**  Display information about the current context in the prompt. 

## REPL Commands

### `.help` - show help message

```
.help                    Show this help message
.info                    View system info
.model                   Change the current LLM
.prompt                  Create a temporary role using a prompt
.role                    Switch to a specific role
.info role               View role info
.exit role               Leave the role
.session                 Begin a session
.info session            View session info
.save session            Save the current session to file
.edit session            Edit the current session with an editor
.clear messages          Erase messages in the current session
.exit session            End the session
.rag                     Init or use a rag
.info rag                View rag info
.exit rag                Leave the rag
.agent                   Use a agent
.info agent              View agent info
.starter                 Use the conversation starter
.exit agent              Leave the agent
.file                    Include files with the message
.continue                Continue the response
.regenerate              Regenerate the last response
.set                     Adjust settings
.copy                    Copy the last response
.exit                    Exit the REPL

Type ::: to start multi-line editing, type ::: to finish it.
Press Ctrl+O to open an editor for editing the input buffer.
Press Ctrl+C to cancel the response, Ctrl+D to exit the REPL.
```

### `.model` - change the current LLM

![repl-model](https://github.com/sigoden/aichat/assets/4012553/950ddda3-a561-4761-ba07-47ca142d35f2)

```
openai:gpt-4o     128000 /     4096  |       5 /     15    👁 ⚒ 
|                 |            |             |       |     |  └─ support function callings
|                 |            |             |       |     └─ support visiion
|                 |            |             |       └─ output price ($/1M)
|                 |            |             └─ input price ($/1M)
|                 |            |
|                 |            └─ max output tokens
|                 └─ max input tokens
└─ model id
```

### `.role` - use a predefined role

Use the role:

```
> .role emoji
emoji> hello
👋
```

View the role details:
```
emoji> .info emoji
name: emoji
prompt: 'I want you to translate the sentences I write into emojis. I will write the sentence, and you will express it with emojis. I just want you to express it with emojis. I don''t want you to reply with anything but emoji. The sentence to be translated: __INPUT__'
```

Leave the role:
```
emoji> .exit role

> hello
Hello there! How can I assist you today?
```

Use the role without switching to it (Can be used in session or agent context):
```
> .role emoji hello
👋

>
```

### `.prompt` - use a temporary role

There are situations where setting a system message is necessary, but modifying the `roles.yaml` file is not ideal.
Use the `.prompt` feature to create a temporary role specifically for this purpose.

```
> .prompt your are a js console

%%> Date.now()
1658333431437
```

### `.session` - begin a chat session

By default, AIChat behaves in a one-off request/response manner.
With sessions, AIChat conducts context-aware conversations.

![aichat-session](https://github.com/sigoden/aichat/assets/4012553/1444c5c9-ea67-4ad2-80df-a76954e8cce0)

#### `.save session` - Save the current session to file

#### `.edit session` - Edit the current session with an editor

### `.rag` - chat with knowledge

Seamlessly integrates document interactions into your chat experience.

![repl-rag](https://github.com/sigoden/aichat/assets/4012553/6f3e5908-9c95-4d7d-aa9c-7e973ecf9354)

### `.agent` - chat with an AI agent

![repl-agent](https://github.com/sigoden/aichat/assets/4012553/d544f00d-5303-4393-a9fb-5e3f20f88412)

#### `.starter <tab>` -  Use the agent's conversation starter

![repl-starter](https://github.com/sigoden/aichat/assets/4012553/6826f5c3-0ebe-4a78-80b9-00ebf9aaafd8)


### `.continue` - continue the response

This command is often used to resume generation that was interrupted due to the response exceeding the length limit.

![repl-continue](https://github.com/sigoden/aichat/assets/4012553/478623ba-ebaa-4855-a232-c16536d1651d)

### `.regenerate` - regenerate the last response

If the response is interrupted or unsatisfactory, you can regenerate it with `.regenerate`.

![repl-regenerate](https://github.com/sigoden/aichat/assets/4012553/72484983-b7ea-4e23-b0a2-a66a24c96922)

### `.file` - read files and use them as input

```
Usage: .file <file>... [-- text...]

.file data.txt
.file config.yaml -- convert to toml
.file screentshot.png -- design a web app based on the image
.file https://ibb.co/a.png https://ibb.co/b.png -- what is the difference?
```

### `.set` - adjust settings (non-persistent)

```
.set <tab>
.set max_output_tokens 4096
.set temperature 1.2
.set top_p 0.8
.set rag_rerank_model <tab>
.set rag_top_k 4
.set function_calling true
.set compress_threshold 1000
.set save true
.set save_session true
.set highlight true
.set dry_run true
```

### `.info` - view information

- `.info`: View system information
- `.info role`: view your current role information.
- `.info session`: view your current session information.
- `.info rag`: view your current RAG information.
- `.info agent`: view your current agent information.


### `.exit` - exit state/program

- `.exit`: Exit the program.
- `.exit role`: Exit the role.
- `.exit session`: Exit the session.
- `.exit rag`: Exit the RAG.
- `.exit agent`: Exit the agent.

