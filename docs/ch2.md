# Operators
**Objectives** :  
> Use primitives and wrapper classes including Math API,
parentheses,
type promotion, and casting to evaluate
arithmetic and boolean expressions

## Order precedence

Unless overridden with parentheses, Java operators follow order of operation, listed in
Table below, by decreasing order of operator precedence.   
If two operators have the same level of precedence, then Java guarantees left-to-
right evaluation for most operators other than the ones marked in the table.

| **Operator**                    | **Symbols and examples**                                                   | **Evaluation**           | **Explanation**                                                                                                                                                              |
|---------------------------------|----------------------------------------------------------------------------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Post-unary operators            | `expression++`, `expression--`                                             | L->R            | Increases/Decrease the value by 1 and returns the **OLD** value                                                                                                              |
| Pre-unary operators             | `++expression`, `--expression`                                             | L->R            | Increases/Decrease the value by 1 and returns the **NEW** value                                                                                                              |
| Other unary operators           | `-`, `!`, `~`, `+`, `(type)`                                               | R->L            | `-` negates a value,<br/>`!` logical NOT (inverts boolean value),<br/>`~` bitwise NOT (inverts bits),<br/>`+` unary plus (no effect),<br/>`(type)` casts to a specific type. |
| Cast                            | `(Type)reference`                                                          | R->L            | Converts a reference from one type to another.                                                                                                                               |
| Multiplication/division/modulus | `*`, `/`, `%`                                                              | L->R            | `*` multiplies , `/` divides , `%` modulus                                                                                                                                   |
| Addition/subtraction            | `+`, `-`                                                                   | L->R            |                                                                                                                                                                              |
| Shift operators                 | `<<`, `>>`, `>>>`                                                          | L->R            | `<<` shifts bits left, `>>` shifts bits right (preserving sign), `>>>` shifts bits right (zero-fill, ignoring sign).                                                         |
| Relational operators            | `<`, `>`, `<=`, `>=`, `instanceof`                                         | L->R            |                                                                                                                                                                              |
| Equal to/not equal to           | `==`, `!=`                                                                 | L->R            |                                                                                                                                                                              |
| Logical AND                     | `&`                                                                        | L->R            |                                                                                                                                                                              |
| Logical exclusive OR            | `^`                                                                        | L->R            | Logical exclusive OR. Value is true only if one value is true and the other is false..                                                                                                                     |
| Logical inclusive OR            | `\|`                                                                       | L->R            |                                                                                                                                                                              |
| Conditional AND                 | `&&`                                                                       | L->R            | Logical AND, short-circuits if the first operand is `false`.                                                                                                                 |
| Conditional OR                  | `\|\|`                                                                     | L->R            | Logical OR, short-circuits if the first operand is `true`.                                                                                                                   |
| Ternary operators               | `boolean expression ? expression1 : expression2`                           | R->L            | Returns `expression1` if the boolean expression is true, otherwise returns `expression2`.                                                                                    |
| Assignment operators            | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `^=`, `\|=`, `<<=`, `>>=`, `>>>=` | R->L            | `=` assigns a value,<br>combined with operators like `+=`, `-=`, etc., to perform an operation and assignment simultaneously.                                                |
| Arrow operator                  | `->`                                                                       | R->L            | Used in lambda expressions to separate parameters and the body of the function.                                                                                              |


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

### Numeric promotion
> RULES
> 1. If two values have different data types, Java will automatically promote one of the values to the larger of the two data types.
>2. If one of the values is integral and the other is floating-point,
>   Java will automatically
>   promote the integral value to the floating-point
>   value’s data type.
>3. Smaller data types, namely, byte, short, and char, are first promoted to int any time
>   they’re used with a Java binary arithmetic operator with a **variable** (as opposed to a
>   value), even if neither of the operands is int.
>4. After all promotion has occurred and the operands have the same data type, the resulting
>   value will have the same data type as its promoted operands.

Examples :
```java
byte b = 10 + 20;// works fine because `10` and `20` are literals, so the calculation is done at **compile time** and the result fits within the range of a `byte`.

byte x = 1;
byte b = x + 20; //does not compile because `x` is a variable of type `byte`, which gets **promoted to `int`** during the addition (rule 1). The result of `x + 20` is an `int`, not a `byte`, causing a compile-time error since an `int` (rule 4) cannot be assigned to a `byte` without explicit casting.
```
## Assigning values
### Casting
> Put simply, **casting a numeric value may change the data type**, while casting an **object only changes the reference to the
object**, not the object itself.
#### Primitive casting
> Casting primitives is required any time you are going from a larger numerical
data type to a smaller numerical data type, or converting from a floating-point
number to an
integral value.

```java
int fish = 1.0; // DOES NOT COMPILE
short bird = 1921222; // DOES NOT COMPILE
int mammal = 9f; // DOES NOT COMPILE
long reptile = 192_301_398_193_810_323; // DOES NOT COMPILE
//With casting
int fish = (int)1.0;
short bird = (short)1921222; // Stored as 20678
int mammal = (int)9f;

long reptile = (long) 192301398193810323; // DOES NOT COMPILE,value is first interpreted as an int by the compiler and is out of range
long reptile = 192301398193810323L;

short mouse = 10;
short hamster = 3;
short capybara = mouse * hamster; // DOES NOT COMPILE - short promoted to int, which cannot be asssigned to short (as ajva this you want an implicit conversion from larger to smaller data type
short capybara = (short)mouse * hamster; // DOES NOT COMPILE  - cast  is applied to mouse, which become int. After, thar both operand are promoted to int because used with *. Making the result an int, which is larger than short
short capybara = (short)(mouse * hamster);//OK instruct the compiler to ignore its default behavior.
```

#### Reference casting
See next chapter.

### Compound Assignment Operator
>A glorified forms of the simple assignment operator,
with a built-in  arithmetic or logical operation that applies the left and right sides of the
statement and stores the resulting value in the variable on the left side of the statement.

> Here the compiler will **automatically cast** the resulting value to the
data type of the value on the left side of the compound operator.
```java

int camel = 2, giraffe = 3;
//BOTH ARE EQUALS : 
camel = camel * giraffe; // Simple assignment operator
camel *= giraffe; // Compound assignment operator
```
Usefull to avoid casting :
```java
long goat = 10;
int sheep = 5;
sheep = sheep * goat; // DOES NOT COMPILE - can't asign a long to an int

//Alternative 
sheep = (int)  (sheep * goat);//OK - explciit casting of long to int
//Smarter Alternative 
sheep *= goat;//OK Sheep is first casted to a long, then ;mutiplicaiton (long * long) is applied , and then results is casted to an int.
```

### Return value of assignement operator
Assignement operator also return a value !
````java
long wolf = 5;
long coyote = (wolf=3);//(wolf=3) does two things.  it sets the value of the variable wolf to be 3
//then,  it returns a value of the assignment, which is also 3.
System.out.println(wolf); // 3
System.out.println(coyote); // 3
````

## Comparing values
### Equality Operators
Depends on datatype :

| **Operator** | **Example**  | **Applies to Primitives**                                 | **Applies to Objects**                                     |
|--------------|--------------|----------------------------------------------------------|------------------------------------------------------------|
| Equality     | `a == 10`    | Returns true if the two values represent the same value   | Returns true if the two references point to the same object |
| Inequality   | `b != 3.14`  | Returns true if the two values represent different values | Returns true if the two references point to different objects |
### Relational Operators
#### instanceof Operator
>One area the exam might try to trip you up on is using instanceof with incompatible
types.  
For example, Number cannot possibly hold a String value, so the following causes a
compilation error:
```java
public void openZoo(Number time) {
if(time instanceof String) // DOES NOT COMPILE
System.out.print(time);
}
```
Calling `instanceof` on null returns false.
```java
System.out.print(null instanceof Object); // false
System.out.print(null instanceof null); // DOES NOT COMPILE
```
### Logical Operators
### Conditional Operators