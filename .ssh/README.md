# `~/.ssh/` – SSH Config & GitHub Setup

**Configuration File:** [config file](./config)

**Purpose:**
The alias **`0x00webs`** is used as a shorthand to connect to GitHub using a specific SSH key. This allows Git operations without specifying `git@github.com` directly, and supports multiple SSH keys if needed.

---

## 1️⃣ Verify GitHub SSH connection

Use the alias in the SSH command:

```bash
ssh -T 0x00webs
```

**Example session:**

```bash
┌─[0x00webs@ubuntu]─(~)                                                                     
└─[12:32]-(^_^)-[$] ssh -T 0x00webs                                                                
Enter passphrase for key '/home/nodewave/.ssh/0x00webs':                                           
Hi 0x00webs! You've successfully authenticated, but GitHub does not provide shell access.
```

**Notes:**

* The first time you connect, GitHub’s host key will be added to `~/.ssh/known_hosts`.
* The username in the config (`User git`) ensures GitHub authentication works; do **not** use your GitHub username here.

---

## 2️⃣ Clone repositories using the alias

Once authentication is confirmed, use the alias when cloning:

```bash
git clone 0x00webs:<github-username>/<repository>.git
```

**Example:**

```bash
git clone 0x00webs:0x00webs/.github.git
```

This will:

* Use the SSH key defined in `~/.ssh/config` for `0x00webs`
* Authenticate automatically with GitHub
* Avoid issues with `Permission denied (publickey)` errors

---

## 3️⃣ Tips & Best Practices

* **Passphrase convenience:** Start the SSH agent and add your key to avoid repeated prompts:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/0x00webs
```

* **Multiple GitHub accounts:** Define additional aliases in your `~/.ssh/config`:

```ssh
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work

Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
```

* **Update remotes for existing repos**:

```bash
git remote set-url origin 0x00webs:<github-username>/<repo>.git
```
