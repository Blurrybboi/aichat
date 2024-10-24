## Env file

AIChat supports env file (`<aichat-config-dir>/.env`) for managing environment variables.

You can put all your secret environment variables in the `.env` file.

## Config-Related Envs

All config items have their related env variables to override its values.
Check [config.example.yaml](https://github.com/sigoden/aichat/blob/main/config.example.yaml) for all config items.

Below are some commonly used configuration items and their corresponding environment variables:

```yaml
model: openai:gpt-4o              # env: AICHAT_MODEL
temperature: null                 # env: AICHAT_TEMPERATURE
top_p: null                       # env: AICHAT_TOP_P

stream: true                      # env: AICHAT_STREAM
save: true                        # env: AICHAT_SAVE
editor: null                      # env: AICHAT_EDITOR
wrap: no                          # env: AICHAT_WRAP
wrap_code: false                  # env: AICHAT_WRAP_CODE

save_session: null                # env: AICHAT_SAVE_SESSION
compress_threshold: 4000          # env: AICHAT_COMPRESS_THRESHOLD
function_calling: true            # env: AICHAT_FUNCTION_CALLING
use_tools: null                   # env: AICHAT_USE_TOOLS

rag_embedding_model: null         # env: AICHAT_rag_embedding_model
rag_reranker_model: null          # env: AICHAT_rag_reranker_model
rag_top_k: 4                      # env: AICHAT_rag_top_k
rag_chunk_size: null              # env: AICHAT_rag_chunk_size
rag_chunk_overlap: null           # env: AICHAT_rag_chunk_overlap

highlight: true                   # env: AICHAT_HIGHLIGHT
light_theme: false                # env: AICHAT_LIGHT_THEME

serve_addr: 17.0.0.1:8000         # env: AICHAT_SERVE_ADDR
```

## Client-Related Envs

- `{client}_API_KEY`: Provide API keys for specific clients, e.g. `OPENAI_API_KEY`, `GEMINI_API_KEY`.
- `AICHAT_PLATFORM`: Combined with `{client}_API_KEY` to run aichat without a configuration file (it will be ignored if a configuration file exists).
  ```
  AICHAT_PLATFORM=openai OPENAI_API_KEY=sk-xxx
  ```
- `AICHAT_PATCH_{client}_CHAT_COMPLETIONS`: Patch chat completions api request url, headers and body.
  ```
  AICHAT_PATCH_OPENAI_CHAT_COMPLETIONS='{"gpt-4o":{"body":{"seed":666,"temperature":0}}}'
  ```
- `AICHAT_SHELL`: Specify the shell; it will override the automatically detected one.
  ```
  AICHAT_SHELL="C:\\Program Files\\Git\bin\\bash.exe"
  ```

## Files/Dirs Envs

- `AICHAT_CONFIG_DIR`: Customize the location of the config dir. Defaults to `<user-config-dir>/aichat`.
- `AICHAT_ENV_FILE`: Customize the location of the `.env` file.
- `AICHAT_CONFIG_FILE`: Customize the location of the `config.yaml` file.
- `AICHAT_ROLES_DIR`: Customize the location of the `roles` dir.
- `AICHAT_SESSIONS_DIR`: Customize the location of the `sessions` dir.
- `AICHAT_RAGS_DIR`: Customize the location of the `rags` dir.
- `AICHAT_FUNCTIONS_DIR`: Customize the location of the `functions` dir.
- `AICHAT_MESSAGES_FILE`: Customize the location of the `messages.md` file.

## Agent-Related Envs

- `{agent}_FUNCTIONS_DIR`: Customize the location of the agent's config dir. e.g. `CODER_FUNCTIONS_DIR`.
- `{agent}_DATA_DIR`: Customize the location of the agent's data dir. e.g. `CODER_DATA_DIR`.

## Logging Envs

- `AICHAT_LOG_LEVEL=debug`: Enable debug logging.
- `AICHAT_LOG_FILE`: Custom the location of the log file, defaults to `<aichat-config-dir>/aichat.log`

## Generic Envs

- `HTTPS_RPOXY`/`ALL_PROXY`: Specify a globally proxy server.
- `NO_COLOR`: Disable the use of color.
- `EDITOR`: Specify the default editor.
- `XDG_CONFIG_HOME`: Locate the config dir.