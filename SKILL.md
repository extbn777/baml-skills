# BAML Skills

## Overview

This skill provides comprehensive knowledge about **BAML (Basically, A Made-up Language)** — a domain-specific language for defining AI functions with structured outputs. Load this skill when the user asks about BAML syntax, LLM client configuration, structured output extraction, prompt engineering, streaming, testing, or any BAML-related topic.

---

## When to load this skill

Load this skill when the user's request involves any of the following:

- Writing or debugging `.baml` files
- Defining BAML functions, classes, enums, or clients
- Configuring LLM providers (OpenAI, Anthropic, Gemini, etc.)
- Structured output extraction from LLMs
- Streaming LLM responses
- Testing BAML functions (`baml test`)
- Using the `baml_client` generated code in Python, TypeScript, Ruby, Go, or Java
- Prompt engineering with Jinja2 templates inside BAML
- Multi-modal inputs (images, audio, documents)
- Error handling, retries, timeouts, and abort signals
- Observability and tracing of LLM calls
- Integrating BAML with frameworks (LangChain, LlamaIndex, etc.)
- Comparing BAML with alternatives (Instructor, Marvin, Outlines, etc.)
- Using the BAML VSCode extension or BAML CLI
- Dynamic types, union types, and complex nested structures

---

## Repository structure

All content lives inside this repository. The agent should route to the correct section based on the user's intent.

```
baml-skills/
├── SKILL.md                          ← This file (entry point)
├── .cursorrules                      ← Documentation writing guidelines
│
├── 01-guide/                         ← Core documentation
│   ├── introduction.mdx
│   ├── why-baml.mdx                  ← Why use BAML over alternatives
│   ├── what-are-function-definitions.mdx
│   ├── what-is-baml_client.mdx       ← Generated client explanation
│   ├── what-is-baml_src.mdx          ← baml_src folder explanation
│   ├── contact.mdx
│   │
│   ├── 01-editors/                   ← Editor setup (VSCode, etc.)
│   ├── 02-languages/                 ← Language-specific guides (Python, TS, Ruby, Go, Java)
│   ├── 03-development/               ← Development workflow
│   │
│   ├── 04-baml-basics/               ← Core BAML usage
│   │   ├── my-first-function.mdx     ← Hello world / getting started
│   │   ├── streaming.mdx             ← Streaming LLM responses
│   │   ├── concurrent-calls.mdx      ← Parallel / concurrent LLM calls
│   │   ├── multi-modal.mdx           ← Images, audio, documents as input
│   │   ├── error-handling.mdx        ← Error types and handling patterns
│   │   ├── abort-signal.mdx          ← Cancelling in-flight requests
│   │   ├── timeouts.mdx              ← Request timeout configuration
│   │   ├── switching-llms.mdx        ← Switching providers at runtime
│   │   └── testing-functions.mdx     ← Writing and running BAML tests
│   │
│   ├── 05-baml-advanced/             ← Advanced patterns
│   ├── 06-prompt-engineering/        ← Jinja2 templates, chat roles, prompt design
│   ├── 07-observability/             ← Tracing, logging, monitoring
│   ├── 08-frameworks/                ← LangChain, LlamaIndex, etc.
│   ├── 09-comparisons/               ← BAML vs Instructor, Marvin, Outlines, etc.
│   └── functions/                    ← Function definition deep-dives
│
├── 02-examples/
│   └── interactive-examples.mdx      ← Interactive playground examples
│
├── 03-reference/                     ← API and language reference
│   ├── overview.mdx                  ← Reference overview
│   ├── generator.mdx                 ← generator {} block reference
│   ├── baml/                         ← BAML language syntax reference
│   ├── baml_client/                  ← Generated client API reference
│   ├── baml-cli/                     ← CLI commands reference
│   ├── vscode-ext/                   ← VSCode extension reference
│   └── cloud/                        ← BAML Cloud reference
│
├── snippets/                         ← Reusable MDX code snippets
│   ├── allowed-role-metadata.mdx
│   ├── allowed-role-metadata-basic.mdx
│   ├── client-constructor.mdx
│   ├── client-response-type.mdx
│   ├── dynamic-class-test.mdx
│   ├── finish-reason.mdx
│   ├── media-url-handler.mdx
│   ├── openapi-howto-rely-on-envvars.mdx
│   ├── role-selection.mdx
│   ├── setting-env-vars.mdx
│   ├── supported-types.mdx
│   ├── supports-streaming.mdx
│   ├── supports-streaming-openai.mdx
│   └── baml/                         ← BAML-specific code snippets
│
├── openapi/                          ← OpenAPI integration
└── pages/                            ← Additional documentation pages
```

---

## Routing guide

Use this table to load the right file for a given user intent.

| User intent | Primary file(s) to load |
|---|---|
| "What is BAML?" / "Why use BAML?" | `01-guide/why-baml.mdx`, `01-guide/introduction.mdx` |
| "How do I write my first BAML function?" | `01-guide/04-baml-basics/my-first-function.mdx` |
| "How does streaming work in BAML?" | `01-guide/04-baml-basics/streaming.mdx`, `snippets/supports-streaming.mdx` |
| "How do I run concurrent LLM calls?" | `01-guide/04-baml-basics/concurrent-calls.mdx` |
| "How do I pass images/audio/files to LLMs?" | `01-guide/04-baml-basics/multi-modal.mdx`, `snippets/media-url-handler.mdx` |
| "How do I handle errors in BAML?" | `01-guide/04-baml-basics/error-handling.mdx` |
| "How do I cancel a request?" | `01-guide/04-baml-basics/abort-signal.mdx` |
| "How do I set timeouts?" | `01-guide/04-baml-basics/timeouts.mdx` |
| "How do I switch LLM providers at runtime?" | `01-guide/04-baml-basics/switching-llms.mdx` |
| "How do I test BAML functions?" | `01-guide/04-baml-basics/testing-functions.mdx`, `snippets/dynamic-class-test.mdx` |
| "How does the generated client work?" | `01-guide/what-is-baml_client.mdx`, `03-reference/baml_client/` |
| "How do I configure LLM clients?" | `snippets/client-constructor.mdx`, `snippets/setting-env-vars.mdx` |
| "What types does BAML support?" | `snippets/supported-types.mdx` |
| "How do I write prompts / chat roles?" | `01-guide/06-prompt-engineering/`, `snippets/role-selection.mdx`, `snippets/allowed-role-metadata.mdx` |
| "How do I observe / trace BAML calls?" | `01-guide/07-observability/` |
| "How do I use BAML with LangChain / LlamaIndex?" | `01-guide/08-frameworks/` |
| "How does BAML compare to Instructor/Marvin?" | `01-guide/09-comparisons/` |
| "What are BAML advanced patterns?" | `01-guide/05-baml-advanced/` |
| "What is the generator block?" | `03-reference/generator.mdx` |
| "BAML CLI commands" | `03-reference/baml-cli/` |
| "VSCode extension" | `03-reference/vscode-ext/`, `01-guide/01-editors/` |
| "BAML language syntax / reference" | `03-reference/baml/`, `03-reference/overview.mdx` |
| "Function definitions" | `01-guide/what-are-function-definitions.mdx`, `01-guide/functions/` |
| "Environment variables / API keys" | `snippets/setting-env-vars.mdx`, `snippets/openapi-howto-rely-on-envvars.mdx` |
| "Interactive examples / playground" | `02-examples/interactive-examples.mdx` |
| "BAML Cloud" | `03-reference/cloud/` |
| "Finish reason / stop reason" | `snippets/finish-reason.mdx` |
| "OpenAPI integration" | `openapi/`, `snippets/openapi-howto-rely-on-envvars.mdx` |

---

## Key BAML concepts (quick reference)

### baml_src folder
All `.baml` source files live in `baml_src/`. These define your functions, data types, LLM clients, and test cases. BAML generates a `baml_client/` folder from these files.

### baml_client folder
Auto-generated code (Python, TypeScript, Ruby, Go, Java) that provides type-safe wrappers to call your BAML functions. Never edit this folder manually — regenerate with `baml generate`.

### Function definition
```baml
function ExtractResume(resume_text: string) -> Resume {
  client GPT4o
  prompt #"
    Extract the resume info from:
    {{ resume_text }}

    {{ ctx.output_format }}
  "#
}
```

### Class definition
```baml
class Resume {
  name string
  email string?
  skills string[]
  experience Experience[]
}
```

### Client definition
```baml
client<llm> GPT4o {
  provider openai
  options {
    model gpt-4o
    api_key env.OPENAI_API_KEY
  }
}
```

### Calling a function (Python)
```python
from baml_client import b

resume = await b.async_client.ExtractResume(resume_text="...")
print(resume.name)
```

---

## Documentation writing rules

When writing or editing content in this repository, follow the rules in `.cursorrules`:

- Titles: first word capitalized, rest lowercase (e.g., `Getting started`, `Error handling`)
- No emojis
- Short paragraphs and sentences — scientific tone
- Every `.mdx` file starts with `---\ntitle:\nsubtitle:\n---`
- Wrap images in `<Frame background="subtle">`
- Use `<Steps>`, `<AccordionGroup>`, `<Tabs>`, `<CodeBlocks>` components for structure
- Code examples default to Python first

---

## Loading strategy

This skill is designed for **on-demand loading**. The agent should:

1. Read this `SKILL.md` first to understand scope and structure.
2. Route to the specific file(s) listed in the routing guide above.
3. Load only the files relevant to the current user query — do not load the entire repository at once.
4. For broad questions ("explain BAML"), load `01-guide/why-baml.mdx` + `01-guide/introduction.mdx`.
5. For code questions, also load the relevant snippet from `snippets/`.
6. For reference lookups, go directly to `03-reference/`.
