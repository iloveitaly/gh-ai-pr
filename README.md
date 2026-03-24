# Generate LLM prompts for pull requests

Writing pull request descriptions can be a bit of a slog, especially when you've got a dozen commits to summarize. This extension gathers your git history and uses your repository's templates to generate a structured prompt for an LLM to do the heavy lifting for you.

## Installation

Install directly as a GitHub CLI extension:

```bash
gh extension install iloveitaly/gh-ai-pr
```

### Requirements
- [GitHub CLI (`gh`)](https://cli.github.com/)
- [uv](https://github.com/astral-sh/uv)

## Usage

Run the command from any branch in your local repository:

```bash
gh ai-pr
```

The tool will find your base branch, extract the history using `git-history-extraction`, locate your PR template, and output an XML-tagged prompt.

## Features

- **History Analysis**: Captures branch intent by extracting structured JSON history of your changes via `git-history-extraction`.
- **Template Awareness**: Prioritizes `.github/PULL_REQUEST_TEMPLATE.md` and falls back to a sane default.
- **Structured Prompts**: Uses XML-style tags to help LLMs parse instructions and context more accurately.
- **Issue Discovery**: Instructs the LLM to use GitHub search tools to link related issues.
- **Portable**: Built with `uv` inline script metadata for reliable execution without managing dependencies.

## [MIT License](LICENSE.md)
