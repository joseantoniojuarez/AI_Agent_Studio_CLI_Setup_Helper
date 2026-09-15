---
name: setup-oracle-ai-agent-studio-cli
description: Prepare a user's macOS or Windows computer for Oracle Fusion AI Agent Studio CLI development. Use when a user asks to install, diagnose, verify, or upgrade the local prerequisites, repository, VS Code extension, AI Studio skills, samples, command shortcut, or authentication needed to use Oracle AI Agent Studio CLI.
---

# Oracle AI Agent Studio CLI Setup

Prepare the local development environment interactively and safely. Follow Oracle's current installation guide as the source of truth. Do not claim a setup is ready until every applicable verification passes.

## Operating rules

- Communicate in English.
- Start with read-only checks. Report what is present, missing, or incompatible before proposing changes.
- Ask for explicit approval immediately before installing software, requesting administrator privileges, modifying a shell profile, cloning/downloading files, opening a sign-in flow, or writing outside the chosen workspace.
- Never open a graphical web browser to download software, repositories, extensions, or documentation. Download required files through the terminal only, using official URLs or an approved terminal package manager. A native installer window may be used after an approved terminal download.
- Never overwrite, move, or delete user files. If a target exists, inspect it and offer a safe alternative such as a new directory.
- Never request, print, persist, or commit a password, access token, API key, or `env.properties` contents. Treat `env.properties` as sensitive.
- Use official sources and installers only. After obtaining the repository, inspect `how-to/install-and-use-fusion-ai-studio-CLI_vscode-codex.md` when it exists and follow it for the current repository layout. Preserve this skill's safety, approval, and authentication constraints if the guide is less specific.
- Use the latest release available in the official Oracle repository. Determine it automatically; do not ask the user to choose a release or default to a hard-coded release name.
- Do not begin filesystem setup from a ChatGPT-only conversation. First ensure that the user is working in a local Codex project whose primary folder is on their computer.
- Use the account that is running the current local Codex session. Do not ask for a username, create another operating-system user, or change accounts.
- If Node.js and npm are both already installed, preserve their versions. Do not label Node.js unsupported, recommend replacing it, or ask to install a different Node.js version unless the user explicitly requests a Node.js change.
- Treat a Node.js runtime without npm as an incomplete developer Node.js installation. This can be Codex's bundled runtime; do not alter it. With approval, install the official Node.js LTS package alongside it.
- Keep the user-facing flow clean. Do not expose raw shell errors, failed command syntax, command transcripts, or recovery attempts. Correct a diagnostic-command error internally and report only the final, actionable result.

## 1. Create or open a local Codex project

Before running any terminal command, determine from the host context whether the conversation is a Codex chat with a local project folder. If it is not, stop before inspecting, downloading, or installing anything.

Tell the user that a standard ChatGPT project preserves chats, sources, and instructions but does not provide direct access to a local folder. To create the required Oracle AI Studio workspace, guide the user to:

1. Open the Codex Projects view in the ChatGPT desktop app.
2. Create a **local project** (not a ChatGPT-only project).
3. Create or attach an empty, user-writable parent folder, such as `Oracle AI Agent Studio CLI`, and make it the primary folder.
4. Start a new Codex chat in that local project.
5. Invoke this skill again from that Codex chat.

Do not ask the user to create `fusion-ai-repo` or `fusion-ai-workspace` manually at this point; create those folders later in the approved local project. If the user already has a local Codex project, use its primary folder without asking for confirmation. Do not use a secondary attached folder because Codex does not automatically discover skills and project configuration from secondary folders.

If a local project is missing, give one short, nontechnical handoff only: tell the user to create or open a **local Codex project**, choose an empty user-writable folder as its primary folder, and invoke this skill again there. Do not run diagnostics first, mention a failed command, preview approvals, or list future installation steps.

## 2. Establish the setup scope

Determine the following without asking the user to confirm routine facts:

1. Detect the operating system and architecture. On macOS, detect Intel versus Apple Silicon. Report the result; do not ask the user to validate it.
2. Use the current local Codex project's primary folder as the setup root and use the current session's operating-system account. Check that the folder is writable. Ask for another location only if it is not writable or the user explicitly requests one.
3. Use Git clone when Git is already available. If Git is unavailable, use the official repository ZIP workflow instead of asking the user to choose a method or install Git.
4. Treat Codex as available because this skill runs in Codex. Record its detected status without asking about the user's intent.
5. Determine the latest available Oracle release branch or tag from the official repository before cloning, then select it automatically. After cloning, inspect the repository layout and the checked-out revision. If no release directories or Git tags are present, record the checked-out branch, commit SHA, and commit date as the selected repository snapshot; do not stop or invent a release directory.

Do not ask whether the user has Fusion AI Studio access, a server URL, or credentials. Authentication is outside this local installation phase.

Follow the applicable platform instructions in **Platform-specific instructions** after the OS is known.

## 3. Inspect prerequisites

Run platform-appropriate read-only checks for:

- Node.js and npm: `node --version` and `npm --version`.
- Git when the clone path is selected: `git --version`.
- VS Code command line availability: `code --version`.
- Codex: `codex --version`; do not interpret an unsigned-in state as an installation failure.
- Free space, write access, and any existing repository/workspace at the chosen location.

Run each check independently with a defensive command-existence probe; do not use a compound diagnostic script, a formatted PowerShell one-liner, or a command whose failure prevents the remaining checks. Treat a missing executable as a normal result, not an error. Capture diagnostic output rather than echoing it to the user.

If a diagnostic command has a syntax or formatting error, correct it and rerun it internally once. If it still cannot run, report only that the specific tool could not be inspected and continue with the unrelated checks. Do not ask the user to fix an agent-generated diagnostic command.

Node.js is required because the AI Studio CLI runs through Node.js. Classify the result precisely:

- Node.js and npm available: report both versions and continue unchanged.
- Node.js available but npm absent: report an incomplete developer Node.js installation. Do not modify the existing or bundled runtime. Offer to install the official Node.js LTS package alongside it.
- Node.js absent: offer to install the official Node.js LTS package.

Present one short readiness summary after all checks complete. Explain only the missing prerequisites and the next required approval. Do not install bundled tools merely because another installation method provides them.

## 4. Install approved prerequisites

Request approvals as separate, predictable decisions in this order when the associated action is needed:

1. Install VS Code.
2. Install official Node.js LTS when Node.js is absent or npm is absent.
3. Clone Oracle's repository or download its official ZIP archive.
4. Install the local Oracle VSIX extension.
5. On Windows, configure the required `aistudio` function in the current user's actual PowerShell host after the skill files are in place. If that host's effective policy is `Restricted`, request one clear approval for the `CurrentUser` `RemoteSigned` change and the profile update together.

Do not combine these into one approval request. Complete every approved download from the terminal; do not open a browser. Install only the approved, missing software. Never replace or modify an existing Node.js or Codex-bundled runtime. Use the applicable platform instructions below for safe choices and commands.

After each installation, open a new terminal session when needed and rerun the associated version check. Stop and diagnose PATH, permission, corporate-device, proxy, or certificate errors before proceeding.

VS Code is required. Git is optional because the ZIP workflow is used when Git is unavailable. Do not request or perform Fusion authentication during this phase.

## 5. Create the repository and workspace

Create the following structure under the chosen parent folder, adapting the root name if it already exists:

```text
my-fusion-agent-studio-cli/
├── fusion-ai-repo/       # Oracle repository clone or extracted archive
└── fusion-ai-workspace/  # Local AI Studio workspace
    ├── .agents/skills/
    └── aiapps/
```

Use `git clone https://github.com/oracle/fusion-ai-studio.git` from the terminal for the clone workflow. For the ZIP workflow, download the archive from the same official repository using a terminal download command and verify the extracted top-level folder before continuing. Do not open GitHub in a browser.

Inspect the cloned or extracted repository before assuming any paths. For the current layout, expect these root-level assets:

```text
extensions/aistudio-extension.zip
.agents/skills/
aiapps/
how-to/install-and-use-fusion-ai-studio-CLI_vscode-codex.md
```

Read the installation guide when present, then use the actual discovered paths. Do not expect `<release>/aistudio/...` folders or skill ZIP files. Record the selected release branch or tag; if neither exists, record the checked-out commit SHA and date as the selected repository snapshot.

## 6. Install the Fusion AI Studio VS Code extension

Locate the extension archive from the repository layout. In the current layout, it is:

```text
extensions/aistudio-extension.zip
```

Inspect the ZIP contents without extracting it first. Confirm that it contains the expected `.vsix` file. Extract it exactly once into a new, nonexisting directory under the approved workspace, then locate the `.vsix` file. Do not use a temporary extract-and-delete workflow.

After separate approval, install the `.vsix` in VS Code using **Extensions: Install from VSIX** (or an equivalent approved VS Code CLI action).

Verify with the Command Palette:

1. Open the palette (`Cmd+Shift+P` on macOS; `Ctrl+Shift+P` on Windows).
2. Search for `Fusion AI Studio`.
3. Confirm that `Fusion AI Studio: Configure Authentication` appears.

If the Command Palette cannot be inspected, verify the extension without using the UI:

1. Run `code --list-extensions` and confirm it includes `oracle.fusion-aistudio-vscode`.
2. Inspect the installed extension's `package.json` and confirm that it declares `Fusion AI Studio: Configure Authentication`.

If either check fails, recheck the VSIX path and installation result before proposing a reinstall.

## 7. Install skills and samples

For the current repository layout:

1. Verify that `repository/.agents/skills/aistudio/SKILL.md` exists.
2. Copy the contents of `repository/.agents/skills/` to `fusion-ai-workspace/.agents/skills/`.
3. Copy the contents of `repository/aiapps/` to `fusion-ai-workspace/aiapps/`.

If the repository instead has a documented legacy layout, follow its installation guide and use the discovered paths; never assume ZIP assets exist.

Before every copy, compare source and destination. When the destination has existing contents, do not merge blindly; show the conflict and ask the user whether to skip, use a new workspace, or manually review it.

Verify the resulting layout includes at least:

```text
fusion-ai-workspace/
├── .agents/skills/aistudio/SKILL.md
└── aiapps/
```

## 8. Open and configure the workspace

Open the appropriate project folder in VS Code. If VS Code displays a workspace-trust prompt, explain that trust enables extension code in this local Oracle workspace and let the user decide.

After the core workspace is working, generate the `aistudio` command with the discovered absolute path to `aistudio.js`; never copy an example path from documentation. On macOS, offer the shell alias as an optional convenience. On Windows, configure the PowerShell function as a required setup step whenever VS Code is newly installed or already present. Obtain the separate approval before editing `~/.zshrc` or the PowerShell profile.

Defer Fusion authentication and never automate it. State in the final report that the user must later run **Fusion AI Studio: Configure Authentication** in VS Code themselves, using administrator-provided details. Do not ask for, receive, display, or handle credentials.

## 9. Verify readiness and report

Run the non-destructive checks that apply:

- Node.js and npm return versions.
- Git returns a version when used.
- VS Code is installed and Fusion AI Studio commands are discoverable.
- The selected repository snapshot and its assets exist.
- The `aistudio` skill and app skills are in `.agents/skills/`.
- Sample apps are in `aiapps/`.
- On Windows, the required `aistudio` PowerShell function resolves and `aistudio --help` succeeds from a fresh instance of the user's selected PowerShell host, outside the workspace.
- On macOS, the optional `aistudio` alias resolves when configured.

Offer to run `aistudio init` only in a new or explicitly nominated project directory. Explain that it creates project files and obtain approval before running it.

Finish with a concise report listing completed checks, installed components, detected Node.js and npm status, actual workspace/repository paths, automatically selected release branch/tag or repository snapshot (commit SHA and date), extension verification, and `aistudio` command verification. State any PowerShell profile conflict or declined approval. State that Fusion authentication is deferred and must be completed manually. Do not include credentials or secret values.

## Platform-specific instructions

### macOS

#### Detect the platform

Run:

```zsh
sw_vers
uname -m
```

Interpret `arm64` as Apple Silicon and `x86_64` as Intel. Choose installers compatible with the detected architecture.

#### Check prerequisites

Run these independently so one missing command does not hide the others:

```zsh
node --version
npm --version
git --version
code --version
codex --version
```

`git` and `codex` are conditional requirements. If VS Code is installed but `code` is unavailable, open VS Code's Command Palette and run **Shell Command: Install 'code' command in PATH**, after user approval.

#### Install missing software

Use terminal-only downloads from official sources. For direct downloads, use `curl` with an official URL selected for the detected architecture. If the user explicitly prefers Homebrew and it is already installed, offer its current package command; Homebrew downloads through the terminal. Do not install Homebrew unless the user specifically asks for it. Never open a browser or a download page.

After a package installer completes, ask the user to reopen Terminal if the command remains unavailable, then rerun the relevant version check.

#### Filesystem and extraction

Use quoted absolute paths. Favor `mkdir -p` for new folders. Do not use a destination that contains an existing Oracle repository or workspace without first inspecting and discussing it.

macOS can extract ZIP files in Finder by double-clicking or with Archive Utility. If using a terminal extractor, list the archive contents first and extract into a clearly named folder under the chosen parent directory.

#### MacOS `aistudio` alias

Use the discovered absolute path to `aistudio.js`. For zsh, the generated line should have this shape:

```zsh
alias aistudio='node "/absolute/path/to/.agents/skills/aistudio/scripts/aistudio.js"'
```

Before adding it, show the exact command, explain that it modifies `~/.zshrc`, and get approval. Preserve the existing file and avoid adding an identical alias twice. Afterward, either start a new zsh session or run `source ~/.zshrc`, then verify `aistudio --help`.

### Windows

#### Detect the platform

Run in PowerShell:

```powershell
$PSVersionTable.PSVersion
[System.Runtime.InteropServices.RuntimeInformation]::OSArchitecture
```

Use architecture-compatible installers. Treat a managed corporate device or policy block as a reason to ask the user to involve their IT administrator rather than attempting workarounds.

#### Check prerequisites

Run these independently:

```powershell
node --version
npm --version
git --version
code --version
codex --version
```

`git` and `codex` are conditional requirements. If VS Code is installed but `code` is unavailable, use VS Code's Command Palette to install the `code` command in PATH, if the installed VS Code version provides that command.

Treat a working `node` command without a working `npm` command as an incomplete developer Node.js installation, which may be Codex's bundled runtime. Do not modify it; request the separate Node.js LTS approval described above.

#### Install missing software

Use the official VS Code **User Installer** by default. It installs for the current account and avoids administrator privileges. Download it from PowerShell, storing it under an approved workspace download folder, and never open a browser. Use the architecture-specific official endpoint with `latest`, for example:

```powershell
https://update.code.visualstudio.com/latest/win32-x64-user/stable
https://update.code.visualstudio.com/latest/win32-arm64-user/stable
```

Use `Invoke-WebRequest` or an equivalent terminal download command, then run the approved installer. If the user explicitly prefers `winget` and it is available, offer its current official package command; `winget` downloads through the terminal. Do not install a package manager merely to perform this setup.

For Node.js LTS, use `winget` when available or resolve the current LTS installer from the official `nodejs.org` distribution metadata and download it from PowerShell. Do not open the Node.js website in a browser.

After a VS Code user installation, verify its launcher directly before relying on PATH:

```powershell
$codeLauncher = Join-Path $env:LOCALAPPDATA 'Programs\Microsoft VS Code\bin\code.cmd'
Test-Path $codeLauncher
& $codeLauncher --version
```

A newly installed `code` command might not be visible in the already-open PowerShell session. Restart PowerShell, then rerun the appropriate version check.

#### Filesystem and extraction

Use `New-Item -ItemType Directory` for directories only after checking for an existing path. Inspect ZIP contents without extracting them first. For example, use `System.IO.Compression.ZipFile` to list the archive entries, then extract exactly once with `Expand-Archive` to a new, nonexisting directory. Do not extract into a temporary directory and delete it afterward.

When copying skills or samples, never use `Copy-Item` without `-Recurse`. Use this safe pattern after confirming the source and destination paths:

1. Confirm that each destination folder (`.agents\skills` and `aiapps`) is absent or empty. Stop and ask the user how to handle nonempty destinations.
2. Create the empty destination folder, if necessary.
3. Copy source contents, not just the source directory, with `Copy-Item -Path (Join-Path $source '*') -Destination $destination -Recurse`.
4. Compare recursive source and destination file counts.
5. Verify that `fusion-ai-workspace\.agents\skills\aistudio\SKILL.md` exists.

For extension verification when the Command Palette is unavailable, run `code --list-extensions` (or the verified `$codeLauncher`) and confirm `oracle.fusion-aistudio-vscode` is listed. Then inspect the installed extension's `package.json` under `$env:USERPROFILE\.vscode\extensions\oracle.fusion-aistudio-vscode*` and confirm it declares `Fusion AI Studio: Configure Authentication`.

#### Required `aistudio` PowerShell function

When VS Code is newly installed or is already present for the current user, configure this function after `fusion-ai-workspace\.agents\skills\aistudio\scripts\aistudio.js` has been verified. This is required so `aistudio` can run from any PowerShell terminal, not only from the workspace directory.

First detect whether the user normally opens **Windows PowerShell 5.1** (`powershell.exe`) or **PowerShell 7** (`pwsh.exe`). These hosts use different `$PROFILE` paths. Determine the user's actual interactive host from their current terminal or project configuration when that information is available. If it cannot be determined safely, ask one concise question. Do not select the shell that happens to run Codex merely because it is available.

Use the selected shell executable to obtain its `$PROFILE` and effective execution policy. Check the policy in that same shell. If the effective policy is `Restricted`, explain that the profile cannot load and ask once for approval to run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
```

Run that command only in the selected user shell and only after approval. Do not change the LocalMachine policy, bypass the policy, or alter the policy when it is not `Restricted`.

Use the discovered absolute Windows path to `aistudio.js`. The function must have this shape:

```powershell
function aistudio { node "C:\absolute\path\.agents\skills\aistudio\scripts\aistudio.js" @args }
```

Before editing, show the exact function and the selected shell's `$PROFILE`. If the policy is `Restricted`, use the single approval already requested for the policy change and profile update. Otherwise, request the profile-modification approval even when the profile does not exist. If needed, create the profile directory and profile file only after approval.

Preserve existing profile content. Use an identifiable managed block for this function and update only that block on later runs. If an unmarked `aistudio` function already exists, do not overwrite it: show its location, explain the conflict, and ask the user whether to replace it. Do not create duplicate function definitions.

Do not create an `aistudio.cmd` file, edit PATH, or place a wrapper beside Node.js as the default solution.

Start a fresh instance of the exact selected shell, set its current directory outside the workspace, then verify `Get-Command aistudio` and `aistudio --help`. Do not report readiness merely because the profile file or function block exists. Report success only when both commands succeed in that fresh terminal. If the policy or profile prevents that verification, report the specific blocker and do not claim the command is ready.

## Official sources

- Oracle setup overview: <https://blogs.oracle.com/fusioncoe/fusion-aistudio-cli>
- Oracle repository: <https://github.com/oracle/fusion-ai-studio>
- Release-specific Oracle installation guide: discover it inside the selected release in the Oracle repository.
- Node.js downloads: <https://nodejs.org/en/download>
- Visual Studio Code downloads: <https://code.visualstudio.com/>
- Codex quickstart: <https://developers.openai.com/codex/quickstart?setup=app>
- Codex projects and local folders: <https://learn.chatgpt.com/docs/projects>
