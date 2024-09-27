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

## Rust source code structure

There are some good rule of thumbs to understand how to divide your code into multiple files.
1) Every source file is it's own module with the name corresponding to it's name.
    - Also important, they have to be declared.
2) Every directory with a `mod.rs` is also a module with the code written in `mod.rs`.
    - These also have to be declared from the parent.
3) If there exists a directory with a matching name to a `.rs` source file, then any `.rs` sourcefile in that directory has to be declared as modules (with the corresponding name) and are thus submodules.
    - Same applies if the module is created using a `mod.rs` file in the directory name.

The reason for each file having to be declared as modules for it to be visible and compiled is because cargo doesn't try to compile unused files, 2nd of all it also aids in organizing the code.

### A simple explaination of modules and module declarations
As an example of what this means. Consider this structure in `src/` for some binary crate
```
src/
|- main.rs
|- backend.rs
|- backend/
    |- cruddata.rs
|- bridge/
    |- mod.rs
    |- requesthelpers.rs
```

For the code from `backend.rs` to be visible and compiled by cargo, you have to declare it as a module `main.rs`.
The `cruddata.rs` file is by default invisible to cargo. However by declaring `cruddata` as a module in `backend.rs` makes it so that the code inside `cruddata.rs` can be used.

So when it comes to the files in `bridge/` the module `bridge` has to be declared in `main.rs` and thus the same ideas from the previous sentence is applied.
Note that here, the `bridge.rs` file is not needed, since the main modules code is now placed inside the `mod.rs` file.

### Visibility

We can talk forever about visibility, but in general, any module importing another module have access to the functions and types inside that modules that are declared as `pub`.
So if `backend.rs` has a function `pub fn connect_to(target: IpAddress) -> ConStatus` and `fn check_connection_certs(target: IpAddress) -> Result<CertType, &str>`, then only `connect_to` is visible when importing `backend` through `use backend`.

Worth pointing out also is that if an import is declared as `pub use amodule::asubmod` then asubmod is also re-exported by the file including the line. (This also applies when you use `pub mod`).

There are more things you can do to control the visibility of a module and it's functions and types.
You can read about it in [ rust documentation about visibility and privacy ](https://doc.rust-lang.org/reference/visibility-and-privacy.html).

## Writing your test

The rule of thumb in cargo is that any function that is declared with the `#[test]` annotation is a test.
So for instance:

```rust
fn add_two_numbers(val1: u32, val2: u32) -> u32 {
    val1 + val2
}

#[test]
fn test_add() {
    assert_eq!(add_two_numbers(3, 2), 5);
}
```
The function `test_add()` will only be compiled and exectued by cargo through `cargo test`.
In addition to `#[test]`, rust also provides some other annotations for things like if a panic (I.e. calling the function with certain input will trigger a controlled crash, a panic) is expected etc.

### Verification
By default, cargo only provides two built in *macros* for verification: `assert!(expr)` and `assert_eq!(val1, val2)`.
These are defined such that `assert_eq!(val1, val2) ==> assert!(val1 == val2)`.

But while `assert_eq!()` is meant for verifying equivalence, while `assert!()` is for verifying any boolean expectation.
If used outside a function annotated with `#[test]`, `assert!()` will trigger if the assertion fails during runtime.

### Recommended crates for testing
One crate I will definitely recommend is the `googletest` crate.
It provides more advanced verification macros and matchers that can be used to make your test more flexible.

One such example the test above `test_add()` can be rewritten using googletest macros as:

```rust
use googletest::prelude::*; //imports the important components from GoogleTest

#[test]
fn test_add() {
    assert_that!(add_two_numbers(3,2), eq(5)); //Uses the eq matcher
}
```
It also adds googletest style expectations -> I.e. asserts that doesn't block the execution of the rest of the test.

```rust
use googletest::prelude::*;

#[gtest]
fn test_add_with_expects() {
    expect_that!(add_two_numbers(4,4), eq(7)); //Will not block the next line
    assert_that!(add_two_numbers(3,2), eq(5));
}
```

There is alot more useful functionality that googletest provides. You can read more about it in the [googletest rust documentation](https://docs.rs/googletest/latest/googletest/index.html) including how you can write your own matchers!!

There is also `rstest` that provides some more additional stuff such as `test_fixtures`.

### Organizing your tests
It is adviced that all the test should be contained within a module that is annotated with `#[cfg(test)]`.

So for example I have this code in the module `mod calculator`.

```rust

fn add_two_numbers(val1: u32, val2: u32) -> u32 {
    val1 + val2
}

fn divide(numerator: u32, denominator: u32) -> Result<u32, &str> {
    if denominator == 0 {
        return Err("Divide by Zero");
    }

    numerator / denominator
}

#[cfg(test)]
mod calculatortest {
    use super::*;

    #[test]
    fn test_add() {
        let (input1, input2) = (1,2);
        assert_eq!(add_two_numbers(input1, input2), input1 + input2);
    }

    #[test]
    fn test_divide() {
        let (num, denom) = (2,1);
        assert_eq!(divide(num, denom).unwrap(), 2);
    }
}
```

The submodule `calculatortest` will only be compiled and the tests executed if you run `$ cargo test`.
There are some in discussion convention about how to organize your tests.
But there seem to be a concensus that unit-tests should be contained within a submodule annotated with `#[cfg(test)]` to the module that is being tested.
*Technically* same goes for integration test.

Tips: If you want your tests to be placed inside a separate sourcefile, then this can be achieved through the use of `#[cfg(test)]` and declaring the module.
This is because test modules also play by the same rule of sourcefile to module relation discussed earlier.

Footnote: General difference between integration and unit-tests only boils down to two points:
* If a test is written solely to test the current module where external dependencies are *mocked*, then it's a unit-test
* If a test uses the actual real components from different modules, then it's an integration test.
(btw, these are the universal definitions of these terms)

With regards to End-to-end tests - that really depends on how your program is supposed to be interacted with.

### Mocking and Expect calls.
Due to the fact that rust lacks inheritance, mocking can initially feel a bit unintuitive.
However, something that is taught in object-oriented programming is that usually, the code should interact with an interface, not a concrete type.

The equivalence to interfaces in rust is, ofc, traits.
As thus, you can always implement your own mock structs that implements the trait the functions in your module are expected to interact with.
There are crates also that provides mockability. But the basics of mocking something in a test-environment in rust is like described here.

When it comes to expect_calls, one of the crates that provides mocking - `mockall` also provides expect calls.
A general advice here is that you shouldn't overly rely on expect_calls to verify your code -> i.e. expect a certain order of function calls.
Tests are for verifying and protecting the expected effect of your code, not your implementation.
However, if the expected effect is that a certain function is called (maybe with a certain set of parameters).
One such case is for instance if your program is for operating a drill, then at the end of your test, you should expect a call to the drill doing the drilling happening.
