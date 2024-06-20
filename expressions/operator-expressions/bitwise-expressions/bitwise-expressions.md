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


1.1.4. The following operations are defined for bool:

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
### Undefined Behavior
### Examples
### References
