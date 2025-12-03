# Methods and Arrays: Annotated Solutions (With Inline Comments)

Each solution includes explanations to help understand the flow and purpose of each step.

## Problem 1 — Sum Using a Method

We loop through the array using indices and accumulate a running total.

```java
public void run() {
    int[] arr = {3, 9, 2, 7, 4};

    int result = sumArray(arr);
    System.out.println("Sum = " + result);
}

public int sumArray(int[] arr) {
    int total = 0;

    // Loop through all elements using indices
    for (int i = 0; i < arr.length; i++) {
        total += arr[i];   // add element to total
    }

    return total;  // return the computed sum
}
```


## Problem 2 — Add a Bonus to Every Mark

Because arrays are passed by reference, modifying `marks[]` inside the method changes it in `run()`. 

In this example, we will consider it an acceptable design decision to modify the original `marks[]` array — presumably, we are no longer interested in the original values in `marks[]`.

```java
public void run() {
    int[] marks = {10, 7, 8, 9, 6};

    // Print original marks
    System.out.print("Original: ");
    for (int i = 0; i < marks.length; i++) {
        System.out.print(marks[i] + " ");
    }
    System.out.println();

    addBonus(marks, 2); // adds +2 to every mark

    // Print updated marks
    System.out.print("After bonus: ");
    for (int i = 0; i < marks.length; i++) {
        System.out.print(marks[i] + " ");
    }
}

public void addBonus(int[] marks, int bonus) {
    // Modify each element by adding the bonus
    for (int i = 0; i < marks.length; i++) {
        marks[i] = marks[i] + bonus;
    }
}
```

## Problem 3 — Count Above Threshold

This demonstrates returning a computed result based on array scanning.

```java
public void run() {
    int[] arr = new int[5];

    // Read 5 integers
    for (int i = 0; i < arr.length; i++) {
        arr[i] = readInt("Enter value #" + (i + 1) + ": ");
    }

    int limit = readInt("Enter limit: ");

    int count = countAbove(arr, limit);

    System.out.println("Count above " + limit + ": " + count);
}

public int countAbove(int[] arr, int limit) {
    int count = 0;

    // Count values strictly greater than limit
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] > limit) {
            count++;
        }
    }

    return count;
}
```


## Problem 4 — Copy Array (Method Returns a New Array)

Before we do anything useful, we'll just try to write a method that simply returns a new copy of an array passed through a parameter.

The `original[]` array is untouched. Our method creates a copy — a new array — as a return result and we store it in `copy[]`.

```java
public void run() {
    int[] original = {4, 1, 9};

    int[] copy = copyArray(original);

    // Print both arrays
    System.out.print("Original: ");
    for (int i = 0; i < original.length; i++) {
        System.out.print(original[i] + " ");
    }
    System.out.println();

    System.out.print("Copy:     ");
    for (int i = 0; i < copy.length; i++) {
        System.out.print(copy[i] + " ");
    }
}

public int[] copyArray(int[] arr) {

    int[] result = new int[arr.length]; // new array of same size

    // Copy values one by one
    for (int i = 0; i < arr.length; i++) {
        result[i] = arr[i];
    }

    return result; // return new independent array
}
```

This is different than working with an array as a reference because we have preserved the unmodified original array.


## Problem 5 — Extract the Middle Pair

For best practice, we compute middle indices using `.length / 2` to avoid hard-coding or using *magic numbers*.

```java
public void run() {
    int[] nums = {4, 7, 9, 12, 15, 20};

    int[] mid = middleTwo(nums);

    System.out.println("Middle two result: " + mid[0] + " " + mid[1]);
}

public int[] middleTwo(int[] nums) {

    int middle = nums.length / 2; // right-middle index
    int leftMiddle = middle - 1;  // left-middle index

    int[] result = new int[2];

    result[0] = nums[leftMiddle];
    result[1] = nums[middle];

    return result;
}
```


## Problem 6 — Multiply All Elements

Here, the design calls for a method that modifies the original array. We'll write a method that uses the array by reference.

```java
public void run() {
    int[] arr = {2, 4, 6};

    System.out.print("Before: ");
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " ");
    }
    System.out.println();

    multiplyAll(arr, 3); // modify array in-place

    System.out.print("After:  ");
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " ");
    }
}

public void multiplyAll(int[] arr, int factor) {

    // Multiply each element
    for (int i = 0; i < arr.length; i++) {
        arr[i] = arr[i] * factor;
    }
}
```


## Problem 7 — Index of Target (Search Method)

A simple linear search using indices. 

```java
public void run() {
    int[] arr = {5, 8, 2, 8, 1};

    int target = readInt("Enter target: ");

    int result = findIndex(arr, target);

    System.out.println("Found at index: " + result);
}

public int findIndex(int[] arr, int target) {

    // Scan array until match found
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i; // return the first match
        }
    }

    return -1; // not found
}
```


## Problem 8 — Reverse Copy

The design specifically calls for a new array, so we have our method make a copy and return it. Unlike Problem 4 (above) though, the new array is filled from back to front. 

```java
public void run() {
    int[] arr = {3, 7, 1, 9};

    int[] reversed = reverseCopy(arr);

    System.out.print("Original: ");
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " ");
    }
    System.out.println();

    System.out.print("Reversed: ");
    for (int i = 0; i < reversed.length; i++) {
        System.out.print(reversed[i] + " ");
    }
}

public int[] reverseCopy(int[] arr) {

    int[] result = new int[arr.length];

    // Fill result from end to beginning
    for (int i = 0; i < arr.length; i++) {
        result[i] = arr[arr.length - 1 - i];
    }

    return result;
}
```


## Problem 9 — Replace Negatives

Modify only negative elements. In this case, we make the design decision to allow overwriting of the original array's values.

```java
public void run() {
    int[] arr = {-3, 4, -1, 7};

    replaceNegatives(arr);

    System.out.print("Updated: ");
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " ");
    }
}

public void replaceNegatives(int[] arr) {

    // Only replace negatives
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] < 0) {
            arr[i] = 0;
        }
    }
}
```


## Problem 10 — Pairwise Sums

Each result element is the sum of two neighbours. The algorithm necessitates a new array that is one element smaller than the original.

```java
public void run() {
    int[] arr = {4, 6, 2, 5};

    int[] result = pairwiseSums(arr);

    System.out.print("Pairwise sums: ");
    for (int i = 0; i < result.length; i++) {
        System.out.print(result[i] + " ");
    }
}

public int[] pairwiseSums(int[] arr) {

    // New array is one element shorter
    int[] sums = new int[arr.length - 1];

    // Add pairs of neighbours
    for (int i = 0; i < sums.length; i++) {
        sums[i] = arr[i] + arr[i + 1];
    }

    return sums;
}
```

