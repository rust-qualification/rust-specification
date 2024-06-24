# 1. Types
## 1.1. Bool Types <a name="bool"></a>
### Description

The boolean type, or bool, is a basic data type that appears in the `language prelude` and represents truth values in logic and Boolean algebra. Boolean values can be used in `conditionals`, `while` expressions and `boolean operations`.

### Legality Rules
1.1.1. <!-- ee7018f0-eca6-4ec1-b645-ffb98940f3ac --> There are two boolean values, `true` and `false`. The boolean value `false` has a bit pattern of `0x00`, while `true` has a bit pattern of `0x01`.  
1.1.2. <!-- 415bc9ad-19fb-4b7f-9423-8656c289a6ab --> The size and alignment of a bool are both 1 byte. 

### Undefined Behavior
It is undefined behavior for a boolean variable to have any bit pattern other than `0x00` or `0x01`. 

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
```
  while condition1 | condition2 {
    // Loop body
  }
```
```
  let byte_pattern: u8 = 0x02;
  let invalid_bool: bool = unsafe { mem::transmute(byte_pattern) };
  if invalid_bool {
    println!("This 'if' causes undefined behavior");
  } 
```

### References
[Boolean Literal Expressions](#boolean-literal) \
[Lazy Boolean Expressions](../../expressions/operator-expressions/lazy-boolean-expressions/lazy-boolean-expressions.md#lazy-boolean-expressions) \
[Bitwise Expressions](../../expressions/operator-expressions/bitwise-expressions/bitwise-expressions.md#bitwise-expressions) \
[Comparison Expressions](../../expressions/operator-expressions/comparison-expressions/comparison-expressions.md#comparison-expressions) \
Type Cast Expressions \
If Expressions \
While Loops Expressions 


# 2. Expressions
## 2.1. Literal Expressions
### 2.1.1. Boolean Literal Expressions <a name="boolean-literal"></a>


### Syntax
   <a name="boolean-literal-syntax"></a>
    
    BooleanLiteral ::= 
        true 
      | false 

### Description
A boolean literal represents the truth values in logic and Boolean algebra.

### Legality Rules
2.1.1.1. <!-- 4980f9e0-3291-41ac-bef8-21acdf3545ba --> 
The type of a boolean literal is [bool](#bool).

### Examples
`
  true
` \
`
  false
`

### References
[Bool Types](#bool) \
[Lazy Boolean Expressions](../../expressions/operator-expressions/lazy-boolean-expressions/lazy-boolean-expressions.md#lazy-boolean-expressions) \
[Bitwise Expressions](../../expressions/operator-expressions/bitwise-expressions/bitwise-expressions.md#bitwise-expressions) \
[Comparison Expressions](../../expressions/operator-expressions/comparison-expressions/comparison-expressions.md#comparison-expressions) \
Type Cast Expressions \
If Expressions \
While Loops Expressions 