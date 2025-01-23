# Setting up a dev container for Rust

* Primary author: [Muhammad Fouly](https://github.com/MuhammadDF)
* Reviewer: [Mohammad Saatialsoruji](https://github.com/meihab)

!!! success
    I have successfuly added admonitions to MkDocs!   
    This is just an example of admonitions you will see
    throughout this tutorial for the purpose side content without disturbing document flow :)

``` py
# I have added the code block extention for my partner - Mohammad Saatialsoruji
# Code blocks are an essential part of project documentation
# We will see these many times throughout the tutorial
print("We love COMP 423!")
```
## Welcome  

This tutorial will provide stepy-by-step instructions for creating a Dev Container in Rust.

## Part 1: Project setup

### Step 1: Creating a directory and a local Git Repository
- Open you terminal or command prompt
- Create a new directory
``` bat
mkdir rust-dev-cont
cd rust-dev-cont
```
- Initialize a new repository
``` bat
git init
```
- Create a README file
``` bat
echo "# Building a Dev Container in Rust" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2: Creating a remote repository
1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
1. Fill in the details as follows:
    - **Repository Name:** rust-dev-cont
    - **Description:** "Personal project for starting a Dev Container in Rust"
    - **Visibility:** Public
1. Do not initialize the repository with a README, .gitignore, or license.
1. Click **Create Repository.**

### Step 3: Link you Local Repository to Github
1. Add the Github repository as a remote: 
``` bat
git remote add origin https://github.com/<your-username>/comp423-course-notes.git
```
Replace `<your-username>` with your GitHub username.
1. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` choose the name `master` for the primary branch, but these days `main` is the standard primary branch name.
1. Push your local commits to the GitHub repository:
``` bat
git push --set-upstream origin main
```
!!! note
    `git push --set-upstream origin main`: This command pushes the `main` branch to the remote repository `origin`. The `--set-upstream` flag sets up the `main` branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing `git push origin` when working on your local `main` branch. This long flag has a corresponding `-u` short flag.
Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use `git log` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2: Setting up the Development Environment

### Step 1: Add Development Container Configuration
``` json
{
  "name": "My Rust Dev Container",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  },
  "postCreateCommand": ""
}
```

``` rust
fn main() {
    println!("HELLO COMP423");
}
```
``` bat
cargo new
```
``` bat
cargo build
```
``` bat
cargo run
```


