# 1. Types
## 1.1. Bool Types <a name="1.1."></a>
### Description

The boolean type, or bool, is a basic data type that represents truth values in logic and Boolean algebra. Boolean values are mainly used in conditionals, in if and while expressions.

### Legality Rules
- 1.1.1. The boolean value false has a bit pattern of 0x00, while true has a bit pattern of 0x01.
- 1.1.2. The size and alignment of a bool are both 1 byte.
- 1.1.3. True is transmuted to 1 and false is transmuted to 0. 
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

1.1.4.7. ` a != b is the same as !(a == b)` \
1.1.4.8. ` a >= b is the same as a == b | a > b` \
1.1.4.9. ` a < b is the same as !(a >= b)` \
1.1.4.10. ` a <= b is the same as a == b | a < b`



### Undefined Behavior
It is undefined behavior for a boolean variable to have any bit pattern other than 0x00 or 0x01. Transmuting a 'u8' to a 'bool' can lead to such invalid boolean values.


### Examples
`
  let x: bool = false;  // explicit type declaration
  let y = true;
`
```
  if x & y {
    println!("they are both true");
  } else {
    println!("they are not both true");
  }
```

### References
[Boolean Literal Expressions](#2.1.1.) \
[Lazy Boolean Expressions](#2.2.1.) \
Type Cast Expressions \
If Expressions \
While Loops Expressions 


# 2. Expressions
## 2.1. Literal Expressions
### 2.1.1. Boolean Literal Expressions <a name="2.1.1."></a>


### Syntax
   <a name="boolean-literal-syntax"></a>
    
    BooleanLiteral ::= 
        true 
      | false 

### Description
A boolean literal represents the truth values in logic and Boolean algebra.

### Legality Rules
2.1.1.1. The type of a boolean literal is [bool](#1.1.).

### Examples
`
  true
` \
`
  false
`

### References
[Bool Types](#1.1.) \
[Lazy Boolean Expressions](#2.2.1.) \
Type Cast Expressions




### 2.2. Operator Expressions
### 2.2.1. Lazy Boolean Expressions <a name="2.2.1."></a>

### Syntax
   <a name="lazy-boolean-expression-syntax"></a>

    LazyBooleanExpression ::= 
        LazyAndExpression
      | LazyOrExpression

    LazyAndExpression ::= 
        BooleanExpression && BooleanExpression

    LazyOrExpression ::= 
        BooleanExpression || BooleanExpression


### Description
The operators || and && represent logical 'or' and logical 'and', between operands of [boolean type](#1.1.). They differ from | and & because they only evaluate the right-hand operand if necessary. Specifically, || evaluates the right operand only if the left is false, and && evaluates the right operand only if the left is true. Thus, a lazy boolean expression performs short-circuit Boolean evaluation.


### Legality Rules
2.2.1.1. The operands of a lazy boolean expression must be of [bool type](#1.1.). \
2.2.1.2. The type of a lazy boolean expression is [bool](#1.1.). \
2.2.1.3. A lazy AND expression uses short-circuit AND logic. \
2.2.1.4. A lazy OR expression uses short-circuit OR logic. 

### Runtime Semantics
2.2.1.5. The evaluation of a lazy AND expression: \
The left operand is evaluated first. 
- If the left operand is true, the right operand is evaluated and returned as the value of the lazy AND expression.
- If the left operand is false, the expression evaluates to false. 

2.2.1.6. The evaluation of a lazy OR expression: \
The left operand is evaluated first. 
- If the left operand is false, the right operand is evaluated and returned as the value of the lazy OR expression.
- If the left operand is true, the expression evaluates to true.

### Examples
```
  let x = false || true; // true 
  let y = false && panic!(); // false, doesn't evaluate `panic!()` 
```

### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.) 