# 2. Expressions
## 2.3. Struct Expressions <a name="struct-expression"></a>

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

2.3.1. <!-- b730fdae-7557-43a0-b8b8-08b6999519c5 --> The type of a struct expression is the type of the constructee.

There are the following types of initializers:
- 2.3.2. Base initializer:

    - 2.3.2.1. <!-- f80fa0d8-b7af-4813-9bcf-c93180afaff8 --> A base initializer specifies an `enum` value, or a `struct` value as a base for construction in a `struct expression`. Its fields fill unmatched fields in the constructee.

    - 2.3.2.2. <!-- 56373834-34cc-41e2-a1f7-71528396212e --> The type of the operand of a base initializer and the type of the constructee shall be compatible.


- 2.3.3. Indexed initializer:

    - 2.3.3.1. <!-- b28816f0-4bff-4d4c-9d91-2325ec1c6c64 --> An indexed initializer specifies the index and initial value of a field in a `struct expression`. An indexed initializer matches a field of the constructee based on its corresponding index. Indices start from 0 and increment sequentially as decimal values. 

    - 2.3.3.2. <!-- 886d3a44-fcba-466d-ab0d-ab8bdc418555 --> The type of the operand of an indexed initializer and the type of the matched field shall be compatible.


- 2.3.4. Named initializer:

    - 2.3.4.1. <!-- faea36c2-0a93-4e1c-acd1-62272765b648 --> A named initializer specifies the name and initial value of a field in a `struct expression`. A named initializer matches a field of the constructee based on its name.

    - 2.3.4.2. <!-- f3930897-1745-4c56-9481-be35348298d5 --> The type of a named initializer and the type of the matched field shall be compatible.


- 2.3.5. Shorthand initializer:

    - 2.3.5.1. <!-- b25dfa42-3096-48c8-bd1e-274facf0a535 --> A shorthand initializer specifies the name of a field in a `struct expression`. A shorthand initializer is equivalent to a named initializer with the identifier matching the field's name, which eliminates the need to write `fieldname: fieldname`.

    - 2.3.5.2. <!-- bff40a5f-511f-4c3d-9455-74e279feed66 --> The type of a shorthand initializer and the type of the matched field shall be compatible.


2.3.6. If the constructee is a record `enum variant` or a `record struct`, then

- For each field of the constructee, the `struct expression` shall either:

    - 2.3.6.1. <!-- fd69399b-a526-4a5e-b9e5-4613ee3ebefb --> Contain at most one matched named initializer, or

    - 2.3.6.2. <!-- 501b97ab-69cb-4635-b36f-33cb5bfb13b3 --> Contain at most one matched shorthand initializer, or

    - 2.3.6.3. <!-- ffa5945e-1bb5-44df-aa1c-237f618477da --> Have exactly one base initializer.

- 2.3.6.4. <!-- 0266f04f-a627-4003-85fc-b0699e2cfc7a --> A base initializer is allowed even if all fields of the constructee have been matched.



2.3.7. If the constructee is a `tuple enum variant` or a `tuple struct`, then

- For each field of the constructee, the `struct expression` shall either:

    - 2.3.7.1. <!-- 0ac502a1-d910-4eed-afb6-de9c7c6b5cee --> Contain at most one matched indexed initializer, or

    - 2.3.7.2. <!-- 0e4de00d-138e-465b-bcbf-451b9b532055 --> Have exactly one base initializer.

- 2.3.7.3. <!-- 7ab47a32-86f1-4f00-9b07-1ed48aadcb2e --> A base initializer is allowed even if all fields of the constructee have been matched.




2.3.8. If the constructee is a [union type](#union), then

- 2.3.8.1. The `struct expression` shall not contain a base initializer.

- For the single field of the constructee, the `struct expression` shall either:

    - 2.3.8.2. <!-- 123a48b7-d1ea-4efb-a53b-1f89cb837195 --> Contain exactly one matched named initializer, or

    - 2.3.8.3. <!-- 787ef148-019a-4599-b0f2-e155512cab99 --> Contain exactly one matched shorthand initializer.



2.3.9. <!-- a63297aa-a4d1-4ae1-819e-66b9c43ce432 --> If the constructee is a `unit enum variant` or a `unit struct`, then the `struct expression` shall have at most one base initializer.


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