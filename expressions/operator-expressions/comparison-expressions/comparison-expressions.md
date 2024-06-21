# 2. Expressions
### 2.4. Operator Expressions
### 2.4.3. Comparison Expressions <a name="2.4.3."></a>

### Syntax
   <a name="comparison-expression-syntax"></a>

    ComparisonExpression ::=
        EqualsExpression
      | GreaterThanExpression
      | GreaterThanOrEqualsExpression
      | LessThanExpression
      | LessThanOrEqualsExpression
      | NotEqualsExpression

    EqualsExpression ::=
        LeftOperand == RightOperand

    GreaterThanExpression ::=
        LeftOperand > RightOperand

    GreaterThanOrEqualsExpression ::=
        LeftOperand >= RightOperand

    LessThanExpression ::=
        LeftOperand < RightOperand

    LessThanOrEqualsExpression ::=
        LeftOperand <= RightOperand

    NotEqualsExpression ::=
        LeftOperand != RightOperand

### Description
A bit expression computes a value by comparing two operands.

### Legality Rules

Used with primitive types.
The same types, not even integer with float, or i64 and i32.
with chars, we compare are compared lexicographically (alphabetical order for letters)
with strings, are compared lexicographically, character by character
with numbers, just compare them
with bools, just compare based on the table
true is considered greater than false.

Used also with tuples, structs, arrays. vectors

pointers, references only with equality

Parentheses are required when chaining comparison operators. For example, the expression a == b == c is invalid and may be written as (a == b) == c.

- A comparison expression is an expression that compares the values of two operands.
- A comparison expression implicitly takes shared borrows of its operands.
- The type of a comparison expression is type bool.

- An equals expression is a comparison expression that tests equality.
- The type of the left operand of an equals expression shall implement the core::cmp::PartialEq trait where the type of the right operand is the trait implementation type parameter.
- The value of an equals expression is the result of core::cmp::PartialEq::eq(&left_operand, &right_operand).

- A greater-than expression is a comparison expression that tests for a greater-than relationship.
- The type of the left operand of a greater-than expression shall implement the core::cmp::PartialOrd trait where the type of the right operand is the trait implementation type parameter.
- The value of a greater-than expression is the result of core::cmp::PartialOrd::gt(&left_operand, &right_operand).

- A greater-than-or-equals expression is a comparison expression that tests for a greater-than-or-equals relationship.
- The type of the left operand of a greater-than-or-equals expression shall implement the core::cmp::PartialOrd trait where the type of the right operand is the trait implementation type parameter.
- The value of a greater-than-or-equals expression is the result of core::cmp::PartialOrd::ge(&left_operand, &right_operand).

- A less-than expression is a comparison expression that tests for a less-than relationship.
- The type of the left operand of a less-than expression shall implement the core::cmp::PartialOrd trait where the type of the right operand is the trait implementation type parameter.
- The value of a less-than expression is the result of core::cmp::PartialOrd::lt(&left_operand, &right_operand).

- A less-than-or-equals expression is a comparison expression that tests for a less-than-or-equals relationship.
- The type of the left operand of a less-than-or-equals expression shall implement the core::cmp::PartialOrd trait where the type of the right operand is the trait implementation type parameter.
- The value of a less-than-or-equals expression is the result of core::cmp::PartialOrd::le(&left_operand, &right_operand).

- A not-equals expression is a comparison expression that tests for inequality.
- The type of the left operand of a not-equals expression shall implement the core::cmp::PartialEq trait where the type of the right operand is the trait implementation type parameter.
- The value of a not-equals expression is the result of core::cmp::PartialEq::ne(&left_operand, &right_operand).

1.1.4. The following operations are defined for bool:
### Equality

| a     | b     | a == b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | true   |


### Greater Than

| a     | b     | a > b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | false  |
| false | false | false  |

### Greater Equal Than

| a     | b     | a >= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | false  |
| false | false | true   |


### Less Than

| a     | b     | a < b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | false  |
| false | true  | true   |
| false | false | false  |

### Less Equal Than

| a     | b     | a <= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | true   |
| false | false | true   |


### Inequality

| a     | b     | a != b |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


1.1.4.7. ` a != b is the same as !(a == b)` \
1.1.4.8. ` a >= b is the same as a == b | a > b` \
1.1.4.9. ` a < b is the same as !(a >= b)` \
1.1.4.10. ` a <= b is the same as a == b | a < b` 

### Runtime Semantics
The evaluation of an equals expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialEq::eq(&left_operand, &right_operand) is called.



The evaluation of a greater-than expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::gt(&left_operand, &right_operand) is called.



The evaluation of a greater-than-or-equals expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::ge(&left_operand, &right_operand) is called.



The evaluation of a less-than expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::lt(&left_operand, &right_operand) is called.



The evaluation of a less-than-or-equals expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::le(&left_operand, &right_operand) is called.



The evaluation of an inequality expression has the following steps:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialEq::ne(&left_operand, &right_operand) is called.

### Examples
```
    2 == 2
    3 > 2
    3 >= 2
    1 < 2
    1 <= 1
    1 != 1
```

### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.)  