> _The content of this page and of the following ones is based on [The Rust Book](https://doc.rust-lang.org/book/)_

## 1. Introduction to Rust

Rust is a low-level compiled programming language (similar to C/C++/C#).

Install Rust on Ubuntu:

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

And check the version with:

```bash
rustc --version
```

Other useful commands:

```bash
# update Rust
rustup update
# Uninstall Rust
rustup uninstall self
# View local docs
rustup doc
```

## 2. Hello World!

Rust files have the `.rs` extension and files are by convention named using `snake_case` (like `hello_world.rs`).

Let's create a Hello World script: 

```rust
fn main(){
	println!("Hello world!");
}
```

As you can see, there is the function, defined by the `fn` key, named `main` and with no parameters passed (void parentheses). The `main` function is special, as it is the first one to be run in the script. 

The body of the function makes us see four things:
- Rust uses indentation with 4 spaces and not a tab
- The `println!` calls a Rust macro: if it was a function, it would be called without "!"
- "Hello World!" is a string and is printed on screen with  a newline 
- The line is ended by a `;`

You can now compile the script:

```bash
rustc hello_world.rs
```

And run the binary executable which is output from that:

```bash
./hello_world # -> outputs "Hello world!" 
```

## 3. Cargo

Cargo does a lot of things in Rust: manages dependencies and projects, checks and builds code. Cargo is already installed if you have installed `rustup` as we did before.

```bash
cargo --version
```

We can create a new project with:

```bash
cargo new hello_cargo --vcs=git
# access the folder
cd hello_cargo/
```

> *`--vcs` is short for **V**ersion **C**ontrol **S**ystem, and in this case is `git`: it initializes the folder with a `.git/` subdirectory and a `.gitignore` file. To avoid if the cargo project is created within an already git-initialized folder.*

Within the repository, we have a TOML file named `Cargo.toml` with this minimal structure:

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

Let's now open the `src/main.rs` script (executed in the project) and we can see that cargo weote the Hello World script that we defined before:

```rust
fn main(){
	println!("Hello world!");
}
```

Now let's first of all build our project:

```bash
cargo build
```

The build creates a `./target/debug/hello_cargo` file for debugging, that you can execute

```bash
./target/debug/hello_cargo
```

If you run `cargo build --release`, you build to release the package and you will get out a `./target/release/hello_cargo` binary.

You can also run the project:

```bash
cargo run
```

We do not specify what cargo has to run: if scripts have not changed, cargo figures out what to run and does not rebuild anything.

You can check if you code compiles without building an executable with:

```bash
cargo check
```

