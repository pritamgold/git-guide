# Part 1: Setting Up Git

## Step 1: Install Git

### On Windows
Download Git from [git-scm.com](https://git-scm.com/downloads/win) and run the installer.

### On macOS
Run the following command in the terminal: `brew install git`

### On Linux
Run the following command in the terminal: `sudo apt-get install git`

Once installed open the terminal and run the following command to verify the installation: `git --version`

## Step 2: Configure Git

   - Set your name and email, which will be associated with your commits:
     ```bash
     git config --global user.name "Your Name"
     git config --global user.email "your.email@example.com"
     ```
   - Verify the configuration:
     ```bash
     git config --global --list
     ```

## Step 3: Generate ssh key for git

- Generate an SSH key:
  ```bash
  ssh-keygen -t ed25519 -C "your.email@example.com"
  ```
  Press Enter to accept defaults.
  
- Copy the public key for git:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```

## Step 4: Create a GitHub Account
- Go to the [GitHub Signup](https://github.com/signup) page and create an account if you don't have one with the necessary information.
- For easier Git authentication, add the ssh key to GitHub. Copy previously copied ssh public key, then add it to GitHub under **Settings > SSH and GPG keys > New SSH key**.
## Step 5: Create a GitHub Repository
- On the top right corner of the GitHub page, click on the `+` button and select `New repository`.  
- Enter the repository name and description.
- Select the repository visibility.
- Click on the `Create repository` button.
- Once the repository is created, you will be redirected to the repository page.
- run `git init` to initialize the repository.
- run `git remote add origin <repository-ssh-url>` to add the remote repository. 

## Step 6: Make Changes and Commit

- Create a new file or edit an existing one (e.g., `README.md`):
  ```bash
  echo "# My First Git hub" > README.md
  ```
- Check the status of your repository:
  ```bash
  git status
  ```
- Stage the changes:
  ```bash
  git add README.md
  ```
- Commit the changes with a message:
  ```bash
  git commit -m "Update README with hub title"
  ```
- Push your committed changes to the remote repository:
  ```bash
  git push origin main
  ```

### To Check existing SSH keys
  ```bash
  ls ~/.ssh
  ```

### Remove all SSH Key
  ```bash
  rm -f ~/.ssh/id_*
  ```

### To Check SSH key connection
  ```bash
  $ ssh -T git@github.com
  ```

## QnA

### 1. Why Do We Need to Configure Git?

We configure Git to:

- **Set your identity** using `user.name` and `user.email`
- **Enable authentication** with Git servers
- Without configuring Git, your commits might not have proper author info, and Git operations with remote repositories may fail.

### 2. What is an SSH key?
An SSH key is a pair of cryptographic files used to securely connect to remote systems.

It has two parts:
- Private key (id_ed25519): Kept secret on your machine.
- Public key (id_ed25519.pub): Shared with the remote service (like GitHub).

It’s like:

- 🔐 Private key = your personal key
- 🏡 Public key = lock on the door at GitHub
- ✅ Only your key can open that lock

### 3. What is the purpose of using an SSH key?
SSH keys are used for secure authentication without using passwords.

In Git (e.g., GitHub, GitLab):
- Authenticate you when you git push, git clone, etc.
- Replace the need to enter a username/password every time.
- Are more secure than passwords or tokens.

In servers (e.g., VPS, cloud):
- Let you SSH (ssh user@server.com) into servers without typing passwords.
- Make automated scripts and deployments safer and easier.

### 4. `git push -u origin main` — What does -u do?
The -u (or --set-upstream) flag sets a tracking relationship between your local branch (main) and the remote branch (origin/main).

You're telling Git:

"Push my local main branch to origin and remember this connection so I can just use git push or git pull next time."

🛠️ **Without -u:**

You'd have to type the full command every time:
```bash
git push origin main
git pull origin main
```

✅ **After setting -u:**

You can simply use:
```bash
git push
git pull
```
Git will automatically know you're referring to origin/main.

#### You only need to use -u once per branch (when first pushing it). After that, Git remembers it.

### 5. Why use `main` instead of `master` in Git?

Modern Git practice prefers using the `main` branch instead of `master` for several reasons:

- **Default Standard**: Platforms like GitHub now default to `main` for new repositories.
- **Consistency**: Using `main` avoids branch name mismatches between local and remote (e.g., push errors).
- **Inclusivity**: The term `main` replaces `master` to promote more inclusive language.
- **Tool Compatibility**: Many CI/CD tools, templates, and GitHub Actions expect the default branch to be `main`.

### ✅ Best Practice:
Right after your first commit, rename the default branch:
```bash
git branch -M main
```
**- To set main as the default for all future Git repos:**
```bash
git config --global init.defaultBranch main
```



