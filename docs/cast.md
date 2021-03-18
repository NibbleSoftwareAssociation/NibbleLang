## Cast

Casting is the process to transform a value of type `T1` in a value of type `T2`.
In Nibble there are only a bunch of automatic casts, mainly concerning numbers:

```
i8 -> i16 -> i32 -> i64 -> 128
 
u8 -> u16 -> u32 -> u64 -> u128

u8 -> i8 -> ...
u16 -> i16 -> ...
u32 -> i32 -> ...
u64 -> i64 -> ...
u128 -> i128 -> ...

f32 -> f64
```

Let's talk about bits:
An `u8` value use a total of 8 bits. For this, an `i8` value can handle numbers from `0` to `255`.
An `u16` value use a total of 16 bits, handling numbers from `0` to `65535`.

This explains why you can convert an `u8` to `u16` but not the other way around, in fact if you  could
transform an `u16` value to an `u8`, the value will lose numbers.

Nibble forbid this by default:

```
mut a -> u8 := 34

b -> u16 := 43

a = b           // Compilation error: Cannot convert implicity an 'u16' value to 'u8' value 
``` 

But if you need to?

Nibble allow explicit conversion using `as` keyword

```
a -> u8 := new u16(45) as u8    // Ok, possible lose will not worry us
```

With `as` keyword, we force the conversion, and for Nibble is ok.

This is not the only way, there are a lot of functions and methods for converting:

```
a := Int.parse("1")?
```

Typically, they perform a copy of the value to convert, and then they return the value converted.

For converting an UDT (User Defined Type), the type need to have a way for returning a copy of itself
converted in another type, this is know as cast override.