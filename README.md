# Practical Rust Cheat Sheet

## Setup

### Articles
https://fasterthanli.me/articles/my-ideal-rust-workflow#code-editor
https://fasterthanli.me/articles/my-ideal-rust-workflow#building-checking-testing-linting

### Rust Analyzer
Use in VSCode - [Link](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)

#### Inline Hints
Rust analyzer can show type hints inline, I generally find it super helpful. Sometimes it can be a little annoying and I'll tweak them but all of the hints are optional in vscode settings

### Use Clippy
```
cargo install clippy
```

## Basics

### Modules and Crates
https://fasterthanli.me/articles/rust-modules-vs-files
Best explainer for how to organize code into modules and crates + how to use them in other parts of the codebase

Happy Path
1) Every folder is a `module` and contains a `mod.rs`
2) Every other first in the folder requiers a `pub mod <file>` in `mod.rs`
3) You can also add `pub use <file>::*` to `mod.rs` to make everything availalbe in the module namespaces

```
/mymodule
    mod.rs
    a.rs
    b.rs
```

mod.rs
```
pub mod a;
pub mod b;

pub use a::*
```

In another module
```
pub use mymodule;

fn some_func() {
    mymodule::b::some_func();
    mymodule::another_func(); // another_func() is in `a.rs` but was exposed in `mod.rs` to the module namespace
}
```

## Must Use Crates
The Rust std crates are extremely barebones. There are a ton of crates that are pretty necessary for day-to-day development. Most of the ones listed below are accepted as the rust way to do things and devs make sure to support them in other crates.

### Itertools
[Docs](https://docs.rs/itertools/latest/itertools/)
Contains a ton of helpful iterator methods for Vecs, Hashmaps, etc

### Chrono
[Docs](https://docs.rs/chrono/latest/chrono/)
Everything related to dates and times

## Helpful Tips and Methods

[Rust Cheat Sheet](https://upsuper.github.io/rust-cheatsheet/?dark,large)

### Option<Result> to Result<Option>
Use `transpose()`
```
let string_x: Option<String> = "1".to_string()
let int_x: i16 = string_x.map(|x| x.parse()).transpose()?;
```

## Debug Stuff

### macros
`println!()` - prints whatever you pass
`dbg!()` - prints variable name and value (super useful!)

