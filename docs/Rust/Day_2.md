> _The content of this page and of the following ones is based on [The Rust Book](https://doc.rust-lang.org/book/)_

## 1. Programming a guessing game

Let's  first of all create a `guessing_game` project:

```bash
cargo new guessing_game
cd guessing_game
```

Let's now modify `src/main.rs` in such a way that it takes the user's guess:

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

Let's break down this code:

- Rust has a *prelude*, i.e. a set of pre-defined items that every program can access. If the library we need to access is not standard, we can import it. There are a set of built-in libraries, such as `random` in python: `std::io` is the library that makes you read/write from/to standard input
- As always, we declare the `main` function (followed by `()` and `{}`) as the entrypoint of our script
- We print some instructions
- We create a variable with `let`. `let` is a declarative statement that binds a value to a variabele:

```rust
let apples = 5; // this is an immutable function
```

- The `apples` variable is immutable, meaning that once we give the variable a value, the value will not change. The `guess` variable we defined is mutable (keyword `mut`): this variable is bound to a particular value, which is a type (`String`) with its *associated function* (indicated by `::`): the `new` function creates  a new empty string. 
- We receive the user input with the `read_line` method associated to `io::stdin()`. We pass the string `&mut guess` as input. The `&` sign means that this is a reference: references make pieces of code accessible to other pieces of code. References are safely and easily managed in Rust: they are immutable by default, so we need to pass `&mut` and not only `&guess` if we wanna maintain the mutability. 
- `io::stdin` returns a `Result`, which is of a particular type: *enumerations* or *enums*. These type of data can be in one or multiple states: each of the possible states is a *variant*. In the case of `io::stdin`, the result tells us the status of the operation. If the operation was successful, we have "Ok" and the function returns the number of bytes passed by the user, if not we have "Err". The error tells us also what is broken in our code. We handle potential errors within the function by using the `expect` method. If the `expect` method catches an error, it wiill return the error code and explanation, if not, it will just return the number of bytes passed by the user. This is possible because all `Result` instances have the `except` method.

> ***Note**: this is different from error handling. With `expect`, the code crashes if there is an error, whereas with error handling this is not the case.*

