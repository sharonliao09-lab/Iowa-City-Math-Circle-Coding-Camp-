---
layout: two-cols
transition: slide-left
---

# <DateTitle offset=4 />

<StartupBadge />

**Agenda**

- Imports / Packages
- *Break*
- Exception Handling
- *No worksheet today*
- Projects Overview
- Saving progress from Binder
- Replit
- Additional Topics Overview

::right::

<Toc minDepth=2 maxDepth=3 mode="onlyCurrentTree" />

---

## Packages

<v-clicks depth=3>

- Large programs can be split into separate files
  - Improves organization
  - **Modularize** code
    - Use the same classes / functions across multiple projects
    - Share your code with others
- Related classes are grouped into **packages**
  - Only **top-level public** classes in a package can be accessed outside the package
    - Only one top-level public class per file. Must match file name
    - This will be clarified later
  - Classes in other packages can be **imported**

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}
// We use an `import` statement to import classes from other packages.
import java.util.Scanner; // Importing the `Scanner` class from the `java.util` package.
import java.util.ArrayList; // Importing the `ArrayList` from the same package.

// This import all of the classes in a package.
import java.util.*;
// We do not recommend importing all classes.
// It can make your code less clear. You may forget which classes you are using.

public class Main { // Top-level public class.
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        
        // ...
        ArrayList<String> arr = new ArrayList<>();
        LinkedList<String> list = new LinkedList<>();
        // ...
        
        scan.close();
    }
}
```

---

### Creating / Using Custom Packages

<StartupBadge />

<v-clicks depth=3>

- In Binder, the `Main` class is already inside a package called `src.workbench`
  - The file `Main.java` is under the folder `workbench` inside the folder `src`
  - The name of a package should match the **directory** that the class is in
    - The directory in this case is `src/workbench/`

</v-clicks>

---
layout: two-cols-header
---

#### Example 1 - Java <logos-java />

::left::

**demo/MyClass.java**

```java {monaco-run} {autorun:false, runnerOptions:{entrypoint:false, file_path:'MyClass.java'}}
package demo;

public class MyClass { // `MyClass` is the top-level public class of `MyClass.java`
    public static void foo() {
        System.out.println("Foo");
    }
    public void bar() {
        System.out.println("Bar");
    }
}

class SecondClass { // `SecondClass` is top-level, but not public.
    public static void baz() {
        System.out.println("Baz");
    }
}
```

::right::

**demo/Main.java**

```java {monaco-run} {autorun:false, runnerOptions:{addSources:['MyClass.java']}}
package demo;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
        
        MyClass.foo();
        MyClass myObject = new MyClass();
        myObject.bar();
        
        // We can also access this class because it is in the same package.
        SecondClass.baz();
    }
}
```

<!-- Instructor should explain demos once they appear. -->

---
layout: two-cols-header
---

#### Example 2 - Java <logos-java />

::left::

**package1/MyClass.java**

```java {monaco-run} {autorun:false, runnerOptions:{entrypoint:false, file_path:'MyClass.java'}}
package package1; // Package #1

// `MyClass` is the top-level public class of 
// `MyClass.java`
public class MyClass {
    public static void foo() {
        System.out.println("Foo");
    }
    public void bar() {
        System.out.println("Bar");
    }
    public void baz() {
        SecondClass.baz();
    }
}

// `SecondClass` is top-level, but not public.
// It cannot be accessed outside the `package1` package.
class SecondClass {
    public static void baz() {
        System.out.println("Baz");
    }
}
```

::right::

**package2/Main.java**

```java {monaco-run} {autorun:false, runnerOptions:{addSources:['MyClass.java']}}
package package2; // Package #2

import package1.*;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
        
        MyClass.foo();
        MyClass myObject = new MyClass();
        myObject.bar();
        
        // We cannot access this class 
        // because it is not top-level public.
        // SecondClass.baz();
    }
}
```

<!-- 
Instructor should explain demos once they appear.
Optionally, demo this in an external environment since today is far less busy.
-->

---

#### Example 3 - Python <logos-python />

<span v-mark.underline.red>We will not cover creating packages in Python, which **follows its own rules**.</span>  
But, here is an example of how to import packages in Python:

```python {monaco-run} {autorun:false}
import cowsay # Import the cowsay package.

cowsay.cow("MOO") # Call a function from the package.
```

---

## Break

Have a break!

<RandomPicture />

---

## Exceptions

<v-clicks depth=2>

- An **exception** is a type of event that disrupts the execution of a program
- **Exceptions** are often used to indicate that a problem occurred in the program  
For example:
  - Array index out of bounds
  - Divide by zero
  - Trying to use an object with value `null`
  - Incorrect usage of a function
  - etc.
- *By default*, when an **exception** occurs, it will stop a program immediately (*termination*)
  - We can **catch** exceptions to prevent the program from *terminating*
  - We can create / **throw** our own exceptions
- We will only be covering exceptions in Java, but note that Python also has exceptions

</v-clicks>

---
hideInToc: true
---

### Example

Examples of common exceptions in Java.

```java {monaco-run} {autorun:false}
public class Main {
    public static void main(String[] args) throws Exception {
        // ArrayIndexOutOfBoundsException
        int[] nums = {1, 2, 3};
        System.out.println(nums[10]); // Index 10 is out-of-bounds.
        
        // ArithmeticException
        int n = 10 / 0; // Dividing by 0 is illegal.
        
        // NullPointerException
        String s = null;
        s.length(); // Don't use an object which is `null`.
        
        // Your own exception!
        throw new Exception("MY EXCEPTION");
    }
}
```

<!-- Run this example with various exceptions. Note the kinds of exceptions that appear in the output. -->

---

## Handling Exceptions

<v-clicks>

- By *handling* an exception, you are instructing the program to do something else instead of *terminating*
- Put the code that can throw exception(s) inside a `try` block
- If an exception is occurs / *thrown*, execution will jump to the start of a `catch` block
- There is also a `finally` block, but we will not cover it

</v-clicks>

---
hideInToc: true
zoom: 0.85
---

### Example

```java {monaco-run} {autorun:false}
public class Main {
    public static void main(String[] args) {
        
        // Start of the `try` block!
        try {
            
            // ArrayIndexOutOfBoundsException
            int[] nums = {1, 2, 3};
            System.out.println(nums[10]); // Index 10 is out-of-bounds.
            
            // ArithmeticException
            int n = 10 / 0; // Dividing by 0 is illegal.
            
            // NullPointerException
            String s = null;
            s.length(); // Don't use an object which is `null`.
            
            // Your own exception!
            throw new Exception("MY EXCEPTION");
        
        // End of the `try` block. Start of the `catch` block!
        } catch (Exception e) {
            System.out.println("A problem occurred!");
            
            // You can also print the details of the exception.
            System.out.println(e.toString());
            System.out.println(e.getMessage());
        }
    }
}
```

---

## Worksheet

No worksheet today!

<!-- There is another slide after this one! -->

---

## Projects

- The next week of content will cover niche topics
- There will be no more worksheets
- **Get into a group to brainstorm project ideas, or *solo it***

---
routeAlias: binder_saving
zoom: 0.9
---

## Saving progress from Binder

**Binder does not save your data for you. Follow these steps to save your files.**  
[Click here to access the visual guide.](media/binder_save.pdf)

### Downloading

To download your files from Binder:

1. In the terminal (the box where your program outputs to), run the command `zip -r workbench.zip .`  
<span text-sm>Don't forget the ".", it's a part of the command</span>
2. In the file explorer (the list of files on the left), right-click / two-finger-click on the file `workbench.zip`. Then, click "Download..." to download the file.  

### Uploading

To upload your files to Binder:

1. Right-click in an empty space inside the file explorer. Then click "Upload..." and upload your `workbench.zip` file that you previously downloaded.
2. In the terminal, run the command `unzip -o workbench.zip`. Your files have been restored!
3. Delete the file `workbench.zip` in the file explorer.

<!-- 
Demonstrate the saving process.
Optionally, demonstrate the janky multiplayer functionality via the preinstalled extension on the next slide.
-->

---

## Collaborating with Binder

[Click here to access the visual guide.](media/binder_collab.pdf)

<!-- Collaborating with Binder is currently broken. Do not follow those instructions. -->

---

## ~~Replit~~

*Update to this slide: Students best no longer use Replit.*

~~Create a Replit account at [replit.com](https://replit.com/).~~

> ~~Replit gives you 1200 minutes per month of usage. **Use it wisely.**~~  
> ~~You also have a limit of 1 collaborator.~~

<!-- Instructor(s) should assist with Replit account setup. Optionally, demonstrate collaborator functionality. -->

---

## Additional Topics Overview

- <Link to="time">Time & Random</Link> - Work with time and generate random numbers
- <Link to="ansi_escape_sequences">Basic ANSI Escape Sequences</Link> - <span class="colorful">Give your text-based programs colors, <strong>other</strong> <i>styles</i></span>, clear the screen, and move the cursor
- <Link to="file_io">File I/O</Link> - Read and write to files to store data
- ~~<Link to="turtle">Turtle</Link> - Use Python to draw colorful spirals~~
- <Link to="lambdas">Lambdas / Anonymous Functions</Link> - Assign functions to variables and call variables as functions
- <Link to="multithreading">Multithreading</Link> - Run multiple functions at the same time

<style>
.colorful {
  background: linear-gradient(to right, pink, red, blue, violet);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  display: inline-block;
}
</style>

<!-- 
Students should "vote" on which topics they find interesting. Topics do not have to be completed in the suggested order that this content was designed with.
If a students requests it, the instructor should be prepared to develop an ad hoc example to show demonstrate the equivalent topic in Python.
-->
