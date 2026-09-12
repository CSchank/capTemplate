---
title: Markdown Pipeline Test
author: capTemplate CI
date: 2026-09-12
---

# Purpose

This document exists to verify that the build pipeline compiles Markdown
deliverables to PDF with pandoc, alongside the LaTeX documents. It is a
temporary artifact and is expected to be deleted once the pipeline is
confirmed working.

Teams who prefer Markdown over LaTeX can write a deliverable this way: any
`.md` file under `docs/` is compiled, except `README.md` and
`Expectations*.md`, which belong to the course instructors.

# Features exercised

The sections below deliberately use constructs that require LaTeX packages
beyond the bare minimum, so that a missing package shows up as a failed
build rather than a silently degraded document.

## Tables

Pandoc renders these using `longtable` and `booktabs`.

| Document type | Source extension | Compiler |
|---------------|------------------|----------|
| LaTeX         | `.tex`           | pdflatex |
| Markdown      | `.md`            | pandoc   |

## Mathematics

Inline math such as $O(n \log n)$, and a displayed equation requiring
`amsmath`:

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$

## Code

```python
def dependencies(document):
    """Recorded from the .fls file pdflatex writes."""
    return manifest[document]
```

## Lists and quotes

1. Ordered item
2. Another item
   - A nested bullet
   - And one more

> A block quote, to confirm the default template styles it.

# Notes

If both `Foo.md` and `Foo.tex` exist in one folder, the Makefile lists the
Markdown rule first, so Markdown wins.
