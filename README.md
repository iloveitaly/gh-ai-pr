# AI Pull Request Generator (`gh ai-pr`)

Generating pull request descriptions shouldn't be a manual chore. This extension analyzes your branch's Git history—including commit titles and extended bodies—and combines them with your project's PR template to generate a perfectly formatted prompt for an LLM.

## Installation

Install it as a GitHub CLI extension to use it across all your local repositories.

```bash
gh extension install <your-username>/gh-ai-pr
```

For local development:

```bash
# Clone the repo
git clone https://github.com/<your-username>/gh-ai-pr
cd gh-ai-pr

# Install locally
gh extension install .
```

## Usage

Simply run the command from any branch in any local repository:

```bash
gh ai-pr
```

The script will:
1. Identify your base branch (e.g., `main` or `master`).
2. Gather all commits on your current branch that aren't in the base branch.
3. Locate your `PULL_REQUEST_TEMPLATE.md` (if it exists).
4. Output a comprehensive prompt you can paste into your favorite LLM (ChatGPT, Claude, Gemini, etc.) to generate your PR description.

## Features

*   **Deep History Analysis**: Pulls not just the commit titles, but the full extended bodies of every commit on the branch.
*   **Template Aware**: Automatically finds and includes your project's `PULL_REQUEST_TEMPLATE.md` from `.github/` or the root directory.
*   **Zero Configuration**: Automatically detects the default branch and your current branch context.
*   **Pathlib Powered**: Modern, robust file and path handling using Python's `pathlib`.
*   **Portable**: Works as a native `gh` extension across your entire machine.

## How it works

The extension follows a robust detection logic:
1. **Base Branch Discovery**: It tries to find the default branch via `gh repo view`, falls back to `origin/HEAD`, and finally checks for local `main` or `master` branches.
2. **Commit Extraction**: It uses `git log` to extract everything between the base branch and your current HEAD.
3. **Template Search**: It scans common locations including `.github/PULL_REQUEST_TEMPLATE/` directories for a matching markdown template.
4. **Prompt Generation**: It assembles these pieces into a structured prompt designed to give an LLM the best possible context for writing your PR.

## [MIT License](LICENSE.md)
