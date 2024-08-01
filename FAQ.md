<details>
<summary>

## Why need compress session?
</summary>

Sessions require context memory. However, The chat API is stateless. Therefore, each request needs to include the chat history.
Chat history grows rapidly with the conversation, leading to a rapid increase in data transmitted to the API server.

This presents two problems:

1. The amount of data the LLM needs to process for each request keeps increasing, resulting in longer response times and increased costs.
2. The data volume may exceed the LLM's processing capacity, leading to errors.

AICHat's strategy is to automatically compress the chat history when the number of tokens in the chat history exceeds a certain value (`compress_threshold`).

</details>

<details>
<summary>

## How to log or debug?
</summary>

Run the following command:
```
AICHAT_LOG_LEVEL=debug aichat
```
Then check the log file `<aichat-config-dir>/aichat.log`.

Detailed request and response data can be found in the log files.

</details>