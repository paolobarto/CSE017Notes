# 2/1/2022 Notes: OOP Applications

**Outline** 
* Java wrapper classes
* Class string
* Exception Handling Classes and mechancism 
* Classes for input/output from/to files

**"student learning outcomes"** 
* Java wrapper classes
* use java string class methods
* Use exception handling 
* Read write from files

---
**Each type will have a primitive type will have a wrapper class.** The wrapped primitive type will provide an interface to allow but better manipulation of the datatype.

For example:
The integer class allows for casting of a string or integer to be an object of type integer.

```js
parseInt(String, int);
///This will cast the string but with an included number system.

System.out.println("111",2);
//7

System.out.println("The maximum integer is "+Integer.MAX_VALUE);
//Proffessor scrolled down but big number

```
Calling Integer allows for use of the methods

Boxing: COnverting from primative type to warpper class 
* type (int-> Integer)

```js
//Automatic boxing
Integer[] intArray={1,2,3,};

//Automatic UNboxing 
int x = intArray[0]
```


The main use for a warpper class is to better manipulate primative types

### String class

* Class to manipulate text - String
* String Objects are immutable (cannot be changed once created)
* Wide set of methods to manipuate String objects (13 constructors and 40 methods)

#### String has lots of methods and constructors, I'm, not going to bother memorizing them.

Split(String): String[]

Returns array of the string between space.

```uml
+replaceFirst(String regex, String): String
all
split
match
```


**regex: regular expression - general pattern in the string**

### Regular Expressions
* Used to describe a general pattern in a text 
* Analyze text for specific patterns - validate user input for example

    phone number (ddd) ddd-dddd
    Social Secutriy Number ddd dd dddd

```java
"java.*" * /stands for any zero or more characters

"\\d{3}-\\d{2}-\\{4}" // \d is a single digit {2} number of digits

"[$+#%]" // any of the included characters can be used

```
Regular expressions [cheat sheet](https://www.rexegg.com/regex-quickstart.html)



```java
"2+3-5".replaceFirst("[+-*/]","%");
//returns 2%3-5

String[] items = 
"02/25/2021".split("/");
//returns items = {"02","25","2021"}

String[] tokens = 
"Java,C?C#,C++".split("[].,?,#]");


"2+3-5".matches("\\d[+-]\\d[+-]\\d");
// returns true

"2+3-5".equals("\\d[+-]\\d[+-]\\d");
//returns false

"044-03-534".matches("\\d{3}-\\d{3}-\\d{3}")


```
Examples:

```java
System.out.println("Hi,ABC, good".matches(".*ABC .*"));
//false

```
StringBuilder is a class that can create mutable classes. 

## Exceptions

* **Exceptions** - runtie error thrown by the program. - causes the program to stop immediately.
* **Handling an Exception** - Avoid immediate termination -infrom the user - continue program or exit with friendly messags. 


**Mechanisms for handling exceptions**

* **Try Block** - chode block where the excpation is thrown
* **Catch** - code block to execute when exception is thown in try


#### Catch Block

* Like a method - called when an exception is thrown in the try block
* Never returns to the try block
* Has one parameter of type throwawble, which is the super clas of all exceptions. 
  * IOexceptions and classnotfoundexception are general excpetions while other would be considered Runtime Exceptions

**Knowing specific expceptions allows for more specific catch blocks to be executed**

Class throwable has:
```java
String message;
String getMessage();
String toString();
String printStacktrace();
```

**Throwing Exceptions**
* Exceptions are thown bt speciic methods or operations (nextInt(),/)
* Programmer can use throw to "throw" their own exceptions in the code.

```java
throw new Exception("Something went Wrong");
```

Throwing new exception created can be used to check for specific entered data, as in a valid type but wrong range. 

```java
Student s = new Student();
processStudent(s);

processStudent(new Student());
//parameter would be considered an anaymous object

```

```java
try {

    //...
    Exception e;
    e=new Exception("Under 30.");
    throw e;
}
catch(Exception ex) {
    System.out.println(ex.getMessage);
}

```

### Creating New Exception Classes
* You can create your own exception classes
* Programmer-created excpetions must be derived from Java Exception classes
* Derived classes must have two constuctors at least

```java 

public class InvalidGPAExcpetion extendes Exception {
    
    public InvalidGPAException() {
        super("Invalid GPA Exception");
    }
    public void getMessage()
    {
        System.out.println("Gpa in invalid. GPA: "+getMessage());
    }
}

```
get notes from last chapter

# 2/3/2022 Notes: Exception Blocks continued
**To Do** 
* Finish Assignment 1 
* Check bookwork

### Multiple Catch blocks 
* Each Catch block is associated with a specific tyoe if exception (type of parameter e)
* A try block may throw exceptions of different types
* Multiple catch blocks - one for each type of exception thrown

* Order of caatch blocks matters
* From specific to general
* Follow the hierarchy of inheritance from sub classes to super classes

### Catch-Declare Rule
* nextInt() throws an exception and does not handle it-(declare rule) 
* The caller of nextInt() decides to handle the exceptino or not
* You can also create methods that throw exceptions and handle them(catch rule)

* **Declare rule** : use the clause 'throws'

```java
public void safeDIvide(int a,int b) throws DivisionByZero
```

```java
Int safeDivide(int a, int b)
    throws DizisionByZeroException
    {
        try{
        if(b==0)
            throw new DivisionByZeroException();
        else 
            return (a/b);

        }
        catch(DivisionByZeroException e {
            return 0;
        })
        
    }
```
  *  Checked Exceptions - Exception for which Java enforces the rule catch or declare
  *  Unchecked Exception - Exception not checked by java or catched 

**I/O excpetions are consifered to be Checked exceptions**

### Finally Block 
* A block after the try block and all its catch blocks 
* The finally block is always executed whether an excpetion is thrown or not

```java
igh University Spring 2022
CSE-017
57
Exception Handling public class FinallyDemo {
    public static void main(String[] args){
        try { exerciseMethod(0);}
        catch(Exception e){
        System.out.println("Caught in main.”); }
 }
 public static void exerciseMethod(int n) throws Exception {
    try{
        if (n > 0)
            throw new Exception();
        else if (n < 0)
            throw new NegativeNumberException();
        else
            System.out.println("No Exception.");
        System.out.println("Still in exerciseMethod.");
    }
    catch(NegativeNumberException e) {
        System.out.println("Caught in exerciseMethod.”);
    }
 finally{
    System.out.println("In finally block.");
    }
    System.out.println("After finally block.");
 }
}
//if n>0 
//In finally block
//Caught in main
```
#### Summary 
* Exception Handling - try - catch - throw - finally
* Deriving new exception classes
* Declare exception - throws
* Catch or declare rule - checked/unchecked exception

## File I/O 

* Accessing fiels on your hard disk or remotely
* Access file properties(size, location/folder/file..)

### Class file 
* Wraffer Class for files 
* Allow access to file properties
* Does file exist....etc

![File Class](https://gyazo.com/3fb4c2f07243e920a9c6b7c11031b95e)

### Reading/Writing to files
* open the file
* read the file
* close the file

### Open Files for reading 
* Create a Scanner object linked to a class File object- Class FIle object is linked to the file 
* Constructor Scanner(File) throws a checked FileNotFoundException

```java
File file = new File ("data.txt");
Scanner fileScanner =  new Scanner(file):
```
### Open Files for writing 
* Create a printwriter object linked to a class file object -  Class File object is linked to the file 
* PrintWriter(File) constructor throws a checked "FileNotFoundException"
  * in output means you cannont write to file

```java
File file = new File("output.txt");
PrintWriter fileWrite = new PrintWriter(file);
```

### Reading from a file
* Use a scanner methods nextInt(),
nextDouble(), next(), nextLine()

### Writing to file 
* Use Print Writer methods print(), println(), printf()

### Close Files
* close() method from class Scanner 
  ```java
  filScanner.close();
  ```
* Close() method from class PrintWriter
  ```java
  fileWrite.CLose
  ```

```java 
//needed imports for file managemnet
import java.util.Scanner;
import java.io.File;
import java.io.PrintWriter;
import java.io.IOException;
```



```java
try {
    studentCount = input.nextInt();
    studentList = new Student[studentCount];
    Scanner readFile = new Scanner(file);
    System.out.println("File opened successfully.");
    for(int i=0; i<studentCount; i++) {
        String fname, lname; int id; double gpa;
        fname = readFile.next();
        lname = readFile.next();
        id = readFile.nextInt();
        gpa = readFile.nextDouble();
        studentList[i] = new Student(fname + " " + lname, id, gpa);
        System.out.println("Student " + (i+1) + ": " + studentList[i].toString());
    }
    readFile.close();
}
catch(InputMismatchException e) {
    System.out.println("Input Format Error.”); System.exit(0);
}
catch(FileNotFoundException e) {
    System.out.println("Cannot open file \”students.txt\”");
}
```


# 2/8/2022 Abstract Classes and Interfaces

**Outline** 
* Polymorphosm 
* Dynamic Binding 
* Abstract Classes
* Interfaces

**Goals**
* Explain polymorhpism and dynamic binding 
* Create and extend abstract classes
* Use interfaces to model common behavior between classes and multim=ple inheritance

## Polymorhism
* Every object of a derived class is an object of that base class
* Polymorhosm a variable of a super type that can refer to a sub type object 

**Dynamic Binding**
* JVM (Java Virtual Machine) decided which method is invoked at runtime
* Variable have a devlared type and an actual type
* Methods are called on the actual type. 

```java
Object obj = new Circle();
System.out.print(obj.toString());
//Compiler looking to see if type Object has toString, then on runtime calling circle toString. 
```

```java

public static void printArray(Object[] list)
{
    for(Object o: list)
        System.out.print(o.toString() + " ");
    System.out.println();
}
//This is considered to by a generic method
```

### Object Casting 
* An object of the sub class is an object of the super class
* An object of the super class is not an object of the sub class

Cannot cast up inheritanec normally

**Up casting**
`Object obj = new Circle();`

**Down Casting**
```java
Circle c = obj; //Error
Circle c = (Circle) obj; //down casting
```

* If the actual type of obj is not Circle, ClassCastExcpetion is thrown

* obj1 == obj2 compare the referances to obj1 and obj2
* obj1.equals(obj2) should compare the attributed of the two objects
* Method `equals()` in class Object compares references only
* Must override `equals()` in every class where you need to compare object attributes

```java
public boolean equals(Object obj) {
    if (obj instanceOf Circle) {
        Circle c = (Circle) obj;
        return (radius == c.getRadius());
    }
    else
        return false;
}
```
## Abstract Classes 
* Abstract class - common behavior for related sub classes
* Interface - common behavior for classes not necessarily related
* When thhe super class is too general that you cannont instantiate it (create objects), the class is made abstact


**Class Shape - abstact class**

* creating a shape object does not make any sense (no real attributes)
* Class **Shape** - abstract methods getArea() and getPerimeter() but with no definiton
* But every subclass must have a getArea and getPermiter method


**Constructors of the abstract class are set to protected since this would allow only the subclasses to create instances of the class**

* Abstract classes cnanot be instntiated - but can be ised as a data type (polymorphism)
* Abstract methods make the class abstract bit the class can be abstract without abstract methods
* Abstract methods must be implemented in the sub class. If they are not, the subclass remains abstract
* A sub class can be abstract even if the super class is not(object and shape)

### Interfaces

* **Interface** - class like constructor for defining common operations (behavior) for objects from unrelated classes
* Similar to abstract classes but contain behavior of objects of unrelated classes
* Examples: Comparable,Edible,Cloneable,Drawable,etc...

* Defined using the keyword interface instead of class
* Contrains only static constant, static methods, and abstract methods,
* A class **implements** an interface **not extends**


**Deafult Definitions**
* Abstract methods in an interface may have a deafult definition 
* When an interface is implemented the deafult definition may be used or overridden


### Interface- Comparable
* java.lang.Comparable: Interface to define the comparable feature between objects of any class
* The interface has only 1 abstract method compareTo()
```java
public interface Comparable<E> {
 int compareTo(E obj);
}
```
`int compareTo()`
* returns 0 if the tow arguments are equal 
* returns > 0 if the first argument comes after the second
* returns < 0 if the first argment comes before the second argument


# 2/10/2022 Interfaces and Abstract Classes continued

**Interfaces-Cloneable**

* Empty Interface to define the ability to be cloned for objects of any class (**marker interface**)
* The interface is empty and is only used to mark a class as having cloneable behavior

```java
public interface Cloneable {
}
```

* Implementing the interface CLoneable consits in overriding the method `clone()` from class Object(Object clone())
* Many classes in Java API implement the interfaces Compareable and Cloneable

```java
Object clone() {
    return this;
}
Object 01 = new Object();
Object 02 = 01.clone();
o2.a=15;
o1.a=35;
//Both would be equal to same place in memory


```

**Deep copy/Shallow Copy**

* **Shallow Copy** - copy of same object's location in memory

```java
Object clone() {
    return this;
}
```

* **Deep Copy** - Different object with same attributes

```java
Object clone() {
    return new Circle(this.getColor(),this.getRadius());
}
```

### Implementing Multiple interfaces 
Java allows for multiple interfaces therefore becoming an workaround for multiple inheritance.

---
# 2/15/2022 Recursion

* Recursion is a trchnique to solve iterative problems that are dificult to solve using loops 
* Painting a surface
* Finding a file in a file hierarchy 
* Drawing or traversnig a tree structure


**Painting a surface** would be divining the larger sections of the wall into a small section. Solving many small problems makes big problems eaiser.

**File searching** would mean looking through each path and going back through subsequent folders

**Drawing or traversing a tree structure** -File searching is also considered a tree- 


## Recursive method is a method that calls itself
**Example: calculating factorial**

```java
n! = n * (n-1)!
5! = 5*4!
4! = 4*3!
3! = 3*2!
2! = 2*1!
1! = 1
```

```java
int factorial(int n) {
    if(n==1||n==0)
        return 1;
    else 
        return n*factorial(n-1);
}

```

In the recursive method the base case must exist. This is where the program will stop and return which would provide values to all other calls in the recursion.

Infinite recursion is when there is no base case, which without would cause a stack overflow.

Stack overflow - stack is full.

```java 

int power(int x, int n) {
    if(n==0)//base case
        x=1;
    else
        return power(x,n-1)*x;
}
```

### Recursive binary search

Using divide and conquer, finding a key in an array of ordered numbers. 

Continuously splits array upon sorted list to know if search value will exist. 

iterative binary search
```java 
int binarySearch(int[] list, int key){
 int first, last, middle;
 first = 0;
 last = list.length-1;
 while (first <= last){
    middle = (last + first) / 2;
    if (key == list[middle]) return middle;
    else if (key < list[middle])
        last = middle - 1;
    else
        first = middle + 1;
 }
 return -1;
```

Recursive binary search
``` java

int binarySearch(int[] list, int key){
    int first = 0;
    int last = list.length-1;
    return binarySearch(list, first, last, key);
}


int binarySearch(int[] list,int first,int last,int key){
    if (first > last) return -1;
    else{
        int middle = (last + first) / 2;
        if (key == list[middle]) return middle;
        else if (key < list[middle])
            last = middle - 1;
        else
            first = middle + 1;
 return binarySearch(list, first, last, key);
 }
}
```

**When extra parameters are needed in recursive call use helper method to assist**


### Recursino vs. iteration
* REcursion usually requires less code
* Recursion reflects the divide-and-conquer strategy for solving a problem
* Recursion requires consecutive calls to the same function (context switching - stack push/pop operations)
* Iterations are perferred by compilers 
* Iterations may be more efficieint (Computationally)


**Recursion is not always good**

An example of this would be the fibonacci series 


Used to model many real-life situations such as the rabbit population growth 

Fibonacci series is F(n)=F(n-1)+F(n-2)

`1 1 2 3 5 8 13`

iterative fib
``` java
int fibonacci(int n){
    int f1=1, f2=1, f=0;
    if (n <= 2)
        return 1;
    else{
        while (n > 0){
            f = f1 + f2;
            f1 = f2;
            f2 = f;
            n = n -1;
        }
     }
 return f;
}
```

recursive fib

``` java
int fibonacci(int n){
    if (n <= 2)
        return 1;
    else
        return fibonacci(n-1) + fibonacci(n-2);
}
```

This is a nice looking code but is very redundant even when just considering 5. 


Although less lines of code may be less efficient.

Use recursion only when the problem is hard to solve using loops. 

```
/users
    /Documents
        /Spring2022
            /eclpise-projects
                /HW2
                    /src
                        test.java
                    /bin
    /Desktop
    /Downloads


```

Using class file to access properties of files 

Allowing us to pass a path of the file into the constructor

`File folder = new File(path)`
`File[] <- folder.listFiles()`


``` java
public static String searchFile(String startPath,String fileName) {
        File folder = new File(startPath);
        if(!folder.isDirectory()) {
            return "";
        }
        else {
            File[] files = folder.listFiles();//return content of folder
            for(int i=0;i<files.length;i++) {
                if(files[i].isFile()) {
                    if(files[i].getName().equals(fileName)) {
                        return files[i].getAbsolutePath();
                    }

                }
                if(files[i].isDirectory()) {
                    //look for filename in sub folder of files
                    String out = searchFile(files[i].getAbsolutePath(), fileName);
                    if(out.equals(""))
                        return out;
                }
            }

        }
        return "";
    }
}
```

# 2/17/2022 Recursion continued ALA 4 start
# 2/22/22 Generic types

## What are generics?
* Genereics allow to specify a range of types allowable for a class, an interface, or a method.
* Used to create classes that hold data of different types.
* Used to create mehtods that accept parameters of different types 


* interface `Compareable<E>` can be implemented for any reference type E

```java
interface Comparable<E> {
    int compareTo(E obj);
}
```

* Generic Class - Class of type `<E>`
* E is the type parameter or generic type
* E can be replaced by any reference type String, Integer, or Student

* Primitive types are **not** allowed as generic type parameters(int,double,char,...)
* Can use any name for the generic type (between <> ) 

Generic Class - `java.util.ArrayList`
* array of objects of any type 
* Array of any size
* The sie of the array may increase or decrease at runtime
* Like a wrapper class for Arrays

* A generic type can be defined for a class or an interface
* A concrete type must be specified when using the generic class/interface
* Either to create objects or use the class as a referance type. 

### Erasure of the Generic Type
* After complile time, E is removed and replaced with the raw type (Object)
* Old way of implementing generics: use type Object intstead of E
* Using array with elements of type Object would also work 


* Using Generics improve software reliability and readablility
* Errors are detected at complile time


### Restrictions on Generic types

* Restriction 1 
  * cannot create instances of generic types
* Restriction 2
  * cannot create array of type generic
* Restriction 3
  * not allowed in static context
* Restriction 4
  * cannot create exception class

### Multilple Generic Types
* A class/interface may have multiple type parameters (generic types)
* Class Pair<E1,E2>

---

# 2/24/22 Generics (Templates)

## Generic Methods 
* A method can be generic - parameters or return value are of type generic
* Printing arrays of different types `printArray()`
* Searching arrays of different types
* Sorting arrays of different types `java.util.Arrays.sort()`
 
Generic method to print arrays of any type E

```java
public static <E> void printArray(E[] list) {
    System.out.print("[ ");
    for (int i=0; i<list.length; i++)
        System.out.print(list[i] + " ");
        System.out.println("]");
}

```

* Sorting arrays of different types `java.util.Arrrays.sort()`
* sort() needs to compare the elements (order them)
* Elements of the array must be compareable


```java
public static <E extends Compareable<E>> void sort(E[] list) {

}
```

**When using generic types `extends` will be used in every case**

There are two different versions of the sort method

* `java.util.Array.sort()` is a generic method and is overlaoded(Compareable or Comparator)

**Compareable**
```java
public static <E> void sort(E[] list)
public static <E> void sort(E[] list,int start, int end )

```

**`Comparator<T>`**
```java
public static <E> void sort(E[] list, Comparator<?, Super E> c)

```

```java
java.util.Comparator

public interface Comparator<T> {
    int compare(T obj1,T obj2);
}
```

* A generic class or interface used without specifting a concrete type, is raw type and will be replaces with Object
  `Stack stack = new Stack();`
  same thing
  `Stack<Object> = new Stack<>`
* Raw types are used for backward compartibility only

* Old Java Cersion of the interface Compareable is not generic

` int compareTo(Object obj)`

### WilCard Generic Type
* Generic types can be restricted to specific types of groups of types 
* `<E extends Compareable<E>>` restircts the type E
* Types of wildcards: ?, ? extends
T, and ? Super T

* Unbounded wildcard ?
  * Equivalent to ? extends Object
* Bounded wildcard ? extends T
  * Generic Type must be T or a subtype of T
* Lower bound wildcard ? Super **T**
  * Generic type must be T or super type of T

# 3/1/22 Algorithim Analysis 

**No Coding just theory**

* Algorithim Design- Finding a computational solution to a problem
* Often many solutions are possible. How to select a solution?
  * Use Algorithim Analysis
  * Example: Binary Seacrh and Linear Search

* Algorithim Analysis: Predict the performance of an algorithm before implementing it (coding)
* Determine the upper bound on the performance of the algorithm based on the problem size

* **Growth Rate** - how fast an algorithms execturion time (or memory space) increases as the input size incresases
* Worst Case analysis


* Theoretical approach independent of computer (Machines) and specific input

* **Big-O** notion - is a mathematical
function for measuring algorithm time
complexity (or space complexity)
based on the input size


* Time complexity- Execution time as a
function of the input size

* Space Complexity- Amount of memory
space as a function of the input size

## Big-O Notation 
* Linear Search 
    `Time(n) = (3n + 2).const=O(n)`
    * Time grows linearly with the input size (n)
    * O(n) - Order of n - Linear Algorithm 


* Mutiplicative constants and non-dominating terms are ignored 

**Useful formulas** 

1+2+3...+n=n(n+1)/2 - O(n^2)

a^0+a^1+a^2...a^n = O(a^n)

2^0 + 2^1+ … + 2^n = 2^(n+1)-1 ≅ O(2n)


**Determining Big-O**
```java

for(int i=0;i<n;i++)
{
    k=k+5
}
```
Time complexity(3*n+1)*const = O(n)

---
```java
for(int i=1; i<= n; i++){
    for(int j=1; j<= n; j++){
        k = k + i + j;
 }
}

```
Time Complexity: (1 + 3*n + 3*n^2) * const = O(n^2)

---
```java
for(int i = 1; i <= n; i++){
    for(int j = 1; j <= i; j++){
        k = k + i + j;
 }
}
```

Time Complexity: [1 + 3*n + 3*(1+2+…+n)] * const
 = n + (n+1)n/2 = O(n^2) - Quadratic

---
```java
for(int i = 1; i <= n; i++){
    k = k + 4;
}
for(int i = 1; i <=n; i++){
    for(int j=1; j<=20; j++){
     k = k + i + j;
    }
}
```
Time Complexity:
 = (1+ 3*n) * const + (1 + 3*n + 3 * 20 * n) * const
 = O(n)

 ---

 ```java
if(list.contains(e)){
    System.out.print(e);
}
else{
    for(Object t: list){
    System.out.print(t);
    }
}
 ```
Time Complexity: (1+ n)*const or ((2* n)+ n)*const = O(n)

---

```java
result=1;
for(int i=1; i<=n; i++)
 result = result * a;
```
Time complexity: (2 + 3 * n) * const = O(n)

---

```java
result = a;
for(int i=1; i<=k; i++)
 result = result * result; c
```
Time complexity: (2 + 3 * log n) * const = O(log n)

---

``` java
int count = 1;
while(count < n)
 count = count * 2;
```
Time complexity: (1 + 2 * n/2) * const = O(n)

---

### Analysis of Binary Search

After each iteration the array size is split into half

Eventually until n/(2^k)=1 since can no longet be split

then from there can be considered log n =k


--- 
### Analysis of Selction sort

since there are nested loops depending on the size of each is considered O(n^2)

--- 
### Analysis Recursive Fibonacci sequence
Time(n) = Time(n-1) + Time(n-2)
Time(n) ~ 2 * Time(n-1)
Time(n-1) = 2 * Time(n-2)
Time(n) = 2 * 2 * Time(n-2)
…
Time(n) = 2^k * Time(n-k)
Time(n) = 2^(n-2) Time(2)
Time(n) = 2^(n) * constant

Recursive Fibonacci: O(2n) - Exponential growth


**Iterative**
```java
public static long fibonacci(long n) {
 long f0=0,f1=1, f2=1;
if(n == 1 || n == 2)
 return f1;
for(int i=3; i<=n; i++){
 f0=1;
 f1=f2;
 f2=f0+f1;
 }
 return f2;
}
```
Time Complexity: (8 + 5 * (n-3)) * const
Iterative Fibonacci: O(n) - Linear growth

---

**O(1) < O(logn) < O(n) < O(n logn) < O(n^2) < O(n^3) < O(2^n)**

---

```java
for (int i = n/2; i > 0; --i){ //n/2
    int x = n * 3;
 while(x > 1){  //log(3n)
    for (int j=0; j < 100; j+=2) //50
        System.out.prinltn(“X: “ + x);
    x = x / 2;
 }
}
```
Therefore time complexity is log(3n)