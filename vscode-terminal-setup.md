# VS Code Terminal Setup

## Opening files from the terminal

To open files in VS Code directly from your terminal using the `code` command:

1. **Open VS Code**
2. **Open the Command Palette** (Cmd+Shift+P on macOS)
3. **Type "shell command"** and select **"Shell Command: Install 'code' command in PATH"**

This creates a symlink that allows you to use `code` from your terminal.

## Usage

After installation, you can open files with:

```bash
code somefilename.py
```

## Verification

Verify the installation by running:

```bash
which code
```

This should show something like `/usr/local/bin/code`.

## Manual Installation (Alternative)

If the automatic installation doesn't work, manually add VS Code to your PATH by adding this line to your `~/.zshrc` file:

```bash
export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
```

Then reload your shell:

```bash
source ~/.zshrc
```
