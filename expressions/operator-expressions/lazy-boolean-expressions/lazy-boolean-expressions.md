# 2. Expressions
### 2.4. Operator Expressions
### 2.4.1. Lazy Boolean Expressions <a name="2.4.1."></a>

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
Lazy AND expressions (&&) and lazy OR expressions (||) differ from bitwise AND (&) and bitwise OR expressions (|), because they only evaluate the right-hand operand if necessary. Also, lazy boolean expressions are only applicable to operands of [bool type](#1.1.).

### Legality Rules
2.4.1.1. The operands of a lazy boolean expression must be of [bool type](#1.1.). \
2.4.1.2. The type of a lazy boolean expression is [bool](#1.1.). \
2.4.1.3. A lazy AND expression uses short-circuit AND logic, with the `&&` operator. \
2.4.1.4. A lazy OR expression uses short-circuit OR logic, with the `||` operator. 


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
2.4.1.5. The evaluation of a lazy AND expression has the following steps: \
- The left operand is evaluated. 
- If the left operand is `true`, the right operand is evaluated and returned as the value of the lazy AND expression.
- If the left operand is `false`, the expression evaluates to `false`. 

2.4.1.6. The evaluation of a lazy OR expression has the following steps: \
- The left operand is evaluated. 
- If the left operand is `false`, the right operand is evaluated and returned as the value of the lazy OR expression.
- If the left operand is `true`, the expression evaluates to `true`.

### Examples
```
  let x = false || true; // true 
  let y = false && panic!(); // false, doesn't evaluate `panic!()` 
```

### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.) 