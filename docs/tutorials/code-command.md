# Setting Up the `code` Command in Your Terminal

This tutorial will guide you through enabling the `code` command in your terminal, allowing you to quickly open projects or folders in Visual Studio Code using the command line.

---

## Step 1: Add the `code` Command to Your PATH

1. Open **Visual Studio Code**.
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac) to open the **Command Palette**.
3. Type:Shell Command: Install 'code' command in PATH
4. Select the option and confirm. This will add the `code` command to your terminal's `$PATH`.

---

## Step 2: Test the `code` Command

1. Open your terminal.
2. Navigate to the folder you want to open in VS Code (for example, `rust-dev-cont`):
```bash
cd /path/to/rust-dev-cont
```
3. Run:
```bash
code . 
```
!!! note
    You can specifiy a file or directory after the `code` command but `code .` just opens the current directory you are in with all of its contents and its more typical and convenient.

!!! Warning
    If the code command doesn't work, restart your terminal for the changes to take effect.
