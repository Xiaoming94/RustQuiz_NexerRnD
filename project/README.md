# Projects

Hello, this is the introductory part of the project part of this Rust introduction.
For me personally, I think the best way learn and mastering a programming language is through regular exercises and ofc doing a project in it.

One of the best thing about rust is that it comes pre-equipped with it's own project-manager/build-system: **cargo**.
Cargo can also act like a package manager for the external dependencies of your cargo-project.
It can even install fully built software if it's available as a `crate`.

Every cargo project consist of at least 1 crate.
The crate and it's binaries (library or otherwise) along with their dependencies are specified by the [Cargo.toml file](https://doc.rust-lang.org/cargo/reference/manifest.html)

You can read more about cargo and what else it can do in alot of places, like [the cargo cookbook](https://doc.rust-lang.org/cargo/) for instance.
However, we will talk about some basic stuff here to get you started:

## Basic cargo project structure

The simplest cargo projects are those that is simply a single crate.
Usually, a crate with the name `mycrate` will have the following structure:

```
mycrate
|- src/         # contains the source code
    |- main.rs
|- Cargo.toml   # The project manifest toml file.
```
Ofc, through some magic in the `Cargo.toml` file, this structure can change, but in general, this is the structure you will find.

### Creating a new Cargo project
To create a new crate, just simply execute the following command:

`$ cargo new <cratename>`

For instance, if I want to create a crate named `hardknocklife`, the command will be `$ cargo new hardknocklife`.
This will put a directory with the name `hardknocklife` in your current `pwd` with the basic structure shown earlier.

By default, this command will also set the version-control-system (VCS) for your crate to `git`. If this is undesired, you can append `--vcs <yourvcs>` to the cargo new command.

If you wish to add a crate without a VCS - recommended if you want to have sub crates in your program be managed as the same project - then you can do that through `--vcs none`.

### Adding external dependencies

You can either add the external dependency to your crate by adding it manually through editing `Cargo.toml`.
For instance if I want to add `googletest` as a dependency, I can do so by adding the following to my `Cargo.toml`

```
[package] # Added when the crate was created
name = "mycrate"
version = "0.1.0"
edition = "2021"

[dependencies]
googletest = "0.10.0"
```
Naturally, cargo has built in commands to add the dependency automatically too.
So if you want to add `googletest` to your crate, you can also execute the following command:
`$ cargo add googletest`.

Remember that external dependencies that is not made by you have to exist as a crate in the cargo repository or you have to add it through the VCS.
You can read more about how `cargo add` works in the [documentation](https://doc.rust-lang.org/cargo/commands/cargo-add.html).

Also, on the first build, there will also be a `Cargo.lock` file created in your crate. **You don't want to add it to gitignore** because that file is important for consistent dependency management.
See [ Cargo.toml vs Cargo.lock ](https://doc.rust-lang.org/cargo/guide/cargo-toml-vs-cargo-lock.html) for more info.

### Building and executing your code.

Cargo has various commands defined to both compile and build, and executing the program itself or running the test.
All possible cargo commands can be found by executing `cargo --list`.
For this section, Instead of going through all of them, I will talk about how to build and execute your code in a cargo project.

* Compiling your code.
`$ cargo build`
  In most cases, this will do the trick.
  Important to know though that by default `$ cargo build` creates a developer build of your code.
  What this means is that the code will have no compile-time optimizations done to
  * Make the code compilation faster
  * To make debugging (through something like gdb) easier
  If you want to compile a release build of your code, run `$ cargo build --release`

* Executing your code
`$ cargo run`
    While in most projects, this should be enough, if you for some reason have multiple binaries defined for this project, you have to specify which binary you want to execute through `--bin <binary name>`.
    This command will also compile your code if changes are made. If this is not desired, you can also just execute the binary manually.

* Executing your tests
`$ cargo test`
    This will execute all tests. We will talk more about writing tests in rust later on :)

