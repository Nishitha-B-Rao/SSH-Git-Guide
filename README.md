# SSH-Git-Guide

This guide provides step-by-step instructions to set up Git, authenticate using SSH, and push your code to GitHub.

## 1. Generate an SSH Key (If Not Already Created)
Run the following command to generate a new SSH key:
```sh
ssh-keygen -t ed25519 -C "your-email@example.com"
```
If you're using an older system that doesn't support Ed25519, use:
```sh
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```
Press **Enter** to save it in the default location (`~/.ssh/id_ed25519` or `~/.ssh/id_rsa`).

## 2. Add the SSH Key to the SSH Agent
Ensure the SSH agent is running:
```sh
eval "$(ssh-agent -s)"
```
Then add the key:
```sh
ssh-add ~/.ssh/id_ed25519  # or ~/.ssh/id_rsa
```

## 3. Add the SSH Key to Your GitHub Account
Copy the SSH key to your clipboard:
```sh
cat ~/.ssh/id_ed25519.pub  # or ~/.ssh/id_rsa.pub
```
Go to **GitHub → Settings → SSH and GPG keys → New SSH key**, then paste the key and save.

## 4. Test the SSH Connection
Verify that SSH authentication is working:
```sh
ssh -T git@github.com
```
If successful, you’ll see:
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 5. Initialize a Git Repository (If Not Already Initialized)
Navigate to your project directory and initialize Git:
```sh
cd /path/to/your/project
git init
```

## 6. Add a Remote Repository
Check if a remote repository exists:
```sh
git remote -v
```
If no remote is listed, add one:
```sh
git remote add origin git@github.com:your-username/your-repo.git
```
If the remote exists but needs updating:
```sh
git remote set-url origin git@github.com:your-username/your-repo.git
```

## 7. Add and Commit Files
```sh
git add .
git commit -m "Initial commit"
```

## 8. Push to GitHub
Check your current branch:
```sh
git branch
```
If your branch is `master`, rename it to `main`:
```sh
git branch -m master main
```
Push the changes:
```sh
git push -u origin main
```

## 9. Handling Push Errors
If you get a `non-fast-forward` error:
```sh
git fetch origin
git pull origin main --rebase
git push origin main
```
If you want to **overwrite** the remote branch (use with caution!):
```sh
git push --force origin main
```

## Troubleshooting
- If you encounter permission errors, ensure your SSH key is added using `ssh-add`.
- If SSH connection fails, check if the SSH agent is running.
- Ensure you added the **public key** (`.pub` file) to GitHub.
- If your push is rejected due to non-fast-forward updates, perform a `git pull --rebase` before pushing.

---
Now you’re all set to use Git with SSH and push your code to GitHub! 🚀

