# Compilation process.
- Compiler  : `rustc`
- extn      : `.rs`
- ecosystem :  `cargo`

# what is cargo ?
 Cargo acts as a unified frontend for compiling code, managing external libraries called `crates`, running tests, generating documentation, and much more, It combines the rols often handled by seperate tools like `make,cmake,package managers (like apt or cvpkg for dependencies), and testing framworks`
```
    #create a new binary project named 'my_project'
    cargo new my_project
    cd my_project
    #compile
    cargo build
    #compile and run
    cargo run
    
``` 
Cargo enforces a standard project layout (placing source code in src/ and project metadata, including dependacies , in `Cargo.toml`), promoting consistency acros Rust projects.

# Basic Program structre
elements:
* **Modules**               : Organize into logical unit, controlling visibility (public.private)
* **Functions**             : Define reusable block of code.
* **Type Definitions**      : create cusotm data structre using `struct, enum or type aliases (type)`
* **Constants and Statics** : Define immutable values known at compile time or globally accessible data with a fixed memory location.
* **use** Statements        : import items (funs, types,etc...) from other modules or external crates into the current scope.

use `{}` define code block.
```
Crucially, when a variable goes out of scope, Rust automatically calls its “drop” logic, freeing associated memory and releasing resources like file handles or network sockets—a core aspect of Rust’s resource management (RAII - Resource Acquisition Is Initialization).
```
unlike C rust generally does not reuire forward declarations for functions or types within the same module; you can call a function defined later in the file, This often encourages a top down-code organization.

**IMPORTATNT EXCEPTION** : Variables must be declared or define before they are used within a scope.

# Entry point 
- main()
```
    fn main(){
        println!("Hello world!");
    }
```
- fn        : keyword to declare a fun.
- main      : program's entry point.
- ()        : encloses funs params.
- {}        : eclose funs body.
- println!  : A **Macro** (indicated by the **!**) printing text to standard output.
- ;         : terminate most statements.

Rust follows indentation conventions similiar to those in C(just for readability).

Rust's  `main()` by default, returns the type `()`, implicitly indicating success.
also can be used to return type `result`.

# Variables
## Immutability by default;
- `let` keyword

``` 
    let variable_name: OptionalType = value;
```
Rust req. variables to be intialized before their first use. preventing errors stemming from unintialized data.
- = perform assignments.

### immutability example
```
    fn main() {
        let x:i32=5; //x is immutatable
        //x = 6; this line would cause a compile-eror!
        println!("the valeus of X is: {}",x);
    }
```
## Enable mutability
### mut keyword
ex: 

```
    fn main(){
        let mut x = 5;
        println!("the value of X is {}",x);
        x = 6;
        println!("the value of X is {}",x);
    }
```
#### in C it is viseversa mutable by default, for immutable we needed to use ` const`


# DataTypes and Annotations
 - Similiar to C
 - must be everyvariable needed one type.
 ### Primitive DATA TYPES
 - **Integers**     :   Signed(``i8,i16,i32,i64,i128,isize``)
                        Unsigned(``u8,u16,u32,u64,u128,usize``). numbers indicate bit width. `isize and usize` are pointer-sized integers(``ptrdiff_t and size_t`` in C).
 - Floating-Point   :   ``f32 and f64`` single prceision and double precision.
 - Boolean          :   `bool`
 - Character        :   `char` represents unicode scalar value (`4` bytes). capable of holding characters like ‘a’, ‘國’, or ‘😂’. ``C char only hold single byte.``

 ## References.
 - similiar to C pointers.references hold the address of a value, introducing a level of indirection.
 - ``Rust refernces can be either immutable or mutable, allowing temperory access to data without tranferring ownership or making a copy.This especially useful for passing data to funs efficiently``
 - `&` -> for create refernces for immutable access.
 - `&mut` -> mutable access.
 - `*` can be used to access(deference) the value behind a reference, althouth in many cases this happens implicitly.
 - ex:
 ```
    fn inc(i: &mut i32){
        *i += 1;
    }
    fn main(){
        let mut v = 5;
        inc(&mut v);//1
        println!(" the value of v is: {v}");
        let r = &mut v;
        inc(r);
        println!(" the value of r is: {}",*r);//2
    }
    
 ```
### Type inference.
- The compiler can often deduce the type based on the assinged value and context.
```
fn main(){
    let answer = 42; //Type i32 by def for integers.
    let pi = 3.14159; // type f64 def for floats.
    let active = true; //bool inferred.
}
```
### Explicit Type annotations
- use colon `:` opertor
- ex:
```
fn main(){
    let count:i32 = 8;
    let temperature:f32 = 21.5;
}
``` 
> C lacks built in type inference like Rust.

# Constants and Static Variables;
 ### const
 - constants represents values that are known at compile time, They must be annotated ``with a type`` and are typically defined in the `global scope`, Though they can also be defined `within funs`.``Constants are effectively inlined whereever they are used`` and ``donot have a fixed memory address``.
 - The nameing convention : ``SCREAMING_SNAKE_CASE``
 - ex:
```
const SECONDS_IN_MINUTE:u32 = 60;
const PI:f32 = 3.14;
fn main(){
    println!(" her are the values {SECONDS_IN_MINUTE} and {PI}");
}
```
### static
- Static variables represent values that have a fixed memory location (static lifetime) throughout the program’s execution. They are initialized once, usually when the program starts. Like constants, they must have an explicit type annotation.  
- The naming convention is also ``SCREAMING_SNAKE_CASE``.
- ex:
```
static APP_NAME:&str = "Rust Explorer";
fn main() {
    println!("welcome to {}!",APP_NAME);
}
```
- Rust strognly `discourages mutable static vaiables (**static mut**)`because modifying global state without sync can easily lead to data races in concurrent code.
- Accessing or modifiying `static mut` variabled req `unsafe` blocks.

##### C vs RUST
- `const` is similiar to C's  `#define`, also highly optimised const variables in C
- `static` is closer to C's global or file-scope `static` variable regarding lifetime and memory location. However, Rust's emphasis on safety arount mutable static is much stricter than C's.

## Funs and Methods
- `fn` to define funs.
- fn funName (parameter list `:(with types)`) and an Optional return type specified after `->`.
ex:
```
    //fun that takes two i32 params adn return an i32
    fn add(a:i32,b:i32) -> i32{
        // the last expression in a block is implicitly retuned if it doesn't end with a semicolon.
        a+b
    }
    //fun takes no params and returns nothing (unit type '()');
    fn greet(){
        println!("Hellow from the greet fun!");
        // no return , implicit return ()
    }
    fn main(){
        let sum = add(4,5);
        println!("sum is {sum}");
        greet();
    }

```
res
```
    sum is 9
    Hellow from the greet fun!
```
<details>
<summary> key points (funs)</summary>

 ```
    1. Parameters types must be exlicitly annoted.
    2. The return tupe is specified after `->`. if omited the returns the unit type ().
    3. The value of the last expression in the fun body is automaticaly returned, unless it ends with a   semicolon ';',  `return` keyword can be used for early returns.
 ```
 </details>

## Methods
- In Rust , _methods_ are similiar to funs but defined within `impl` blocks and are associated with a specific type (like a `struct` or `enum`).
- first param is `self`,`&self` or `&mut self`, which referes to the instance the method is called on - similiar to the imipicit `this` in `C++`
> methods are accessing using `.` operator like instance.method() and can be chained.

<details> 
<summary> Example on Methods in Rust</summary>

```
    struct Point{
        x:i32,
        y:i32,
    }

    impl Point{
        // Method that calculates the distance from the origin
        fn magnitude(&self)-> f64{
            ((self.x.pow(2) + self.y.pow(2))as f64).sqrt()
        }
    }
    fn main(){
        let p = Point{x:3,y:4};
        println!("Distance from orign {}",p.magnitude());
    }

```
```Result:
    Distance from Origin : 5
```

</details>

<details>
  <summary>Key points on methods</summary>
    <div style="border: 4px solid #007acc;">

```
    1. Methods are funs tied to a type and defined in `impl` bloks.
    2. The first parameter is typically self,&self,&mut self, representing the instance.
    3. Methods are called using .
    4. Methods without a 'self' paramerter eg (String::new()) are called associated funs.These are often used as constructors or for operations related to the type but not a specific instance.
```
</details>

## Control Flow Constructs.

1. Conditional execution with **if, if else and  else**
<details>
  <summary>Conditional execution example</summary>
<div style="border-left: 4px solid #007acc;">

```
    fn main(){
        let number = 6;
        if number % 4 == 0{
            println!("{} is div by 4",number);
        }else if number % 3 == 0{
            println!("{} is div by 3", number);
        }else{
            println!("{} is not div byt 4 and 3",number);
        }
    }
```

</details>

    
```
    Take aways
    - Conditions must evalute to a bool. unlike C, integers are not automatically treated as true(non-zero) or false (zero).
    - Paranthesis () around condition are not req.
    - Curly braces {} around the blocks are mandatory, even in single statements.
    - `if` is an expression in Rust, means it can return a value: 
    - ex
        fn main(){
            let condition = true;
            let number = if condition{4} else{ 6};
            println!("the number is {}", number);
        }
        result => The number is 4

```
2. Repetition: loop, while, and for
- Rust offers  three looping constructs:
    1. > **loop** : create an infinite loop typically exited using **break**. break an also return a value from the loop.
    <details>
      <summary>loop example</summary>
    
    ```
        fn main(){
            let mut counter = 0;
            let result = loop{
                counter +=1;
                if counter == 10{
                    break counter * 2;// exit the loop and return counter * 2
                }
            };
            println!("{result}");
        }
    ```
    </details>

    2. > **While** : Executes the blocks as long as boolean condition returns true

    <details>
      <summary>while example</summary>
    
    ```
        fn main(){
            let mut number = 3;
            while number != 0{
                println!("{}!", number);
                number -= 1; 
            }
        }
    
    ```
    </details>

    3. > **for**    : iterates over elements prodcued by an iterator. This is the most common and idiomatic loop in Rust. it's fundamentally differenct from C's typical index-based `for` loop.

    <details>
      <summary>for loop exmaple</summary>
    
    ```

        fn main(){
            //Iterate over a range 0->4
            for i in 0..5{
                println!("{i} ");
            }
            // iterate over elements in an array.
            let a = [10,20,30,40,50];
            // `.iter()` creates an iterator over refernces;
            for element in a {// or explicitle `a.iter()`
                        println!("The value is: {}", element);
            }
        }
    ```
    </details>

    - > continue skips, and break breaks the loop but give return.

## Control flow comparisons with C

```
    1. Rust enforces bool conditions in if and while. C allows integer conditions (0 is false, non-zero is true).

    2.Rust requires braces {} for if/else/while/for blocks. C allows omitting them for single statements, which can be error-prone.

    3. Rust’s for loop is exclusively iterator-based. C’s for loop is a general structure with initialization, condition, and increment parts.

    4. Rust prevents assignments within if conditions (e.g., if x = y { ... } is an error), avoiding a common C pitfall (if (x = y) vs. if (x == y)).

    5. Rust has match, a powerful pattern-matching construct (covered later) that is often more versatile than C’s switch.
    
```
