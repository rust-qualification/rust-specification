# 2. Expressions
### 2.4. Operator Expressions
### 2.4.2. Bitwise Expressions <a name="bitwise-expressions"></a>

### Syntax
   <a name="bitwise-expression-syntax"></a>

    BitwiseExpression ::=
        BitwiseAndExpression
      | BitwiseOrExpression
      | BitwiseXOrExpression
      | BitwiseNotExpression
      | BitwiseShiftLeftExpression
      | BitwiseShiftRightExpression

    BitwiseAndExpression ::=
        LeftOperand & RightOperand

    BitwiseOrExpression ::=
        LeftOperand | RightOperand

    BitwiseXorExpression ::=
        LeftOperand ^ RightOperand

    BitwiseNotExpression ::=
        ! Operand

    BitwiseShiftLeftExpression ::=
        LeftOperand << RightOperand

    BitwiseShiftRightExpression ::=
        LeftOperand >> RightOperand

    LeftOperand ::=
        Expression

    RightOperand ::=
        Expression

    Operand ::=
        Expression
        
### Description
A bit expression computes a value by performing bit arithmetic operations on two operands.

### Legality Rules

2.4.2.1. <!-- 58fa3a4b-f15b-41f3-b8b3-2f607b8b8688 --> Bit expressions are used with `integer` and [boolean](../../../types/bool/bool.md#bool) values.

2.4.2.2. <!-- d7a0044c-a6c7-4a18-8b26-d6f3ff619e7b --> Except for shift left and right expressions, which are not used with values of [bool](../../../types/bool/bool.md#bool) type.



There are the following comparison expressions:


2.4.2.3. <!-- ba09332a-f44d-46e7-9dd2-38885daa3435 --> `BitAnd`:
- A bit AND expression performs bit OR arithmetic.

- The type of the left operand of a bit and expression shall implement the `core::ops::BitAnd` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit AND expression shall be `core::ops::BitAnd::Output`.

- The value of a bit AND expression shall be the result of `core::ops::BitAnd::bitand(left_operand, right_operand)`.


2.4.2.4. <!-- 071612e5-2ff0-4fe2-827b-a2eb4dbd3aaf --> `BitOr`:
- A bit OR expression performs bit OR arithmetic.

- The type of the left operand of a bit or expression shall implement the `core::ops::BitOr` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit OR expression shall be `core::ops::BitOr::Output`.

- The value of a bit OR expression shall be the result of `core::ops::BitOr::bitor(left_operand, right_operand)`.



2.4.2.5. <!-- e74c08ba-07fe-4c10-b68e-1028b289ea77 --> `BitXor`: 
- A bit XOR expression performs bit exclusive OR arithmetic.

- The type of the left operand of a bit xor expression shall implement the `core::ops::BitXor` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit XOR expression shall be `core::ops::BitXor::Output`.

- The value of a bit XOR expression shall be the result of `core::ops::BitXor::bitxor(left_operand, right_operand)`.



2.4.2.6. <!-- 4be64039-f32e-4940-bd34-05226e987c3b --> `BitNot`: 
- A negation expression performs negation to its operand.

- The type of the operand of a bit negation expression shall implement the `core::ops::Not` trait.

- The type of a bit negation expression shall be `core::ops::Not::Output`.

- The value of a bit negation expression shall be the result of `core::ops::Not::not(operand)`.



2.4.2.7. <!-- e2dcd73e-8e58-4302-ad00-a0443924c533 --> `Shift left expression`: 
- A shift left expression performs bit shift left arithmetic.

- The type of the left operand of a shift left expression shall implement the `core::ops::Shl` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a shift left expression shall be `core::ops::Shl::Output`.

- The value of a shift left expression shall be the result of `core::ops::Shl::shl(left_operand, right_operand)`.



2.4.2.8. <!-- 8ef4930a-5429-45cc-bbe1-1e651b203d39 --> `Shift right expression`: 
- A shift right expression performs bit shift right arithmetic.

- The type of the left operand of a shift right expression shall implement the `core::ops::Shr` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a shift right expression shall be `core::ops::Shr::Output`.

- The value of a shift right expression shall be the result of `core::ops::Shr::shr(left_operand, right_operand)`.



2.4.2.9. <!-- 1b093a78-f66d-4803-988c-d30851762abb --> The following operations are defined for [bool](../../../types/bool/bool.md#bool): <a name="bitwise-tables"></a>


### Bitwise NOT 

| b     | !b    |
|-------|-------|
| true  | false |
| false | true  |


### Bitwise OR 

| a     | b     | a \| b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


### Bitwise AND 

| a     | b     | a & b  |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | false  |

### Bitwise XOR

| a     | b     | a ^ b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |

### Runtime Semantics
2.4.2.10. <!-- 544fd80d-8fa9-43bf-b728-dcfa7d4ce16d --> The evaluation of a bit and expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitAnd::bitand(left_operand, right_operand)` is called.



2.4.2.11. <!-- 655da84b-0292-4b89-b976-83c49f762828 --> The evaluation of a bit or expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitOr::bitor(left_operand, right_operand)` is called.



2.4.2.12. <!-- 98d30a3d-3f93-4012-afca-19117782571c --> The evaluation of a bit xor expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitXor::bitxor(left_operand, right_operand)` is called.



2.4.2.13. <!-- b65fbcb8-1870-48f8-9181-e4cbbf9d5bd6 --> The evaluation of a bitwise negation expression has the following steps:

- The operand is assessed.

- If the operand is of an `integer` type, the negation expression results in the bitwise negation of that operand.

- If the operand is of type [bool](../../../types/bool/bool.md#bool), negation results in false, if the operand is true, and vice versa.

- If the type of operand is neither an `integer` nor [bool](../../../types/bool/bool.md#bool), then `core::ops::Not::not(operand)` is called.



2.4.2.14. <!-- 7420df68-e9e5-4e5e-9cd1-c444c3268d19 --> The evaluation of a shift left expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::Shl::shl(left_operand, right_operand)` is called.



2.4.2.15. <!-- e4b1e172-0294-4bd2-8fbf-ff03fb58a001 --> The evaluation of a shift right expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::Shr::shr(left_operand, right_operand)` is called.


### Examples
```
0b1010 & 0b1100
0b1010 | 0b0011
1 ^ 0
true & false
true | false
true ^ false
!false
10 << 2
-10 >> 2
```
### References
[Bool Types](../../../types/bool/bool.md#bool) \
[Boolean Literal Expressions](../../boolean-literal-expressions/boolean-literal-expressions.md#boolean-literal) \
If Expressions \
While Loops Expressions 