# 1. Types
## 1.2. Union Types <a name="1.2."></a>

### Syntax
   <a name="union-syntax"></a>
    
    Union ::=
        union Identifier GenericParameters? WhereClause? { StructFields? }

### Description
A union type is an abstract data type that is a sum of other types, similar to the C union.

### Legality Rules
1.2.1. A union's size is determined by the size of its largest field.

1.2.2. A union without any union fields is rejected, but can still be consumed by macros. 

1.2.3. The name of a union field shall be unique within the union field list. 

1.2.4. The type of a union field shall be one of the following:
- 1.2.4.1. A copy type
- 1.2.4.2. A mutable reference type
- 1.2.4.3. core::mem::ManuallyDrop
- 1.2.4.4. A tuple type where all fields can hold valid union types
- 1.2.4.5. An array type with elements that can be valid union types

1.2.5. By default, the memory layout of a union is undefined, but the #[repr(...)] attribute specifies a fixed layout. 

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
Recursive Types

# 2. Expressions
## 2.2. Field Access Expressions <a name="2.2."></a>


### Syntax
   <a name="field-access-expression-syntax"></a>

    FieldAccessExpression ::=
        Expression.FieldSelector

    FieldSelector ::=
        DecimalLiteral
      | Name

### Description
A field access expression is an expression used to access a field of a value from a data structure like structs, unions, enums, traits, or tuples.
The container operand indicates the value from which the field is accessed and a field selector determines which field of the container is selected.

### Legality Rules
2.2.1. The type of a field access expression corresponds to the type of the field that is selected for access.

2.2.2. Reading the selected field of a union shall require the use of an unsafe context.

2.2.3. Writing to the selected field of a union where the type of the selected field implements the core::marker::Copy trait or the core::mem::ManuallyDrop trait shall not require unsafe context.

2.2.4. Writing to and then reading from the selected field of a union subject to attribute repr is equivalent to invoking function core::mem::transmute<write_type, read_type>(field_bits):
- write_type is the type used at the time of writing the selected field
- read_type is the type used at the time of reading the selected field, and 
- field_bits is the bit representation of the selected field.

### Runtime Semantics
2.2.5. Evaluating a field access expression involves evaluating its container operand.

### Undefined Behavior
Reading a selected field of a union type when the union contains data that is invalid for that field's type results in undefined behavior.

### Examples
`
    let f = unsafe { myUnion.myField }; // accessing a union field
` \
`
    ("hi", 14, false).1 // accessing a tuple field
`

### References
[Union Types](#1.2.) \
[Struct Expressions](#2.3.) \
Generics \
Unsafe \
Weak keywords \
Patterns \
Borrowing 