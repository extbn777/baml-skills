---
name: baml
description: Comprehensive knowledge about BAML (Basically, A Made-up Language) — a DSL for defining type-safe AI functions with structured outputs. Covers BAML syntax, LLM client configuration, structured output extraction, prompt engineering, streaming, testing, and full TypeScript/Next.js/React integration.
---

# BAML Skills

## Overview

This skill provides comprehensive knowledge about **BAML (Basically, A Made-up Language)** — a domain-specific language for defining AI functions with structured outputs. The primary stack for this project is **TypeScript + Next.js + React**. Load this skill when the user asks about BAML syntax, LLM client configuration, structured output extraction, prompt engineering, streaming, testing, or TypeScript/Next.js integration with BAML.

---

## When to load this skill

Load this skill when the user's request involves any of the following:

- Writing or debugging `.baml` files
- Defining BAML functions, classes, enums, or clients
- Configuring LLM providers (OpenAI, Anthropic, Gemini, etc.)
- Structured output extraction from LLMs
- Streaming LLM responses in TypeScript or via Next.js API routes
- Testing BAML functions (`baml test`)
- Using the `baml_client` generated code in **TypeScript** (primary) or other languages
- Setting up BAML in a **Next.js** project (App Router or Pages Router)
- Calling BAML functions from **React** components or hooks
- Prompt engineering with Jinja2 templates inside BAML
- Multi-modal inputs (images, audio, documents)
- Error handling, retries, timeouts, and abort signals
- Observability and tracing of LLM calls
- Integrating BAML with frameworks (Next.js, LangChain, LlamaIndex, etc.)
- Comparing BAML with alternatives (Instructor, Marvin, Outlines, Vercel AI SDK, etc.)
- Using the BAML VSCode extension or BAML CLI
- Dynamic types, union types, and complex nested structures
- Configuring environment variables for BAML in Next.js (`.env.local`, `NEXT_PUBLIC_*`)
- Streaming BAML responses to the browser via Next.js Route Handlers or Server Actions

---

## Primary stack context

This project is built with **TypeScript**, **Next.js**, and **React**. When generating code examples or answering questions, always default to this stack.

### TypeScript — calling a BAML function
```typescript
import { b } from '@/baml_client';

const resume = await b.ExtractResume({ resume_text: '...' });
console.log(resume.name);
```

### Next.js Route Handler — streaming BAML output
```typescript
// app/api/extract/route.ts
import { b } from '@/baml_client';
import { NextRequest } from 'next/server';

export async function POST(req: NextRequest) {
  const { text } = await req.json();

  const stream = b.stream.ExtractResume({ resume_text: text });

  return new Response(
    new ReadableStream({
      async start(controller) {
        for await (const chunk of stream) {
          controller.enqueue(new TextEncoder().encode(JSON.stringify(chunk)));
        }
        controller.close();
      },
    }),
    { headers: { 'Content-Type': 'application/json' } }
  );
}
```

### React hook — consuming a BAML stream
```typescript
// hooks/useBAMLStream.ts
import { useState } from 'react';

export function useBAMLStream() {
  const [result, setResult] = useState<string>('');
  const [loading, setLoading] = useState(false);

  async function run(text: string) {
    setLoading(true);
    const res = await fetch('/api/extract', {
      method: 'POST',
      body: JSON.stringify({ text }),
    });
    const reader = res.body!.getReader();
    const decoder = new TextDecoder();
    while (true) {
      const { done, value } = await reader.read();
      if (done) break;
      setResult(prev => prev + decoder.decode(value));
    }
    setLoading(false);
  }

  return { result, loading, run };
}
```

### Next.js environment setup (`.env.local`)
```bash
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
# Never prefix LLM keys with NEXT_PUBLIC_ — keep them server-side only
```

### generator block for TypeScript
```baml
generator target {
  output_type typescript
  output_dir ../
  version "0.75.0"
  default_client_mode async
}
```

---

## Repository structure

All content lives inside this repository. The agent should route to the correct section based on the user's intent.

```
baml-skills/
├── SKILL.md                          ← This file (entry point)
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
│   ├── 02-languages/                 ← Language guides — prioritize TypeScript
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
│   ├── 08-frameworks/                ← Next.js, LangChain, LlamaIndex, etc.
│   ├── 09-comparisons/               ← BAML vs Instructor, Vercel AI SDK, etc.
│   └── functions/                    ← Function definition deep-dives
│
├── 02-examples/
│   └── interactive-examples.mdx      ← Interactive playground examples
│
├── 03-reference/                     ← API and language reference
│   ├── overview.mdx                  ← Reference overview
│   ├── generator.mdx                 ← generator {} block reference
│   ├── baml/                         ← BAML language syntax reference
│   ├── baml_client/                  ← Generated client API reference (TypeScript-first)
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
| "How do I set up BAML in a Next.js project?" | `01-guide/02-languages/`, `03-reference/generator.mdx`, `snippets/setting-env-vars.mdx` |
| "How do I call BAML from a React component?" | `01-guide/04-baml-basics/my-first-function.mdx`, `01-guide/02-languages/` |
| "How do I stream BAML from a Next.js Route Handler?" | `01-guide/04-baml-basics/streaming.mdx`, `snippets/supports-streaming.mdx` |
| "How do I write my first BAML function?" | `01-guide/04-baml-basics/my-first-function.mdx` |
| "How does streaming work in BAML?" | `01-guide/04-baml-basics/streaming.mdx`, `snippets/supports-streaming.mdx` |
| "How do I run concurrent LLM calls?" | `01-guide/04-baml-basics/concurrent-calls.mdx` |
| "How do I pass images/audio/files to LLMs?" | `01-guide/04-baml-basics/multi-modal.mdx`, `snippets/media-url-handler.mdx` |
| "How do I handle errors in BAML?" | `01-guide/04-baml-basics/error-handling.mdx` |
| "How do I cancel a request?" | `01-guide/04-baml-basics/abort-signal.mdx` |
| "How do I set timeouts?" | `01-guide/04-baml-basics/timeouts.mdx` |
| "How do I switch LLM providers at runtime?" | `01-guide/04-baml-basics/switching-llms.mdx` |
| "How do I test BAML functions?" | `01-guide/04-baml-basics/testing-functions.mdx`, `snippets/dynamic-class-test.mdx` |
| "How does the generated client work in TypeScript?" | `01-guide/what-is-baml_client.mdx`, `03-reference/baml_client/` |
| "How do I configure LLM clients?" | `snippets/client-constructor.mdx`, `snippets/setting-env-vars.mdx` |
| "What types does BAML support?" | `snippets/supported-types.mdx` |
| "How do I write prompts / chat roles?" | `01-guide/06-prompt-engineering/`, `snippets/role-selection.mdx`, `snippets/allowed-role-metadata.mdx` |
| "How do I observe / trace BAML calls?" | `01-guide/07-observability/` |
| "How do I use BAML with Next.js / frameworks?" | `01-guide/08-frameworks/` |
| "How does BAML compare to Vercel AI SDK / Instructor?" | `01-guide/09-comparisons/` |
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
| "TypeScript types for BAML output" | `snippets/supported-types.mdx`, `snippets/client-response-type.mdx` |

---

## Key BAML concepts (quick reference)

### baml_src folder
All `.baml` source files live in `baml_src/`. These define your functions, data types, LLM clients, and test cases. BAML generates a `baml_client/` folder from these files.

### baml_client folder
Auto-generated **TypeScript** code that provides type-safe wrappers to call your BAML functions. Never edit this folder manually — regenerate with `baml generate`. Import via `import { b } from '@/baml_client'`.

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

### Calling a function (TypeScript)
```typescript
import { b } from '@/baml_client';

// Async call
const resume = await b.ExtractResume({ resume_text: '...' });

// Streaming call
const stream = b.stream.ExtractResume({ resume_text: '...' });
for await (const partial of stream) {
  console.log(partial);
}
const final = await stream.getFinalResponse();
```

---

## Loading strategy

This skill is designed for **on-demand loading**. The agent should:

1. Read this `SKILL.md` first to understand scope and structure.
2. Route to the specific file(s) listed in the routing guide above.
3. Load only the files relevant to the current user query — do not load the entire repository at once.
4. For broad questions ("explain BAML"), load `01-guide/why-baml.mdx` + `01-guide/introduction.mdx`.
5. For TypeScript/Next.js integration questions, prioritize `01-guide/02-languages/` and `01-guide/08-frameworks/`.
6. For code questions, also load the relevant snippet from `snippets/`.
7. For reference lookups, go directly to `03-reference/`.
8. Always default to **TypeScript** examples unless the user explicitly requests another language.
