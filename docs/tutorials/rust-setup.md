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

---

## Welcome  

This tutorial will provide step-by-step instructions for creating a Dev Container in Rust.

!!! info
    This tutorial is highly inspired by a [previous tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/) my professor [Kris Jordan](https://www.linkedin.com/in/krisjordan/) had already made so you might see a lot of similarities and I would highly recommend you check his out!

---

## Let's start with the prerequisites
Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at [GitHub.](https://github.com/)
1. Git installed: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.
1. Visual Studio Code (VS Code): Download and install it from [here.](https://code.visualstudio.com/)
1. Docker installed: Required to run the dev container. [Get Docker here.](https://www.docker.com/products/docker-desktop)

!!! note
    For this tutorial, you do not need to install anything other than VSCode, Docker and Git. You should not install Rust. That is the role of the dev container!

---

## Part 1: Project setup (Setting up your directory, Git, and Github)

### Step 1: Creating a directory and a local Git Repository
- Open you terminal or command prompt.
- Create a new directory:
``` bat
mkdir rust-dev-cont
cd rust-dev-cont
```
- Initialize a new repository
``` bat
git init
```
- Create a README file and add the following
``` bat
echo "# Building a Dev Container in Rust" > README.md
git add README.md
git commit -m "Initial commit with README"
```
!!! note
    The command `echo` sends the string in quotation marks to the specified place.
    Usually without any place to go, it just sends it back to stdout which is your terminal by default.
    However, if you have taken 211 before, you know that the `>` operator writes whatever is on the left of it (which could be the output of a program) to the specified place on the right. If the file does not exist already, it creates it.

---

### Step 2: Creating a remote repository
1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
1. Fill in the details as follows:
    - **Repository Name:** rust-dev-cont
    - **Description:** "Personal project for starting a Dev Container in Rust"
    - **Visibility:** Public
1. Do not initialize the repository with a README, .gitignore, or license.
1. Click **Create Repository.**

---

### Step 3: Link you Local Repository to Github
1. Add the Github repository as a remote: 
``` bat
git remote add origin https://github.com/<your-username>/rust-dev-cont.git
```
Replace `<your-username>` with your GitHub username.
1. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` use the name `master` for the primary branch. However, these days `main` is the standard primary branch name.

1. Push your local commits to the GitHub repository:
``` bat
git push --set-upstream origin main
```
!!! note
    `git push --set-upstream origin main`: This command pushes the `main` branch to the remote repository `origin`. The `--set-upstream` flag sets up the `main` branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing `git push origin` when working on your local `main` branch. This long flag has a corresponding `-u` short flag.
You can now refresh your browser to see that the same commit you made locally has now been pushed to the remote Github Repo. You can also use `git log` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub.

---

## Part 2: Setting up the Development Environment

Before you begin developing in Rust, you need to set up your development environment! 
### What is a Development (Dev) Container?

In essence, a **dev container** is a preconfigured environment defined by a set of configuration files usually using Docker to create isolated setups for development. You can think of it a mini computer running inside your computer including everything you need to work on a project. Your dev container will include the right programming language, tools, libraries and dependencies. This is why you don't need to install Rust for the purpose of this tutorial. The dev container ensures that your development environment is consistent and works across different machines.

#### Why is this valuable?

In the technology industry, teams often work on complex projects that require a specific set of tools and dependencies to function correctly. Without a dev container, each developer must manually set up their environment. The can lead to errors, wasted time, and inconsistencies. With a dev container:

- Everyone works in an identical environment, reducing bugs caused by "it works on my machine" issues.
- Onboarding new team members becomes faster and easier, as they can start coding with just a few steps.
- Dependencies and tools remain isolated, avoiding conflicts with other projects or the local system.

---

### How are Software Project Dependencies Managed?

To effectively manage software dependencies, it's important to use a reliable package manager. Dependencies are external libraries or tools that your project relies on, and managing them ensures your project uses the correct versions, avoiding compatibility issues.

#### **Dependency Management in Rust**

In Rust, dependencies are managed using **Cargo**, the package manager and build system. Cargo automates tasks like:  

1. **Declaring Dependencies**: Dependencies are specified in the `Cargo.toml` file.  
2. **Installing Dependencies**: Cargo fetches and installs the required libraries from [crates.io](https://crates.io/).  
3. **Ensuring Consistency**: The `Cargo.lock` file ensures that all team members use the exact same dependency versions.

For example, in the `Cargo.toml` file:
```toml
[dependencies]
serde = "1.0"
```
We will see an example of this later on!

---

### Step 1: Add Development Container Configuration

1. In VS Code, open the `rust-dev-cont` directory. You can do this via: File > Open Folder.
1. Install the Dev Containers extension for VS Code.
1. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:  

`.devcontainer/devcontainer.json`

### Want a Shortcut to Open Projects in VS Code?

For more convenience, you can set up the `code` command in your terminal, allowing you to open projects directly from the command line.  
[Check out the tutorial here!](code-command.md)

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- `name`: A descriptive name for your dev container.
- `image`: The Docker image to use, in this case, the latest version of a Rust environment. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!
- `customizations`: Adds useful configurations to VS Code, like installing the Rust Analyzer extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar (i.e `rust-lang.rust-analyzer`). Adding extensions here ensures other developers on your project have them installed in their dev containers automatically. Remember, we are trying to get rid of manually installing a bunch of software.
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

---

### Step 2. Reopen the Project in a VSCode Dev Container
Reopen the project in the container by pressing Ctrl+Shift+P (or Cmd+Shift+P on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This will take a few minutes for the first time to download and install the image and everything.

Once your dev container setup completes, open a new terminal pane within VSCode, and try running `rustc --version` to see your dev container is running a recent version of Rust without you having to even manually download or install anything! (As of January 2025, the latest stable Rust version is 1.83.0.) The `latest` keyword in the `image` specification should take care of that!

---

## Part 3: Developing in Rust

### Creating a New Package
To start a new package with Cargo, use cargo new:
``` bat
cargo new hello_world --vcs none
```
The `--vcs none` flag tells cargo to not create a git repository for you which is the default behavior.  
!!! warning
    If you forgot the `--vcs none` flag, it's no problem. You can run the following commands to delete the Git repository.  
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

2 directories, 2 files
```
You can checkout the Cargo.toml in VSCode to see something like this (Hint: this is what we talked about up there ^^^):

``` toml
[package]
name = "hello_world"
version = "0.1.0"
edition = "2021"

[dependencies]
```
This is called a [manifest](https://doc.rust-lang.org/cargo/appendix/glossary.html#manifest), and it contains all of the metadata that Cargo needs to compile your package. This file is written in the [TOML](https://toml.io/) format.

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

---

### Finally... Compiling and Running

We can now compile like so:

``` bat
cargo build
   Compiling hello_world v0.1.0 (file:///path/to/package/hello_world)
```

The `cargo build` command compiles your Rust project and generates an executable kind of like `gcc [filename.c] -o [output_filename]` that you may remember from COMP 211

#### How It Works

**Compilation**:
`cargo build` compiles your project and places the resulting binary or library in the `target/debug` directory by default.

**Default Build Mode**:
By default, `cargo build` compiles in debug mode. Debug builds prioritize faster compilation and include debug symbols, making them suitable for development and testing.


After building, the binary (executable) will be located in:
``` bat
target/debug/hello_world
```

You can finally run the executable manually to see the desired output:
``` bat
./target/debug/hello_world
```


You can also use the following command to compile and then run it, all in one step:
``` bat
cargo run
```

You should now see:
``` bat
HELLO COMP423
```
!!! success
    Congratulations! You have built a development container in Rust!

---

## Part 4: Pushing to Github
You can now run the following commands in order to push your amazing new Dev Container project to Github for the world to see

``` bash
git add . # this is for staging your changes
git commit -m "Successfully printed HELLO COMP423 with my own Rust Dev Container"
git push
```

Congrats you have now finished the tutorial!

---

## References

1. [Kris Jordan’s COMP 423 Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/)  
   Inspiration and structure for this tutorial.

1. [Rust Documentation: Creating a New Project](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html)  
   Official guide to creating a new Rust project with Cargo.

2. [Rust: Learn Rust](https://www.rust-lang.org/learn)  
   Rust's official learning resource.

3. [MkDocs Material Documentation](https://squidfunk.github.io/mkdocs-material/)  
   Comprehensive guide to using MkDocs Material.

4. [Markdown Guide: Basic Syntax](https://www.markdownguide.org/basic-syntax/)  
   A beginner-friendly guide to Markdown syntax.





