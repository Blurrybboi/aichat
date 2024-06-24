AIChat supports the following environment variables:

- `HTTPS_RPOXY`/`ALL_PROXY`: Specify a globally proxy server.
- `NO_COLOR`: Disable the use of color.
- `EDITOR`: Specify the default buffer editor.

<br>

- `{client}_API_KEY`: Provide API keys for specific clients, e.g. `OPENAI_API_KEY`, `GEMINI_API_KEY`.
- `AICHAT_PLATFORM`: Combined with `{client}_API_KEY` to run aichat without needing a configuration file.
- `AICHAT_LIGHT_THEME`: Enable a light theme.
- `AICHAT_NO_DANGEROUSLY_FUNCTIONS`: Set `dangerously_functions_filter: null` 

<br>

- `AICHAT_CONFIG_DIR`: Customize the location of the config dir. Defaults to `<user_config_dir>/aichat`.
- `AICHAT_CONFIG_FILE`: Customize the location of the `config.yaml` file.
- `AICHAT_ROLES_FILE`: Customize the location of the `roles.yaml` file.
- `AICHAT_MESSAGES_FILE`: Customize the location of the `messages.md` file.
- `AICHAT_SESSIONS_DIR`: Customize the location of the `sessions` dir.
- `AICHAT_RAGS_DIR`: Customize the location of the `rags` dir.
- `AICHAT_FUNCTIONS_DIR`: Customize the location of the `functions` dir.
- `AICHAT_AGENTS_FUNCTIONS_DIR`: Customize the location of the `functions/agents` dir.
- `AICHAT_AGENTS_CONFIG_DIR`: Customize the location of the `agents` dir.
