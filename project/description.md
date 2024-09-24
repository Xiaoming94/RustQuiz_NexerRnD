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

