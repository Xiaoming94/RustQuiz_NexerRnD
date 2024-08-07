# Basic Questions

These are the basic questions. The goal is to teach you the basics in a practical way, you can also use these to test your knowledge if you taken some of the other courses like the ones I recommended in [README](../README.md).

I've decided to divide these questions into parts.

## Part 1
This part is meant for whoever is doing this quiz to familiarize with the Rust syntax. 
### Question 1
Consider this rust function:
```rust
fn add_two_numbers(a: u32, b: u32) -> u32 {
    a + b
}
```
This function is roughly be translate to this function if written in C++ 
```C++
//necessary includes
std::uint32_t add_two_numbers(std::uin32_t a, std::uint32_t b) 
{
    return a + b;
}
```

* From this snippet alone, what do you think is the `fn` part in the rust code?
* What is to the right of the `->` charcters?

### Question 2
To spice things up a bit, lets add some prints. Lets add some additional operations in the `add_two_numbers` function in rust.

```rust
fn add_two_numbers(a: u32, b: u32) -> u32 {
    let ans = a + b;
    println!("adding numbers: {a} + {b} = {ans}");
    ans
}
```

* Why is there an exclaimation mark in the `println!()` function?
* What do you think the `let` keyword means?
* [*This one is harder*] The last part of this function can also be written as `return ans;`
  * What does the semicolon `;` do?
  * Why do you need it if you use `return`?
  * What would happen if you used `;` without `return`?
  * [*Discussion/thinking*] Why does rust have 2 different ways of returning something from a function? When should you use one or the other (Hint: Look at the next question)?

### Question 3

Consider this rust function
```rust
fn print_even_numbers(numbers_vec: Vec<i32>)
{
    fn is_even(number: i32) -> bool { number % 2 == 0 }
    for number in numbers_vec {
        if is_even(number) {
            print!("{number} ");
        }
    }
}
```
* What is this function doing?
* What is the return type of this function?
* What do you think is going on on the 2nd line of this function?

This code of block can also be re-written as
```rust
fn print_even_numbers(numbers_vec: Vec<i32>)
{
    let is_even = |number| number % 2 == 0;
    for number in numbers_vec {
        if is_even(number) {
            print!("{number} ");
        }
    }
}
```
* What do you think is happened to `is_even`?
* [*Discussions/thinking*] What is the benefit of this syntax compared to the previous one?

### Question 4

Let's use the `print_even_numbers` function from before and add some more context around it.
```rust
fn print_even_numbers(numbers_vec: Vec<i32>) {
    let is_even = |number| number % 2 == 0;
    for number in numbers_vec {
        if is_even(number) {
            print!("{number} ");
        }
    }
}

fn main() {
    let my_numbers = vec![1,4,6,2,5,6,8];
    let more_numbers = Vec::from([3,2,4,1,2,5,6]);
    print_even_numbers(my_numbers);
    print_even_numbers(more_numbers);
}
```
* What will this program print to the command line?
* What do you think on Line1 and Line2 of the `main()`?

## Part 2
