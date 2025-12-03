# Arrays and Methods

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

### Behaviour of Arrays vs Primitives as Parameters
For a clear comparison of this behaviour, see [this note](https://davecheng-tech.github.io/Class-Notes-and-Addenda/ICS3U/methods_primitives_vs_arrays) for a side-by-side illustration of what happens to an `int` vs `int[]` when used in a method parameter.


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

<br>

# Practice Problems — Arrays and Methods

Each problem reinforces the ideas from the above lesson: passing arrays to methods, modifying arrays inside methods, and returning arrays from methods.  

Annotated solutions to these problems can be found [here](SOLUTIONS.md).


## Problem 1 — Sum Using a Method

Write a method `sumArray(int[] arr)` that returns the sum of all elements in the array.

In your `run()` method:

- Create an `int[]` with 5 values  
- Call `sumArray(arr)`  
- Print the returned sum

### Example Input
```
[3, 9, 2, 7, 4]
```

### Example Output
```
Sum = 25
```

<br>

## Problem 2 — Add a Bonus to Every Mark

Write a method:

```java
public void addBonus(int[] marks, int bonus)
```

that increases **every** mark in the array by the given bonus amount.

In your `run()` method:

- Create an array of 5 marks  
- Print the original marks on one line  
- Call `addBonus(marks, 2)` to add `+2` to all marks  
- Print the updated marks on one line

### Example Output
```
Original: 10 7 8 9 6
After bonus: 12 9 10 11 8
```

<br>

## Problem 3 — Count Above Threshold

Write a method:

```java
public int countAbove(int[] arr, int limit)
```

that returns how many values in the array are **greater than** `limit`.

In your `run()` method:

- Ask the user for 5 integers and store them in an array  
- Ask for a `limit` value  
- Call `countAbove(arr, limit)` and print the result

### Example Input
```
Values: 8 12 3 14 6
Limit: 10
```

### Example Output
```
Count above 10: 2
```

<br>

## Problem 4 — Copy Array (Method Returns New Array)

Write a method:

```java
public int[] copyArray(int[] arr)
```

that returns a **new** array containing the same values as `arr`.

In your `run()` method:

- Create an `int[]` with a few values  
- Call `copyArray(arr)` and store the result  
- Print both arrays on separate lines

### Example Input
```
[4, 1, 9]
```

### Example Output
```
Original: 4 1 9
Copy:     4 1 9
```

<br>

## Problem 5 — Extract the Middle Pair

Write a method:

```java
public int[] middleTwo(int[] nums)
```

that returns a new array of size 2 containing the **two middle elements** of an **even-length** input array.

In your `run()` method:

- Create an even-length `int[]`  
- Call `middleTwo(nums)`  
- Print the two returned values

### Example Input
```
Input array: [4, 7, 9, 12, 15, 20]
```

### Example Output
```
Middle two result: 9 12
```

<br>

## Problem 6 — Multiply All Elements

Write a method:

```java
public void multiplyAll(int[] arr, int factor)
```

that **modifies** the original array by multiplying each element by `factor`.

In your `run()` method:

- Create a small `int[]`  
- Print it  
- Call `multiplyAll(arr, factor)`  
- Print the array again to show the change

### Example Input
```
Array: 2 4 6
Factor: 3
```

### Example Output
```
Before: 2 4 6
After:  6 12 18
```

<br>

## Problem 7 — Index of Target (Method)

Write a method:

```java
public int findIndex(int[] arr, int target)
```

that returns the index of `target`, or `-1` if it does not exist in the array.

In your `run()` method:

- Create an `int[]` with some values  
- Ask the user for a target number  
- Call `findIndex(arr, target)` and print the result

### Example Input
```
Array:  [5, 8, 2, 8, 1]
Target: 8
```

### Example Output
```
Found at index: 1
```

(You may choose to return the **first** index where it appears.)

<br>>

## Problem 8 — Reverse Copy

Write a method:

```java
public int[] reverseCopy(int[] arr)
```

that returns a **new array** containing the values of `arr` in reverse order.

In your `run()` method:

- Create an `int[]`  
- Call `reverseCopy(arr)`  
- Print both the original and reversed arrays

### Example Input
```
[3, 7, 1, 9]
```

### Example Output
```
Original: 3 7 1 9
Reversed: 9 1 7 3
```

<br>

## Problem 9 — Replace Negatives

Write a method:

```java
public void replaceNegatives(int[] arr)
```

that modifies the array by turning all **negative numbers** into `0`.

In your `run()` method:

- Create an `int[]` that includes negative and positive values  
- Print it  
- Call `replaceNegatives(arr)`  
- Print the updated array

### Example Input
```
[-3, 4, -1, 7]
```

### Example Output
```
Updated: 0 4 0 7
```

<br>

## Problem 10 — Pairwise Sums

Write a method:

```java
public int[] pairwiseSums(int[] arr)
```

that returns a **new array** containing the sums of each pair of neighbours.  
The new array will have length `arr.length - 1`.

In your `run()` method:

- Create an `int[]`  
- Call `pairwiseSums(arr)`  
- Print the result

### Example Input
```
[4, 6, 2, 5]
```

### Example Output
```
Pairwise sums: 10 8 7
```
