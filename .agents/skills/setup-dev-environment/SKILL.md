---
name: setup-dev-environment
description: Set up a developer's environment for this project. Use this skill when a user wants to set up their development environment, install dependencies, or asks about "setup", "getting started", "dev environment", or similar.
---

## Steps

Follow these steps in order. Notify the user of progress at each step.

### Step 1: Check Bun Installation

**Tell the user:**
> "Checking if Bun is installed. Bun is the JavaScript runtime and package manager used by this project - it's significantly faster than npm/yarn and provides built-in TypeScript support and test runner."

Run `bun --version` to check if bun is installed.

**If bun is installed:** Notify user it's already installed and proceed to Step 2.

**If bun is NOT installed:** Tell the user you're installing it, then detect the OS from `user_info` and run the appropriate command:

- **macOS/Linux** (OS Version contains `darwin` or `linux`):
  ```bash
  curl -fsSL https://bun.com/install | bash
  ```

- **Windows** (OS Version contains `windows`):
  ```powershell
  powershell -c "irm bun.sh/install.ps1|iex"
  ```

After installation completes, source the shell config based on the user's shell:
- For `zsh`: `source ~/.zshrc`
- For `bash`: `source ~/.bashrc`
- For other shells: determine the appropriate config file

Then verify installation with `bun --version`.

### Step 2: Install Dependencies

**Tell the user:**
> "Installing project dependencies. This downloads all the packages defined in package.json - React, TanStack Router, TanStack Query, shadcn/ui components, Tailwind CSS, and development tools like Biome and Playwright."

Run in the project root:

```bash
bun install
```

### Step 3: Install Playwright Chromium (Optional)

**IMPORTANT:** You MUST ask the user and wait for their response before proceeding. Do NOT continue until they answer.

**Ask the user** if they want to install Chromium for e2e testing:

- **Prompt:** "Do you want to install Chromium for e2e testing? This is optional - you can skip it if you don't plan to run Playwright tests locally."
- **Options:** "Yes, install Chromium" / "No, skip for now"

**If user chooses yes:**

Tell the user:
> "Installing Chromium browser for Playwright. This project uses Playwright for end-to-end testing - it needs a real browser to run tests against. Chromium is the open-source version of Chrome and is the default browser for this project's e2e tests."

Run:

```bash
bunx playwright install chromium
```

**If user chooses no:**

Tell the user:
> "Skipping Chromium installation. You can install it later by running `bunx playwright install chromium` if you need to run e2e tests."

### Step 4: Check shadcn MCP Server

**Tell the user:**
> "Checking if the shadcn MCP server is enabled. This project uses shadcn/ui for UI components. The MCP (Model Context Protocol) server allows me to add new shadcn components directly - like buttons, dialogs, forms - without you having to run commands manually."

Check if it's enabled:

1. Look for MCP tool descriptors by checking if files exist in a path like `mcps/project-*-shadcn/tools/` (the mcps folder path is provided in the system prompt)

2. **If MCP tools are found:** Tell the user shadcn MCP is already enabled and ready to use.

3. **If MCP tools are NOT found:** Tell the user they need to enable it manually and explain why:
   > "The shadcn MCP server needs to be enabled. This is a one-time setup that lets me add UI components for you automatically."
   
   Then provide instructions based on their environment:
   - **Cursor:** Go to Settings (Cmd/Ctrl + ,) → Features → MCP → Enable "Project MCP Servers"
   - **Claude Code:** Check `.claude/mcp.json` exists and restart Claude Code
   
   **IMPORTANT:** You MUST ask the user to confirm before proceeding. Do NOT continue until they respond.
   
   Ask: "Let me know once you've enabled the MCP server so I can continue with the setup (or say 'skip' to continue without it)."

### Step 5: Notify About Recommended Extensions (IDE only)

**Skip this step if user is using Claude Code (terminal).** This step only applies to IDE users (Cursor/VSCode).

**Tell the user:**
> "Here are some recommended extensions that will improve your development experience with this project:"

List the extensions with explanations:

- **biomejs.biome** - "Provides real-time linting and formatting feedback. This project uses Biome instead of ESLint/Prettier - it's faster and has both linting and formatting in one tool."
- **bradlc.vscode-tailwindcss** - "Gives you autocomplete for Tailwind CSS classes, hover previews of what styles they apply, and highlights invalid class names."
- **ms-playwright.playwright** - "Lets you run and debug e2e tests directly from the editor, with features like 'Pick locator' to help write tests."

Tell the user these can be installed via the Extensions panel (Cmd/Ctrl + Shift + X).

### Step 6: Completion

**Tell the user:**
> "Setup complete! Your development environment is ready."

Summarize what was set up:
- Bun runtime
- Project dependencies
- Playwright browser (Chromium) - if installed, or note it was skipped
- shadcn MCP server status
- Recommended extensions (IDE only)

Then explain the key commands they can use:
- `bun run dev` - "Starts the development server on port 3000 with hot reload"
- `bun run check` - "Runs Biome to check for linting and formatting issues"
