# Purpose
This repository is to test and experiment with Git CLI commands' usage and functionalities.

# Getting Started

Install Git CLI and associate it with the github account. General steps to be followed are as follows.

- **Set Up Your Git Username and Email:** These are used in your commits, and GitHub will associate them with your GitHub account.
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
- **Generate an SSH Key:** This is the most secure and convenient way to authenticate your GitHub account in the Git CLI.
  - **Check if you already have an SSH key:** Look for files named id_rsa and id_rsa.pub (or other key pairs). If they exist, you already have a key.
  ```bash
  ls -al ~/.ssh
  ```
  - **Generate a new SSH key (if needed):** Use rsa instead of ed25519 if your system doesn’t support ed25519.
  ```bash
  ssh-keygen -t ed25519 -C "your-email@example.com"
  ```
  When prompted, accept the default file location by pressing Enter, and optionally add a passphrase.
  - **Add your SSH key to the ssh-agent:** Start the ssh-agent in the background and add your SSH key.
  ```bash
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519
  ```
  - **Add the SSH key to your GitHub account:** Copy the SSH key to your clipboard
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```
  Go to your GitHub SSH settings and click "New SSH key". Paste your key and give it a title.
- **Authenticate GitHub via SSH:** To test your connection to GitHub, use below command. If everything is set up correctly, you’ll see a message saying you’ve successfully authenticated.
```bash
ssh -T git@github.com
```

**Note:** If you prefer to use HTTPS instead of SSH, google it!

# Git in Action

Now that terminal has been set up to recognise the user/account to be associated with commits/push etc, steps to create a new repo are as follows.

- **Create a New Local Git Repository**
  - Create a directory for your project (if it doesn't already exist).
  ```bash
  mkdir my-git-project
  cd my-git-project
  ```
  - Initialize Git in the directory. This creates an empty Git repository in your current directory.
  ```bash
  git init
  ```
- **Create a Test File**
  - Create a simple file to track.
  ```bash
  echo "Hello Git!" > testfile.txt
  ```
  - Check the file's status. This shows the status of files in your repository. You should see that testfile.txt is untracked.
  ```bash
  git status
  ```
- **Stage the File**
  - Add the file to the staging area. This prepares the file to be included in the next commit.
  ```bash
  git add testfile.txt
  ```
- **Make a Commit**
  - Commit the changes with a message.
  ```bash
  git commit -m "Initial commit: add testfile.txt"
  ```
- **Create a New GitHub Repository**
  - Go to GitHub and create a new repository with name 'my-git-project', and don't initialize it with a README or .gitignore since you've already set up a local repository.
  - Copy the GitHub repository URL (https://github.com/yourusername/my-git-project.git) or if you prefer SSH (git@github.com:yourusername/my-git-project.git)
- **Connect Your Local Repo to GitHub**
  - Add the GitHub repository as a remote. Replace url with SSH if preferred.
  ```bash
  git remote add origin https://github.com/yourusername/my-git-project.git
  ```
  - Verify the remote: Check that your remote URL has been set correctly.
  ```bash
  git remote -v
  ```
- **Push Your Commit to GitHub**
  - Push your local repository to GitHub
  ```bash
  git push -u origin master
  ```
  The -u origin master option sets origin (GitHub) as the default remote for future git push commands on the master branch.
- **Verify the Commit on GitHub**
  - Go to your GitHub repository in the browser. You should see the testfile.txt file and your first commit with the message "Initial commit: add testfile.txt".

# Git Going

To update your local repository with new changes from the remote repository, and then commit your own changes back to GitHub, use commands indicated below.

```bash
# Navigate to your local repo
cd my-git-project

# Pull the latest changes
git pull origin master

# Make your changes (edit files, create new ones etc.)

git status						# Check status of your repository
git add testfile.txt					# Stage changes (or use git add . to stage all)
git commit -m "Add some new changes to testfile.txt"	# Commit changes
git push origin master					# Push changes back to GitHub
```

