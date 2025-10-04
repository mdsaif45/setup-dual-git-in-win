---

## Setup Multiple GitHub Accounts on One System (Work + Personal)

Follow these steps to configure **multiple GitHub accounts** (e.g., *work* and *personal*) on the same computer using SSH keys.

---

### **Step 1 — Generate SSH Keys**

```bash
cd ~/.ssh/

# Generate SSH key for Work account
ssh-keygen -t ed25519 -C "git@workmail.com" -f id_work

# Generate SSH key for Personal account
ssh-keygen -t ed25519 -C "git@personalmail.com" -f id_personal
```

---

### **Step 2 — Start SSH Agent and Add Keys**

```bash
eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_work
ssh-add ~/.ssh/id_personal
```

---

### **Step 3 — Add SSH Keys to GitHub**

Display each public key and copy it:

```bash
cat ~/.ssh/id_work.pub
cat ~/.ssh/id_personal.pub
```

Then go to your respective GitHub accounts and add them:

* **Work Account** → *GitHub → Settings → SSH and GPG Keys → New SSH Key* → Paste `id_work.pub`
* **Personal Account** → *GitHub → Settings → SSH and GPG Keys → New SSH Key* → Paste `id_personal.pub`

---

### **Step 4 — Create SSH Config File**

```bash
nano ~/.ssh/config
```

Add the following configuration:

```bash
# Work GitHub
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_work

# Personal GitHub
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_personal
```

Save and exit (`Ctrl + O`, `Enter`, `Ctrl + X`).

---

### **Step 5 — Test SSH Connections**

```bash
ssh -T git@github-work
ssh -T git@github-personal
```

If successful, GitHub will respond:

```
Hi <username>! You've successfully authenticated...
```

---

### **Step 6 — Clone Repositories**

Use the correct host alias (`github-work` or `github-personal`):

```bash
# Personal account
git clone git@github-personal:mdsaif45/repo.git

# Work account
git clone git@github-work:company/repo.git
```

---

### **Step 7 — Set Git User Details Per Repository**

For example, inside your personal repository:

```bash
cd D:/personal-repos/my-repo

git config user.name "MD SAIF"
git config user.email "mdsaif0405@gmail.com"
```

For your work repository:

```bash
cd D:/work-repos/company-repo

git config user.name "Your Work Name"
git config user.email "git@workmail.com"
```

---

**Done!**
You can now use multiple GitHub accounts seamlessly on the same machine without SSH key conflicts.

---
