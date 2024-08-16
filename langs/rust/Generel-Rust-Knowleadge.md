[The rust book](https://doc.rust-lang.org/book/title-page.html)
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