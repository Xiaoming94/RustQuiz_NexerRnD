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
* What is happening in the first and second `let a` statement?
    * Btw, you can reproduce the effect of these lines without using the 2nd `let a`, how? (hint: `let mut a = ...;`)
* What is happening in the `let ...` statement before the 2nd `println!()`?
* How do you think the `if let ...` statement is evaluated?

The code before the last print is related to the `Option<>` type, which is an `enum`.
Enums in rust will be explored later.
For now, just understand that enums in rust are very different from traditional enums found in C/C++ and Java.

#### Question 7
```rust
mod util {
    pub fn calc_sum(a: u32, b: u32) -> u32 {
        a + b
    }
}

fn main() {
    // Do something?
}
```
* What is the purpose of the `mod` and `pub` keywords?
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

#### Question 4
Lets look at some basic type conversion. Consider the followin snippets:
a)
```rust
fn main() {
    let my_var = -1;
    let anover_var: u32 = my_var.try_into().unwrap();
}
```
* What would actually happen when you execute this code?
* What is the `try_into()` function?

b)
```rust
fn main() {
    let my_var: i32 = -42;

    println!("my_var: {}", my_var);
    println!("my_var as unsigned int: {}", my_var as u32);
    println!("my_var as float: {}", my_var as f32);
    println!("my_var as a char: {}", my_var as char);
}
```
* What would the print outs be?

c)
```rust
struct OneStruct(u32, u32);
struct AnotherStruct(u32, u32);

fn main() {
    let my_object = OneStruct(1,0);
    let another_type = my_object as AnotherStruct;
}
```
* As a matter of fact, this code will NOT compile, why?

Later on, we will explore how to convert between custom types the correct way.

### Part2.2 Custom data types

In rust, there are generally two types of custom data-types, structs and enums.
Naturally, you can also declare type-aliases through the `type` keyword
```rust
type ChessBoard = HashSet<(u32,u32)>;
```
But Enums and Structs are the two go-to ways to actually create custom made data-types.
Structs are basically a way to create a compound 

#### Question 5)
Look carefully at the following code
```rust
mod shapes {
    pub struct Rectangle {
        width: f32,
        height: f32,
    }

    impl Rectangle {
        pub fn new(width: f32, height: f32) -> Self {
            Rectangle {
                width: width,
                height: height,
            } 
        }

        pub fn area(&self) -> f32 {
            self.width * self.height
        }

        pub fn circumference(&self) -> f32 {
            2 * (self.width + self.height)
        }
    }
}
```
* What is happening in the `impl` code block?
* What are the difference between the function `new()` and the functions `area()` and `circumference()`?
* Baring the fact that the struct `Rectangle` is defined in a module `shape`, how would can you initialize it? (hint: there are two ways.)
    * Bonus question: Do you **need** a `new()` function to instantiate the struct `Rectangle`?
* (Highly recommended that you do these in the playground or godbolt) Now that you have seen a struct, how would you go about writing a struct for 
    * a *square*?
    * a *circle*? (the constant for PI is available if you add `use std::f32::consts::PI;` before the declaration of Circle);

#### Question 6)
The code above can also be rewritten like this, using something called a *tuple struct*:
```rust
mod shapes {
    pub struct Rectangle(f32, f32);
    
    impl Rectangle {
        pub fn new(width: f32, height: f32) -> Self {
            Rectangle(width, height)
        }

        pub fn area(&self) -> f32 {
            let Rectangle(width, height) = self;
            width * height
        }

        pub fn cirumference(&self) -> f32 {
            let Rectangle(width, height) = self;
            2 * (width + height)
        }
    } 
}
```
* What do you think are the pros and cons of a struct defined this way?
* There is a way where you can (through pattern matching) deconstruct the struct from Question 4 into it's fields, how?

#### Question 7)
NOTE: We will actually explore rust Enums through multiple question. While we are at it however, keep in mind of how tuple structs works.

Consider this following example implementation of geometrical shapes.

```rust
enum ShapeTypes {
    Circle,
    Rectangle,
}

struct Shape {
    shape_t : ShapeType,
    width: f32,
    height: f32,
}

impl Shape {
    pub fn new(width: f32, height: f32, shape: ShapeType) -> Self {
        match shape {
            ShapeType::Rectangle => create_rectangle(width, height),
            ShapeType::Circle => create_circle(width),
        }
    }

    fn create_rectangle(width: f32, height: f32) -> Self {
        Shape {
            shape_t: ShapeType::Rectangle,
            width: width,
            height: height,
        }
    }

    fn create_circle(radius: f32) -> Self {
        Shape {
            shape_t: ShapeType::Circle,
            width: radius,
            height: radius,
        }
    }

    pub fn area(&self) -> f32 {
        match self.shape_t {
            ShapeType::Circle => circle_area(self.width),
            ShapeType::Rectangle => rectangle_area(self.width, self.height),
        }
    }

    fn circle_area(radius: f32) -> f32 {
        radius * PI.pow(2) 
    }

    fn rectangle_area(width: f32, height: f32) -> f32 {
        width * height as f32
    } 
} 
```

This implementation is not really ideal... but ignore it for now.
* What's the difference between using an enum in `match` vs using some other types? (like a string or numeric type (u32,i32,f32))
* While not related to enums, what do you think is the difference between the functions declared with `pub fn` and those declared with only `fn`?
* (Recommended to use playground) You can also avoid creating functions like `create_rectangle()` and `rectangle_area()` using the syntax
```rust

match shape_t {
    ShapeType::Circle => {
        //do something
    }
}
```
* How can this be accomplished?
* Which do you prefer and why?

#### Question 8
We can, actually, ditch the structs in the previous code like this
```rust
enum Shapes {
    Circle(f32),
    Rectangle(f32, f32),
}

fn area(geometric_shape: Shapes) -> f32 {
    //Do Something
}

```
* How would you instantiate a shape this way?
* How would you implement the function `area()` here?
    * Using `let if`
    * Using `match`

#### Question 9
As a matter of fact, with enums in rust, this is also legal:

```rust
enum Shapes {
    Circle(f32),
    Rectangle(f32, f32),
}

impl Shapes {
    fn area(&self) -> f32 {
        match *self {
            Circle(radius) => f32 * PI.pow(2),
            Rectangle(width, height) => width * height,
        }
    }
}
```
* How should the user of this enum call the function area?
* So, when should a struct be used? When should an enum be used?
* Without thinking about the implemented functions. How do you think the enum `Option<T>` is defined?

## Part 3
In the last part where we explored the rust type-system, you might have an impression of rust's type-system being pretty stiff and strict.
Which it is - There is alot of discourse about why the type-system in rust being the way it is.

### Part 3.1 What is a trait?
The concept of traits is kinda in it's name, that the type has a certain characteristics about it defined by it's traits.
In terms of programming, rust's traits can be thought of as something similar to interfaces.

#### Question 1
Let's implement geometrical shapes using a trait instead 
```rust
trait Shape {
    fn shape_name();
    fn area(&self) -> f32;
    fn circumference(&self) -> f32;
}

struct Rectangle {
    width: f32,
    height: f32,
}

impl Shape for Rectangle {
    fn area(&self) -> f32 {
        self.width * self.height
    }

    fn circumference(&self) -> f32 {
        2.0 * (self.width + self.height)
    }
}
```

* Using this example as reference, how would you implement shapes for:
    * Circle?
    * Square?

* If you want functions/methods specific to Rectangle (or any other struct), how would you go about implementing these?

### Part 3.2 Rust's built in traits

Out-of-the-box, rust has alot of traits built-in.
