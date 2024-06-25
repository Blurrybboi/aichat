## Usage

```
Usage: aichat [OPTIONS] [TEXT]...

Arguments:
  [TEXT]...  Input text

Options:
  -m, --model <MODEL>        Select a LLM model
      --prompt <PROMPT>      Use the system prompt
  -r, --role <ROLE>          Select a role
  -s, --session [<SESSION>]  Start or join a session
      --save-session         Forces the session to be saved
  -a, --agent <AGENT>        Start a agent
  -R, --rag <RAG>            Start a RAG
      --serve [<ADDRESS>]    Serve the LLM API and WebAPP
  -e, --execute              Execute commands in natural language
  -c, --code                 Output code only
  -f, --file <FILE>          Include files with the message
  -S, --no-stream            Turn off stream mode
  -w, --wrap <WRAP>          Control text wrapping (no, auto, <max-width>)
  -H, --no-highlight         Turn off syntax highlighting
      --light-theme          Use light theme
      --dry-run              Display the message without sending it
      --info                 Display information
      --list-models          List all available chat models
      --list-roles           List all roles
      --list-sessions        List all sessions
      --list-agents          List all agents
      --list-rags            List all RAGs
  -h, --help                 Print help
  -V, --version              Print version
```

## Examples

```sh
aichat                                          # Enter REPL
aichat hello                                    # Generate response

aichat -e install nvim                          # Execute command
aichat -c fibonacci in js                       # Generate code

aichat --serve                                  # Run server

aichat -r role1                                 # Use role 'role1'
aichat -s                                       # Use session 'temp'
aichat -s session1                              # Use session 'session1'
aichat -a agent1                                # Use agent 'agent1'
aichat -R rag1                                  # Use RAG 'rag1'

aichat --info                                   # View system info
aichat -r role1 --info                          # View role info
aichat -s session1 --info                       # View session info
aichat -a agent1 --info                         # View agent info
aichat -R rag1 --info                           # View RAG info

cat data.toml | aichat -c to json > data.json   # Pipe Input/Output
data=$(aichat -S "$data")                       # Invoke in script

aichat -f a.png -f b.png diff images            # Use files
```

## Execute Command

Simply input what you want to do in natural language, and aichat will prompt and run the command that achieves your intent.

![aichat-execute](https://github.com/sigoden/aichat/assets/4012553/f99bcd8f-26be-468f-a35e-197e65260f91)

**AIChat is aware of OS and shell you are using, it will provide shell command for specific system you have.**

## Shell Integration

This is a **very handy feature**, which allows you to use `aichat` intelligent completions directly in your terminal.

![aichat-integration](https://github.com/sigoden/aichat/assets/4012553/873ebf23-226c-412e-a34f-c5aaa7017524)

AIChat offers shell integration scripts for for bash, zsh, PowerShell, fish, and nushell. You can find them on GitHub at [https://github.com/sigoden/aichat/tree/main/scripts/shell-integration](https://github.com/sigoden/aichat/tree/main/scripts/shell-integration).

## Shell Autocompletion

The shell autocompletion suggests commands, options, and filenames as you type, enabling you to type less, work faster, and avoid typos.

![aichat-autocompletions](https://github.com/sigoden/aichat/assets/4012553/29dd7497-441f-4b64-b36e-2bcbc5e66202)

AIChat offers shell completion scripts for bash, zsh, PowerShell, fish, and nushell. You can find them on GitHub at [https://github.com/sigoden/aichat/tree/main/scripts/completions](https://github.com/sigoden/aichat/tree/main/scripts/completions).

## Generate Code

By using the `--code` or `-c` parameter, you can specifically request pure code output.

![aichat-code](https://github.com/sigoden/aichat/assets/4012553/2bbf7c8a-3822-4222-9498-693dcd683cf4)

**The `-c/--code` with pipe ensures the extraction of code from Markdown.**

## Use Files

The `-f/--file` can be used to send files to LLMs.

We can send image files. This makes AIChat similar to an OCR tool.
```sh
aichat -f screenshot.png Output the text in the screenshot image
```

Typing long texts into the CLI is inconvenient, We can save the text to a file and send the file.
```sh
aichat -f data.txt
```

We can input text as well as include file.

```sh
aichat -f data.txt summarize
```

It is also possible to include multiple text documents at the same time.

You can use --dry-run to see how the AI chatbot processes multiple files.

```sh
$ echo "This is file1" > file1.txt
$ echo "This is file2" > file2.txt
$ aichat --dry-run -f file1.txt -f file2.txt Use multiple files
Use multiple files
`file1.txt`:
~~~~~~
This is file1

~~~~~~
`file2.txt`:
~~~~~~
This is file2

~~~~~~
```

## Run Server

AIChat comes with a built-in lightweight http server.

```
$ aichat --serve
Chat Completions API: http://127.0.0.1:8000/v1/chat/completions
Embeddings API:       http://127.0.0.1:8000/v1/embeddings
LLM Playground:       http://127.0.0.1:8000/playground
LLM Arena:            http://127.0.0.1:8000/arena?num=2
```

Change the listening address:
```
$ aichat --serve 0.0.0.0
$ aichat --serve 8080
$ aichat --serve 0.0.0.0:8080
```
