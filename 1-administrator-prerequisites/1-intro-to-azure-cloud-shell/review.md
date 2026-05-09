# Azure Cloud Shell - Study Review

## Core Idea

Azure Cloud Shell is a browser-accessible command-line environment for managing Azure resources. It gives you an authenticated shell without requiring local installation of Azure CLI, Azure PowerShell, or supporting tools.

For AZ-104, know when Cloud Shell is useful, how files persist, and what its limits are.

## Key Capabilities

- Access a command-line environment from a browser.
- Choose either `Bash` or `PowerShell`.
- Manage Azure resources using current Azure CLI and PowerShell modules.
- Persist files across sessions with `CloudDrive`.
- Store reusable scripts, SSH keys, and other admin files.
- Edit files with the Cloud Shell editor.
- Use preinstalled tools such as `git`, `vim`, `nano`, `kubectl`, `Helm`, `Terraform`, `Ansible`, and `AzCopy`.

## How It Works

You can open Cloud Shell from:

- `https://shell.azure.com`
- The Azure portal.
- Microsoft Learn code snippets.

When you start Cloud Shell:

- Azure allocates a temporary host for the session.
- The environment is already authenticated with your Azure account.
- You choose `Bash` or `PowerShell`.
- Files in the temporary session are not the same as persisted files in `CloudDrive`.
- Sessions terminate after `20 minutes` of inactivity.

Persistent storage:

- `CloudDrive` persists files between sessions.
- CloudDrive uses an Azure file share tied to a specific region.
- Files such as scripts and SSH keys can be reused from different devices.

Editor access:

- Use the Cloud Shell editor from the browser interface.
- In Classic mode, use `code <filename>` to edit a file.

## When To Use

Use Azure Cloud Shell when you need to:

- Manage Azure from a browser-based device.
- Avoid installing local tools.
- Use Azure CLI or Azure PowerShell quickly.
- Access saved scripts from `CloudDrive`.
- Make small edits to scripts or files from the browser.
- Troubleshoot or administer resources when away from your normal admin workstation.

## When Not To Use

Do not use Azure Cloud Shell when you need:

- Long-running scripts that exceed the inactivity window.
- `sudo` or full admin access to the shell host.
- Tools that are not supported in the limited Cloud Shell environment.
- Multiple Cloud Shell sessions at the same time.
- Persistent storage in multiple regions without additional synchronization.
- A custom VM or container environment.

## Exam Triggers

- Browser-based command line for Azure: `Azure Cloud Shell`.
- Choice of shell: `Bash` or `PowerShell`.
- Persist scripts between sessions: upload to `CloudDrive`.
- Session inactivity timeout: `20 minutes`.
- Edit persisted script in browser: Cloud Shell editor or `code <filename>` in Classic mode.
- No local Azure CLI install needed: use Cloud Shell.
- Need full custom tooling or sudo: use another environment, such as a VM.

## Knowledge Check Answers

1. Access Azure Cloud Shell from Windows 11 by using a browser such as Microsoft Edge to sign in to an Azure subscription.
2. Store a reusable script by uploading it to `CloudDrive` in an Azure Cloud Shell session.
3. To make small changes to a stored script, use the Cloud Shell editor and save it directly to `CloudDrive`.
