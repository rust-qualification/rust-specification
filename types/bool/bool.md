# 1. Types
## 1.1. Bool Types <a name="1.1."></a>
### Description

The boolean type, or bool, is a basic data type that appears in the `language prelude` and represents truth values in logic and Boolean algebra. Boolean values are mainly used in conditionals, `while` expressions and `boolean operations`.

### Legality Rules
- 1.1.1. There are two boolean values, `true` and `false`. The boolean value `false` has a bit pattern of `0x00`, while `true` has a bit pattern of `0x01`.
- 1.1.2. The size and alignment of a bool are both 1 byte.

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
  <!-- let byte_pattern: u8 = 0x02;
  let invalid_bool: bool = unsafe { mem::transmute(byte_pattern) };
  if invalid_bool {
    println!("This 'if' causes undefined behavior");
  } -->
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