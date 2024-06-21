# 1. Types
## 1.2. Union Types <a name="1.2."></a>

### Syntax
   <a name="union-syntax"></a>
    
    Union ::=
        union Name GenericParameters? WhereClause? { StructFields? }

### Description
A union type is an abstract data type that is a sum of other types. Union fields share the same storage. Rust's unions are interoperable with C. The initialization and read, write operations of unions are explained in struct expression and field access expression.

### Legality Rules
1.2.1. A union without any union fields is rejected, but can still be consumed by `macros`. 

1.2.2. The name of a union field shall be unique within the union field list. 

1.2.3. The union can accept `generic parameters`, to enable multiple different field types.

1.2.4. The union can include a `where clause` to specify constraints on the `generic parameters`. 

1.2.4. The type of a union field shall be one of the following:
- 1.2.4.1. A `copy` type
- 1.2.4.2. A mutable `reference type`
- 1.2.4.3. `core::mem::ManuallyDrop`
- 1.2.4.4. A `tuple` type where all fields can hold valid union types
- 1.2.4.5. An `array` type with elements that can be valid union types

1.2.5. By default, the memory layout of a union is undefined, but the `#[repr(...)]` attribute specifies a fixed layout. 

### Examples
<pre>
union MyUnion {
    f1: u32,
    f2: f32,
}

union GenericUnion<A, B>
where
    X: Copy,
    Y: Copy,
{
    x: X,
    y: Y,
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