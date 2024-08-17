[The rust book](https://doc.rust-lang.org/book/title-page.html)
https://doc.rust-lang.org/book/ch03-02-data-types.html
# A few very basic things 

## immutability 
every variable is immutable if not specifed otherwiese with the mut keyword

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
fn print_labeled_measurement(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```

**Statements** are instructions that perform some action and do not return a value.

- **Expressions** evaluate to a resultant value.
