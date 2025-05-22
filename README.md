RUST QUIZ Nexer Engineering
================

This repo contains a set of Quiz, problems and some other material useful for learning Rust. These are tailored specifically for C++ developers at Nexer Engineering SW.

## How to do work with the quizzes.

There are 3 categories of quizzes/problems prepared in this repo organized in the subdirectories in this repo. 
* `./basics` - These are meant to teach/practice the basics of the language
* `./`


## Quick words from me regarding rust

Rust is a programming language created, developed and maintained mainly by Mozilla Foundation. Initially, it was made to create the new web-engine for Firefox. From my experience in University is that people call this things like

* Love child of C++ and Haskell
* Haskell for C++ enthusiasts
* C++ if it was created today
* C++ with Haskell's type system.

While these description all touches the essence of rust to a certain degree, but, in my opinion, their helpfulness in learning the language is limited - especially if you are only familiar with C++. In fact, I think learning Rust is easiest if you go in with an open mind. "Empty your cup" so to say.

With that said, there might be multiple elements in rust that is recognizable to the programmer learning it. Rust is a multi-paradigm programming language. While the core of the programming language is still *imperative*, it has comparatively more declarative elements compared to more conventional imperative languages like C/C++. It also has some recognizable elements from object oriented languages.

## Dispelling some myth around Rust

### You will not have memory leaks in rust
This is false, system-level programming languages (like C++ and Rust) that supports heap-memory-allocation that also doesn't provide garbage-collection all run into risks of leaking memory. Rust is not an exception. In fact, there are usecases where you want your code to be able to relinquish resources on to certain parts of the memory - one such use case is FFI.

### You will not have code undefined behaviours in Rust.
Rust out of the box, don't allow you to write code that triggers undefined behaviours. However, the need to support such code is why the rust provides the `unsafe` keyword. With that said, all this means is that whenever you read a block of code written inside `unsafe {}`  you will instantly know that there are certain action in the code that can trigger undefined behaviour or other operations that can be considered unsafe.
