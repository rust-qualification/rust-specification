# 2. Expressions
## 2.2. Field Access Expressions <a name="2.2."></a>


### Syntax
   <a name="field-access-expression-syntax"></a>

    FieldAccessExpression ::=
        Expression.FieldSelector

    FieldSelector ::=
        FieldIndex
      | FieldName

    FieldIndex ::= 
        DecimalLiteral

    FieldName ::=
        Name

### Description
A field access expression is an expression used to access a field of a value from a data structure, such as `structs`, `unions` and `tuples`.
The container operand indicates the data structure from which the field is accessed and a field selector determines which field of the container is selected.

### Legality Rules
2.2.1. The type of a field access expression corresponds to the type of the field that is selected for access.

2.2.1. The value of a field access expression corresponds to the value of the field that is selected for access.

2.2.2. Reading the selected field of a union shall require the use of an `unsafe context`.

2.2.3. Writing to the selected field of a union where the type of the selected field implements the `core::marker::Copy` trait or the `core::mem::ManuallyDrop` trait shall not require `unsafe context`.

2.2.5. In `tuples`, fields are accessed using an index corresponding to each field. Tuple indices start from 0 and increment sequentially as decimal values. 

2.2.6. In `structs` and `unions`, fields are accessed using the name of the selected fields.

### Runtime Semantics
2.2.7. The characteristic of unions is that all fields share the same storage. Consequently, writing to one field of a union will overwrite its other fields.

2.2.8. Evaluating a field access expression involves evaluating its container operand.

2.2.4. Writing to and then reading from the selected field of a union subject to attribute `repr` is equivalent to invoking function `core::mem::transmute<write_type, read_type>(field_bits)`:
- `write_type` is the type used at the time of writing the selected field
- `read_type` is the type used at the time of reading the selected field, and 
- `field_bits` is the bit representation of the selected field.

### Undefined Behavior
Reading a selected field of a [union type](#1.2.), when the union contains data that is invalid for that field's type, results in undefined behavior.

### Examples
`
    let f = unsafe { myUnion.myField }; // accessing a union field with name myField
` \
`
    ("hi", 14, false).1 // accessing the second tuple field
`
```
    union MyUnion {
        integer: i32,
        float: f32,
    }

    fn main() {
        unsafe {
            let mut my_union = MyUnion { integer: 5 };
            let float = my_union.float; // undefined behavior
        }
    }
```

### References
[Union Types](#1.2.) \
Generics \
Unsafe \
Weak keywords \
Patterns \
Borrowing \
Implementations 