# Setup VSCode Git + GPG

This guide shows how to configure your **VSCode inbuilt Git tools** to work with **GitHub** and optionally **sign commits using GPG**. It also explains how to update your `.gitconfig` for a smooth workflow.

---

## 1️⃣ Prerequisites

* **VSCode** installed with Git integration (built-in).
* **Git** installed (Ubuntu/Debian):

```bash
sudo apt update
sudo apt install git gnupg2 pinentry-curses
```

* A **GitHub account**.
* Optional: **GPG installed** if you want signed commits.

---

## 2️⃣ Generate a GPG key (optional)

If you want to sign commits:

```bash
gpg --full-generate-key
```

* **Algorithm**: ECC → Curve 25519 (default)
* **Usage**: Sign only
* **Set name/email**: Your GitHub username/email
* **Passphrase**: choose a secure one

Export your **public key** to add it to GitHub:

```bash
gpg --armor --export <your-email@example.com>
```

* Go to **GitHub → Settings → SSH and GPG keys → New GPG key**
* Paste the public key and save.

---

## 3️⃣ Configure Git

Edit your `~/.gitconfig` (or create it) with the following recommended setup:

```ini
[user]
    name = Your Name
    email = you@example.com
    signingkey = <YOUR_GPG_KEY_ID>
    ; gpgSign = true                 ; uncomment to sign all commits

[core]
    editor = code --wait
    excludesfile = ~/.gitignore_global
    autocrlf = input
    safecrlf = true
    precomposeunicode = true

[color]
    ui = auto
    branch = auto
    diff = auto
    status = auto

[init]
    defaultBranch = main

[pull]
    rebase = false
    ff = only

[push]
    default = simple

[credential]
    helper = manager-core
    useHttpPath = true

[merge]
    tool = vscode

[mergetool "vscode"]
    cmd = code --wait --merge $MERGED $LOCAL $BASE $REMOTE
    trustExitCode = false

[diff]
    tool = vscode
    renames = copies

[difftool "vscode"]
    cmd = code --wait --diff $LOCAL $REMOTE

[commit]
    gpgSign = true                 ; uncomment to sign commits by default

[alias]
    st = status -sb
    ci = commit
    co = checkout
    br = branch
    df = diff
    dff = difftool
    mt = mergetool
    amend = commit --amend --no-edit
    fixup = commit --fixup
    wip = "!git add -A && git commit -m \"WIP\""
    lg = log --graph --decorate --pretty=format:'%C(yellow)%h%Creset %C(cyan)%an%Creset %C(green)(%cr)%Creset %C(red)%d%Creset%n  %s' --abbrev-commit
    lga = log --graph --all --decorate --oneline
```

> Save this file as `~/.gitconfig`. For machine-specific settings, use `~/.gitconfig.local` and include it via `[include]`.

---

## 4️⃣ Test VSCode Git with GPG

1. Open a repo in VSCode.
2. Stage changes in **Source Control**.
3. Commit using the built-in commit box.
4. If signing is enabled, VSCode will prompt for your GPG passphrase.

Verify commit signature:

```bash
git log --show-signature -1
```

* Should display: `Good signature from "Name <your-email@example.com>"`

---

## 5️⃣ Optional: Skip GPG signing

If you **don’t want to use GPG**:

```bash
git config --global commit.gpgsign false
```

* VSCode commits will no longer fail with `gpg: invalid user ID`.
* You can still manually sign commits with `-S` if needed.

---

## 6️⃣ Tips & Best Practices

* **Aliases**: Use `st`, `ci`, `co`, `lg` for faster workflow.
* **VSCode diffs/merge**: Set your editor in `.gitconfig` for better visual tools.
* **Multiple accounts**: Use `[includeIf "gitdir:~/work/"]` to auto-switch `.gitconfig` per repo directory.
* **Credential caching**: `manager-core` stores GitHub credentials securely.

---

### TL;DR

1. Install Git & GPG.
2. Generate and register your GPG key (optional).
3. Update `~/.gitconfig` with recommended settings.
4. Use VSCode Source Control to commit; it will honor your Git and GPG settings.
5. Disable signing if you prefer not to use GPG. (may cause commit failures otherwise)
