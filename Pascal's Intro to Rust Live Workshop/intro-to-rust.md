## [Notion Page](https://www.notion.so/egghead/Tour-of-Rust-Pre-workshop-Essential-Questions-2d2fa6853883477fb7e1e674498e0f94)

[What is Rust and why is it so popular?](https://www.notion.so/egghead/What-is-Rust-and-why-is-it-so-popular-Stack-Overflow-Blog-a3e265423ede4908b3a3953b41c335b6)

Just going to say that I really liked the pre-workshop meeting and I think it's really going to help me out with the workshop tomorrow. Really happy we had that. 

## Goal of this course:

Teach intro to Rust and why it's a good language to learn. Get some basics down to be able to create your own small application. 

## [Github Repository](https://github.com/PascalPrecht/intro-to-rust)

## Post Workshop Notes:

I like how the instructor repeated the question he was about to work through/answer. Really helps people to make sure they understand the question that was being asked. 

We only went about 15 minutes over so if we started exactly on time and he didn't answer every question, possibly let other people in the chat try to answer questions, he wouldn't have had to hurry so much towards the end. It was just about the last 30 minutes where he had to speed up to make sure that he got all of the information across in time. We went through about 3 or 4 sections in the last 30 minutes where we spent a good 3 hours on the other 6 sections. 

He did a great job answering questions! He went into detail with every question to make sure that whoever asked it got a full answer and made sure they understood the content. 

## Next Time:

Like I said above, a small adjustment with how long questions took and starting around 10 minutes late. Fixing that would fix the need to rush at the end and he would be able to fit in all of the info that he wanted to without rushing. 

## Live Workshop Notes:

Start by cloning the repo and running the command in the README to get the rust tools necessary for the workshop.

[Rust book](https://doc.rust-lang.org/book)

Anything that can be written in C and C++ can be written in Rust. 

Rust compared to other languages, rust will try to give you the best of both worlds. Doesn't have a garbage collector. Must write memory safe code. 

The compiler doesn't allow you to write code that isn't memory safe. No 'Cannot read property type of null'. 

Downside - hard at first, lots of compiler errors. 

### Terminal
```bash
mkdir -p src/hello-world
cd src/
touch [main.rs](http://main.rs/)
```

Every rust project has to have a `main` file.

function = `fn`

Create a `main` function to say hello world. To print to the console you use `println`. 

### main.rs
```rs
fn main () {
  println!("Hello world");
}
```

You can basically create your own language inside of rust using `macros`. We are using the `!` macro. Won't go into detail about macros. 

Now we can compile by using `rustc [main.rs](http://main.rs)` in the terminal.

Run the file by using `./main`.

What happens if I use `println` without the `!`. It's not a macro, its function call. There is no function call `println`. 

Rust does a great job at error messaging. 

Every statement inside the body of a function, should have a semicolon unless dealing with a return statement. 

## Exercise 1

(This is exactly what we just did. I followed along with the instructor so I already had the exercise done.)

We can do basically the same thing with Cargo, one of the tools we installed. It's the package manager to download packages. It also allows us to create packages. 

`cargo new` creates a new project. 

### Terminal
```bash
cargo new say-my-name
```

This creates a new folder for our project. We are going to get it to say our name. This now comes with a `Cargo.toml` file. toml is an extension to yaml. 

Cargo.toml file [explanations](https://doc.rust-lang.org/cargo/reference/manifest.html)

To compile with cargo, use `build` command. 

```bash
cargo build
```

That gives us a `Cargo.lock` file and `target` folder. 

`target` has a debug folder. 

To run `./target/debug/say-my-name`, you have to be in the top level folder above `./target/debug/say-my-name`. 

`cargo build --release` optimizes the build. 

[crates.io](http://crates.io) is where you would upload your package. It will also create documents for you package. 

You can also use `cargo run --release` instead of `./target/debug/say-my-name` to have your file be ran. Definitely much easier. 

### Exercise 2

## Section 3

You use variables using the `let` keyword. 

```rs
fn main() {

    let name = "Lucas Minter";

    println!("Hello, {}", name);
}
```

Then using `cargo run`, you see `Hello, Lucas Minter` printed to the console. 
```rs
fn main() {

    let name = "Lucas Minter";

    println!("Hello, {}", name);

    name = "Alice";

    println!("Hello, {}", name);
}
```

This gives us an error because `name` is not mutable. 

You have to use `mut` to allow a variable to be mutable. 

`println` stands for print line. It basically does what `.chomp` does in Ruby where it automatically creates a new line. 

`fist_name: "Lucas"` is not a string. It is a string slice. Use `to_string()` to make them strings. 

```rs
struct Person {
    first_name: String, 
    name: String,
}

fn main() {

    let person = Person{
        fist_name: "Lucas".to_string(),
        name: "Minter".to_string(),
    }

    println!("Hello, {}", person);
}
```

Gives the error: `Person` cannot be formatted with the default formatter.

By using `#[derive(debug)]`, we can make rust figure it out on its own. 

help: a field with a similar name exists: `first_name` - this usually means you have a typo somewhere. 

```rs
#[derive(Debug)]
struct Person {
    first_name: String, 
    name: String,
}

fn main() {

    let person = Person {
        first_name: "Lucas".to_string(),
        name: "Minter".to_string(),
    };

    print!("{:?}", person);
}
```

Type annotations are usually a good thing but not always necessary. It comes with something called `type inference`. The compiler will figure it out on its own. 

### Exercise 3

Time to look into user inputs! 

Rust comes with a standard library. https://doc.rust-lang.org/std/index.html

The `read_line` function asks the user for input. How do we get ahold of `std::io`. 

To import, you use `use`. 

We need a buffer now.

```rs
let buffer = String::new();

io::stdin().read_line(buffer);
```

It has to be mutable. 

```rs
io::stdin().read_line(&mut buffer)
```

When you have error cases in Rust, you will get something thats called a result. It resolves with a `type` or an `error`.

`.unwrap` gives us the value, if there is an error, the program will crash. It's a lazy way to deal with errors. 

```rs
use std::io;

fn main() {

    println!("Please enter your name:");

    let mut buffer = String::new();

    io::stdin().read_line(&mut buffer).unwrap(); //Result<usize, E>

    println!("Hello, {}", buffer);
}
```

## Short break

When you have a variable like foo, but you aren't using it anymore. 

You don't have to worry about memory management, memory safety,  in JS. 

In Rust, the concept of ownership, There's only one variable at a time that can own the value of something. 

```rs
let foo = [ 3, 4, 5, 5] // foo owns

someFunction(foo); //someFunction owns

println!("{}", foo)
```

Once a function is done, the values inside of it are done being used and ownership can be passed on. 

After `someFunction(foo); //someFunction owns`, foo is no longer used and isn't needed. 

This is where borrowing comes in. 

```rs
main {
  let foo = [ 3, 4, 5, 5] // foo owns
  
  someFunction(&foo); //someFunction owns
  
  println!("{}", foo)
}
```

This is the entire life of `foo`. ^

We have to be explicit where we want to use a reference or give a value. 

`String -> &String(reference to string) -> &str(slice)`

```rs
io::stdin().read_line(&mut buffer).unwrap();
```

^ Give me a string that you own, I borrow it, mutate it, when I'm done with my work, your buffer has been mutated.

Must make sure that the variable is mutable to use it and types must be the same. 

```rs
let mut buffer = String::new();

io::stdin().read_line(&mut buffer).unwrap();
```

### Exersize 4

We are going to work on a function that adds numbers together. 

```rs
fn sum(a: u32, b: u32) -> u32
```

`u32` basically means any integer. 

```rs
fn sum(a: u32, b: u32) -> u32 {
    let result = a + b
    result
}
```

But to save some keystrokes: 

```rs
fn main() {
    let result = sum(4, 3);

    println!("Result: {}", result)
}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}
```

We can have the user put in two numbers: 

```rs
fn main() {

    let mut first = String::new();

    println!("Please enter a number: ", result)
    io::stdin().read_line(&mut first).unwrap();

    let mut second = String::new();
    io::stdin().read_line(&mut second).unwrap();

    println!("Result: {}", result)

}
```

This will not work. 

String comes with a parse function. It's either a value of a certain type or an error. The type depends on what the value is being cast too. 

`.unwrap` only works good when everything is inputed correctly. 

Having issues with:

```
io::stdin().read_line(&mut first).unwrap();
^^ use of undeclared type or module `io`
```

Figure it out. Didn't import `io`. 

We have to use `.trim()` but I'm not sure why. Got lost trying to debug. 

### Exercise 5 and 6

Error handling using pattern matching. 

```rs
match fisrt.trim().parse() {
  Ok(value) => {
    //do something value
  }, 
  Err(error) => {
    // do something error
  }
}
```

To show with our example we have been working on: 

```rs
match fisrt.trim().parse() {
  Ok(value) => {
    
  }, 
  Err(error) => {
    // do something error
  }
}
```

If you want to tell the compiler that you aren't using something and don't want an error, you use an underscore. `_error`. for example. 

Current example: 

```rs
fn main() {

    let mut first = String::new();

    println!("Please enter a number: ");
    io::stdin().read_line(&mut first).unwrap();

    let mut a:u32 = 0;
    
    match first.trim().parse() {
        Ok(value) => a = value, 
        Err(_error) => eprintln!("This is unfortunately not a number.")
    }
    
    let mut second = String::new();

    println!("Please enter a second number: ");
    io::stdin().read_line(&mut second).unwrap();

    let mut b:u32 = 0;
    match second.trim().parse() {
        Ok(value) => b = value, 
        Err(_error) => eprintln!("This is unfortunately not a number.")
    }

    let result = sum(a, b);
    println!("Result: {}", result);

}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}
```

### Exercise 7

In case we are having an error, we want to print the line and exit with an error number. 

We use `exit` to stop the program and exit with an error number that we provide. 

```rs
match first.trim().parse() {
  Ok(value) => a = value, 
  Err(_error) => {
    eprintln!("This is unfortunately not a number."),
    process::exit(1)
  },
}
```

### Exercise 8

Now we look at loops. If we wrap the whole function in a loop, it will not end. It will restart until we give it not a number. If you want it to loop through a certain number of times, you could use a `for` loop, similar to JavaScript.

At this point, we were nearing the end of the workshop and the instructor sped up to try and get through everything in the allotted time. Hard to take notes.