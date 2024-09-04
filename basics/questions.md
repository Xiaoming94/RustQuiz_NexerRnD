# Basic Questions

These are the basic questions. The goal is to teach you the basics in a practical way, you can also use these to test your knowledge if you taken some of the other courses like the ones I recommended in [README](../README.md).

I've decided to divide these questions into parts.

A tip from my end when you are working your way through the quiz, if there are code you want to try and execute yourself,
Rust is supported on [godbolt](https://godbolt.org/).
You can also try your code in the [rust playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)

## Part 1
This part is meant for whoever is doing this quiz to familiarize with the Rust syntax. 
#### Question 1
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

#### Question 2
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

#### Question 3

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

#### Question 4

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
* What do you think is happening on Line1 and Line2 of the `main()`?

#### Question 5
This question uses a custom defined struct.
```rust
#[derive(Debug)]
struct MyStruct {
    name: String,
    age: u32,
}

impl MyStruct {
    fn new(name: &str, age: u32) -> Self {
        MyStruct {
            name: String::from(name),
            age: age,
        }
    } 
}

fn function_with_struct1(arg: MyStruct) {
    println!("{:?}", arg);
}

fn function_with_struct2(arg: MyStruct) {
    println!("{:?}", arg);
}

fn main() {
    let struct_instance = MyStruct::new("Alex", 20);
    function_with_struct1(struct_instance);
    function_with_struct2(struct_instance);
}
```
There will be a separate sections about structs later. For now consider the C++ code below as the equivalent:
```C++
struct MyStruct {
    std::string name;
    std::uint32_t age;

    MyStruct(std::string name, std::uint32_t age):
        m_name(name),
        m_age(age)
    {}
}

void functionWithStruct1(const MyStruct arg) {
    std::cout << "{" << arg.m_name << ", " << arg.m_age <<"}" << std::endl;
}

void functionWithStruct2(const MyStruct arg) {
    std::cout << "{" << arg.m_name << ", " << arg.m_age <<"}" << std::endl;
}

int main() {
    const auto structInstance{MyStruct("Alex", 20)};

    functionWithStruct1(structInstance);
    functionWithStruct2(structInstance);
}

```
* If you try and compile the rust code, you will notice that the code fails to compile, why?
* Do you have any suggestions how to fix this? (Don't spend too much time here since we will explore this in later parts)

#### Question 6
Consider this following, slightly larger rust snippet:

```rust
fn tuple_function(arg: u32) -> (u32, u32) {
    (arg+1, arg+2)
}

fn divide_if_even(arg: u32) -> Option<u32> {
    match arg % 2 {
        0 => Some(arg/2),
        _ => None,
    }
}

fn main() {
    let a: u32 = 2;
    let a = a + 4;
    
    //Print 1
    println!("{a}");

    let (var1, var2) = tuple_function(a);
    println!("Var1 : {var1}, Var2 : {var2}");

    if let Some(half_a) = divide_if_even(a) {
        println!("Half of {a} is: {half_a}");
    }
}

```
* What's the console output of this program?
* What do you think is happening in the first and second `let a` statement?
    * Btw, you can reproduce the effect of these lines without using let, how? (hint: `let mut a = ...;`)
* What do you think is happening in the `let ...` statement before the 2nd `println!()`?
* How do you think the `if let ...` statement is evaluated?

The code before the last print is related to the `Option<>` type, which is an `enum`.
Enums in rust will be explored later.
For now, just understand that enums in rust are very different from traditional enums found in C/C++ and Java.

#### Question 7
```rust
mod util {
    fn calc_sum(a: u32, b: u32) -> u32 {
        a + b
    }
}

fn main() {
    // Do something?
}
```
* What do you think the `mod` keyword's doing?
* How should you call the function `calc_sum()` from the `main()` function?

## Part2

This part of the quiz is about rusts' type system.
Colloquially, rust is described as a **statically typed** language with a **strong type-system** - within the programming language community.
However, what does this mean for a simple programmer?
There is alot of material online that describes these terms, including alot alot of material of how a type system can or should be designed.
This is called type-theory.
In short however, a overly simplified way of looking at these terms is that they can be boiled down to the following:
* **Statically typed**: The type of a variable/object is determined before the code is executed (For instance, during compilation or when loading the code into the interpreter).
* **Dynamically typed**: The type of a variable/object is determined runtime.
* **Strong type-system**: The type system is pretty strict - usually with no (pre-determined) implicit type-casting.
* **Weak type-system**: There are alot more implicit type-casting and other ways of bypassing the type-checking.

Note:
    The terms *strong* and *weak* type-systems are actually not universally defined, and the difference is constantly debated.
    This is way generally in type-theory, the term **type-safety** is preferred.
    Thus, another way you can define these two weaker terminologies is:

* **Strong type-system**: The type system and it's type-safety is strictly enforced with no way of bypassing it.
* **Weak type-system**: There are known ways to bypass the type-system and thus the type-safety that comes with it.

Fruit for thought: Rust's strict type-system is one of the reasons why rust is considered to be memory-safe too, Why?

## Part 2.1 the basics
Basics of rust type system

#### Question 1)

Consider the following code:
```rust
fn string_function1(arg: &str) {
    println!("{arg}");
}

fn string_function2(arg: String) {
    println!("{arg}");
}

fn main() {
    string_function1("Hello my string");
    string_function2("Hello my string");
}

```

Which equivalently in C++ can be written as.
```C++
void stringFunction1(const char* arg) {
    std::cout << arg << std::endl;
}

void stringFunction2(const std::string& arg) {
    std::cout << arg << std::endl;
}

int main() {
    stringFunction1("Hello my string");
    stringFunction2("Hello my string");
}

```
* The rust version of this simple program will actually fail to compile, why?
* Any suggestion on how to fix it (hint: there are at least 2 ways)?

#### Question 2)
Consider the code snippet below
```rust
fn unsigned_int_function(arg: u32) -> u32 {
    arg + 2
}

fn signed_int_function(arg: i32) -> i32 {
    arg + 2
}

fn main() {
    let my_var = 42;
    let results1 = unsigned_int_function(my_var);
    let results2 = signed_int_function(my_var);
    //...
}
```
* Once again, this code will not compile, why?
* Any suggestions on how to fix it?

#### Question 3)
Consider this small snippet of code
```rust
fn identity_function<T>(obj: T) -> T{
    obj
}

fn main() {
    println!("{:?}", identity_function(1337));
}
```
* What do you think the return type of the function `identity_function()` is?
* What do you call the types that are declared like `T` inside the `< >` brackets? (Hint: It's actually NOT a tempalte).

### Part2.2 Custom data types

In rust, there are generally two types of custom data-types, structs and enums.
Naturally, you can also declare type-aliases through the `type` keyword
```rust
type ChessBoard = HashSet<(u32,u32)>;
```
But Enums and Structs are the two go-to ways to actually create custom made data-types.

#### Question 4)
Look carefully at the following code
```rust


```
