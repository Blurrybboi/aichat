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

![aichat-repl-model](https://github.com/sigoden/aichat/assets/4012553/950ddda3-a561-4761-ba07-47ca142d35f2)

### `.role` - use a predefined role

```
.role                    Create or switch to a specific role
.info role               View role info
.edit role               Edit the current role
.save role               Save the current role to file
.exit role               Leave the role
```

![aichat-repl-role](https://github.com/user-attachments/assets/b07523ff-fe64-4895-ae90-91eef12c6963)

### `.prompt` - use a temporary role

Compared to `.role`, `.prompt` does persist to a file; it creates and switches to a temporary role.

![aichat-repl-prompt](https://github.com/user-attachments/assets/c979bce8-2d66-4540-b34b-fda78afbe432)

### `.session` - begin a chat session

```
.session                 Begin a session
.empty session           Erase messages in the current session
.compress session        Compress messages in the current session
.info session            View session info
.edit session            Edit the current session
.save session            Save the current session to file
.exit session            End the session
```

![aichat-repl-session](https://github.com/user-attachments/assets/d962c726-99a9-4638-b8d8-0b6064edbdb4)

### `.rag` - chat with knowledge

```
.rag                     Init or use the RAG
.rebuild rag             Rebuild the RAG to sync document changes
.sources rag             View the RAG sources in the last query
.info rag                View RAG info
.exit rag                Leave the RAG
```

![aichat-repl-rag](https://github.com/user-attachments/assets/8ca6b54a-c721-485b-b083-e6a93ecce4b0)

### `.agent` - chat with an AI agent

```
.agent                   Use a agent
.starter                 Use the conversation starter
.variable                Set agent variable
.save agent-config       Save the current agent config to file
.info agent              View agent info
.exit agent              Leave the agent
```

![repl-agent](https://github.com/user-attachments/assets/0b7e687d-e642-4e8a-b1c1-d2d9b2da2b6b)

### `.file` - read files and use them as input

```
Usage: .file <file>... [-- text...]

.file data.txt
.file config.yaml -- convert to toml
.file screentshot.png -- design a web app based on the image
.file https://ibb.co/a.png https://ibb.co/b.png -- what is the difference?
.file https://github.com/sigoden/aichat/blob/main/README.md -- what is the features of AIchat?
```

### `.continue` - continue the response

This command is often used to resume generation that was interrupted due to the response exceeding the length limit.

![repl-continue](https://github.com/sigoden/aichat/assets/4012553/478623ba-ebaa-4855-a232-c16536d1651d)

### `.regenerate` - regenerate the last response

If the response is interrupted or unsatisfactory, you can regenerate it with `.regenerate`.

![repl-regenerate](https://github.com/sigoden/aichat/assets/4012553/72484983-b7ea-4e23-b0a2-a66a24c96922)

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

![aichat-repl-delete](https://github.com/user-attachments/assets/7dc41e4d-090f-4951-b185-aff3dc6e1a6f)

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
