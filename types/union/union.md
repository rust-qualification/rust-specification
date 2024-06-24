# 1. Types
## 1.2. Union Types <a name="union"></a>

### Syntax
   <a name="union-syntax"></a>
    
    Union ::=
        union Name GenericParameters? WhereClause? { StructFields? }

### Description
A union type is an abstract data type that is a sum of other types. Union fields share the same storage. Rust's unions are interoperable with C. The initialization and read, write operations of unions are explained in struct expression and field access expression.

### Legality Rules
1.2.1. <!-- 7f345296-9cec-4bb7-a0f1-7abf0b45bd3c --> A union without any union fields is rejected, but can still be consumed by `macros`. 

1.2.2. <!-- 6356434c-6cdb-47cd-8e99-cff31c5bef14 --> The name of a union field shall be unique within the union field list. 

1.2.3. <!-- e1c2f91e-7a68-48bd-b103-66749e82703c --> The union can accept `generic parameters`, to enable multiple different field types.

1.2.4. <!-- 93059842-a3be-4dd1-92c7-1b79f40e252f --> The union can include a `where clause` to specify constraints on the `generic parameters`. 

1.2.5. The type of a union field shall be one of the following:
- 1.2.5.1. <!-- 26ad2e4a-ff73-4eb4-b16f-d33a6e5d7e7f --> A `copy` type
- 1.2.5.2. <!-- 11a3041f-f307-4ff4-acf3-fb256baf9f49 --> A mutable `reference type`
- 1.2.5.3. <!-- 847acf71-84b6-4ace-92d8-9e127ba0911e --> `core::mem::ManuallyDrop`
- 1.2.5.4. <!-- 218f449a-7973-4157-8a92-87645b9ceedc --> A `tuple` type where all fields can hold valid union types
- 1.2.5.5. <!-- d1b5850a-f09d-4785-9d56-6ec53d7cfccf --> An `array` type with elements that can be valid union types

1.2.6. <!-- 3e3ac7d8-8bac-427d-8898-6ae9fc6277d4 --> By default, the memory layout of a union is undefined, but the `#[repr(...)]` attribute specifies a fixed layout. 

### Examples
<pre>
union MyUnion {
    f1: u32,
    f2: f32,
}
</pre>
<pre>
union GenericUnion<X, Y>
where
    X: Copy,
    Y: Copy,
{
    x: X,
    y: Y,
}
</pre>

### References
[Field Access Expressions](../../expressions/field-access-expressions/field-access-expressions.md#field-access-expressions) \
[Struct Expressions](../../expressions/struct-expressions/struct-expressions.md#struct-expressions) \
Generics \
Unsafe \
Weak keywords \
Patterns \
Type Representation \
Recursive Types \
Implementations