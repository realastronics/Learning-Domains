# JAVA

Java is a **high-level, statically typed, object-oriented programming language** developed by Sun Microsystems (now Oracle). It is designed to be **portable, secure, and scalable**.

Object-oriented programming models software as interacting objects that **encapsulate data and behavior**, improving structure, reuse, and maintainability.

### 1) Java Platform Components

- **JVM (Java Virtual Machine)**: Executes bytecode and manages memory
- **JRE (Java Runtime Environment)**: JVM + core libraries (for running programs)
- **JDK (Java Development Kit)**: JRE + compiler and development tools (for writing programs)

Basic Syntax:

```java
class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java");
    }
}
```

**Explanation of syntax:**

1. public - makes the method accessible from anywhere, the JVM must be able to call it outside the class. If not public, the **program** won’t run.
2. static - belongs to the class and tells the JVM this method can be called for execution without creating an object
3. void - is to declare the method returns nothing
4. main - is a special method name from where the JVM starts execution of the program
5. String[] args - stores command line arguments allowing the data to be passed when running the program.

### 2) Variable Types in JAVA

**Primitive variables** store the actual data value directly in memory (such as `int`, `double`, and `boolean`). Assigning one primitive variable to another copies the value, so changes to one do not affect the other. Primitives are fast and are mainly used for simple data like numbers, characters, and logical values. These are stored in the stack.

**Non-primitive/reference variables** store a reference/address to an object in memory rather than the data itself. Examples include `String`, arrays, and objects of classes.

When a reference variable is assigned to another, both point to the same object, so changes affect both references. Reference types allow Java to model complex data and support object-oriented programming. Reference variables themselves are stored on the stack, _while the objects they point to are stored on the heap_

### 3) Java Portability & WORA

**Java is portable** because it _does not compile directly to machine code_. Instead, Java source code is compiled into **bytecode**, which is **platform-independent**.

This bytecode is executed by the **Java Virtual Machine (JVM)**. Each operating system has its own JVM, which converts bytecode into native machine instructions.

Because of this, the same Java program can run on any system that has a JVM. This is called **Write Once, Run Anywhere (WORA)**.

**Summary:** Java’s portability comes from bytecode + JVM, not the OS.

### 4) Data Types in JAVA

|Data Type|Size|Range / Description|
|---|---|---|
|`byte`|1 byte|−128 to 127|
|`short`|2 bytes|−32,768 to 32,767|
|`int`|4 bytes|−2³¹ to 2³¹−1|
|`long`|8 bytes|−2⁶³ to 2⁶³−1|
|`float`|4 bytes|~6–7 decimal digits|
|`double`|8 bytes|~15 decimal digits|
|`char`|2 bytes|Unicode character (0–65,535)|
|`bool`|JVM dependent|`true` or `false`|

### 5) Input in Java

For accepting user input in java we use a class named “Scanner” which has to be imported from the util package.

```java
import Java.until.Scanner; // this imports the Scanner class

public static void Main(Strings[] args){

		Scanner object_name = new Scanner(System.in); //this allows the program to read user input
		
		System.out.println("Enter your age ");
		int age = object_name.nextInt(); //nextInt takes integer input
		//nextLine would take String input.
		//nextBoolean would let you take true/false as input.
	}
}
```

**A ‘single’ `Scanner` object can be reused to take multiple inputs; you do not need to change the object name each time.**

### Logical Operators

|Operator|Name|Description|Example|
|---|---|---|---|
|&&|Logical and|Returns true if both statements are true|x < 5 &&  x < 10|
||||Logical or|
|!|Logical not|Reverse the result, returns false if the result is true|!(x < 5 && x < 10)|

### 6) Loops

```java
// This is the syntax of a for loop in java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Below is the while loop that requires an initial condition 

int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

**Rule:** flags must be **initialized before the loop**.

|Aspect|Flag|Check|
|---|---|---|
|What it is|Variable|Condition|
|Purpose|Store state|Test condition|
|Usually type|`boolean`|Expression|
|Lifetime|Persists|Instant|

### **7) Switch**

`switch` selects a code block to execute based on the value of an expression.

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Invalid");
}
```

### 8) Arrays

An **array** is a data structure that stores **multiple values of the same data type** in a single variable. Arrays in Java have a **fixed size.**

```java
int[] arr = {1, 2, 3, 4, 5};
String[] fruits = {"apple", "banana"}
system.out.println(fruits[]);
// this prints the entire array
// to get a specific element from the array specify it's index.
```

To find the length of an array:

```java
//gives the length of an array
int number = fruits.length; 
// we can use a loop to print all elements of an array
for (int i = o; i< fruits.length; i++){
	System.out.print(fruits[i]);
	}
```

### 9) Methods

A Java method is the same concept as a C function, except it must be defined inside a class. They must have a return type, like void or int.

Below is an example of a method in JAVA which is within the main method

If a method is being called inside a main method **(which is static)** our created method needs to be static too.

```java
    static void DoSomething(String name){
        System.out.println("Happy Birthday to " + name);
        System.out.println("Happy nigga day!!");
    }
```

methods are unfamiliar with any variables declared in other methods, and to fix that, we have:

**Parameters and Arguments**

- Parameters are variables listed in the method definition, ex - String name.
- Arguments are the actual values passed when calling the method, ex - value in name.
- Each parameter must have a defined data type.

Overloaded Methods: are methods in JAVA that share the same name but have different parameters. Method’s name + parameters = unique method signature, each method must have a unique signature, methods can have same name but not the same signature.

**Varargs:** are variable arguments

### 10) HashMap

Similar to a dictionary in Python, a feature in JAVA that’s like an add-on to an array with key: value pairing. Values can only be modified and accessed using keys

## Object Oriented Programming

**In Java, every runnable program must contain a `public static void main(String[] args)` method; without `main`, code cannot be executed directly.**

### 1) Class in Java

A **class** in Java is a **blueprint** or template used to create objects. It defines **what data an object will have** (variables/fields) and **what actions it can perform** (methods). A class itself does not occupy much memory; memory is allocated only when objects of the class are created.

### Structure of a Class

```java
classCar {
int speed;// data (fields)

voidaccelerate() {// behavior (method)
        speed +=10;
    }
}
```

- Variables → represent the state of an object
- Methods → define the behavior of an object

### ArrayLists

A resizeable array that stores objects (autoboxing).

### **@Override in Java**

It's an **annotation** — a label you put above a method to tell the compiler:

_"I intend this method to be overriding a method from a parent class or interface. If it doesn't actually match any parent method, throw a compile error."_

```java
@Override
public int compareTo(HeapEntry other) { ... }
```

Without `@Override` — if you typo the method name like `comareTo`, Java silently creates a brand new method instead of overriding. Your code compiles but behaves wrongly. With `@Override`, Java catches it immediately.