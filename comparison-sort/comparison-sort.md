# Comparison Sort

![image](https://github.com/dopecello/algo-repo/assets/105554094/25d6c3be-f1fe-4699-ac63-a8e2024416d6)
![image](https://github.com/dopecello/algo-repo/assets/105554094/bb61c65c-9ef3-4f11-b43e-f615c33eb3af)
![image](https://github.com/dopecello/algo-repo/assets/105554094/c7291140-bdce-44e3-b14c-1b152c278c83)
![image](https://github.com/dopecello/algo-repo/assets/105554094/928c300c-ffba-42f9-940f-b31b9b16b34e)

## What I don't know right off the bat

When I read this problem, I initially never that about different versions of sorting algorithms. From the problem description, there is a **comparison sort** and a **counting sort**. 

### Comparison Sort

From the [notes here](http://www.cs.cmu.edu/~avrim/451f11/lectures/lect0913.pdf), it gives a reference to an academic paper about Comparison-Based Lower Bounds for Sorting. Definitely a heady topic. I skimmed through it and learned the following:

- The fastest time a sorting algorithm gun run is something to the extent of  `Ω(n log n)` (or like the problem says, `n x log n`)
- There are names for this type of algorithm: Quicksort, Mergesort, and Insertion-Sort
- The business of sorting is derived from the Divide and Conquer (DAC) algorithm.
     - **Divide**: This involves dividing the problem into smaller sub-problems.
     - **Conquer**: Solve sub-problems by calling recursively until solved.
     - **Combine**: Combine the sub-problems to get the final solution of the whole problem.
- The point of DAC stems from the ability to solve a larger problem by breaking it down into smaller components instead of attacking a large problem head-on. It also increases the speed of solving large problems. 

Although it is important to know. A traditional DAC algorithm need not be made for this problem. I delved into what the problem requires to be solved. An *alternative sort.*

### Counting Sort

The other sorting method, the counting sort, does not require comparison. Instead, we can create an integer array whose index range covers the entire range of values in the array to sort. 

### How to set up the problem

I first needed to know how to make an array filled with 100 zeros while not sacrificing the speed of the algorithm. [This StackOverflow article](https://stackoverflow.com/questions/1295584/most-efficient-way-to-create-a-zero-filled-javascript-array) showed me that there is one slow solution and 2 fast solutions:

- Slow 
     - `new Array(len).fill(0);`
- Fast 
     - `(arr = []).length = len; arr.fill(0);`
     - `arr = Array(n)`

I asked ChatGPT to give me an explanation one which one is better so I can understand it a little better that the one-upping on StackOverflow. My prompt was: `Given that I am to make a counting sorting algorithm for an array of integers of a length of 100, how do I set up the problem by reating a results array that is an array of one hundred zeros? I saw that (arr = []).length = len; arr.fill(0); and arr = Array(n); were two possible approaches. Can you tell me what is the most efficient solution and explain why? Please isolate you answer on only how to create the array with 100 zeros.`

The response from ChatGPT is as follows:

> Creating a new array filled with a certain number of zeros can be done with the `Array()` constructor and the `fill()` method in JavaScript. Here's how you can do it:

```javascript
let arr = new Array(100).fill(0);
```

> In this line, `new Array(100)` creates a new array with 100 undefined elements, and `fill(0)` fills every element in the array with 0.

> Now, regarding the efficiency of the two approaches you've mentioned:

```javascript
// Approach 1
let arr1 = [];
arr1.length = 100;
arr1.fill(0);

// Approach 2
let arr2 = new Array(100).fill(0);
```

> Both approaches will result in an array of 100 zeros. However, the second approach is more concise and arguably more readable. 

> Performance-wise, both should be roughly similar. Both `Array(n).fill(0)` and `(arr = []).length = n; arr.fill(0);` are O(n) operations - they take linear time in the size of the array. However, there may be minor differences in performance between the two due to how JavaScript engines optimize the operations, but these differences would likely be negligible and are not typically a concern unless you are dealing with extremely large arrays or need to perform this operation an extremely large number of times.

> So in summary, the following is an efficient way to create an array of 100 zeros:

```javascript
let arr = new Array(100).fill(0);
```

> This is both readable and efficient in terms of time complexity.

From this response, I will take the bottom solution as it is more readable


## My first attempt

I tried implementing the efficient solution first and came up with the following:

```javascript
function countingSort(arr) {
    let results = new Array(100).fill(0)
    const sorted = arr.sort((a, b) => a + b)
    for (let i = 0; i < arr.length; i++) {
        results[sorted[i]] += 1
    }
    return results;
}
```

To my surprise, I actually nailed it with this solution. Passed all test cases. First, I made the array of zeros like I researched. Then, all I did was sort the numbers in ascending order using the `sorted` syntax. Then, I figured that now that it is sorted, the value of `i` in the sorted index **will correspond** with the index of the results array I made, so, if the number was 59, then the 59th index of `results` would add one to it. Lo and behold, it worked. I'm really proud of myself!

## What I learned

- How to construct an array dynamically. I created an array with 100 zeros in it as a result for this problem. That solution looked like:
```javascript
let arr = new Array(100).fill(0);
```