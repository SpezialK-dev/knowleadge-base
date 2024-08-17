[The rust book](https://doc.rust-lang.org/book/title-page.html)
https://doc.rust-lang.org/book/ch03-02-data-types.html
# A few very basic things 

## immutability 
every variable is immutable if not specifed otherwiese with the mut keyword
This also applies to reference so we there we also need to specify it with the keyword
### Constants

use the const instead of the let keyword. They can never be mutable and the type of a const must be clear and annotatetd. Also const have to be knowen at compile time and cannot be computated at runtime

They are valid in the scope for the entire runtime
#### Naming convention for consts
all uppercase letters
## shadowing 

is when you have 2 variables that have the same name but are different types. Can be used for type conversions

Shadowing creates a copy that is only valid for the scope in which it was created there. afterwards the variable returns to the same value. 

Shadowing can be used on immutable variables. without having to make the variable mutable we can change its value but only in limited situations. 


## Datatypes



### Integer types 

| length  | sigend | unsigned |
| ------- | ------ | -------- |
| 8 -bit  | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

arch is dependet on what architekture you are on. 

### Floating point types 

f32 - single precision float 
f64 - double precision float

### Arrays 

Store data on the Stack rather than on the heap

vectors are similar but can grow and shrink in size. Arrays are fixed in size


```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

i32 is the type and 5 the amount of elements
that is only needed if you want to specify the type but you can also just leave it away

##### Array filled with the same data 

```rust
let a = [3; 5];
let a = [3, 3, 3, 3, 3];
```
both of these are equivalent

## Funktions

snake case 

```rust
fn print_labeled_measurement(value: i32, unit_label: char) -> i32 {
    println!("The measurement is: {value}{unit_label}");
}
```

**Statements** are instructions that perform some action and do not return a value.
**Expressions** evaluate to a resultant value.

Expressions do not include ending semicolons. 
If you add a semicolon to the end of aIf you add a semicolon to the end of an expression, you turn it into a statement.If you add a semicolon to the end of an expression, you turn it into a statement.If you add a semicolon to the end of an expression, you turn it into a statement.n expression, you turn it into a statement.

return values must be indicated with an arrow -> 
In Rust, the return value of the function is synonymous with the value of the final expression in the block of the body of a function.


## If else

you can use an if else in a let statment

```rust
   let number = if condition { 5 } else { 6 };
```


## Loops
How you can return values from loops 

loop is an infinite loop, that has to be closed with a break otherwise it will run indefinitely 

```rust
n main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```


### Loop labels 

are a way to let break or contine a specific loop

These have to start with a single quote
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

## Mem Management
if we pass a variable to a function and we dont copy it will be invalidated afterwards if it was a more complex type like a string. Since the funktion would take Ownership

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```
### creating deep copys of times


we use the .copy() thus we create a deep copy that does not invalidate s1
but rather allocates new memory. This copies heap data. 
```rust
  let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {s1}, s2 = {s2}");
```

this is only needed for data types such as strings which can be determined at runtime and dont have a fixed size. 



### Best practice  

if its larger data types simply pass them by reference something that should be done anyways. 

Also you can only have one mutable reference to an object, that can then be the only reference to said object. 