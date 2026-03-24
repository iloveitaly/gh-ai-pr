# AI Pull Request Generator (`gh ai-pr`)

Generating pull request descriptions shouldn't be a manual chore. This extension analyzes your branch's Git history—including commit titles and extended bodies—and combines them with your project's PR template to generate a structured, XML-tagged prompt for an LLM.

## Installation

Install it directly as a GitHub CLI extension:

```bash
gh extension install iloveitaly/gh-ai-pr
```

### Requirements
- [GitHub CLI (`gh`)](https://cli.github.com/)
- [uv](https://github.com/astral-sh/uv) (for running the underlying extraction tool)

## Usage

Simply run the command from any branch in any local repository:

```bash
gh ai-pr
```

The script will:
1.  **Identify your base branch** (e.g., `main` or `master`) automatically.
2.  **Extract Git History**: Uses [`git-history-extraction`](https://github.com/iloveitaly/git-history-extraction) to gather comprehensive JSON data of your branch's changes.
3.  **Locate PR Templates**: Scans your repository for `PULL_REQUEST_TEMPLATE.md` or uses a sane fallback if none is found.
4.  **Generate Prompt**: Outputs a structured XML prompt containing the history and template, ready to be pasted into Claude, ChatGPT, or Gemini.

## Features

*   **Deep Context**: Unlike simple log tools, it captures the full intent of your changes by leveraging JSON-formatted history.
*   **Template Aware**: Respects your repository's existing PR templates while providing a high-quality fallback for projects without one.
*   **Structured Output**: Uses XML-style tags (`<git_history>`, `<pr_template>`) to help LLMs parse and follow instructions more accurately.
*   **Smart Issue Discovery**: Explicitly instructs the LLM to use GitHub search tools (like MCP) to link related issues and mention them in the description.
*   **Self-Managing**: Built with `uv` inline script metadata, ensuring it runs with the correct environment every time.

## How it works

1.  **History Analysis**: It calls `uv tool run git-history-extraction@latest` to get a structured representation of every change on your branch since it diverged from the base branch.
2.  **Template Priority**: It prioritizes `.github/PULL_REQUEST_TEMPLATE.md`, then other common locations, and finally falls back to a comprehensive default if no local template is found.
3.  **Contextual Instructions**: The final prompt includes specific instructions for the LLM to search for related issues and follow the specific formatting requirements of the provided template.

## [MIT License](LICENSE.md)
