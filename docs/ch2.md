# Operators
**Objectives** :  
> Use primitives and wrapper classes including Math API,
parentheses,
type promotion, and casting to evaluate
arithmetic and boolean expressions

## Order precedence
| *Type*                     | **Operator**                    | **Symbols and examples**                                                   | **Evaluation**           | **Explanation**                                                                                                                                                             |
|----------------------------|---------------------------------|----------------------------------------------------------------------------|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unary                      | Post-unary operators            | `expression++`, `expression--`                                             | L->R            | Increases/Decrease the value by 1 and returns the **OLD** value                                                                                                             |
| Unary                      | Pre-unary operators             | `++expression`, `--expression`                                             | L->R            | Increases/Decrease the value by 1 and returns the **NEW** value                                                                                                                 |
| Unary                      | Other unary operators           | `-`, `!`, `~`, `+`, `(type)`                                               | R->L            | `-` negates a value,<br/>`!` logical NOT (inverts boolean value),<br/>`~` bitwise NOT (inverts bits),<br/>`+` unary plus (no effect),<br/>`(type)` casts to a specific type. |
| Unary                      | Cast                            | `(Type)reference`                                                          | R->L            | Converts a reference from one type to another.                                                                                                                              |
| Binary Arithmetic Operator | Multiplication/division/modulus | `*`, `/`, `%`                                                              | L->R            | `*` multiplies , `/` divides , `%` modulus                                                                                                                                  |
| Binary Arithmetic Operator | Addition/subtraction            | `+`, `-`                                                                   | L->R            |                                                                                                                                                                             |
| Binary Arithmetic Operator | Shift operators                 | `<<`, `>>`, `>>>`                                                          | L->R            | `<<` shifts bits left, `>>` shifts bits right (preserving sign), `>>>` shifts bits right (zero-fill, ignoring sign).                                                        |
|                            | Relational operators            | `<`, `>`, `<=`, `>=`, `instanceof`                                         | L->R            |                                                                                                                                            |
|                            | Equal to/not equal to           | `==`, `!=`                                                                 | L->R            |                                                                                                                                                                             |
|                            | Logical AND                     | `&`                                                                        | L->R            |                                                                                                                                                                             |
|                            | Logical exclusive OR            | `^`                                                                        | L->R            |                                                                                                                                                                             |
|                            | Logical inclusive OR            | `\|`                                                                       | L->R            |                                                                                                                                                                             |
|                            | Conditional AND                 | `&&`                                                                       | L->R            | Logical AND, short-circuits if the first operand is `false`.                                                                                                                |
|                            | Conditional OR                  | `\|\|`                                                                     | L->R            | Logical OR, short-circuits if the first operand is `true`.                                                                                                                  |
|                            | Ternary operators               | `boolean expression ? expression1 : expression2`                           | R->L            | Returns `expression1` if the boolean expression is true, otherwise returns `expression2`.                                                                                   |
|                            | Assignment operators            | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `^=`, `\|=`, `<<=`, `>>=`, `>>>=` | R->L            | `=` assigns a value, combined with operators like `+=`, `-=`, etc., to perform an operation and assignment simultaneously.                                                  |
|                            | Arrow operator                  | `->`                                                                       | R->L            | Used in lambda expressions to separate parameters and the body of the function.                                                                                             |


### Bitwise Complement Operator (`~`)

- The **bitwise complement** operator (`~`) flips all the 0s and 1s in a number.
- It can only be applied to **integer numeric types** such as: `byte`, `short`, `char`, `int`, `long`.

#### Rule:
To find the **bitwise complement** of a number:
> complement = `value` *  `-1` - `1`

```java
int value = 3;         // Binary (last 4 bits): 0011 (32bits : 00000000 00000000 00000000 00000011)
int complement = ~value; // Binary: 1100 (bitwise complement)
System.out.println(value);      // Output: 3
System.out.println(complement); // Output: -4 (3*-1 -1) 
```
## Binary Arithmetic Operator 
All of the arithmetic operators may be applied to any Java primitives,
with the exception of boolean.  
Furthermore, only the addition operators
`+` and `+=` may be applied to String values, which results in `String` concatenation

### Numeric promortion

-  When you’re converting from a smaller to a larger data type (ex : int to long), numeric promotion
is **automatically** applied.  
- When you’re converting from a larger to a smaller data type (long to int),
**casting is explicitly required**, else compilation error as you might loose info.
- Smaller data types, namely, byte, short, and char, **are first promoted to int** any time
   they’re used with a Java binary arithmetic operator with a variable (as opposed to a
   value), even if neither of the operands is int.
- After all promotion has occurred and the operands have the same data type, the resulting
   value will have the s**ame data type as its promoted operands**.

