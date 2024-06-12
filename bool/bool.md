# 1. Types
## 1.1. Bool Types <a name="1.1."></a>
### Description

The boolean type, or bool, is a basic data type that represents truth values in logic and Boolean algebra. It is commonly used in various expressions, such as:
- Conditions in if and while expressions.
- Operands in [lazy boolean](#2.2.1.) operator expressions. 

### Compilation
- 1.1.1. The boolean value false has a bit pattern of 0x00, while true has a bit pattern of 0x01.
- 1.1.2. The size and alignment of a bool are both 1 byte.
- 1.1.3. A bool is always initialized to a valid value (meaning transmute::<bool, u8>(...) is always valid, but not the reverse as some bit patterns are invalid for bools).
- 1.1.4. The following operations are defined for bool:

### 1.1.4.1. Logical NOT 

| b     | !b    |
|-------|-------|
| true  | false |
| false | true  |


### 1.1.4.2. Logical OR 

| a     | b     | a \| b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


### 1.1.4.3. Logical AND 

| a     | b     | a & b  |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | false  |

### 1.1.4.4. Logical XOR

| a     | b     | a ^ b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |

### 1.1.4.5. Equal To

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

1.1.4.7. ` a != b is the same as !(a == b)` \
1.1.4.8. ` a >= b is the same as a == b | a > b` \
1.1.4.9. ` a < b is the same as !(a >= b)` \
1.1.4.10. ` a <= b is the same as a == b | a < b`



### Runtime


### Undefined Behavior
1.1.5. It is undefined behavior for a boolean variable to have any bit pattern other than 0x00 or 0x01.


### Examples
`
  let x: bool = false;
`

### References
[Boolean Literal Expressions](#2.1.1.) \
[Lazy Boolean Expressions](#2.2.1.)



# 2. Expressions
## 2.1. Literal Expressions
### 2.1.1. Boolean Literal Expressions <a name="2.1.1."></a>


#### Syntax
   <a name="boolean-literal-syntax"></a>
    
    BooleanLiteral ::= 
        true 
      | false 

#### Description
A boolean literal denotes the truth values in logic and Boolean algebra.

#### Compilation
2.1.1.1. The type of a boolean literal is [bool](#1.1.).

#### Examples
`
  true
` \
`
  false
`

#### References
[Bool Types](#1.1.) \
[Lazy Boolean Expressions](#2.2.1.)







### 2.2. Operator Expressions
### 2.2.1. Lazy Boolean Expressions <a name="2.2.1."></a>

#### Syntax
   <a name="lazy-boolean-expression-syntax"></a>

    LazyBooleanExpression ::= 
        LazyAndExpression
      | LazyOrExpression

    LazyAndExpression ::= 
        LeftOperand && RightOperand

    LazyOrExpression ::= 
        LeftOperand || RightOperand


#### Description
The operators || and && apply to operands of [boolean type](#1.1.). The || operator represents logical 'or', and the && operator represents logical 'and'. They differ from | and & in that they only evaluate the right-hand operand if necessary. Specifically, || evaluates the right operand only if the left is false, and && evaluates it only if the left is true. Thus, a lazy boolean expression performs short-circuit Boolean evaluation.



#### Compilation
2.2.1.1. A lazy AND expression uses short-circuit AND logic. \
2.2.1.2. A lazy OR expression uses short-circuit OR logic. \
2.2.1.3. The operands of a lazy boolean expression must be of [bool type](#1.1.). \
2.2.1.4. The type of a lazy boolean expression is [bool](#1.1.).



#### Runtime
2.2.1.5. The evaluation of a lazy AND expression: \
The left operand is evaluated first. 
- If the left operand is true, the right operand is evaluated and returned as the value of the lazy AND expression.
- If the left operand is false, the expression evaluates to false.
2.2.1.6. The evaluation of a lazy OR expression: \
The left operand is evaluated first. 
- If the left operand is false, the right operand is evaluated and returned as the value of the lazy OR expression.
- If the left operand is true, the expression evaluates to true.

#### Examples
```
  let x = false || true; // true 
  let y = false && panic!(); // false, doesn't evaluate `panic!()` 
```

#### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.) 