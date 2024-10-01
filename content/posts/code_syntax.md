---
author: ["Mariusz Gumienny"]
title: "Code Syntax Guide"
date: "2019-03-10"
description: "Sample article showcasing basic code syntax and formatting for HTML elements."
summary: "Sample article showcasing basic code syntax and formatting for HTML elements."
tags: ["markdown", "syntax", "code", "gist"]
categories: ["themes", "syntax"]
series: ["Themes Guide"]
ShowToc: true
TocOpen: true
---

### Inline Code

`This is Inline Code`

### Only `pre`

<pre>
This is pre text
</pre>

### Code block with backticks

```{hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with backticks and language specified

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with backticks and language specified with line numbers

```html {linenos=true}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block with line numbers and <mark>highlighted</mark> lines

- PaperMod supports `linenos=true` or `linenos=table`

```html {linenos=true,hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

- <del>With `linenos=inline` line <mark>**might not** get highlighted</mark> properly.<del>

```html {linenos=inline,hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
    <meta
      name="description"
      content="Sample article showcasing basic Markdown syntax and formatting for HTML elements."
    />
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### Code block indented with four spaces

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>

### Code block with Hugo's internal highlight shortcode

{{< highlight html >}}

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Example HTML5 Document</title>
</head>
<body>
  <p>Test</p>
</body>
</html>

{{< /highlight >}}

### Github Gist

{{< gist 0x8b cc825d44d52545b3bd6c6ad32fc66124 >}}

## Fragment kodu z mojego projektu

Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.

```python {linenos=true,hl_lines=["26-28","10-13"],linenostart=575}
def initialize_self_guided_rag_agent():
    workflow = StateGraph(AnswerState)

    workflow.add_node("retrieve_documents", _retrieve_documents)
    workflow.add_node("grade_documents", _grade_documents)
    workflow.add_node("generate_answer", _generate_answer)
    workflow.add_node("transform_query", _transform_query)
    workflow.add_node("decrease_iteration_limit", _decrease_iteration_limit)
    workflow.add_node("generate_search_engine_query", _generate_search_engine_query)
    workflow.add_node("search_and_index_documents", _search_and_index_documents)

    workflow.add_edge(START, "retrieve_documents")
    workflow.add_edge("retrieve_documents", "grade_documents")
    workflow.add_edge("generate_search_engine_query", "search_and_index_documents")
    workflow.add_edge("search_and_index_documents", "retrieve_documents")
    workflow.add_conditional_edges(
        "grade_documents",
        _decide_to_generate,
        {
            "generate_search_engine_query": "decrease_iteration_limit",
            "give_up": END,
            # "transform_query": "transform_query",
            "generate_answer": "generate_answer",
        },
    )
    workflow.add_conditional_edges(
        "decrease_iteration_limit",
        _decide_to_failsafe,
        {
            "break": END,
            "continue": "generate_search_engine_query",
        },
    )
    workflow.add_edge("transform_query", "retrieve_documents")
    workflow.add_conditional_edges(
        "generate_answer",
        _evaluate_answer_grounding_and_relevance,
        {
            "not supported": "generate_answer",
            "useful": END,
            "not useful": "transform_query",
        },
    )

    compiled_workflow = workflow.compile()

    return compiled_workflow


class AnswerGenerationError(Exception):
    pass
```

### Elixir

```elixir {linenos=true,hl_lines=["26-28","10-13"]}
defmodule DataMatrix do
  @moduledoc """
  Library that enables programs to write Data Matrix
  barcodes of the modern ECC200 variety.
  Docs: https://github.com/0x8b/datamatrix
  """

  alias DataMatrix.{Bits, Encode, Matrix, ReedSolomon, Render}

  @default_opts [
    quiet_zone: 1,
    shape: :square
  ]

  def encode(data, opts \\ [])

  def encode(data, opts) when is_binary(data) do
    opts = Keyword.merge(@default_opts, opts)

    case Encode.encode(data, opts[:version] || opts[:shape] || :square) do
      {:ok, version, data_codewords} -> {:ok, "abc"}
      {:error, error} -> {:error, error}
    end
  end

  def encode(data, _opts) when is_nil(data) or data == <<>> do
    {:error, "Zero length data"}
  end

  defp do_encode(version, data_codewords, opts) do
    error_codewords = ReedSolomon.encode(version, data_codewords)

    Matrix.new(version)
    |> Matrix.draw_patterns()
    |> Matrix.draw_data(Bits.extract(data_codewords <> error_codewords))
    |> Matrix.draw_quiet_zone(opts[:quiet_zone] || 1)
    |> Matrix.export()
  end

  def format(matrix, _, opts \\ [])

  def format(matrix, :svg, opts) do
    Render.SVG.format(matrix, opts)
  end

  def format(matrix, :png, opts) do
    Render.PNG.format(matrix, opts)
  end

  def format(matrix, :text, opts) do
    Render.Text.format(matrix, opts)
  end
end
```
