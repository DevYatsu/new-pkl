# new-pkl

Fastest pkl-parsing crate out there!

## Features

- Parse Pkl string into a structured representation (hashmap) in rust
- Parse Pkl string into an AST
- Support for strings, integers (decimal, octal, hex, binary), floats, boolean and multiline strings
- Support for nested objects, amends declaration, amends expression and chained amends declaration
- Support for classical identifiers, $identifiers, _identifiers and illegal identifiers
- Support for class instance

## Usage

Here's an example of how to parse a PKL string and retrieve values from the context:

```rust
use new_pkl::{Pkl, PklResult, PklValue};

fn main() -> PklResult<()> {
    let source = r#"
    bool_var = true
    int_var = 42
    float_var = 3.14
    string_var = "hello"
    object_var {
        key1 = "value1"
        key2 = 2
    }
    "#;

    let mut pkl = Pkl::new();
    pkl.parse(source)?;

    println!("{:?}", pkl.get("int_var")); // Ok(PklValue::Int(100))

    // Get values
    println!("{:?}", pkl.get_bool("bool_var")); // Ok(true)
    println!("{:?}", pkl.get_int("int_var")); // Ok(42)
    println!("{:?}", pkl.get_float("float_var")); // Ok(3.14)
    println!("{:?}", pkl.get_string("string_var")); // Ok("hello")
    println!("{:?}", pkl.get_object("object_var")); // Ok(HashMap with key1 and key2)

    // Modify values
    pkl.set("int_var", PklValue::Int(100));

    // Remove values
    pkl.remove("float_var");
    println!("{:?}", pkl.get_float("float_var")); // Err("Variable `float_var` not found")

    Ok(())
}
```

### LICENSE

This project is licensed under the MIT License. See the (LICENSE)[./LICENSE] file for details.
