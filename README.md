````markdown
# cv-rust

A simple starter Rust project bootstrapped with Cargo. This README outlines how to set up, build, run, and version‐control the project from scratch, including pushing to GitHub.

---

## Table of Contents

1. [Overview](#overview)  
2. [Prerequisites](#prerequisites)  
3. [Project Initialization](#project-initialization)  
   - [1. Install Rust & Cargo](#1-install-rust--cargo)  
   - [2. Create a New Cargo Project](#2-create-a-new-cargo-project)  
   - [3. Directory Structure](#3-directory-structure)  
4. [Building & Running](#building--running)  
   - [Compile & Run in Dev Mode](#compile--run-in-dev-mode)  
   - [Compile in Release Mode](#compile-in-release-mode)  
5. [Adding Dependencies](#adding-dependencies)  
6. [Version Control with Git](#version-control-with-git)  
   - [1. Initialize or Verify a Local Git Repo](#1-initialize-or-verify-a-local-git-repo)  
   - [2. Create a New GitHub Repository](#2-create-a-new-github-repository)  
   - [3. Link Local → Remote & Push](#3-link-local--remote--push)  
7. [Project Layout](#project-layout)  
8. [Common Cargo Commands](#common-cargo-commands)  
9. [Contributing](#contributing)  
10. [License](#license)  

---

## Overview

This repository serves as a boilerplate for any new Rust project. It is initialized with Cargo and demonstrates:

- How to create a Rust binary using `cargo new`
- Where to find the generated files and directories  
- Basic commands to build, run, and test
- How to add external crates (dependencies)
- How to initialize, link, and push to GitHub

Feel free to fork and adapt this for your own Rust applications or libraries.

---

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Rust & Cargo** (via [rustup](https://rustup.rs/))  
- **Git** (for version control)  
- (Optional) A GitHub account to host your remote repository  

> **Tip:** If you don’t yet have Rust/Cargo installed, follow the instructions below. If you already have them, skip to the “Create a New Cargo Project” section.

---

## Project Initialization

### 1. Install Rust & Cargo

Rust’s official installer is called **rustup**, which installs both the Rust compiler (`rustc`) and Cargo (the package manager/build tool).

1. Open your terminal and run:
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
````

2. Follow the on-screen prompts. By default, it installs the **stable** toolchain.
3. Once installation finishes, you may need to update your `PATH`. Run:

   ```bash
   source $HOME/.cargo/env
   ```
4. Verify the installation:

   ```bash
   rustc --version
   cargo --version
   ```

   You should see something like:

   ```
   rustc 1.xx.x (yyyy-mm-dd)
   cargo 1.xx.x (yyyy-mm-dd)
   ```

---

### 2. Create a New Cargo Project

1. Navigate to the directory where you want to keep all your Rust projects. For example:

   ```bash
   cd ~/projects
   ```

2. Run the following command to create a new binary (executable) named `my_rust_app`:

   ```bash
   cargo new my_rust_app
   ```

   * You can replace `my_rust_app` with any desired project name.
   * By default, this initializes a Git repository (if Git is installed).

3. Change into the newly created directory:

   ```bash
   cd my_rust_app
   ```

At this point, Cargo has generated:

```
my_rust_app/
├── Cargo.toml
└── src
    └── main.rs
```

---

### 3. Directory Structure

* **`Cargo.toml`**

  * The project manifest. Holds metadata (name, version, authors, edition) and dependencies.
  * Example content:

    ```toml
    [package]
    name = "my_rust_app"
    version = "0.1.0"
    edition = "2021"

    [dependencies]
    ```
* **`src/main.rs`**

  * The entry point for a binary crate. By default, it contains:

    ```rust
    fn main() {
        println!("Hello, world!");
    }
    ```

You can create additional modules, a `lib.rs`, or integration tests as needed.

---

## Building & Running

### Compile & Run in Dev Mode

To compile and run the project with debug symbols (unoptimized):

```bash
cargo run
```

* The first invocation will download and compile the Rust standard library (if not already in your local toolchain).
* You should see output similar to:

  ```
  Compiling my_rust_app v0.1.0 (~/projects/my_rust_app)
   Finished dev [unoptimized + debuginfo] target(s) in 1.23s
    Running `target/debug/my_rust_app`
  Hello, world!
  ```

If you only want to compile (without running), use:

```bash
cargo build
```

* The resulting binary will be placed in `target/debug/my_rust_app`.

---

### Compile in Release Mode

For an optimized, production-ready build:

```bash
cargo build --release
```

* The optimized executable will be found at `target/release/my_rust_app`.

---

## Adding Dependencies

Whenever you need third-party crates (libraries), add them under the `[dependencies]` section in `Cargo.toml`. For example, to include `serde` and `serde_json`:

```toml
[dependencies]
serde = "1.0"
serde_json = "1.0"
```

After saving `Cargo.toml`, run:

```bash
cargo build
```

Cargo will fetch, compile, and link those crates automatically.

---

## Version Control with Git

You can (and should) put this project under Git version control, then push it to a remote repository on GitHub (or any other Git host).

### 1. Initialize or Verify a Local Git Repo

Most of the time, `cargo new` auto-initializes Git if Git is installed. Check with:

```bash
cd ~/projects/my_rust_app
git status
```

* If you see:

  ```
  On branch main
  nothing to commit, working tree clean
  ```

  Git is already initialized.

* If instead you see:

  ```
  fatal: not a git repository (or any of the parent directories): .git
  ```

  then initialize and make the initial commit:

  ```bash
  git init
  git add .
  git commit -m "Initial commit: created Rust project with Cargo"
  ```

> **Tip:** Create a `.gitignore` so build artifacts (e.g., `target/`) are not committed.
> Example `.gitignore`:
>
> ```
> /target/
> **/*.rs.bk
> .DS_Store
> ```
>
> Then:
>
> ```bash
> git add .gitignore
> git commit -m "Add .gitignore"
> ```

---

### 2. Create a New GitHub Repository

1. Log in to [GitHub](https://github.com/).
2. Click the **+** icon in the upper-right → **New repository**.
3. Set:

   * **Repository name**: `my_rust_app` (or your chosen name).
   * **Description**: e.g., “Starter Rust project generated via Cargo.”
   * **Public** or **Private**, as desired.
   * Leave “Initialize this repository with a README” **unchecked** (so there’s no conflict with your local commits).
4. Click **Create repository**.

GitHub will then display instructions like:

```bash
git remote add origin https://github.com/<YOUR_USERNAME>/my_rust_app.git
git branch -M main
git push -u origin main
```

---

### 3. Link Local → Remote & Push

Copy and run the lines provided by GitHub inside your local project directory:

```bash
git remote add origin https://github.com/<YOUR_USERNAME>/my_rust_app.git
git branch -M main
git push -u origin main
```

* **`git remote add origin …`** sets up GitHub as your remote named `origin`.
* **`git branch -M main`** ensures your branch is called `main`.
* **`git push -u origin main`** pushes your commits and sets `origin/main` as the upstream.

After a successful push, navigate to:

```
https://github.com/<YOUR_USERNAME>/my_rust_app
```

to confirm all files (including `Cargo.toml` and `src/`) are visible.

---

## Project Layout

```text
my_rust_app/
├── .gitignore          # (optional) Exclude /target and other files
├── Cargo.toml          # Project metadata & dependencies
└── src
    ├── main.rs         # Binary entry point
    └── lib.rs          # (optional) Library code if you choose to split logic
```

As your application grows, you might add:

```
my_rust_app/
├── Cargo.toml
├── src/
│   ├── main.rs
│   ├── lib.rs
│   ├── module1.rs
│   └── bin/
│       └── another_binary.rs
└── tests/
    └── integration_test.rs
```

* **`main.rs`**: Contains the `fn main()` function for the binary.
* **`lib.rs`**: Optional library crate you can call from `main.rs` or other binaries.
* **`module1.rs`**: A separate module you can import.
* **`tests/`**: Integration tests run with `cargo test`.

---

## Common Cargo Commands

* **Compile & Run**

  ```bash
  cargo run
  ```
* **Compile Only**

  ```bash
  cargo build
  ```
* **Compile Optimized (Release)**

  ```bash
  cargo build --release
  ```
* **Check (Type-check without producing binary)**

  ```bash
  cargo check
  ```
* **Run Tests**

  ```bash
  cargo test
  ```
* **Format Code**

  ```bash
  cargo fmt
  ```
* **Lint with Clippy**

  ```bash
  cargo clippy
  ```

  *(Install with `rustup component add clippy` if not already present.)*
* **Generate Documentation**

  ```bash
  cargo doc --open
  ```
* **Clean Build Artifacts**

  ```bash
  cargo clean
  ```

---

## Contributing

1. **Fork** this repository on GitHub.
2. **Create a new branch** for your feature or bug fix:

   ```bash
   git checkout -b feature/my-feature
   ```
3. **Make your changes**, then stage and commit:

   ```bash
   git add .
   git commit -m "Add awesome feature"
   ```
4. **Push** your branch:

   ```bash
   git push -u origin feature/my-feature
   ```
5. On GitHub, open a **Pull Request** to `main`.
6. After review and approval, your changes will be merged.

---

## License

This project is released under the [MIT License](LICENSE). Feel free to use, modify, and distribute as you see fit.

---

*Happy coding with Rust & Cargo!*

```
```
