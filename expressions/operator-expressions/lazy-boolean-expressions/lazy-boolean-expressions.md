# 2. Expressions
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
A lazy boolean expression performs short-circuit Boolean arithmetic. 
Lazy AND expressions (&&) and lazy OR expressions (||) differ from bitwise AND (&) and bitwise OR expressions (|), because they only evaluate the right-hand operand if necessary.

### Legality Rules
2.2.1.1. The operands of a lazy boolean expression must be of [bool type](#1.1.). \
2.2.1.2. The type of a lazy boolean expression is [bool](#1.1.), and has a value of either `true` or `false`. \
2.2.1.3. A lazy AND expression uses short-circuit AND logic, with the `&&` operator. \
2.2.1.4. A lazy OR expression uses short-circuit OR logic, with the `||` operator. 

### Runtime Semantics
2.2.1.5. The evaluation of a lazy AND expression: \
The left operand is evaluated first. 
- If the left operand is `true`, the right operand is evaluated and returned as the value of the lazy AND expression.
- If the left operand is `false`, the expression evaluates to `false`. 

2.2.1.6. The evaluation of a lazy OR expression: \
The left operand is evaluated first. 
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


