# 1. Types
## 1.2. Union Types <a name="1.2."></a>

### Syntax
   <a name="union-syntax"></a>
    
    Union ::=
        union Name GenericParameters? WhereClause? { StructFields? }

### Description
A union type is an abstract data type that is a sum of other types, similar to the C union.

### Legality Rules
1.2.1. A union's size is determined by the size of its largest field.

1.2.2. A union without any union fields is rejected, but can still be consumed by `macros`. 

1.2.3. The name of a union field shall be unique within the union field list. 

1.2.4. The type of a union field shall be one of the following:
- 1.2.4.1. A `copy` type
- 1.2.4.2. A mutable reference type
- 1.2.4.3. `core::mem::ManuallyDrop`
- 1.2.4.4. A `tuple` type where all fields can hold valid union types
- 1.2.4.5. An `array` type with elements that can be valid union types

1.2.5. By default, the memory layout of a union is undefined, but the `#[repr(...)]` attribute specifies a fixed layout. 

### Runtime Semantics
1.2.6. The characteristic of unions is that all fields share the same storage. Consequently, writing to one field of a union can overwrite its other fields.


### Examples
<pre>
union MyUnion {
    f1: u32,
    f2: f32,
}
</pre>

### References
[Field Access Expressions](#2.2.) \
[Struct Expressions](#2.3.) \
Generics \
Unsafe \
Weak keywords \
Patterns \
Type Representation \
Recursive Types \
Implementations

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

2.2.2. Reading the selected field of a union shall require the use of an `unsafe context`.

2.2.3. Writing to the selected field of a union where the type of the selected field implements the `core::marker::Copy` trait or the `core::mem::ManuallyDrop` trait shall not require `unsafe context`.

2.2.4. Writing to and then reading from the selected field of a union subject to attribute `repr` is equivalent to invoking function `core::mem::transmute<write_type, read_type>(field_bits)`:
- `write_type` is the type used at the time of writing the selected field
- `read_type` is the type used at the time of reading the selected field, and 
- `field_bits` is the bit representation of the selected field.

2.2.5. In `tuples`, fields are accessed using an index corresponding to each field. Tuple indices start from 0 and increment sequentially as decimal values. Leading zeros are not allowed. 

2.2.6. For `structs` and `unions`, the field selector corresponds to the name of the selected field.

### Runtime Semantics
2.2.7. Evaluating a field access expression involves evaluating its container operand.

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




## 2.3. Struct Expressions <a name="2.3."></a>


### Syntax
   <a name="struct-expression-syntax"></a>

    StructExpression ::=
        Constructee { StructExpressionData? }

    Constructee ::=
        PathExpression

    StructExpressionData ::=
        BaseInitializer
      | FieldInitializerList (, BaseInitializer | ,?)

    BaseInitializer ::=
        .. Expression

    FieldInitializerList ::=
        FieldInitializer (, FieldInitializer)*

    FieldInitializer ::=
        IndexedInitializer
      | NamedInitializer
      | ShorthandInitializer

    IndexedInitializer ::=
        FieldIndex : Expression

    NamedInitializer ::=
        Name : Expression

    ShorthandInitializer ::=
        Name


### Description
A struct expression constructs a value of a `struct`, `enum`, or `union`. It consists of a path to the `struct`, `enum` variant, or `union` item being created, followed by the field values of the item, which can be specified in any order.


### Legality Rules

2.3.1. The type of a struct expression is the type of the constructee.

There are the following types of initializers:
- 2.3.2. Base initializer:

    - 2.3.2.1. A base initializer specifies an enum value, or a struct value as a base for construction in a struct expression. Its fields fill unmatched fields in the constructee.

    - 2.3.2.2. The type of the operand of a base initializer and the type of the matched field shall be compatible.


- 2.3.3. Indexed initializer:

    - 2.3.3.1. An indexed initializer specifies the index and initial value of a field in a struct expression. An indexed initializer matches a field of the constructee based on its index.

    - 2.3.3.2. The type of the operand of an indexed initializer and the type of the matched field shall be compatible.


- 2.3.4. Named initializer:

    - 2.3.4.1. A named initializer specifies the name and initial value of a field in a struct expression. A named initializer matches a field of the constructee based on its name.

    - 2.3.4.2. The type of a named initializer and the type of the matched field shall be compatible.


- 2.3.5. Shorthand initializer:

    - 2.3.5.1. A shorthand initializer specifies the name of a field in a struct expression. A shorthand initializer is equivalent to a named initializer with the identifier matching the field's name.

    - 2.3.5.2. The type of a shorthand initializer and the type of the matched field shall be compatible.


2.3.6. If the constructee is a record `enum variant` or a `record struct`, then

- For each field of the constructee, the struct expression shall either:

    - 2.3.6.1. Contain at most one matched named initializer, or

    - 2.3.6.2. Contain at most one matched shorthand initializer, or

    - 2.3.6.2. Have exactly one base initializer.

- 2.3.6.3. A base initializer is allowed even if all fields of the constructee have been matched.



2.3.7. If the constructee is a `tuple enum variant` or a `tuple struct`, then

- For each field of the constructee, the struct expression shall either:

    - 2.3.7.1. Contain at most one matched indexed initializer, or

    - 2.3.7.2. Have exactly one base initializer.

- 2.3.7.3. A base initializer is allowed even if all fields of the constructee have been matched.




2.3.8. If the constructee is a [union type](#1.2.), then

- 2.3.8.1. The struct expression shall not contain a base initializer.

- For the single field of the constructee, the struct expression shall either:

    - 2.3.8.2. Contain exactly one matched named initializer, or

    - 2.3.8.3. Contain exactly one matched shorthand initializer.



2.3.9. If the constructee is a `unit enum variant` or a `unit struct`, then the struct expression shall have at most one base initializer.


### Runtime Semantics
2.3.10. The evaluation of a struct expression evaluates its operands from left to right.

### Examples
<pre>
    enum Role {
        Musician,
        Actor
    }

    struct Employee {
        name: String,
        age: u16,
        role: Role
        salary: u32
    }

    let maria = Employee {
        name: "maria".to_string(),
        age: 50,
        role: Role::Musician
        salary: 50_000
    };

    let age = 45;

    let miguel = Employee {
        name: "miguel".to_string(), // named initializer
        age, // shorthand initializer
        .. maria // base initializer: same salary and role to maria
    };

    union MyUnion {
        int: u32,
        float: f32
    }

    // one field at a time
    let u1 = MyUnion { int: 0 };
    let u2 = MyUnion { float: 0.0 };

</pre>

### References
[Union Types](#1.2.) \
Generics \
Unsafe \
Weak keywords \
Patterns \
Borrowing \
Implementations
