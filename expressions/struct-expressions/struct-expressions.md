# 2. Expressions
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

    - 2.3.2.1. A base initializer specifies an `enum` value, or a `struct` value as a base for construction in a `struct expression`. Its fields fill unmatched fields in the constructee.

    - 2.3.2.2. The type of the operand of a base initializer and the type of the constructee shall be compatible.


- 2.3.3. Indexed initializer:

    - 2.3.3.1. An indexed initializer specifies the index and initial value of a field in a `struct expression`. An indexed initializer matches a field of the constructee based on its corresponding index. Indices start from 0 and increment sequentially as decimal values. 

    - 2.3.3.2. The type of the operand of an indexed initializer and the type of the matched field shall be compatible.


- 2.3.4. Named initializer:

    - 2.3.4.1. A named initializer specifies the name and initial value of a field in a `struct expression`. A named initializer matches a field of the constructee based on its name.

    - 2.3.4.2. The type of a named initializer and the type of the matched field shall be compatible.


- 2.3.5. Shorthand initializer:

    - 2.3.5.1. A shorthand initializer specifies the name of a field in a `struct expression`. A shorthand initializer is equivalent to a named initializer with the identifier matching the field's name, which eliminates the need to write `fieldname: fieldname`.

    - 2.3.5.2. The type of a shorthand initializer and the type of the matched field shall be compatible.


2.3.6. If the constructee is a record `enum variant` or a `record struct`, then

- For each field of the constructee, the `struct expression` shall either:

    - 2.3.6.1. Contain at most one matched named initializer, or

    - 2.3.6.2. Contain at most one matched shorthand initializer, or

    - 2.3.6.3. Have exactly one base initializer.

- 2.3.6.4. A base initializer is allowed even if all fields of the constructee have been matched.



2.3.7. If the constructee is a `tuple enum variant` or a `tuple struct`, then

- For each field of the constructee, the `struct expression` shall either:

    - 2.3.7.1. Contain at most one matched indexed initializer, or

    - 2.3.7.2. Have exactly one base initializer.

- 2.3.7.3. A base initializer is allowed even if all fields of the constructee have been matched.




2.3.8. If the constructee is a [union type](#1.2.), then

- 2.3.8.1. The `struct expression` shall not contain a base initializer.

- For the single field of the constructee, the `struct expression` shall either:

    - 2.3.8.2. Contain exactly one matched named initializer, or

    - 2.3.8.3. Contain exactly one matched shorthand initializer.



2.3.9. If the constructee is a `unit enum variant` or a `unit struct`, then the `struct expression` shall have at most one base initializer.


### Runtime Semantics
2.3.10. The evaluation of a `struct expression` evaluates its operands from left to right.

### Examples
<pre>
    struct Employee {
        name: String,
        age: u16,
        salary: u32
    }

    let maria = Employee {
        name: "maria".to_string(),
        age: 50,
        salary: 50_000
    };

    let age = 45;

    let miguel = Employee {
        name: "miguel".to_string(), // named initializer
        age, // shorthand initializer
        .. maria // base initializer: same salary to maria
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
Union Types \
Generics \
Unsafe \
Weak keywords \
Patterns \
Borrowing \
Implementations