# 🍵Java Notes  by Rubi raj

## 📝Index

<!-- TOC -->

* [🔍 What is Java ?](#-what-is-java-)
    * [🤔 Meaning of Java ?](#-meaning-of-java-)
* [🔍 Variables](#-variables)
* [🔍 Data Types](#-data-types)
* [🔍 JVM Memory](#-jvm-memory)
* [🔍 Naming Convention](#-naming-convention)
* [🔍 String](#-string)
    * [1️⃣ Why is String immutable❓](#1-why-is-string-immutable)
    * [2️⃣ Can we make String mutable❓](#2-can-we-make-string-mutable)
    * [3️⃣ What is String Constant Pool ?](#3-what-is-string-constant-pool-)
    * [4️⃣ String use `char[]` or `byte[]` to hold value❓](#4-string-use-char-or-byte-to-hold-value)
    * [🔹Java 8 and bellow](#java-8-and-bellow)
    * [🔹 After Java 9 (Compact Strings)](#-after-java-9-compact-strings)
    * [5️⃣ Explain internal working of concatenation❓](#5-explain-internal-working-of-concatenation)
    * [🔍 Abstract class vs Interface](#-abstract-class-vs-interface)
    * [Abstract class](#abstract-class)
    * [Interface](#interface)
    * [🔍 final vs finally vs finalize ?](#-final-vs-finally-vs-finalize-)
    * [🔍 equals() vs hashCode()](#-equals-vs-hashcode)
    * [🔍 Comparable vs Comparator](#-comparable-vs-comparator)
    * [🔹 Comparable](#-comparable)
    * [🔹 Comparator](#-comparator)
    * [🔍 How HashMap internally works ?](#-how-hashmap-internally-works-)
    * [What is Hash Collision ?](#what-is-hash-collision-)
    * [Internal Implementation](#internal-implementation)
* [🔍 Java Programs ?](#-java-programs-)
* [🔍 String Programs ?](#-string-programs-)
* [🔍 Concepts from core Java ?](#-concepts-from-core-java-)
* [🔍 Q/A](#-qa)
* [Exceptions in Java](#exceptions-in-java)
    * [ArithmeticException](#arithmeticexception)
    * [ArrayIndexOutOfBoundsException](#arrayindexoutofboundsexception)
    * [ClassNotFoundException](#classnotfoundexception)
    * [FileNotFoundException](#filenotfoundexception)
    * [IOException](#ioexception)
    * [InterruptedException](#interruptedexception)
    * [NoSuchFieldException](#nosuchfieldexception)
    * [NoSuchMethodException](#nosuchmethodexception)
    * [NullPointerException](#nullpointerexception)
    * [NumberFormatException](#numberformatexception)
    * [RuntimeException](#runtimeexception)
    * [StringIndexOutOfBoundsException](#stringindexoutofboundsexception)
    * [InputMismatchException](#inputmismatchexception)
* [Java Notes by Rubi raj Mani](#java-notes-by-rubi-raj-mani)
    * [1️⃣ How a Java Class will Load ?](#1-how-a-java-class-will-load-)
    * [3️⃣ Method Overloading vs Overriding](#3-method-overloading-vs-overriding)
        * [Hashtable vs Hashmap vs ConcurrentHashMap](#hashtable-vs-hashmap-vs-concurrenthashmap)

<!-- TOC -->

1. What is Java ?
2. OOPS
3. Variables
4. Data Types
5. JVM Memory
6. Naming convention
7. String vs String Builder vs String Buffer
8. Abstraction vs Interface
9. final vs finally vs finalize
10. equals() vs hashCode()
11. Comparable vs Comparator
12. How HashMap internally works ?

## 🔍 What is Java ?

* Java is a high level, robust, **object-oriented** and secure programming language.
* Robust, Portable, Platform-independent, Secured, High Performance, Multithreaded, Architecture Neutral,
  Object-Oriented, Interpreted, and Dynamic.
* **Author:-** James Gosling
* **Year**:- 1995

### 🤔 Meaning of Java ?

Java is an **island in Indonesia** where the first coffee was produced (called **Java coffee**). </br>
It is a kind of espresso bean. **Java name was chosen by James Gosling** while having a cup of coffee nearby his office.

## 🔍 Variables

Variable is a key to store their values. There are three types of variables.

* **Local Variable** - Declaring inside a method or block
* **Instance Variable** - Declaring inside a class
* **Static Variable** - Declaring inside a class with static keyword.

## 🔍 Data Types

* **Primitive** - byte, short, int, long, float, double, char and boolean
* **Non-Primitive** (Reference data type) String, Array

## 🔍 JVM Memory

* **Method Area** - Metadata of the class, Blueprint of the class.
    * Static variables
    * Class name
    * Immediate parent class name
    * Methods
    * Variables information
* **Heap Memory** - All objects is stored in the heap area. (**Instance variables**)
* **Stack Memory** - Thread audit information, **Reference variables.**
* **PC Registers** - Store address of **current execution thread information**. Each thread has separate PC
  Registers.
* **Native Method Stack** - Native methods are the ones that are written in some other language but integrated in the
  JDK.

## 🔍 Naming Convention

| Type          | Description                                | Example                            |
|---------------|--------------------------------------------|------------------------------------|
| **Class**     | It should start with the uppercase letter. | `public class Employee`            |
| **Interface** | It should start with the uppercase letter. | `interface Printable`              |
| **Methods**   | It should start with lowercase letter.     | `void draw()`                      |
| **Variable**  | It should start with lowercase letter.     | `id, name`                         |
| **Package**   | It should be a lowercase letter.           | `java, lang, java.util, java.lang` |
| **Constant**  | It should be in uppercase letters.         | `RED, YELLOW, MIN_AGE = 18;`       |

## 🔍 String

📝 String variable can be created in two ways. **String literal** and **String Object**

```java
// String literals | stored in String Constant Pool(SCP).
String s1 = "Hello";

// String object | stored in Heap Memory like other objects. also in SCP.
String s2 = new String("world");
```

| Feature               | String       | StringBuffer                   | StringBuilder                |
|-----------------------|--------------|--------------------------------|------------------------------|
| **Mutability**        | Immutable    | Mutable                        | Mutable                      |
| **Thread Safe**       | ❌ No         | ✅ Yes (synchronized)           | ❌ No                         |
| **Overrides euqal()** | ✅ Yes        | ❌ No  </br>(value compared ==) | ❌ No</br>(value compared ==) |
| **Memory**            | SCP and Heap | Heap                           | Heap                         |

### 1️⃣ Why is String immutable❓

* Security (used in class loading, DB URLs, etc.)
* Thread-safety by design
* String pool
* Hashcode caching (important for HashMap)

### 2️⃣ Can we make String mutable❓

No. String class is final and immutable by design.

### 3️⃣ What is String Constant Pool ?

String Constant Pool ia a special memory area designed only for Strings.
It's present inside Heap Space.

### 4️⃣ String use `char[]` or `byte[]` to hold value❓

### 🔹Java 8 and bellow

* String stored data as `char[]`.
* Each `char` = **2 bytes**
* Java uses **UTF-16**
* So every character took **2 bytes**, even if it was simple ASCII

### 🔹 After Java 9 (Compact Strings)

* Java 9 introduced **Compact Strings**, String stored data as `byte[]`.
    * `byte[] value` → actual data
    * `coder` → tells encoding type

| coder value | Meaning                  |
|-------------|--------------------------|
| 0           | LATIN1 (1 byte per char) |
| 1           | UTF16 (2 bytes per char) |

```java
final char[] value; // Always 2 bytes per character.
final byte[] value; // 1 byte (Latin1) and 2 bytes (UTF16).
```

### 5️⃣ Explain internal working of concatenation❓

**Q1**
<!-- @formatter:off -->
```java
String a = "aaa";
String b = "bbb";
String t = a + b; // execute at Runtime

System.out.println("aaabbb" == t); // Output:- false 

/* Because it's actually forming
 * String t = new StringBuilder().append(a).append(b).toString();
 * Now 't' is stored in Heap, so comparing memory make false.
 */ 
```

**Q2**

```java
String a = "Hello" + "World"; // executes at compile time

/**
 *  1. The concordination will take place at compile time.
 *  2. No StringBuilder is created, no conversion takes place, 
 *     both the literals are added together at compile time.
 *  3. The final result "Hello World" gets saved in Stirng Constant Pool.
 */
/

```
<!-- @formatter:on -->

## 🔍 Abstract class vs Interface

### Abstract class

* Contains both **abstract and non-abstract method**.
* abstract methods can have implementation details.
* Can extend class also implement interface's.

### Interface

* Only **abstract methods** are allowed (**only method signature**).
* After Java 8, **default** / **static** methods are allowed.
* Variables are by default (**public, static, final**)
* Can **extend only interface** (**multiple interface**) is possible.

## 🔍 final vs finally vs finalize ?

* **final** - Is a keyword, to define constants, to prevent inheritance, and restrict method overriding.
* **finally** - A block used with try-catch to ensure a section of code always executes.
* **finalize** - is method Called by GC before object destruction. **Deprecated in (Java 9+)**

## 🔍 equals() vs hashCode()

* They are used to compare if two objects are same or not.
* They are used in Hashing based data structures like Hashset, HashMap and HashTable.
* They are used in String.
* Both methods are part of Object class.
* `hashCode()` - It is used to create hash value for an object. **Hash means a unique integer** value that can be
  assigned to
  your object for its identification.

> Note:- As per the contract, whenever we override `equals()`, we must override `hashCode()` as well.

## 🔍 Comparable vs Comparator

### 🔹 Comparable

Comparable is an interface which provide `public int compareTo(T o);` method.
Which is useful when we want sorting in Objects.

* Class should implement Comparable interface.
* Only one sorting logic required.

For example `x.compareTo(y)`

* `x > y` value will be 1
* `x = y` value will be 0
* `x < y` value will be -1

### 🔹 Comparator

* Comparator is a Functional Interface which provide `int compare(T o1, T o2);`
* It will be declared outside the class, in `Collections.sort(List<T> list, Comparator<? super T> c)`
* We can write multiple sorting logic.
* Want runtime sorting flexibility

> **Comparable** is used to define **natural ordering inside the class** using compareTo().</br>
> **Comparator** is used to define **custom sorting logic outside the class** using compare().

In Java 8+, Comparator became powerful:

<!-- @formatter:off -->

```java
// Natural sorting
employeeList.sort(
      Comparator.comparing(Employee::getSalary)
);

// Reversed sorting
employeeList.sort(
      Comparator.comparing(Employee::getSalary).reversed()
);
```
<!-- @formatter:on -->

## 🔍 How HashMap internally works ?

> * Default capacity is **16**.
> * Internally HashMap contains **Array of LinkedList**.
> * HashMap uses **Hashing**.
> * All the key value pairs are stored in Heap, only the **Address is stored in a array bucket**.
> * put(), get(), remove() all these operations are **O(1)** Time complexity.
> * On Collision Time Complexity is **O(1 + length of LinkedList)**

### What is Hash Collision ?

Two different or same key Hash value become the same called Collision.

<!-- @formatter:off -->
```java
{"rubi":27, "kavin":23}

hash(rubi)  --> 6
hash(kavin) --> 6
// Both output value is same, this is called collision.
```
<!-- @formatter:on -->

### Internal Implementation

* Hashmap will pass **Key to Hash function**, output will be used for **indexing the array**.
* If Collision happened it will be added in LinkedList of the same index.

## 🔍 Java Programs ?

1. Leap Year
2. Armstrong Number
3. Prime Number
4. Twin Prime Number
5. Factorial of a Number
6. Fibonacci series
7. um of natural numbers
8. Integer Palindrome
9. largest of three numbers
10. swap two numbers
11. swap two numbers without using 3rd variables
12. km-meter / meter-km conversion
13. Shortest division of a Number

## 🔍 String Programs ?

1. String palindrome
2. Letter count in a sentence
3. word count in a sentence
4. remove vowels from a string
5. delete given character from a given String
6. reverse a string
7. reverse letters of word in a String
8. Print the series of given number (1 to 9) for given number of times. For example, write number 9, 3 times means 9,
   99, 999
9. Biggest number amount 3 numbers
10. Biggest number among 10 numbers
11. Biggest number among N numbers
12. Reverse letters of words in a given sentence
13. Count number of distinct letters in a given sentence
14. Get set of numbers and store in a list and sum only even numbers
15. Perform exercise 3 by storing data to arraylist and then perform
16. Assign numbers starting from 1 to 26 for English letters a to z and find out sum of a given sentence
17. Find out first N prime numbers and print in reverse order
18. Get two numbers in two different variables, swap and print output
19. Get N numbers and store in an array list. Sort the values without using inbuilt function
20. Merge two arrays and create a new array with numbers in sorted order. Should not use inbuilt function.
21. Delete given character from the given sentence
22. Delete vowels from the given sentence
23. Sort letters of a sentence in alphabetical order
24. consecutive letters // parallel letters
25. Sentence reverse
26. get numbers from user continuously if 100 means exit the program and find smallest and greatest number
27. In each word print 3rd letter
28. In each word print last letter
29. find letter without space in a sentence
30. reverse each word

## 🔍 Concepts from core Java ?

1. OOP'S concepts (Data Abstraction, Encapsulation, Inheritance, Polymorphism)
2. Basic Java constructs like loops and data types
3. String handling
4. Collection framework
5. Multithreading
6. Exception handling
7. Generics
8. Synchronisation
9. Serialisation & De-serialisation
10. Concurrent collection
11. Access specifier
12. Memory Management in java (Heap,Stack,Garbage Collections)
13. Innerclass/Outerclass
14. File Handling
15. String Inbuild Methods

## 🔍 Q/A

1. What is Stack ?
2. Garbage Collector?
3. Every array type implements the interfaces Cloneable and java.io.Serializable.
4. Shallow copy vs Deep copy
5. typecasting
6. date class
7. anagram
8. Design pattern
9. recursion
10. sorting techniques
11. searching techniques
12. webserver architecture
13. Remove duplicates from an array
14. Printing patterns
15. The square root of a number
16. Reverse array in place
17. Reverse words of sentence
18. Binary search
19. String Anagram
20. Print all permutations of String

<!-- @formatter:off -->

```java
//-------Important String Inbuild Methods--------//
String a = "some text";

charAt();

a.subString(2); // it display the string in 2nd position onwords
a.subString(2,4); // it display the 2nd position to 3rd position strings(in between Strings)

a.replace('a','f');
a.replaceAll('a','f');

a.contains('good');
a.toUpperCase();
a.toLowerCase();

a.join(" | ","Rubi","Anand",Charles); O/P :- Rubi | Anand | Charles

a="good morning to all"
a.split(" ")               O/p:- good
                                 morning
                                 to
                                 all
char c[]=a.toCharArray(); // it converts string to character arrays

a.matches("good") //it matches two strings and return boolean value
a.equals(b); //boolean result
a.equalsIgnoreCase(b);

a.startsWith("Go"); //boolean result
a.startsWith("Go",3); //boolean result
a.endsWith("od") // boolean result

a.indexof("h") // display the index num /else return -1
a.indexOf("h",3) // display the index num /else return -1
a.lastIndexOf("i") // display the index num /else return -1
a.lastIndexOf("h",3) // display the index num /else return -1
```
<!-- @formatter:on -->

## Exceptions in Java

### ArithmeticException

It is thrown when an exceptional condition has occurred in an arithmetic operation.

### ArrayIndexOutOfBoundsException

It is thrown to indicate that an array has been accessed with an illegal index. The index is either negative or greater
than or equal to the size of the array.

### ClassNotFoundException

This Exception is raised when we try to access a class whose definition is not found

### FileNotFoundException

This Exception is raised when a file is not accessible or does not open.

### IOException

It is thrown when an input-output operation failed or interrupted

### InterruptedException

It is thrown when a thread is waiting , sleeping , or doing some processing , and it is interrupted.

### NoSuchFieldException

It is thrown when a class does not contain the field (or variable) specified

### NoSuchMethodException

It is thrown when accessing a method which is not found.

### NullPointerException

This exception is raised when referring to the members of a null object. Null represents nothing

### NumberFormatException

This exception is raised when a method could not convert a string into a numeric format.

### RuntimeException

This represents any exception which occurs during runtime.

### StringIndexOutOfBoundsException

It is thrown by String class methods to indicate that an index is either negative than the size of the string

### InputMismatchException

If you are entering wrong datatype.

---

# Java Notes by Rubi raj Mani

## 1️⃣ How a Java Class will Load ?

1. Initializes **static variables**, Execute **static blocks**<br>
   📌Note: Static block **runs only once**, no matter how many objects you create.
2. Instance initialization blocks (Empty block)
3. Invoke Default Constructor, Parent class constructor is called first. super();

```text
Class loading (only once)
 ├─ Static variables
 └─ Static blocks

Object creation (every time)
 ├─ Memory allocation
 ├─ Parent constructor
 ├─ Instance variables
 ├─ Instance blocks
 └─ Constructor

```

## 3️⃣ Method Overloading vs Overriding

<!-- @formatter:off -->
 ```java
print(int i);
print(long l);
print(String string);
add(int a, int b);
add(long a, long b);
```
<!-- @formatter:on -->

### Hashtable vs Hashmap vs ConcurrentHashMap

| Hashtable | HashMap | ConcurrentHashMap |
|-----------|---------|-------------------|
| Legacy    |         |                   |

