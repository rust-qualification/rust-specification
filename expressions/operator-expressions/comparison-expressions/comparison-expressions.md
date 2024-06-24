# 2. Expressions
### 2.4. Operator Expressions
### 2.4.3. Comparison Expressions <a name="comparison-expressions"></a>

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
A bit expression computes a value by comparing two operands. These operands can be of primitive types or other standard library types and data structures such as tuples, structs, arrays, and vectors.

### Legality Rules
2.4.3.1. A comparison expression compares the values of two operands.

2.4.3.2. A comparison expression implicitly takes shared borrows of its operands.

2.4.3.3. The type of a comparison expression is of type `bool`.

2.4.3.4. Both operands in these expressions should be of the same type, even within the same category of integers. 

2.4.3.5. Some specific comparison rules for different primitive types:
- 2.4.3.5.1. `Chars` are compared lexicographically.
- 2.4.3.5.2. `Strings` are compared lexicographically, character by character
- 2.4.3.5.3. `Numbers` are compared on their numerical values.
- 2.4.3.5.4. `Bools` are compared based on the following [tables](#comparison-tables). 

2.4.3.6. `Pointers` and `references` can also be compared, only using the equality and inequality expressions.

2.4.3.7. When chaining comparison operators, parentheses are required. For example, the expression a == b == c is invalid and should be written as (a == b) == c. 

There are the following comparison expressions:
2.4.3.8. `==`:
- An `equals` expression checks equality.
- The type of the left operand of an equals expression shall implement the `core::cmp::PartialEq` trait and the type of the right operand is the trait implementation type parameter.
- The value of an equals expression is the result of `core::cmp::PartialEq::eq(&left_operand, &right_operand)`.

2.4.3.9. `>`:
- A `greater-than` expression checks for a greater-than relationship.
- The type of the left operand of a greater-than expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a greater-than expression is the result of `core::cmp::PartialOrd::gt(&left_operand, &right_operand)`.

2.4.3.10. `>=`:
- A `greater-than-or-equals` expression checks for a greater-than-or-equals relationship.
- The type of the left operand of a greater-than-or-equals expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a greater-than-or-equals expression is the result of `core::cmp::PartialOrd::ge(&left_operand, &right_operand)`.

2.4.3.11. `<`:
- A `less-than` expression checks for a less-than relationship.
- The type of the left operand of a less-than expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a less-than expression is the result of `core::cmp::PartialOrd::lt(&left_operand, &right_operand)`.

2.4.3.12. `<=`:
- A `less-than-or-equals` expression checks for a less-than-or-equals relationship.
- The type of the left operand of a less-than-or-equals expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a less-than-or-equals expression is the result of `core::cmp::PartialOrd::le(&left_operand, &right_operand)`.

2.4.3.13. `!=`:
- A `not-equals` expression checks for inequality.
- The type of the left operand of a not-equals expression shall implement the `core::cmp::PartialEq` trait and the type of the right operand is the trait implementation type parameter.
- The value of a not-equals expression is the result of `core::cmp::PartialEq::ne(&left_operand, &right_operand)`.

2.4.3.14. The following operations are defined for bool: <a name="comparison-tables"></a>
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
The evaluation of an `equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialEq::eq(&left_operand, &right_operand)` is called.



The evaluation of a `greater-than` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::gt(&left_operand, &right_operand)` is called.



The evaluation of a `greater-than-or-equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::ge(&left_operand, &right_operand)` is called.



The evaluation of a `less-than` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::lt(&left_operand, &right_operand)` is called.



The evaluation of a `less-than-or-equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::le(&left_operand, &right_operand)` is called.



The evaluation of an `inequality` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialEq::ne(&left_operand, &right_operand)` is called.

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
[Bool Types](#bool) \
[Boolean Literal Expressions](#boolean-literal)  