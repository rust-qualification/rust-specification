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
2.4.3.1. <!-- 35bd3b3e-959c-41d9-936d-e70c110dd8b5 --> A comparison expression implicitly takes shared borrows of its operands.

2.4.3.2. <!-- 915004e3-13c5-445a-9159-f29f39b65362 --> The type of a comparison expression is of type `bool`.

2.4.3.3. <!-- 99af6d58-c504-41dd-a325-9341bd0ae9a8 --> Both operands in these expressions should be of the same type, even within the same category of integers. 

2.4.3.4. <!-- 6c5a6810-b9b6-4095-ad98-fbc655f415d0 --> Some specific comparison rules for different primitive types:
- 2.4.3.4.1. <!-- 17b4e671-32b1-4dea-bd1c-8692e6bc6eb9 --> `Chars` are compared lexicographically.
- 2.4.3.4.2. <!-- c0bf0f1e-01cf-4657-9261-fd2dd4fef6db --> `Strings` are compared lexicographically, character by character
- 2.4.3.4.3. <!-- 6a2df541-702c-45c2-9c93-e01610846161 --> `Numbers` are compared on their numerical values.
- 2.4.3.4.4. <!-- ce008a05-6b67-4e02-85c6-38374ab3a561 --> `Bools` are compared based on the following [tables](#comparison-tables). 

2.4.3.5. <!-- 40e36ca8-a41f-4093-a3c2-8ed49161d7f6 --> `Pointers` and `references` can also be compared, only using the equality and inequality expressions.

2.4.3.6. <!-- 4eff8002-c02a-43d4-8773-ac28a98e0218 --> When chaining comparison operators, parentheses are required. For example, the expression a == b == c is invalid and should be written as (a == b) == c. 

There are the following comparison expressions:

2.4.3.7. `==` <!-- 04aa0dda-0706-44cb-9ab3-7945aeb58bb3 --> :
- An `equals` expression checks equality.
- The type of the left operand of an equals expression shall implement the `core::cmp::PartialEq` trait and the type of the right operand is the trait implementation type parameter.
- The value of an equals expression is the result of `core::cmp::PartialEq::eq(&left_operand, &right_operand)`.

2.4.3.8. `>` <!-- 9289fb9d-67b5-4f30-bf22-2b9d646677aa --> :
- A `greater-than` expression checks for a greater-than relationship.
- The type of the left operand of a greater-than expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a greater-than expression is the result of `core::cmp::PartialOrd::gt(&left_operand, &right_operand)`.

2.4.3.9. `>=` <!-- 8c9f42c4-79b2-4017-ace4-81d08549c196 --> :
- A `greater-than-or-equals` expression checks for a greater-than-or-equals relationship.
- The type of the left operand of a greater-than-or-equals expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a greater-than-or-equals expression is the result of `core::cmp::PartialOrd::ge(&left_operand, &right_operand)`.

2.4.3.10. `<` <!-- 4e4cbbd1-2bb4-40e4-b8ad-394526322e95 --> :
- A `less-than` expression checks for a less-than relationship.
- The type of the left operand of a less-than expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a less-than expression is the result of `core::cmp::PartialOrd::lt(&left_operand, &right_operand)`.

2.4.3.11. `<=` <!-- 02e86ee3-3ff4-4756-b7fb-d82534a35556 --> :
- A `less-than-or-equals` expression checks for a less-than-or-equals relationship.
- The type of the left operand of a less-than-or-equals expression shall implement the `core::cmp::PartialOrd` trait and the type of the right operand is the trait implementation type parameter.
- The value of a less-than-or-equals expression is the result of `core::cmp::PartialOrd::le(&left_operand, &right_operand)`.

2.4.3.12. `!=` <!-- ac7610ba-251c-4854-bffc-3c0b9f8fdb7c --> :
- A `not-equals` expression checks for inequality.
- The type of the left operand of a not-equals expression shall implement the `core::cmp::PartialEq` trait and the type of the right operand is the trait implementation type parameter.
- The value of a not-equals expression is the result of `core::cmp::PartialEq::ne(&left_operand, &right_operand)`.

2.4.3.13. <!-- e420b920-c632-48bb-ab6c-e3f069f3b893 --> The following operations are defined for bool: <a name="comparison-tables"></a>
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


2.4.3.14. <!-- 776d385c-c14e-4a68-a8ad-bb4170d0a41d --> ` a != b is the same as !(a == b)` \
2.4.3.15. <!-- 7eb21a55-d01d-4115-9c46-1d733586abeb --> ` a >= b is the same as a == b | a > b` \
2.4.3.16. <!-- d2b1ae2b-5b9e-4133-852c-a0433a2d3ca5 --> ` a < b is the same as !(a >= b)` \
2.4.3.17. <!-- 4c3ff96c-5612-4e32-baf8-3b97aa49a52f --> ` a <= b is the same as a == b | a < b` 

### Runtime Semantics
2.4.3.18. <!-- d6922c6a-99f3-4a86-880d-30ca8c6a6ffd --> The evaluation of an `equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialEq::eq(&left_operand, &right_operand)` is called.



2.4.3.19. <!-- 0db0958b-439a-43ce-b4ef-4e32d0d3a3e7 --> The evaluation of a `greater-than` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::gt(&left_operand, &right_operand)` is called.



2.4.3.20. <!-- 9f1414ba-1b4b-4d7f-a1f0-a092426a27fe --> The evaluation of a `greater-than-or-equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::ge(&left_operand, &right_operand)` is called.



2.4.3.21. <!-- aa51863d-72de-461d-a746-0e1048dc52a7 --> The evaluation of a `less-than` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::lt(&left_operand, &right_operand)` is called.



2.4.3.22. <!-- 5cadfee2-3331-44f2-a8f3-64264c74e81c --> The evaluation of a `less-than-or-equals` expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::cmp::PartialOrd::le(&left_operand, &right_operand)` is called.



2.4.3.23. <!-- 5aa7b5c9-8c01-41f1-9b9b-3cf089141848 --> The evaluation of an `inequality` expression has the following steps:

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
[Bool Types](../../../types/bool/bool.md#bool) \
[Boolean Literal Expressions](../../../types/bool/bool.md#boolean-literal) 