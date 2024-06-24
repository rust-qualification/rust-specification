# 2. Expressions
### 2.4. Operator Expressions
### 2.4.1. Lazy Boolean Expressions <a name="lazy-boolean-expressions"></a>

### Syntax
   <a name="lazy-boolean-expression-syntax"></a>

    LazyBooleanExpression ::= 
        LazyAndExpression
      | LazyOrExpression

    LazyAndExpression ::= 
        LeftOperand && RightOperand

    LazyOrExpression ::= 
        LeftOperand || RightOperand


### Description
A lazy boolean expression performs short-circuit Boolean arithmetic. 
Lazy AND expressions (&&) and lazy OR expressions (||) differ from bitwise AND (&) and bitwise OR expressions (|), because they only evaluate the right-hand operand if necessary. Also, lazy boolean expressions are only applicable to operands of [bool type](../../../types/bool/bool.md#bool).

### Legality Rules
2.4.1.1. <!-- 8ee2a7bd-59c9-4479-9516-5519af52aa3b -->  The operands of a lazy boolean expression must be of [bool type](../../../types/bool/bool.md#bool). \
2.4.1.2. <!-- 44418fad-561e-488e-9a04-30a4701aa735 -->  The type of a lazy boolean expression is [bool](../../../types/bool/bool.md#bool). \
2.4.1.3. <!-- 8d4fd9cd-5ef4-46e0-877d-a5194aab3f2c -->  A [lazy AND expression](#lazy-boolean-tables) uses short-circuit AND logic, with the `&&` operator. \
2.4.1.4. <!-- d05986fe-54a4-4142-93b1-fc7a557d1884 -->  A [lazy OR expression](#lazy-boolean-tables) uses short-circuit OR logic, with the `||` operator. 

2.4.1.5. The following operations are defined for bool: <a name="lazy-boolean-tables"></a>
### Lazy Boolean OR 

| a     | b     | a \|\| b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


### Lazy Boolean AND 

| a     | b     | a && b  |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | false  |
| false | false | false  |


### Runtime Semantics
2.4.1.6. <!-- 266ee141-7c6b-4738-bc33-24a72e8e3d99 --> The evaluation of a lazy AND expression has the following steps:
- The left operand is assessed. 
- If the left operand is `true`, the right operand is assessed and returned as the value of the lazy AND expression.
- If the left operand is `false`, the expression evaluates to `false`. 

2.4.1.7. <!-- 0735bf32-a30d-4a64-8ca1-8ad873bc9e04 --> The evaluation of a lazy OR expression has the following steps:
- The left operand is assessed. 
- If the left operand is `false`, the right operand is assessed and returned as the value of the lazy OR expression.
- If the left operand is `true`, the expression evaluates to `true`.

### Examples
```
  let x = false || true; // true 
  let y = false && panic!(); // false, doesn't evaluate `panic!()` 
```

### References
[Bool Types](../../../types/bool/bool.md#bool) \
[Boolean Literal Expressions](../../../types/bool/bool.md#boolean-literal) 