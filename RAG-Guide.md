RAG can improve the efficacy of large language model (LLM) applications by leveraging custom data

AIChat has a built-in vector database and full-text search engine, eliminating reliance on third-party services and  providing ready-to-use RAG functionality.

![aichat-rag](https://github.com/user-attachments/assets/81b81409-460a-4aec-9e08-a3c3da5492d0)

## Document Sources

AIChat can build RAG knowledge bases from a variety of document sources.

| Source                  | Example                                              |
| ----------------------- | ---------------------------------------------------- |
| Files                   | `/tmp/dir1/file1;/tmp/dir1/file2`                    |
| Directory               | `/tmp/dir1/`                                         |
| Directory (extensions)  | `/tmp/dir2/**/*.{md,txt}`                            |
| Url                     | `https://sigoden.github.io/mynotes/tools/linux.html` |
| RecursiveUrl (websites) | `https://sigoden.github.io/mynotes/tools/**`         |

> `**` is used to distinguish between Url and RecursiveUrl

## Custom Document Loaders

By default, AIChat can only process text files. We need to configure the `document_loaders` so AIChat can handle binary files such as PDFs and DOCXs.

```yaml
# Define document loaders to control how RAG and `.file`/`--file` load files of specific formats.
document_loaders:
  # You can add custom loaders using the following syntax:
  #   <file-extension>: <command-to-load-the-file>
  # Note: Use `$1` for input file and `$2` for output file. If `$2` is omitted, use stdout as output.
  pdf: 'pdftotext $1 -'                         # Load .pdf file, see https://poppler.freedesktop.org to set up pdftotext
  docx: 'pandoc --to plain $1'                  # Load .docx file, see https://pandoc.org to set up pandoc
```

The `document_loaders` configuration item is a map where the key represents the file extension and the value specifies the corresponding loader command.

To ensure the loaders function correctly, please verify that the required tools are installed.

## Use Reranker

AIChat RAG defaults to the `reciprocal_rank_fusion` algorithm for merging vector and keyword search results.

However, using a reranker to combine these results is a more established method that can yield greater relevance and accuracy.

You can add the following configuration to specify the default reranker.

```yaml
rag_reranker_model: null                    # Specifies the rerank model to use
```

You can also dynamically adjust the reranker using the `.set` command.

```
.set rag_reranker_model <tab>
```