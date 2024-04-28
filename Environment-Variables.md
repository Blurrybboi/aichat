AIChat supports the following environment variables:

- `AICHAT_CONFIG_DIR`: specify the configuration directory, defaults to <user_config_dir>/aichat.
- `AICHAT_ROLES_FILE`: custom the `roles.yaml` file path.
- `AICHAT_LIGHT_THEME`: use light theme.
- `{client}_API_KEY`: set the API key for a client. The prefix is the client's name or type. e.g. `OPENAI_API_KEY`, `GEMINI_API_KEY`.
- `HTTPS_RPOXY`/`ALL_PROXY`: set proxy server.
- `AICHAT_CLIENT_TYPE`: combined with `{client}_API_KEY`, allow aichat to run without a config file.