AIChat supports the following environment variables:

- `HTTPS_RPOXY`/`ALL_PROXY`: Define a proxy server.
- `AICHAT_CONFIG_DIR`: Specify the directory for configuration files. Defaults to `<user_config_dir>/aichat`.
- `AICHAT_ROLES_FILE`: Customize the location of the `roles.yaml` file.
- `AICHAT_LIGHT_THEME`: Enable a light theme.
- `{client}_API_KEY`: Provide API keys for specific clients, e.g. `OPENAI_API_KEY`, `GEMINI_API_KEY`.
- `AICHAT_PLATFORM`: Combined with `{client}_API_KEY` to run aichat without needing a configuration file.
- `AICHAT_NO_DANGEROUSLY_FUNCTIONS`: Set `dangerously_functions_filter: null` 