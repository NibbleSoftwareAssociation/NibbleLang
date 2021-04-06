## Variables

In Nibble, you can declare a variable with the `let` keyword.

```
let a = 2
let b = "Hello"
let c = new Foo()
```

The type of variable can be written in the form of `let i:T = expr` where `i` is the name of the variable
and `T` is the type of the variable:

```nibble
let a: i32 = 56
let b: String = "Brum"
let c: Foo = new Foo()
```

A variable must be declared with a value because Nibble doesn't provide a default value.

```
let a: i32    // Compilation error: 'a' must be declared with a value
```

This is to avoid default behaviors and to keep safe from NPE (NullPointerException).
In fact a variable isn't nullable by default and since all data in Nibble are objects this 
would lead to set default values to null.

For more explanation read [Nullable Documentation](nullable.md).

You can declare multiple variable in a single line

```
let a = b = 3
```
or
```
let c, d = 1, 2
```

Variables in Nibble are immutable by default, this means that you can't assign another value to a variable
once declared.

```
let a = "3"

a = "My string"     // Compilation error: Can't reassign a value to an immutable variable
```

You need to mark your variable with the `mut` keyword:

```
mut let a = 3

a = 4               // Ok
```

Once declared a variable with a type `T1`, you can't reassign the variable with a value of type `T2`.
In Nibble, variables are statically typed.

```
mut let a = 3           // a has i8 as type

a = "Hello"             // Compilation Error: Can't assign a String type to a i8 type
```

There are few ways where you can assign a value of `T2` to a variable of type `T1`, this is documented in [Cast documentation](cast.md). 

Nibble allow declaring dynamically typed variables, with `dyn` keyword:

```
dyn let a = 3

a = "Hello"             // Ok, a dynamic variable is mutable by default
```

This is possible because the variable is redeclare when it is assigned a type of value other than it's type.

```
dyn let a = 3
a = 4                   // No problems here
a = '1'                 // '1' is a Char, a is destroyed and recreated in order to handle Char type
```

Because of this, `dyn` keyword slow the speed of the program. If you need a variable that hold value of multiple types 
in a range, it's better for you, and the program to use a `sumtype`.

## Constants

In Nibble, you can declare a constant value with `const` keyword.

```
const a = 3
```

Constants must have a literal as rvalue, like `3`, `"Hello"` or `(2, 'a')`, or even a simple lambda like `{a, b => print(a + b)}`.

A constant cannot change its value.

```
const a = [1, 2, 3]
a = [4, 5]              // Compilation error: Reassign of a constant
```

Collection literals need to contain only literals.

In collection literals, you can't even reassign the value of a particular value of the collection:

```
const a = [1, 2, 3]
a[0] = 2                // Compilation error: Reassign of a constant
```

This is because const reference both to `a` and both to `a`'s values. 

If you want to modify the value's of `a` you can use the `mut` keyword with `const`:

```
mut const a = [1, 2, 3]
a[0] = 1                // Ok

a = [5, 6, 7]           // Compilation error: Reassign of a constant
```

### Difference between Immutable variables and Constants

You could ask yourself: "So what's the difference between an immutable variable and a constant?"

The answer is: "Performance"

A constant assignment is executed on compile time, an immutable variable assignment is always executed on running time.

This is why you are allowed to declare a constant only with literals.

My advice is to use immutable variables if you have low number of variables reading, else a constant.

### Shadowing of variables

Some programming languages allow you to redeclare the same variable with a different type:

```rust
// Rust
fn main() {
    let a: i8 = 3;
    println!(a);
    let a: String = String::from("Hello");
    println!(a);
}
```
This is know as Shadowing of the variable `a` which will contains, in the end, values of `String` type.

This is not allowed in Nibble, once a variable is declared, you can't declare a variable with the same name 
in the current or inner scope.

```
let a: i8 = 6
let a: String = "Nibble"   // Compilation error: Variable 'a' already declared in the same scope
```

If a variable needs to handle multiple values of different types, use a `sumtype`.

### Scope of a variable

The visibility of a variable is defined in the scope where it's been declared:

```
func main() {
    let a = 0
    
    first : {
        let a = 1        // Compilation error: Variable 'a' already declared in the same scope
        let b = 0
    }
    
    second : {
        let b = "Scope"  // Ok
    }
}
```

In the first block, we cannot redeclare `a` because the block already contain a reference to a variable named `a`.

This is not true in the second case: the first block declare the `b` variable, but the life of `b` ends when the scope
of the first block is finished (`}`).

The second block doesn't have a reference to a variable named `b`, and so he can declare the `b` variable.