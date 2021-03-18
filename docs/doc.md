<div align="center">
  <h1>The Nibble Programming Language</h1>
  <hr/>
</div>

## Data types

In addition to UDTs (User Defined Types), Nibble has a set of "primitive" types, so called because they
represent the basic data.

These types are:

```
i8              // signed integer 8 bit
i16             // signed integer 16 bit
i32             // signed integer 32 bit
i64             // signed integer 64 bit
i128            // signed integer 128 bit
u8              // unsigned integer 8 bit
u16             // unsigned integer 16 bit
u32             // unsigned integer 32 bit
u64             // unsigned integer 64 bit
u128            // unsigned integer 128 bit
f32             // float with 32 bit precision
f64             // float with 64 bit precision
Char            // Character type
Boolean         // Boolean type
String          // String type
```

Integers and floats are objects as well as Char, Boolean or String instance.

Nibble has some types for primitive collections too:

```
[1,2,3,4]                   // Array type
{"one": 1}                  // Map type
(1, "Hello", new Foo())     // Tuple type
```

### Array Type

Array type is defined as ```[]T```, note that we do not declare a length: in fact, arrays' length, by default is no-fixed:
```
arr: []i8 := []
arr[0] = 1
arr[1] = 2
arr[2] = 3
// arr = [1,2,3]
```
A fixed-lengt is defined as ```[expr]T``` where ```T``` is any type, and ```expr``` represent
the length for the array.

### Map Type

Map type is a collection of pair defined as ```{T1 -> T2}``` where ```T1``` represent the key and ```T2``` represent the value.

### Tuple Type

A tuple is a collection of values of different types. 
Tuples are constructed using parentheses ```()```, and each tuple itself is a value with type signature 
```(T1, T2, ...)```, where ```T1```, ```T2``` are the types of its members.
Functions can use tuples to return multiple values, as tuples can hold any number of values.


