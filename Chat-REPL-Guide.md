The core of AIChat is Chat-REPL.

## REPL Features

- **Tab Autocompletion:** All REPL commands have completions.
    * `.<tab>` to complete REPL commands. 
    * `.model< tab>` to complete chat models.
    * `.set <tab>` to complete config keys.
    * `.set key <tab>` to complete config values.
- **Multi-line Support:** Input multi-line text in the following ways:
    * Press `ctrl+o` to edit buffer with an external editor (recommend).
    * Paste multi-line text (requires terminal support for bracketed paste).
    * Type `:::` to start multi-line editing, type `:::` to finish it.
    * Use hotkey `{ctrl,shift,alt}+enter` to insert a newline directly.
- **History Search:** Press `ctrl+r` to search the history. Use `↑↓` to to navigate through the history.
- **Configurable Keybinding:** Emacs-style bindings and basic VI-style.
- **[Custom REPL Prompt](https://github.com/sigoden/aichat/wiki/Custom-REPL-Prompt):** Display information about the current context in the prompt. 

## REPL Commands

### `.help` - show help message

```
.help                    Show this help message
.info                    View system info
.model                   Change the current LLM
.prompt                  Create a temporary role using a prompt
.role                    Create or switch to a specific role
.info role               View role info
.edit role               Edit the current role
.save role               Save the current role to file
.exit role               Leave the role
.session                 Begin a session
.empty session           Erase messages in the current session
.compress session        Compress messages in the current session
.info session            View session info
.edit session            Edit the current session
.save session            Save the current session to file
.exit session            End the session
.rag                     Init or use the RAG
.rebuild rag             Rebuild the RAG to sync document changes
.sources rag             View the RAG sources in the last query
.info rag                View RAG info
.exit rag                Leave the RAG
.agent                   Use a agent
.starter                 Use the conversation starter
.variable                Set agent variable
.save agent-config       Save the current agent config to file
.info agent              View agent info
.exit agent              Leave the agent
.file                    Include files with the message
.continue                Continue the response
.regenerate              Regenerate the last response
.copy                    Copy the last response
.set                     Adjust runtime configuration
.delete                  Delete roles/sessions/RAGs/agents
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

#### `.save role` - save the current role to file

#### `.edit role` - Edit the current role

### `.prompt` - use a temporary role

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

#### `.empty session` - Erase messages in the current session

#### `.compress session` - Compress messages in the current session

#### `.save session` - save the current session to file

#### `.edit session` - edit the current session

### `.rag` - chat with knowledge

Seamlessly integrates document interactions into your chat experience.

![repl-rag](https://github.com/user-attachments/assets/81b81409-460a-4aec-9e08-a3c3da5492d0)

#### `.rebuild rag` - rebuild the RAG to sync document changes

#### `.sources rag` - view the RAG sources in the last query

### `.agent` - chat with an AI agent

![repl-agent](https://github.com/user-attachments/assets/0b7e687d-e642-4e8a-b1c1-d2d9b2da2b6b)

#### `.starter` - use the agent's conversation starter

#### `.variable <name> <value>` -  set agent variable

#### `.edit agent-config` - edit the current agent config

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
.file https://github.com/sigoden/aichat/blob/main/README.md -- what is the features of AIchat?
```

### `.set` - Adjust runtime configuration

```
.set <tab>
.set max_output_tokens 4096
.set temperature 1.2
.set top_p 0.8
.set dry_run true
.set stream false
.set save true
.set function_calling true
.set use_tools <tab>
.set agent_prelude temp
.set save_session true
.set compress_threshold 1000
.set rag_reranker_model <tab>
.set rag_top_k 4
.set highlight true
```

### `.delete` - delete roles/sessions/RAGs/agents

![repl-delete](https://github.com/user-attachments/assets/e4b3fbf9-4685-41c4-a698-2d79fb5cd608)

### `.info` - view information

- `.info`: View system info
- `.info role`: View role info
- `.info session`: View session info
- `.info rag`: View RAG info
- `.info agent`: View agent info

### `.exit` - exit role/session/rag/agent

- `.exit`: Exit the program.
- `.exit role`: Exit the role.
- `.exit session`: Exit the session.
- `.exit rag`: Exit the RAG.
- `.exit agent`: Exit the agent.
