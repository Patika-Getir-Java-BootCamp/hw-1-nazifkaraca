## <h1>Getir Java Spring Bootcamp Homework 1 Answers</h1>

<h2>1 – Why we need to use OOP? Some major OOP languages?</h2>

One of the most important reasons why we use OOP is that modularity and code reusability, maintainability, readability, data security and real-world representation. These necessities make OOP usage inevitable, and also paves developing scalable apps. <br> Some of the major OOP languages consists Java, C#, Python, C++, JavaScript (with ES6 and beyond), Swift, Ruby and PHP.

<hr>

<h2>2- Interface vs Abstract class?</h2>

Both interfaces and abstract classes is being used to achieve <b>abstraction</b> in Object-Oriented Programming. While <b>interfaces</b> only contains method signatures, <b>abstract classes</b> can have both abstract (without implementation) and concrete (with implementation) methods. In short terms, interfaces only dictates <b>what to use</b> not <b>how to use</b>.

Furthermore, <b>interfaces</b> does not support constructors and a class can implement multiple interfaces. On the other hand, <b>abstract classes</b> supports constructors and a class can only inherit from <b>one abstract class</b>.

<hr>

<h2>3- Why wee need equals and hashcode? When to override?</h2>

The <code>equals()</code> method is used to compare the <b>contents of two objects</b> instead of their memory addresses. However, by default, <code>equals()</code> checks if two objects refer to the same memory location. In order to compre objects based on their data, we must override <code>equals()</code>.

    class Person {
        String name;

        Person(String name) {
            this.name = name;
        }

        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true; // Check if same memory reference
            if (obj == null || getClass() != obj.getClass()) return false; // Check class type
            Person person = (Person) obj;
            return name.equals(person.name); // Compare field values
        }
    }

    public class Main {
        public static void main(String[] args) {
            Person p1 = new Person("Alice");
            Person p2 = new Person("Alice");

            System.out.println(p1.equals(p2)); // true (now compares content)
        }
    }

The <code>hashCode()</code> method generates a <b> unique integer value</b> for an object, which is used in hash-based collections like <code>HashSet</code>, <code>HashMap</code>, <code>HashTable</code>.

Hash-based collections use <code>hashCode()</code> for efficient lookup and storage. If two objects are equal (<code>equals</code> is <code>true</code>), they must have the same <code>hashCode()</code>.

In short, <code>equals()</code> should be overriden when comparing objects based on <b>custom fields</b>, <code>hashCode()</code> should be overriden when using objects in hash-based collections (<code>HashMap</code>, <code>HashSet</code>, etc.).

<hr>

<h2>4- Diamond problem in Java? How to fix it?</h2>

The <b>Diamond Problem</b> is a well-known issue in multiple inheritance, where a class inherits from two classes that have a common ancestor. This leads to ambiguity in method resolution.

Java <b>does not support multiple inheritance</b> with classes to avoid ambiguity. The reasons why Java does not support are:

- Ambiguity in method resolution
- Diamond Problem (which method should be interited?)
- Increases complexity in method calls
- Causes maintainability issues

<h6>We can solve this issue with <b>default methods</b>. If two interfaces define the same method, the implementing class must resolve the conflict.</h6>

    interface A {
        default void show() {
            System.out.println("A's method");
        }
    }

    interface B extends A {
        default void show() {
            System.out.println("B's method");
        }
    }

    interface C extends A {
        default void show() {
            System.out.println("C's method");
        }
    }

    class D implements B, C {
        // Must resolve ambiguity
        @Override
        public void show() {
            System.out.println("D's method");
            B.super.show();  // Explicitly calling B's method
        }
    }

    public class Main {
        public static void main(String[] args) {
            D obj = new D();
            obj.show(); // Calls D's method and explicitly calls B's method
        }
    }

<h6>Also, instead using inheritance, we can use composition by creating instances of the required classes.</h6>

    class A {
        void show() {
            System.out.println("A's method");
        }
    }

    class B extends A {
        void show() {
            System.out.println("B's method");
        }
    }

    class C extends A {
        void show() {
            System.out.println("C's method");
        }
    }

    // Instead of extending both B and C, D will have instances of B and C
    class D {
        private B objB = new B();
        private C objC = new C();

        void show() {
            System.out.println("D's method");
            objB.show(); // Call B's method
            objC.show(); // Call C's method
        }
    }

    public class Main {
        public static void main(String[] args) {
            D obj = new D();
            obj.show();
        }
    }

<hr>

<h2>5- Why we need Garbagge Collector? How does it run?</h2>

The Garbage Collector (GC) is a memory management feature in Java that automatically reclaims unused memory, preventing memory leaks and improving application performance. It works by identifying unreachable objects and removing them from the heap, freeing space for new allocations.

Java does not allow manual memory management, reducing the risk of memory corruption and dangling pointers. The GC runs automatically based on JVM heuristics, but developers can suggest execution using <code>System.gc()</code>. Different GC algorithms, such as Serial, Parallel, G1 and ZGC, can be used.

<hr>

<h2>6- Java ‘static’ keyword usage?</h2>

The <b>static</b> keyword in Java used to define class-level members, meaning <b>they belong to the class itself rather than instances of the class</b>. It can be applied to variables, methods, blocks and nested classes. Static variables are shared across all instances of a class, useful for constants.

Static methods can be called without creating an object, but they cannot access instance variables directly. Static blocks are executed once when the class is loaded, useful for initialization tasks. Static nested classes exist independently of outer class instances. <code>static</code> improves memory efficiency and is widely used in utility classes and singleton patterns.

<hr>

<h2>7- Immutability means? Where, How and Why to use it?</h2>

<b>Immutability</b> means that an object's state cannot be changed after it is created. In Java, immutable objects ensure <b>thread safety, caching efficiency, and predictability</b>. They are commonly used in multi-threading, caching, and functional programming.

<b>Where?</b> Immutable classes like String, Integer, and BigDecimal are widely used in Java collections and concurrency. <b>How?</b> To create an immutable class, declare fields as private final, do not provide setters, and ensure defensive copying of mutable objects. <b>Why?</b> Immutability prevents unexpected state changes, simplifies debugging, enhances performance in concurrent applications, and avoids synchronization issues.

<hr>

<h2>8- Composition and Aggregation means and differences?</h2>

<b>Composition</b> and <b>Aggregation</b> are both types of association in OOP that define relationships between classes, but they differ in ownership and dependency.

<b>Composition</b> represents a strong relationship where one class cannot exist without the other (e.g., a Car has an Engine—if the Car is destroyed, the Engine is too). In Java, this is typically implemented by defining an object as a private field inside another class.

<b>Aggregation</b>, on the other hand, is a weaker relationship where the contained object can exist independently (e.g., a Library has Books, but Books can exist without the Library). Composition implies tighter coupling, whereas Aggregation allows more flexibility and reuse.

<hr>

<h2>9- Cohesion and Coupling means and differences?</h2>

<b>Cohesion</b> and <b>Coupling</b> are fundamental software design principles that impact maintainability and scalability.

<b>Cohesion</b> refers to how closely related and focused the responsibilities of a class or module are; high cohesion means a class does one specific task well, leading to better reusability and maintainability.

<b>Coupling</b>, on the other hand, measures the degree of dependency between different classes or modules; low coupling is desirable because it reduces interdependencies, making the system easier to modify and extend.

<b>Difference:</b> High cohesion improves code clarity and modularity, while low coupling enhances flexibility and reduces the risk of changes affecting multiple components. To achieve best practice, aim for high cohesion and low coupling for scalable and maintainable software.

<hr>

<h2>10- Heap and Stack means and differences?</h2>

In Java, Heap and Stack are two types of memory used for different purposes during program execution.

<b>Heap memory</b> is used for dynamic memory allocation, where objects and class instances are stored and managed by the Garbage Collector. It is shared across all threads and has a larger but slower memory space.

<b>Stack memory</b>, on the other hand, is used for method execution, storing primitive variables, method calls, and references to objects. It operates in a <b>Last In, First Out (LIFO)</b> manner and is faster but limited in size.

<b>Difference:</b> The heap is used for long-lived objects, while the stack is used for temporary execution-related data. Stack memory is automatically managed, whereas heap memory requires garbage collection.

<hr>

<h2>11- Exception means? Type of Exceptions?</h2>

An exception in Java is an unexpected event that disrupts the normal flow of a program during execution. Java provides a structured way to handle exceptions using <b>try-catch-finally blocks</b> to ensure graceful error handling. Types of exceptions:

- <b>Checked Exceptions (compile-time)</b> – must be handled using try-catch or declared with throws (e.g., IOException, SQLException).
  <br>
- <b>Unchecked Exceptions (runtime)</b> – occur due to programming errors and do not require mandatory handling (e.g., NullPointerException, ArrayIndexOutOfBoundsException).
  <br>
- <b>Errors</b> – critical system failures that cannot be recovered from (e.g., OutOfMemoryError, StackOverflowError). Proper exception handling improves reliability, prevents crashes, and enhances debugging.

<hr>

<h2>12- How to summarize ‘clean code’ as short as possible?</h2>

Clean Code is readable, maintainable, and efficient code that follows best practices like meaningful naming, simplicity, modularity, and proper error handling. It avoids redundancy, uses consistent formatting, and promotes high cohesion with low coupling. The goal is to make code easy to understand, modify, and extend while minimizing complexity.

<hr>

<h2>13- What is the method of hiding in Java?</h2>

<b>Method Hiding</b> in Java occurs when a static method in a subclass has the same signature as a static method in its superclass. Unlike method overriding, which is based on dynamic method dispatch (runtime polymorphism), method hiding is resolved at compile-time based on the reference type. Since static methods belong to the class, not instances, the subclass method hides the superclass method rather than overriding it.

    class Parent {
        static void display() {
            System.out.println("Parent's static method");
        }
    }

    class Child extends Parent {
        static void display() {  // Method hiding, not overriding
            System.out.println("Child's static method");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Parent obj = new Child();
            obj.display(); // Calls Parent's display() because method hiding is resolved at compile-time
        }
    }

<b>In overriding</b>, the method is resolved based on the actual object <b>(runtime)</b>, but in <b>method hiding</b>, the method is resolved based on the reference type <b>(compile-time)</b>.

<hr>

<h2>14- What is the difference between abstraction and polymorphism in Java?</h2>

Abstraction and Polymorphism are both key OOP principles in Java, but they serve different purposes.

- <b>Abstraction</b> is about hiding implementation details and exposing only the necessary functionality. It is achieved using abstract classes and interfaces. For example, a Vehicle class can have an abstract method move(), while subclasses (Car, Bike) provide their specific implementations. Abstraction improves modularity and security by preventing direct access to complex logic.
  <br>
- <b>Polymorphism</b> allows one interface to be used for multiple forms, enabling dynamic method binding. It is achieved through method overloading (compile-time) and method overriding (runtime). For instance, a print() method can be defined differently in multiple classes, and Java decides at runtime which version to execute. Polymorphism enhances flexibility, reusability, and code maintainability.
