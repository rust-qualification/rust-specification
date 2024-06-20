# 2. Expressions
### 2.2. Operator Expressions
### 2.2.3. Comparison Expressions <a name="2.2.3."></a>

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

### Legality Rules
1.1.4. The following operations are defined for bool:
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

### 1.1.4.6. Greater Equal Than

| a     | b     | a >= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | true   |
| false | true  | false  |
| false | false | true   |


### 1.1.4.6. Less Than

| a     | b     | a < b  |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | false  |
| false | true  | true   |
| false | false | false  |

### 1.1.4.6. Less Equal Than

| a     | b     | a <= b |
|-------|-------|--------|
| true  | true  | true   |
| true  | false | false  |
| false | true  | true   |
| false | false | true   |


### 1.1.4.6. Inequality

| a     | b     | a != b |
|-------|-------|--------|
| true  | true  | false  |
| true  | false | true   |
| false | true  | true   |
| false | false | false  |


1.1.4.7. ` a != b is the same as !(a == b)` \
1.1.4.8. ` a >= b is the same as a == b | a > b` \
1.1.4.9. ` a < b is the same as !(a >= b)` \
1.1.4.10. ` a <= b is the same as a == b | a < b` 

### Runtime Semantics


### Examples
```
```

### References
[Bool Types](#1.1.) \
[Boolean Literal Expressions](#2.1.1.)  

