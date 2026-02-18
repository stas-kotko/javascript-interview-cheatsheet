# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A JavaScript interview cheatsheet — a collection of Markdown files covering JS concepts for technical interview preparation. There is no application code, build system, or tests. The repository is purely documentation.

## Linting

Markdown files are linted with markdownlint. Config is in `.markdownlint.json`:
- Hard tabs are allowed
- Up to 3 consecutive blank lines permitted (MD012)
- MD032 (blanks around lists) and MD034 (bare URLs) are disabled

## Content Structure

All content lives under `topics/`. Single-page topics are standalone `.md` files; multi-file or growing topics are grouped into kebab-case subdirectories (browser, design-patterns, functions, objects, prototypes, runtime, testing).

### Naming Conventions

- **Folders**: kebab-case (`design-patterns/`, `runtime/`)
- **Files**: kebab-case (`web-workers.md`, `async-defer.md`)
- **Numeric prefixes**: `NN-` with hyphen, only when ordering matters within a folder (e.g., `01-objects.md`, `02-objects-configuration.md`)
- Use a **folder** when a topic has 2+ files or is a category expected to grow
- Use a **standalone file** for self-contained single-page topics

## Writing Conventions

- Content uses JS code blocks with explanatory comments inline
- Topics cover concepts, gotchas, and tricky interview questions rather than being tutorials
- Existing files mix prose explanations with code examples — match this style when editing
