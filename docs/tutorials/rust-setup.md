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

## Prerequsites
Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at [GitHub.](https://github.com/)
1. Git installed: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.
1. Visual Studio Code (VS Code): Download and install it from [here.](https://code.visualstudio.com/)
1. Docker installed: Required to run the dev container. [Get Docker here.](https://www.docker.com/products/docker-desktop)

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

### What is a Development (Dev) Container?
A dev container ensures that your development environment is consistent and works across different machines. At its core, a dev container is a preconfigured environment defined by a set of files, typically leveraging Docker to create isolated, consistent setups for development. Think of it as a "mini computer" inside your computer that includes everything you need to work on a specific project—like the right programming language, tools, libraries, and dependencies.

Why is this valuable? In the technology industry, teams often work on complex projects that require a specific set of tools and dependencies to function correctly. Without a dev container, each developer must manually set up their environment, leading to errors, wasted time, and inconsistencies. With a dev container, everyone works in an identical environment, reducing bugs caused by "it works on my machine" issues. It also simplifies onboarding new team members since they can start coding with just a few steps.

### How are software project dependencies managed?
To effectively manage software dependencies, it's important to understand package and dependency management. In most software projects, you rely on external libraries or packages to save time and leverage work that has already been done by others. Managing these dependencies ensures that your project has access to the correct versions of these libraries, avoiding compatibility issues.

These libraries are installed using cargo, a package manager for Rust.

In summary, the the devcontainer.json file specifies configuration for a consistent development environment using a Docker image. The requirements.txt file ensures all needed Rust package for our project are installed when the container is created. Together, these files automate the process of setting up a developer environment, making it easier for you and others to work on the project.

Lets establish your development environment:


### Step 1: Add Development Container Configuration

1. In VS Code, open the `rust-dev-cont` directory. You can do this via: File > Open Folder.
1. Install the Dev Containers extension for VS Code.
1. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:  

`.devcontainer/devcontainer.json`

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- `name`: A descriptive name for your dev container.
- `image`: The Docker image to use, in this case, the latest version of a Rust environment. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!
- `customizations`: Adds useful configurations to VS Code, like installing the Rust Analyzer extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.
- `postCreateCommand`: A command to run after the container is created. In our case, we do not need to install anything extra for us to print a simple string in Rust.
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

### Step 2. Reopen the Project in a VSCode Dev Container
Reopen the project in the container by pressing Ctrl+Shift+P (or Cmd+Shift+P on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running rust --version to see your dev container is running a recent version of Python without much effort! (As of January 2025, the latest stable Rust version is 1.84.0.)

## Part 3: Developing in Rust

### Creating a New Package
To start a new package with Cargo, use cargo new:
``` bat
cargo new hello_world --vcs none
```
The `--vcs none` flag tells cargo to not create a git repository for you which is the default behavior.  
!!! warning
    If you forgot the `--vcs none` flag no problem. You can run the following commands to delete the Git repository.  
    ``` bat
    cd hello_world
    rm -rf .git
    ```
    This removes the Git repository from the project while keeping the project files.
#### Let's check out what Cargo has created:
Run the following commands:
``` bat
cd hello_world
tree
```
The output should be something like:
``` bat
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```
You can checkout the Cargo.toml in VSCode to see something like this:

``` toml
[package]
name = "hello_world"
version = "0.1.0"
edition = "2021"

[dependencies]
```
This is called a [manifest](https://doc.rust-lang.org/cargo/appendix/glossary.html#manifest), and it contains all of the metadata that Cargo needs to compile your package. This file is written in the [TOML](https://toml.io/) format

Here’s what’s in `src/main.rs`:
``` rust
fn main() {
    println!("Hello, world!");
}
```
Cargo generated a “hello world” program for you, otherwise known as a [binary crate](https://doc.rust-lang.org/cargo/appendix/glossary.html#crate). Let’s compile it but first change it to be the follwing:

``` rust
fn main() {
    println!("HELLO COMP423");
}
```
### Finally... Compiling and Running

We can no compile like so:

``` bat
cargo build
   Compiling hello_world v0.1.0 (file:///path/to/package/hello_world)
```

The `cargo build` command compiles your Rust project and generates an executable kind of like `gcc [filename.c] -o [output_filename]` that you may remember from COMP 211

After building, the binary (executable) will be located in:
``` bat
target/debug/hello_world
```

You can finally run the executable manually to see the desired output:
``` bat
./target/debug/hello_world
```


You can also use the following command to compile and then run it, all in one step
``` bat
cargo run
```

You should now see:
``` bat
HELLO COMP423
```
Congratulations! You have built a development container in Rust!


