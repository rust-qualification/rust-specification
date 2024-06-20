# 2. Expressions
### 2.2. Operator Expressions
### 2.2.3. Comparison Expressions <a name="2.2.3."></a>

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

### Legality Rules

Used with primitive types.

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
### 1.1.4.5. Equality

| a     | b     | a == b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | true   |


### 1.1.4.6. Greater Than

| a     | b     | a > b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | false  |
| false | false | false  |

### 1.1.4.6. Greater Equal Than

| a     | b     | a >= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | false  |
| false | false | true   |


### 1.1.4.6. Less Than

| a     | b     | a < b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | false  |
| false | true  | true   |
| false | false | false  |

### 1.1.4.6. Less Equal Than

| a     | b     | a <= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | true   |
| false | false | true   |


### 1.1.4.6. Inequality

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
The evaluation of an equals expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialEq::eq(&left_operand, &right_operand) is invoked.



The evaluation of a greater-than expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::gt(&left_operand, &right_operand) is invoked.



The evaluation of a greater-than-or-equals expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::ge(&left_operand, &right_operand) is invoked.



The evaluation of a less-than expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::lt(&left_operand, &right_operand) is invoked.



The evaluation of a less-than-or-equals expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialOrd::le(&left_operand, &right_operand) is invoked.



The evaluation of a not-equals expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::cmp::PartialEq::ne(&left_operand, &right_operand) is invoked.

### Examples
```
    12 == 12
    42 > 12
    42 >= 35
    42 < 109
    42 <= 42
    12 != 42
```

### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.)  

