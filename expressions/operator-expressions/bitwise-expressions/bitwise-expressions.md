# 2. Expressions
### 2.2. Operator Expressions
### 2.2.3. Bitwise Expressions <a name="2.2.3."></a>

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
A bit expression is an expression that computes a value from two operands using bit arithmetic.
### Legality Rules

They are used with primitive types, bitwise and, or, xor, not are also used with bools.

BitAnd: bit and
- The type of the left operand of a bit and expression shall implement the core::ops::BitAnd trait where the type of the right operand is the trait implementation type parameter.

- The type of a bit and expression is associated type core::ops::BitAnd::Output.

- The value of a bit and expression is the result of core::ops::BitAnd::bitand(left_operand, right_operand).




BitOr: bit or
- The type of the left operand of a bit or expression shall implement the core::ops::BitOr trait where the type of the right operand is the trait implementation type parameter.

- The type of a bit or expression is associated type core::ops::BitOr::Output.

- The value of a bit or expression is the result of core::ops::BitOr::bitor(left_operand, right_operand).



BitXor: bit exclusive

- The type of the left operand of a bit xor expression shall implement the core::ops::BitXor trait where the type of the right operand is the trait implementation type parameter.

- The type of a bit xor expression is associated type core::ops::BitXor::Output.

- The value of a bit xor expression is the result of core::ops::BitXor::bitxor(left_operand, right_operand).



BitNot: negation

- The type of the operand of a negation expression with a BitwiseNegationOperator shall implement the core::ops::Not trait.

- The type of a negation expression with a BitwiseNegationOperator is associated type core::ops::Not::Output.

- The value of a negation expression with a BitwiseNegationOperator is the result of core::ops::Not::not(operand).



Shift left expression: shift left arithmetic

- The type of the left operand of a shift left expression shall implement the core::ops::Shl trait where the type of the right operand is the trait implementation type parameter.

- The type of a shift left expression is associated type core::ops::Shl::Output.

- The value of a shift left expression is the result of core::ops::Shl::shl(left_operand, right_operand).



Shift right expression: Arithmetic right shift on signed integer types, logical right shift on unsigned integer types.

- The type of the left operand of a shift right expression shall implement the core::ops::Shr trait where the type of the right operand is the trait implementation type parameter.

- The type of a shift right expression is associated type core::ops::Shr::Output.

- The value of a shift right expression is the result of core::ops::Shr::shr(left_operand, right_operand).


1.1.4. For bool:

### 1.1.4.1. Bitwise NOT 

| b     | !b    |
|-------|-------|
| true  | false |
| false | true  |


### 1.1.4.2. Bitwise OR 

| a     | b     | a \| b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


### 1.1.4.3. Bitwise AND 

| a     | b     | a & b  |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | false  |

### 1.1.4.4. Bitwise XOR

| a     | b     | a ^ b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |

### Runtime Semantics

The evaluation of a bit and expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::ops::BitAnd::bitand(left_operand, right_operand) is invoked.



The evaluation of a bit or expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::ops::BitOr::bitor(left_operand, right_operand) is invoked.



The evaluation of a bit xor expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::ops::BitXor::bitxor(left_operand, right_operand) is invoked.



The evaluation of a negation expression with a BitwiseNegationOperator proceeds as follows:

- The operand is evaluated.

- If the type of the operand is an integer type, then the negation expression evaluates to the bitwise negation of the operand.

- If the type of the operand is bool, then the result is computed as follows, depending on the value of the operand:

- If the type of operand is neither an integer type nor bool, then core::ops::Not::not(operand) is invoked.



The evaluation of a shift left expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::ops::Shl::shl(left_operand, right_operand) is invoked.



The evaluation of a shift right expression proceeds as follows:

- The left operand is evaluated.

- The right operand is evaluated.

- core::ops::Shr::shr(left_operand, right_operand) is invoked.

### Examples
```
    0b1010 & 0b1100
    0b1010 | 0b0011
    0b1010 ^ 0b1001
    13 << 3
    -10 >> 2
    true & false
    !false
    -42
```
### References
