# Making Decisions
**Objectives** :
> -  Create program flow control constructs including if/else,
switch statements and expressions, loops, and break and continue
statements
> - Implement polymorphism and differentiate object type versus
    reference type. Perform type casting, identify object types
    using instanceof operator and pattern matching
 


# Creating Decision-Making Statements
## If
Be careful with tricky indentation : 
```java
if(hourOfDay < 11)
    System.out.println("Good Morning");//exectued only if <11
    morningGreetingCount++;//ALWAYS EXCEUTED
```
And with dataType 
```java
int hourOfDay = 1;
if(hourOfDay) { // DOES NOT COMPILE
   }
```
With **Pattern Matching** :
 - Since java 16?? Pattern Matching  allows to  not only check the type but also
introduce a variable to cast the value directly if the type check passes.
 - Note that type of the pattern variable must be a subtype of the variable on the left side of the
expression. It cannot be the same type (It cannot be the same type (as it would be pointless to create a new variable of the same type).
```java
void compareIntegers(Number number) {
    if(number instanceof Integer) {
        Integer data = (Integer)number;
        System.out.print(data.compareTo(5));
    }
}
//become
void compareIntegers(Number number) {
    if(number instanceof Integer data) {//variable data in this example is referred to as the pattern variable
        System.out.print(data.compareTo(5));
    }
}
//can also add includes expressions
void printIntegersGreaterThan5(Number number) {
    if(number instanceof Integer data && data.compareTo(5)>0)//can  filter>5
        System.out.print(data);
}

Integer value = 123;
if(value instanceof Integer) {}
        if(value instanceof Integer data) {} // DOES NOT COMPILE,  type for 'data' MUST be a subtype of Integer.
```

### Flow - Scoping
The compiler applies flow scoping when working with pattern matching.  
Flow scoping means the **variable is only in scope when the compiler can definitively determine its type**.
```java
void printIntegerTwice(Number number) {
    if (number instanceof Integer data)
        System.out.print(data.intValue());
    System.out.print(data.intValue()); // DOES NOT COMPILE - (as data is  undefined)
}
```
```java
void printIntegersOrNumbersGreaterThan5(Number number) {
    if(number instanceof Integer data || data.compareTo(5)>0)//DOES NOT COMPILE (as its checked even if number does not inherit Integer)
        System.out.print(data);
    }
    
void printIntegersAndNumbersGreaterThan5(Number number) {
    if(number instanceof Integer data && data.compareTo(5)>0)//COMPILE
        System.out.print(data);
    }
```
Tricky:
```java
void printOnlyIntegers(Number number) {
    if (!(number instanceof Integer data))
        return;
    System.out.print(data.intValue());//COMPILE !! compiler can define data scope
}
//Explanation, if we reverse the boolean expression, it is equal to 
void printOnlyIntegers(Number number) {
    if (number instanceof Integer data)
        System.out.print(data.intValue());
    else
        return;
}
```
## Switch
From java 14, case values can be combined:
```java
switch(animal) {
    case 1://BEFORE
    case 2: System.out.print("Lion");
}
switch(animal) {
    case 1,2: System.out.print("Lion");//SINCE JAVA 14
}

switch(month) {}//COMPILE - switch statement is not required contain any case statements
```
Switch is :
- allowed for 
  - int and Integer
  -  byte and Byte
  -  short and Short
  -  char and Character
  -  String
  -  enum values
  -  var (if the type resolves to one of the preceding types)
- not allowed for :
  - boolean and Boolean (not enough values)
  - long  and Long (too much values)
  - float and Float (too much values)
  - double and Double (too much values)
Case values MUST be compile-time constant values of the same data type as the switch value.
```java
final int getCookies() {
    return 4;
}
void feedAnimals(int numberOfAnimals) {
    final int bananas = 1;
    int apples = 2;
    final int cookies = getCookies();
    switch (numberOfAnimals) {
        case bananas:
        case apples: // DOES NOT COMPILE - not a constant [not marked as final] 
        case getCookies(): // DOES NOT COMPILE - method evaluated at runtime
        case cookies: // DOES NOT COMPILE - method evaluated at runtime
        case 3 * 5:
}
```

PAGE 115