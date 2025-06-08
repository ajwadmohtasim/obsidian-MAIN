### 1. How many types of java constructors are there? Describe the difference between Constructor and Method.
Constructor -> Default(Non parameterized), Parameterized, Copy

| Constructor                         | Method                                  |
| ----------------------------------- | --------------------------------------- |
| Initializes the values of a class   | Exposes the behaviors of an object.     |
| There's no return type.             | There may or may not be return type     |
| Naming must be same as it's Class   | Can be anything except the Class's name |
| Invoked Implicitly when using 'new' | Invoked Explicitly via method call      |
| Cannot be static, final or abstract | Can be static, final or abstract        |

### 2. What are the access modifiers in java? How do they differ from each other?
Access Modifiers -> Default, Private, Public, Protected.

| Accessible from any class | Same Class | Same Package | Outside Package(Subclass) | Outside Package (Non subclass) |
| ------------------------- | ---------- | ------------ | ------------------------- | ------------------------------ |
| Private                   | yes        | -            | -                         | -                              |
| Default                   | yes        | yes          | -                         | -                              |
| Protected                 | yes        | yes          | yes                       | -                              |
| Public                    | yes        | yes          | yes                       | yes                            |


### 3. How can we create a copy constructor? Show with example.
```java
class A{
	int a;
	A(int x) {this.a = x;}
	A(A t){ this.a = t.a; }
}
public class Main{
	public static void main(String[] args) {
		A a1 = new A(5);
		A a2 = new A(a1);
	}
}
```
### 4. Is java pass-by-value or pass-by-reference for both primitive(int, double, char) and non-primitive(Object, Arrays) cases.
When you pass a **primitive type** (e.g., `int`, `double`, `char`), Java creates a **copy** of the value and passes it to the method. Any changes inside the method **do not** affect the original variable.
**Example:**
```java
public class PassByValueExample {
    public static void modify(int x) {
        x = 10; // Modifies the local copy, not the original variable
    }
    public static void main(String[] args) {
        int a = 5;
        modify(a);
        System.out.println(a); // Output: 5 (Original value remains unchanged)
    }
}
```
Non-primitive types (e.g., objects, arrays) are also **passed by value**, but in this case, the **value being passed is a reference** to the object.
This means:
- The reference (memory address) is copied, not the actual object.
- Both the original and copied references **point to the same object**.
- Modifying the object **affects the original**, but reassigning the reference inside the method does not.

**Example: Modifying Object Properties**
```java
class Person {
    String name;
}
public class PassByValueRef {
    public static void modify(Person p) {
        p.name = "Alice"; // Modifies the same object in memory
    }
    public static void main(String[] args) {
        Person person = new Person();
        person.name = "Bob";
        modify(person);
        System.out.println(person.name); // Output: Alice (Object is modified)
    }
}
```
**Why does it change?** The `modify()` method receives a copy of the reference to `person`, but both point to the **same memory location**.

**Example: Reassigning Reference Inside Method (No Effect)**
```java
class Person {
    String name;
}
public class PassByValueRef {
    public static void modify(Person p) {
        p = new Person(); // This creates a new object (new memory address)
        p.name = "Charlie"; // This only modifies the new object
    }
    public static void main(String[] args) {
        Person person = new Person();
        person.name = "Bob";

        modify(person);
        System.out.println(person.name); // Output: Bob 
    }
}
```
**Why doesn’t it change?**
- `p` inside `modify()` is a copy of the reference.
- Assigning `p` to a new object only changes **the local copy of the reference**, not the original.
### 5. What is inheritance in Java? Types of inheritance in Java.
Inheritance is the process of inheriting properties and behaviors from another class. 
Types of inheritance in java -> Single, Multi-level, Hierarchical.
Java does not have multiple inheritance.
![InheritanceJava.jpg|500](https://d2jdgazzki9vjm.cloudfront.net/images/core/typesofinheritance.jpg)
### 6. Why Multiple Inheritance is not supported in Java? What's the workaround?
Multiple inheritance can cause an ambiguity when calling Objects of different classes. Let's say Class C inherits from both A and B. Now, if A and B both had a common method then when calling this method, we shall face ambiguity to decide which method should be called.
Since compile time error is better than runtime error, when dealing with this, it will throw compile time error and Java won't allow you to write code like this.

So, to reduce the complexity and simplify multiple inheritance are dealt with interfaces and abstract classes. 
### 7. Can we override static method? and Main Method?
No, we cannot override static method. Because, static methods are not associated with instance of a class, but with the class itself. So we cannot just modify the behavior of it in any way. Similarly we also cannot override a main method since it's static as well. 
### 8. Talk about Method Overloading and Method Overriding. How does these achieve polymorphism? 

| Method Overloading                                                              | Method Overriding                                                                        |
| ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Compile time polymorphism                                                       | Run-time polymorphism                                                                    |
| Method overloading is done within the same class                                | Method overriding needs at-least two classes to work as it follows an IS-A relationship. |
| Must have different numbers of parameter, if same it must be of different type. | Same number of parameter and same type.                                                  |
| Return type can be same or different.                                           | Must be same or covariant.                                                               |
| Increases readability                                                           | Provides specific implementation according to needs.                                     |

### 9. What is Super in Java? super can be used to invoke parent class method and constructor - Show with example.
It's a special keyword that refers to the immediate parent class. 
```java
class Animal{
	void eat() {System.out.println("Animal eats.");}
}
class Dog extends Animal {
	void eat() {
		super.eat(); // invoking parent class method.
		System.out.println("Dog eats");
	}
	Dog() {
		super(); // invoking parent class contructor(In this case default).
	}
}
class A{
	public static void main(String[] args) {
		Dog a = new Dog();
		a.eat();
	}
}
```
### 10. Describe the difference between Abstraction and Encapsulation in Java.

| Abstraction                                     | Encapsulation                                                              |
| ----------------------------------------------- | -------------------------------------------------------------------------- |
| Hides implementation                            | Protects data                                                              |
| Problems solved at interface level              | Problems solved at implementation level                                    |
| Uses Abstract class and interface to achieve it | Uses access specifiers (Private, Protected) along with getters and setters |
### 11. What is abstract class? How does it achieve abstraction?
It's a special type of super-class that achieves abstraction with the help of hiding implementations of unwanted methods. It gives the class an abstract method with no implementations and this allows to be later implemented by the sub classes based on their needs. It kind of forces the subclass to implement the abstract method. 
```java
abstract class A{
	abstract void ok();
}
class B extends A{
	void ok() { System.out.println("Ok !");}
}
class C extends A{
	void ok() { System.out.println("Ok Ok!"); }
}
class Main{
	public static void main(String[] args) {
		B b = new B();
		b.ok() //outputs : Ok !
		C c = new C();
		c.ok() //outputs : Ok Ok!
	}
}
```
### 12. What is Java Interface? How's it different from abstract class? What does it achieve? Why do we use it? 
This is a special blueprint that allows Java to contain methods with no implementations and only the signature of it. The fields are **public static final** by default. Unlike abstract class, it cannot have constructors or instance fields as well as concrete methods. 
### 13. Describe the relationship between classes and interfaces.
![interface.jpg|500](https://d2jdgazzki9vjm.cloudfront.net/images/core/interfacerelation.jpg)
### 14. How do we implement multiple inheritance in Java by interface.
```java
interface A { void m1(); }
interface B { void m2(); }
class C implements A,B {
	public void m1() { ... }
	public void m2() { ... }
}
class Main {
	public static void main(String[] args) {
		C c = new C();
		c.m1();
		c.m2();		
	}
}
```
### 15. Describe the difference between Abstract class and interface.

| Abstract Classes                                           | Interface                                          |
| ---------------------------------------------------------- | -------------------------------------------------- |
| Can have abstract and non abstract method                  | can only have abstract, default and static methods |
| Doesn't support multiple inheritance                       | Supports multiple inheritance                      |
| Can have final, non-final, static and non-static variables | only static and final variables                    |

### 16. What is Runtime and Compile-time
When the JVM is executing the program we call it runtime and all the processes before the java compiler compiles the source code into bytecode are called compile-time. 
### 17. Write FileNotFoundException, IOException, NullPointer, ArrayIndexOutOfBoundsException Error code.
```java
import java.io.*;
public class ExceptionHandlingDemo {
    public static void main(String[] args) {
        try {
            // 1. FileNotFoundException (Trying to read a non-existent file)
            FileReader file = new FileReader("non_existent_file.txt");
            BufferedReader reader = new BufferedReader(file);
            System.out.println(reader.readLine()); // Reading file content

            // 2. IOException (General I/O issue)
            reader.close(); // Closing the reader
            reader.readLine(); // Attempting to read after closing (IOException)

            // 3. NullPointerException
            String str = null;
            System.out.println(str.length()); // Accessing length of null

            // 4. ArrayIndexOutOfBoundsException
            int[] arr = new int[3];
            System.out.println(arr[5]); // Accessing invalid index

        } catch (FileNotFoundException e) {
            System.out.println("Error: File not found!");
        } catch (IOException e) {
            System.out.println("Error: Issue with file input/output!");
        } catch (NullPointerException e) {
            System.out.println("Error: Null reference encountered!");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Array index out of bounds!");
        } finally {
            System.out.println("Execution completed!");
        }
    }
}

```
### 18. Difference between throw and throws
`throw` is used to explicitly show and error, while `throws` declares that a method might throw an exception.
```java
public class ThrowExample {
    static void checkAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be 18 or above.");
        } else {
            System.out.println("You are eligible.");
        }
    }
    public static void main(String[] args) {
        checkAge(16); // Throws IllegalArgumentException
    }
}

import java.io.*;
public class ThrowsExample {
    static void readFile() throws FileNotFoundException {
        FileReader file = new FileReader("non_existent.txt"); 
        // May throw FileNotFoundException
    }
    public static void main(String[] args) {
        try {
            readFile();
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
    }
}

```
### 20. If exception is not handled, how does JVM work with the errors?
The JVM firsts checks if the exception is handled or not -> If not handled, it provides a default exception handler (Prints description, stack tree, terminates the program).
If handled -> normal flow of the code is maintained. 
### 23. How many types of multitasking are there in java? Which one is better? Describe it's advantage.
1. process-based (Multiprocessing)
2. thread-based (Multithreading)

**Process-based multitasking** is the feature that allows your computer to run two or more programs concurrently. Each process have its own <u>address in memory</u>  i.e. each process allocates separate memory area. 
**Thread-based multitasking** allows running multiple threads inside a single process. The threads share the same address space.

Process-Based -> Runs multiple program but single task
Thread-Based -> Runs multiple tasks but single program

**Multithreading** is better than **Multiprocessing** as threads share a common memory area. They don't allocate separate memory area so saves memory, and context-switching between the threads takes less time than process.

**Advantages of Java Multithreading:**
1. Doesn't block the user because threads are independent.
2. Can perform many operations together, saves time.
3. Doesn't effect other thread if one gets affected.

### 22. What if we call run() method directly instead start() method when creating threads? How does Join() work?
When creating a thread using the `Thread` class or `Runnable` interface, we're supposed to start the thread using `start()` method. However, there's always a `run()` inside the Class's definition and if we call that instead, we won't be starting a separate thread and it will act like a normal method. So, there won't be any concurrent process happening.
```java
class A extends Thread {
	public void run() {
		for (int i = 1; i < 5; i++ ) {
			try{
				Thread.sleep(500);
			} catch (InterruptedException e) {
				System.out.println(e);
			}
			System.out.print(i);
		}
		System.out.println();
	}

	public static void main(String[] args) {
		A a1 = new A();
		A a2 = new A();
		a1.run();
		a2.run();
		a1.start();
		a2.start();
	}
}
```
**Output:**
```
1234
1234
1122334
4
```
`join()` method makes the thread wait until another thread finishes execution.
we use this to ensure a thread completes first before moving to the next task. Useful in syncing.
```java
public static void main(String[] args) {
	A a1 = new A();
	A a2 = new A();
	a1.start();
	try {
		a1.join();
	} catch (InterruptedException e) {
		System.out.println(e);
	}
	a2.start();
}
```
**Output:**
```
1234
1234
```
### 22. How do you set Thread Priorities? 
```java
class MyThread extends Thread {
    public void run() {
        System.out.println(Thread.currentThread().getName() + " Priority: " + Thread.currentThread().getPriority());
    }
}

public class ThreadPriorityExample {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        t1.setPriority(Thread.MIN_PRIORITY); // Priority 1
        t2.setPriority(Thread.NORM_PRIORITY); // Priority 5
        t3.setPriority(Thread.MAX_PRIORITY); // Priority 10

        t1.start();
        t2.start();
        t3.start();
    }
}
```
**output:**
```
Thread-0 Priority: 1
Thread-2 Priority: 10
Thread-1 Priority: 5
```
### 23. Discuss about Daemon Threads in Java.

A **daemon thread** is a special type of thread in Java that runs **in the background** to support other non-daemon (user) threads. These threads perform tasks such as **garbage collection, monitoring, and logging**, and they **do not prevent the JVM from exiting** when all user threads finish execution. So, when all the user threads
dies, JVM terminates this thread automatically.

```java
public class TestDaemonThread1 extends Thread {

    public void run() {
        // Checking if the thread is a daemon
        if (Thread.currentThread().isDaemon()) {
            System.out.println("Daemon thread work");
        } else {
            System.out.println("User thread work");
        }
    }

    public static void main(String[] args) {
        // Creating threads
        TestDaemonThread1 t1 = new TestDaemonThread1();
        TestDaemonThread1 t2 = new TestDaemonThread1();
        TestDaemonThread1 t3 = new TestDaemonThread1();

        // Setting t1 as a daemon thread
        t1.setDaemon(true);

        // Starting the threads
        t1.start();
        t2.start();
        t3.start();
    }
}

```
**output:**
```
daemon thread work
user thread work
user thread work
```

1. Copy Constructor
2. Multiple Inheritance
3. Super to invoke parent class
4. initialize blank variable
5. Deep copy and shallow copy
6. 7. interface + abstract

```java


```