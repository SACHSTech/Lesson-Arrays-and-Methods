# Methods and Arrays

This lesson explains how arrays behave when you pass them into methods, modify them inside methods, and return them from methods. Understanding this behaviour is essential for writing clean, reusable, and well‑structured programs.

Each technique includes:

1. **The goal** — What problem we are solving  
2. **The design approach** — Why this technique works  
3. **The code** — A clear example program  
4. **Explanation** — What is happening step-by-step  


## 1. Arrays as Parameters

### Goal  
Use a method to process an array (sum, count, search, etc.) that was created elsewhere.

### Design Approach  
When you pass an array to a method, Java passes a **reference**, not a copy.  
This means the parameter variable refers to the **same array** as the variable in `run()`.

This is useful for performing calculations or searching the array without changing it.

### Code: Summing Elements

```java
public class Example1 extends ConsoleProgram {
    public void run() {

        int[] intArray = {5, 6, 7, 8};

        int sum = sumArray(intArray);

        System.out.println("Sum = " + sum);
    }

    public int sumArray(int[] myArray) {
        int total = 0;

        for (int i = 0; i < myArray.length; i++) {
            total += myArray[i];
        }

        return total;
    }
}
```

### Explanation  
`myArray` and `intArray` both reference the **same** array. Here, the method reads the data but does not modify it.


## 2. Modifying Arrays Inside Methods

### Goal  
Understand that changes inside a method affect the original array.

### Design Approach  
Since arrays are passed by reference, updating elements in the parameter array updates the original one.  

This is ideal for methods that:

- enforce a rule on every element  
- adjust values  
- clean/normalize data  

### Code: Modifying the First Element

```java
public class Example2 extends ConsoleProgram {
    public void run() {

        int[] intArray = {5, 6, 7, 8};

        increaseFirst(intArray, 3);

        System.out.println(intArray[0]);  // prints 8
    }

    public void increaseFirst(int[] myArray, int increase) {
        myArray[0] = myArray[0] + increase;
    }
}
```

### Explanation  
Because both variables refer to the same array, updating `myArray[0]` updates `intArray[0]`.

This technique is heavily used when you want helper methods that “apply a rule” to an entire dataset.


## 3. Returning Arrays From Methods

### Goal  
Create new arrays inside a method and return them to the caller.

### Design Approach  
Methods can:

- create a new array  
- fill it with selected or transformed data  
- return the array reference  

This is useful when you need a derived result:
- the first and last elements  
- a filtered list  
- a list of differences or statistics  

### Code: Returning a New Array

```java
public class Example3 extends ConsoleProgram {
    public void run() {

        int[] fullArray = {5, 6, 7, 8};

        int[] result = firstLast(fullArray);

        // result now contains [5, 8]
    }

    public int[] firstLast(int[] fullArray) {

        int[] output = new int[2];

        output[0] = fullArray[0];
        output[1] = fullArray[fullArray.length - 1];

        return output;
    }
}
```

### Explanation  
The method:

1. Allocates a new 2‑element array  
2. Copies the first and last values  
3. Returns the reference  

The resulting array is **independent** from the original:

```
fullArray  --->  [5][6][7][8]

result     --->  [5][8]
```


## Summary

In summary, remember these quirks about working with arrays and methods:

- **Arrays as parameters**: Methods receive references, not copies.
- **Modifying arrays inside methods**: Changes inside the method affect the original array.
- **Returning arrays**: Methods can create and return new arrays
