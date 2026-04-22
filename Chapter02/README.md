# Chapter 2: Working With Java Primitive Data Types

### Exam Objectives
* *Use primitives and wrapper classes*

### **2.3.1 Declare and initialize variables**

Legal declarations of variables:
```java
int m = 20; int p = m = 10; //resetting m to 10 and using the new value of m to initialize p
int a, b = 10, c = 20; //a is declared but not initialized. b and c are being declared as well as initialized
String s1 = "123", s2; //Only s1 is being initialized
```
Illegal declarations of variables:
```java
int a = 10, int b;//You can have only one type name in one statement.
int a, Object b;//You can have only one type name in one statement.
int x = y = 10;//Invalid, y must be defined before using it to initialize x.
```

### **2.3.2 Uninitialized variables and Default values**

The JVM assigns 0 (or 0.0) to all numeric variables (i.e. byte, char, short, int, long, float, and double), false to boolean variables, and null to reference variables for static and instance variables.

Any local variable should be initialized before being used, or you get a *compiler* error.

#### **Compile Time Constant**

```java
public class TestClass {
    public static void main(String[] args) throws Exception { 
        int val; //val not initialized here 
        val = 10; 
        System.out.println(val); //compiles fine
    }
}
```
Next code, shows a path that is never covered. It will not compile:
```java
public class TestClass {
    public static void main(String[] args) throws Exception {
        int val;
        int i = 0; //LINE 4
        if (i == 0) {
            val = 10;
        }
        System.out.println(val); //val may not be initialized
    }
}
```
Now, we can make some changes to fix it:
```java
public class TestClass {
    public static void main(String[] args) throws Exception {
        int val;
        final int i = 0; //LINE 4
        if (i == 0) {
            val = 10;
        }
        System.out.println(val); //val is initialized
    }
}
```
Or, we can add the missing *else* path:
```java
public class TestClass {
    public static void main(String[] args) throws Exception {
        int val;
        int i = 0; //LINE 4
        if (i == 0) {
            val = 10;
        } else {
            val = 20;
        }
        System.out.println(val); //val is initialized
    }
}
```
### **2.3.3 Assigning values to variables**

#### **Literals rules**

1. Java allows underscores between two digits in numeric literals, remember *"_"* can be placed at the beginning, end or next to a decimal dot.
```java
double d1 = 1_000__000.0; //valid: 1000000.0
double d2 = _1_000_000.0; //invalid: _ at the beginning
double d3 = 1_000_000_.0; //invalid: _ next to the decimal dot
double d4 = 1_000_000.0_; //invalid: _ at the end
```
2. Java allows numeric values to be written in hexadecimal (starts with 0x or 0X), octal (starts with 0), or binary (starts with 0b or 0B) formats.
```java
int hex = 0xF; // hexadecimal value for 15
int oct = 017; // octal value for 15
int bin = 0b1111; // binary value for 15
```
#### **Assigning value of one type to a variable of another type**

```java
byte b = 10; //b is 8 bits
char c = 'x'; //c is 16 bits
short s = 300; //s is 16 bits
int i; //i is 32 bits
long l; //l is 64 bits
float f; //f is 32 bits
double d; //d is 64 bits
//no special care is needed for any of the assignments below 
i = b;
i = s; 
l = i; 
f = i; 
d = f;
//observe that the type of the target variable is larger than the type of the source variable in all of the assignments above.
```
Assigning a smaller type to a larger type is known as _"widening conversion"_ or _"implicit widening conversion"_.

The following lines will cause a compilation error:

```java
//assuming variable declarations specified above 
c = i; 
i = l; 
b = i; 
f = d; 
// observe that the type of the target variable on the left is smaller than the type of the source variable(on the right) in all of the assignments above.
```

In the _"implicit narrowing"_, the compiler fit an int literal into a smaller variable type if it fits:
```java
byte b1 = 10; //byte is 8 bits from -128 to 127, so it can fit 10
byte b2 = 128; // error, it cannot fit the 128 value into a byte
```

The "_explicit narrowing_" or _casting_ is the way to tell the compiler that we are ensuring that the value will fit, or we do not care about the "spillage".
```java
byte b2 = (byte) 128; // b2 holds the value of -128
```