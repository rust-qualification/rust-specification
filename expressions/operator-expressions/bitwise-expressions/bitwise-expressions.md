# 2. Expressions
### 2.4. Operator Expressions
### 2.4.2. Bitwise Expressions <a name="bitwise-expressions"></a>

### Syntax
   <a name="bitwise-expression-syntax"></a>

    BitExpression ::=
        BitAndExpression
      | BitOrExpression
      | BitXOrExpression
      | BitNotExpression
      | ShiftLeftExpression
      | ShiftRightExpression

    BitAndExpression ::=
        LeftOperand & RightOperand

    BitOrExpression ::=
        LeftOperand | RightOperand

    BitXorExpression ::=
        LeftOperand ^ RightOperand

    BitNotExpression ::=
        ! Operand

    ShiftLeftExpression ::=
        LeftOperand << RightOperand

    ShiftRightExpression ::=
        LeftOperand >> RightOperand

### Description
A bit expression computes a value by performing bit arithmetic operations on two operands.

### Legality Rules
Bit expressions are used with `integer` and [boolean](../../../types/bool/bool.md#bool) values.
Shift left and right expressions are not used with values of [bool](../../../types/bool/bool.md#bool) type.

BitAnd: bit and
- The type of the left operand of a bit and expression shall implement the `core::ops::BitAnd` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit AND expression shall be `core::ops::BitAnd::Output`.

- The value of a bit AND expression shall be the result of `core::ops::BitAnd::bitand(left_operand, right_operand)`.




`BitOr`: bit or
- The type of the left operand of a bit or expression shall implement the `core::ops::BitOr` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit OR expression shall be `core::ops::BitOr::Output`.

- The value of a bit OR expression shall be the result of `core::ops::BitOr::bitor(left_operand, right_operand)`.



`BitXor`: bit exclusive

- The type of the left operand of a bit xor expression shall implement the `core::ops::BitXor` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a bit XOR expression shall be `core::ops::BitXor::Output`.

- The value of a bit XOR expression shall be the result of `core::ops::BitXor::bitxor(left_operand, right_operand)`.



`BitNot`: negation

- The type of the operand of a bit negation expression shall implement the `core::ops::Not` trait.

- The type of a bit negation expression shall be `core::ops::Not::Output`.

- The value of a bit negation expression shall be the result of `core::ops::Not::not(operand)`.



`Shift left expression`: shift left arithmetic

- The type of the left operand of a shift left expression shall implement the `core::ops::Shl` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a shift left expression shall be `core::ops::Shl::Output`.

- The value of a shift left expression shall be the result of `core::ops::Shl::shl(left_operand, right_operand)`.



`Shift right expression`: Arithmetic right shift on signed integer types, logical right shift on unsigned integer types.

- The type of the left operand of a shift right expression shall implement the `core::ops::Shr` trait and the type of the right operand shall be the trait implementation type parameter.

- The type of a shift right expression shall be `core::ops::Shr::Output`.

- The value of a shift right expression shall be the result of `core::ops::Shr::shr(left_operand, right_operand)`.


<!-- e420b920-c632-48bb-ab6c-e3f069f3b893 --> The following operations are defined for [bool](../../../types/bool/bool.md#bool): <a name="bitwise-tables"></a>


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

The evaluation of a bit and expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitAnd::bitand(left_operand, right_operand)` is called.



The evaluation of a bit or expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitOr::bitor(left_operand, right_operand)` is called.



The evaluation of a bit xor expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::BitXor::bitxor(left_operand, right_operand)` is called.



The evaluation of a bitwise negation expression has the following steps:

- The operand is assessed.

- If the operand is of an integer type, the negation expression results in the bitwise negation of that operand.

- If the operand is of type [bool](../../../types/bool/bool.md#bool), negation results in false if the operand is true, and vice versa.

- If the type of operand is neither an integer nor [bool](../../../types/bool/bool.md#bool), then `core::ops::Not::not(operand)` is called.



The evaluation of a shift left expression has the following steps:

- The left operand is assessed.

- The right operand is assessed.

- `core::ops::Shl::shl(left_operand, right_operand)` is called.



The evaluation of a shift right expression has the following steps:

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
[Boolean Literal Expressions](../../../types/bool/bool.md#boolean-literal) 
If Expressions \
While Loops Expressions 