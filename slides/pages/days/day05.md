---
layout: two-cols
transition: slide-left
---

# <DateTitle offset=4 />

<StartupBadge />

**Agenda**

- Recursion
- Sorting Methods 
- Imports / Packages
- *Break*
- Exception Handling
- *No worksheet today*
- Projects Overview
- Saving progress from Binder
- Replit
- Additional Topics Overview

::right::

<Toc class="text-xl" minDepth=2 maxDepth=3 mode="onlyCurrentTree" />
--- 

### Recursion

<v-clicks depth=3>

- Recursion is when a program repeatedly calls its own method. 
- It includes a base case in which the program immediately breaks out if the condition is true. 
- Recursion is helpful for several sorting and searching methods, as we will see in the coming slides.

</v-clicks>

---

### Factorial Recursive Method 

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

public class Factorial {
    public static int factorial(int n) {
        if (n <= 1) {
            return 1;
        }
        return n * factorial(n - 1);
    }

    public static void main (String[] args) {
        factorial(5);
        /**
        factorial(5) = 5 * factorial(4) = 120
        factorial(4) = 4 * factorial(3) = 24
        factorial(3) = 3 * factorial(2) = 6
        factorial(2) = 2 * factorial(1) = 2
        factorial(1) = 1;
        **/
       
    }

}

```
---

### Searching Methods 

<v-clicks depth=3>

- Searching methods, such as linear and binary search, are useful when finding a target value in an array. 
- However, these two methods are vastly different in their runtimes and efficiency. 

</v-clicks>

---

## Linear Search

<v-clicks depth=3>

- Linear search has a runtime complexity of O(n). 
- The worse case scenario is when the target value is at the end of an array, forcing the program to look through every other value beforehand. 
- This makes linear search a very arduous process. But what search can we use instead to optimize runtime complexity?

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

//GeeksForGeeks
public class LinearSearch {

  	static int search(int a[], int n, int x)
    {
        for (int i = 0; i < n; i++) {
            if (a[i] == x)
                return i;
        }

        return -1;
    }
``` 
---

### Binary Search 

<v-clicks depth=3>

- Binary search is where a program repeatedly cuts an array in half to find a target value. It requires a **sorted array** in increasing value. 
- If the target value is less than or greater than one half, we can discard that part until we find the value. 

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

//CodeHS
 public class BinarySearch {
    public static int binarySearch(int[] numbers, int target) {
        int begin = 0;
        int end = numbers.length - 1;
        int counter = 0;

        while (begin <= end) 
        {
            counter++;
            // Find mid-point
            int mid = (begin + end) / 2;
            int current = numbers[mid];

            // Test mid-point
            if (target == current) 
            {
                System.out.println("Binary Search Steps: " + counter);
                return mid;
            }
            // Too high
            else if (target < current) 
            {
                end = mid - 1;
            }
            // Too low
            else 
            {
                begin = mid + 1;
            }
        }
        return -1; // Not found
    }
 }

```
---

### Recursive Binary Search

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

//GeeksForGeeks
 int binarySearch(int arr[], int l, int r, int x) {
    if (r >= l && l <= arr.length - 1) {

        int mid = l + (r - l) / 2;

        // If the element is present
        // at the middle itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than mid, then it can
        // only be present in left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);

        // Else the element can only be present
        // in right subarray
        return binarySearch(arr, mid + 1, r, x);
    }

    // We reach here when element is not present in
    // array
    return -1;
}

```
---

### Runtime Complexity 

<v-clicks depth=3>

- Binary Search has a runtime complexity of O(log n), making the search time grow logarithmically with the data size. 
- Because of this, binary search is significantly faster than linear search.
- However, if a program contains a small, unsorted array, linear search may be a better option.

</v-clicks>

---

### Sorting Methods 

<v-clicks depth=3>

- Sorting methods are also helpful to find a target value in an array. 
- There are several sorting methods, but we will go over Selection, Insertion, and Merge Sort.

</v-clicks>

--- 

### Selection Sort 

<v-clicks depth=3>

- Selection Sort is a searching algorithm, where the program repeatedly finds the smallest element in the array and adds it to the front. 
- The runtime complexity of Selection Sort is O(n2), which makes it a bit slower than other sorting methods, such as Merge Sort. 

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

//Baeldung
public static void sortAscending(final int[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        int minElementIndex = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[minElementIndex] > arr[j]) {
                minElementIndex = j;
            }
        }

        if (minElementIndex != i) {
            int temp = arr[i];
            arr[i] = arr[minElementIndex];
            arr[minElementIndex] = temp;
        }
    }
}

```
---

### Insertion Sort 

<v-clicks depth=3>

- Insertion Sort compares two adjacent values and swaps the two positions if the second element is smaller than the first. 
- The best runtime complexity of Insertion Sort is O(n) if the array is already sorted.
- The average and worst case is O(n2) if the array is randomly or reversed ordered. 

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

public static void  insertionSort(int arr[], int n)
{
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;

        /* Move elements of arr[0..i-1], that are
           greater than key, to one position ahead
           of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

```
---

### Merge Sort 

<v-clicks depth=3>

- Merge Sort, or the "divide and conquer" method, recursively divides an input array into two halves before recursively sorting them and merging them back together to obtain the final array.
- The best runtime complexity of Merge Sort is O(n log n) when the array is sorted or nearly sorted. 
- The average and worst case is also O(n logn) when the array is randomly or reverse ordered. 

</v-clicks>

---

```java {all|1-3|1-3,12,15,19|5-6|5-6,16|7-8|10|all}

//Baeldung
public static void mergeSort(int[] a, int n) {
    if (n < 2) {
        return;
    }
    int mid = n / 2;
    int[] left = new int[mid];
    int[] right = new int[n - mid];

    for (int i = 0; i < mid; i++) {
        left[i] = a[i];
    }
    for (int i = mid; i < n; i++) {
        right[i - mid] = a[i];
    }
    mergeSort(left, mid);
    mergeSort(right, n - mid);

    merge(a, left, right, mid, n - mid);
}

```
--- 

### Packages

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
