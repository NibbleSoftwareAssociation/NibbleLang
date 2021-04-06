## Nullable

The null pointer is heavily criticized because it leads to the most infamous error of OOP 
languages: the `NullPointerException`

Let me show you some example:

```java
//java
public class Main {
  public static main(string[] args) {
    String mystring;
    
    System.out.println(mystring.toLowerCase());
  }
}
```

Here `mystring` is a reference object, but it doesn't point to any object.
Java assign to `mystring` the `null` default value. This means that `mystring` doesn't point
to anything. So what happens when I call `mystring.toLowerCase()`? The JVM raise a `NullPointerException`
breaking the execution of the program.

The `NullPointerException` bug is difficult to find, and the newest programming languages
drop `null` for new ways to handle this state.

Nibble it's not far behind, encapsulating the `null` value in `Option` enum:

```
pub enum Option<T> {
    Some -> T,
    None
}

mut a -> Option<i8> := Option::None
```

This can be written in a more beautiful way, because `None` always refer 
to `Option::None`, `Option::` can be omitted:

```
mut a -> Option<i8> := None
```

Also, there is a shortcut for `Option<i8>`, that is `i8?`:

```
mut a -> i8? := None
```

In order to assign a value to `a` we can use `Option::Some`, `Some` or we can assign 
the value, Nibble will do the backend:

```
a = Option::Some(1)         // Ok
a = Some(2)                 // Ok
a = 3                       // Ok
```

We can check if `a` is `None` in these ways:

```
if a == None {
    println("a is None, I can't use it")
}
```

or

```
match a {
    None => {
        a = 1
        println("a was None, now it is 1")
    }
}else{
    print("A is not None")
}
```

