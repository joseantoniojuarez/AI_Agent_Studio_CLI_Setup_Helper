# Oracle AI Agent Studio CLI Setup Helper

Get an Oracle AI Agent Studio development environment ready with a single request.

This repository contains a Codex skill that prepares a safe, local workspace for Oracle AI Agent Studio CLI development. It handles the setup work that can otherwise slow down the first step: prerequisites, the Oracle repository, the VS Code extension, skills, sample apps, and a ready-to-use project structure.

> Builders gonna build!

## What the skill prepares

- A local Codex project and workspace structure.
- Node.js and npm checks, while preserving an existing developer Node.js installation.
- Visual Studio Code and the Fusion AI Studio VS Code extension.
- The current Oracle Fusion AI Studio repository snapshot, its skills, and sample apps.
- A project layout ready for AI Agent Studio development.
- On Windows, a verified `aistudio` PowerShell command that works outside the workspace.
- On Mac, an alias to `aistudio` command that works outside the workspace.

The skill works on macOS and Windows. It uses terminal-based downloads, asks for approval before every material change, avoids overwriting existing files, and defers Fusion authentication to the user.

The setup has been tested on both platforms.

## Use the skill

1. Create or open a local Codex project and select an empty, user-writable folder as its primary folder.
2. Copy the `setup-oracle-ai-agent-studio-cli` folder into that project's `.agents/skills/` directory, or install it in your personal `.agents/skills/` directory.
3. Start a Codex chat in the local project.
4. Invoke the skill:

   ```text
   $setup-oracle-ai-agent-studio-cli
   ```

   Or simply ask Codex to prepare your computer for Oracle AI Agent Studio CLI development.

The full workflow is defined in [SKILL.md](setup-oracle-ai-agent-studio-cli/SKILL.md).

## What to expect

The skill first checks the local environment, then requests focused approvals for only the changes that are needed. It automatically detects the operating system, selects the current Oracle repository snapshot, and keeps Fusion credentials out of the setup flow.

After the setup, open the workspace in VS Code and begin building AI Agent Studio apps, workflows, agents, business objects, tools, and more.

## Source material

- [Oracle Fusion AI Studio repository](https://github.com/oracle/fusion-ai-studio)
- [Oracle Fusion AI Agent Studio CLI overview](https://blogs.oracle.com/fusioncoe/fusion-aistudio-cli)
