# Azure Cloud Shell - Study Review

## Core Idea

Azure Cloud Shell is a browser-based command-line environment for managing Azure resources. It provides an authenticated shell without requiring Azure CLI, Azure PowerShell, or related tools to be installed on the local device.

Cloud Shell is useful when you need to manage Azure resources from a browser-based device, such as another computer, a personal machine, or a device where you cannot install administrative tools.

## Key Capabilities

- Access Azure management tools directly from a web browser.
- Choose either Bash or PowerShell.
- Manage Azure resources such as virtual machines, storage, and networking.
- Use Microsoft-managed, up-to-date Azure CLI and PowerShell modules.
- Persist scripts, SSH keys, and other files between sessions through CloudDrive.
- Edit files directly in the browser through the Cloud Shell editor.
- Use common preinstalled tools such as `git`, `vim`, `nano`, `kubectl`, `Helm`, `Terraform`, `Ansible`, `AzCopy`, `npm`, `pip`, and database clients.

## How To Access Cloud Shell

Cloud Shell can be opened from:

- Direct URL: `https://shell.azure.com`
- The Azure portal
- Microsoft Learn code snippets

When a session starts, Azure allocates a temporary host that is already configured with Bash, PowerShell, Azure CLI, Azure PowerShell, and other common tools.

## Sessions And Persistence

Cloud Shell sessions run on temporary hosts. The shell environment itself is not permanent.

Important exam point: sessions terminate after 20 minutes of inactivity. When that happens, the session state is lost, but files stored in CloudDrive persist.

Use CloudDrive when you need scripts or files available across sessions and devices. You can upload a script once, then use it again from future Cloud Shell sessions.

Cloud Shell can also mount an Azure File Share. The file share is tied to a specific Azure region.

## Editing Files

Cloud Shell includes a browser-based editor for changing scripts and files stored in CloudDrive or a mounted file share.

You can open the editor from the Cloud Shell interface or, in Classic mode, with:

```bash
code filename.txt
```

Use the Cloud Shell editor when a script already exists in CloudDrive and only small changes are needed.

## When To Use Cloud Shell

Use Azure Cloud Shell when you need to:

- Run Azure CLI or PowerShell commands without installing tools locally.
- Manage Azure resources from any browser-based device.
- Access a secure, authenticated command-line environment.
- Use either Bash or PowerShell based on preference or task.
- Keep scripts, SSH keys, or small files available between sessions.
- Quickly edit scripts stored in CloudDrive.

## When Not To Use Cloud Shell

Do not use Azure Cloud Shell when you need:

- A long-running session or script that may exceed the inactivity timeout.
- Full administrator privileges such as `sudo`.
- Unsupported custom tools or deeply customized environments.
- Storage spread across multiple regions.
- Multiple concurrent Cloud Shell sessions.
- Heavy automation that should run in a dedicated VM, container, pipeline, or automation account.

## Exam Triggers

- Browser-based Azure command line: Azure Cloud Shell.
- No local install of Azure CLI or PowerShell: Azure Cloud Shell.
- Need Bash or PowerShell from the Azure portal: Azure Cloud Shell.
- Need files to persist between Cloud Shell sessions: CloudDrive.
- Need to edit a script stored in CloudDrive: Cloud Shell editor.
- Session idle for 20 minutes: session terminates; CloudDrive files remain.
- Need multiple simultaneous sessions or `sudo`: Cloud Shell is not the right tool.

## Knowledge Check Answers

1. Access Cloud Shell from Windows 11 by using a browser, such as Microsoft Edge, and signing in to an Azure subscription.
2. Store a frequently used script by uploading it to CloudDrive in Azure Cloud Shell.
3. Modify a stored script by using the Cloud Shell editor and saving it directly to CloudDrive.
