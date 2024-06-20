# 1. Types
## 1.1. Bool Types <a name="1.1."></a>
### Description

The boolean type, or bool, is a basic data type that appears in the `language prelude` and represents truth values in logic and Boolean algebra. Boolean values are mainly used in conditionals, in `if` and `while` expressions.

### Legality Rules
- 1.1.1. The boolean value `false` has a bit pattern of `0x00`, while `true` has a bit pattern of `0x01`.
- 1.1.2. The size and alignment of a bool are both 1 byte.
- 1.1.3. `true` is transmuted to the `u8` value `1`, and `false` is transmuted to the `u8` value `0`.

### Undefined Behavior
It is undefined behavior for a boolean variable to have any bit pattern other than `0x00` or `0x01`. Transmuting a `u8` to a `bool` can lead to such invalid boolean values.


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
  let invalid_bool: bool = unsafe { mem::transmute(0x02) };
  if invalid_bool {
    println!("This causes undefined behavior");
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