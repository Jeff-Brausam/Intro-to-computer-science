# Intro to computer science

As a self taught developer I find these concepts difficult to grasp, so these notes are really just to help me understand.
The goal of this is provide a stronger foundation and understanding of computer science and algorithms.

## The Big O notation

### What is Big O notation?

Big O notation is used in Computer Science to describe the performance or complexity of an algorithm. Big O specifically describes the worst-case scenario, and can be used to describe the execution time required or the space used (e.g. in memory or on disk) by an algorithm.

From a purely mathematical perspective, say we have the equation 3x² + x + 1. If we plug in 5, the first term will be 75, the second term will be 5, and the third will be 1. If we plug in huge numbers, these differences become more drastic.

Most of the piece of the pie comes from the first term, to the point we can just ignore the other terms.

In computer science, this is usually represented with n instead of x. So for n terms, it's going take us n\*n time to go through our inputs.

### How do I identify the Big O complexity?

In general easiest way to identify the Big O is really to just look for loops. The more nested loops that you have, the higher big O notation there is.
My general rules of thumb are:
If it can be accessed directly, it is a constant.
If it uses recursion in some way, it is usually logarithmic (because you are splitting the work in half each cycle).
If you have one loop, it would be linear.
If you have two loops, it would be quadratic.

Here is a little cheat sheet: https://www.bigocheatsheet.com/

### Big O complexities

| notation     | name            |
| ------------ | --------------- |
| O(1)         | constant        |
| O(log(n))    | logarithmic     |
| O((log(n))c) | polylogarithmic |
| O(n)         | linear          |
| O(n)²        | quadratic       |
| O(nc)        | polynomial      |
| O(cn)        | exponential     |

### Computational complexity vs Spatial complexity

Computational complexity is usually what people refer to unless stating otherwise with the Big O notation. Computational complexity has to do with processing (CPU related tasks), and how much time will it take to do the said task. This is also referred to as time complexity. 

Spatial complexity has to do with how much storage (RAM) will this take to complete the said task? If you have to add more arrays, it can become expensive in memory. This can become an issue if you are using something like functional programming on a device that needs to work on a device with extremely small memory.

### Know the trade-offs

Knowing the trade-offs between algorithms is one of the most important skills that you can have. You really need to gather as much information as you can before implementation. The best answer you can have in an interview when asked about big O is "it depends." You need to really pull out as much information as you can and look at things at a scale.

What are your users like? Where do they live? What kind of devices is this program running on? What kind of input or data are you taking in? Is your input already sorted or unsorted? How important is optimizing this?

Human time is almost always more valuable than computer time. Sometimes readability is better than optimization. Only try to optimize as you scale up.

## Algorithms

## Iterative Sorts

#### Bubble Sort

The bubble sort algorithm does this: Go through each number individually in a list, and assess whether or not the number on the left is bigger or smaller, if it is bigger the two numbers switch place. 

This algorithm is really never used, if ever in the real world. 

```javascript 
const BubbleSort = (nums) => { 
   let swapped = false; 
   do { 
     swapped = false; 
     for (let i = 0; i < nums.length; i++) { if (nums[i] > nums[i + 1]) { 
       const temp = nums[i]; 
       nums[i] = nums[i + 1]; 
       nums[i + 1] = temp; 
       swapped = true; 
      } 
     } 
    } while (swapped); 
    return nums; 
  };
```
#### Insertion Sort 

The insertion sort algorithm does this: You create two parts to your list. You treat the first part of your list as sorted and the second part of your list as unsorted. Its easiest to conceptualize as cards: We start with an empty left hand and the cards face down on the table. We then remove one card at a time from the table and insert it into the correct position in the left hand. To find the correct position for a card, we compare it with each of the cards already in the hand, from right to left. At all times, the cards held in the left hand are sorted, and these cards were originally the top cards of the pile on the table. 

The algorithm sorts the input numbers in place: it rearranges the numbers within the array A, with at most a constant number of them stored outside the array at any time. The input array A contains the sorted output sequence when the INSERTION-SORT procedure is finished.

Below the insertion algorithm solved like this. By definition a list of one is already sorted, so most people treat the first index (of [0]) as sorted, and the rest unsorted. From there, you start with the next element in the list (in this case, the [1] index, the second element) and loop backwards over our sorted list, asking "is the element that I'm looking to insert larger than what's here? If not, you work your way to the back of the array. If you land at the first element of the sorted part of the list, what you have is smaller than everything else and you put it at the start. You then repeat this until you've done it over the whole list!


```javascript
const InsertionSort = (arr) => {
  for (let i = 1; i < arr.length; i++) {
    let numberToInsert = arr[i];
    let j;

    for (j = i - 1; arr[j] > numberToInsert && j >= 0; j--) {
      arr[j + 1] = arr[j];
    }

    arr[j + 1] = numberToInsert;
  }
  return arr;
};
```

##### When would I use an insertion sort over a quick/merge sort?
The case in which you would use an insertion sort is when a list is pretty close to already being sorted. But if it isn't, then something like merge or quick sort would be better.

## Recursion
The point of recursion is to break down a problem, into smaller problems, until you have a problem that you can solve.
Rather than using loops, you instead are having the function call itself until solved.
  
The tradeoff is readability vs performance. Frequently but not always an iterative solution will be faster and more efficent as the problem scales. Realizing these patterns is extremely important, as you will see the concept of recursion in merge and quick sorts. 

Recursion consists of two things: a base case - a case where the problem is defined as complete, and a recursive call - a call to the same function, until it solves itself.

Here are some common examples:

```javascript 
function fibonacci(n) {
  // base case
  if (n === 2 || n === 1) {
    return 1;
  } else if (n <= 0) {
    return 0;
  }

  // recursive calls
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```
```javascript
function nestedAdd(array) {
  let sum = 0;
  for (let i = 0; i < array.length; i++) {
    const current = array[i];
    if (Array.isArray(current)) {
      sum += nestedAdd(current);
    } else {
      sum += current;
    }
  }
  return sum;
}
```
```javascript
function factorial(n) {
  if (n >= 1) return;
  return n * factorial(n - 1);
}
```
## Merge Sort 
Merge sort is a sort that recursively divides the set into groups of at most two, then recursively sorts each half. It compares each number one at a time, moving the smallest number to the left of the pair. 

So we need two functions. One is the first function to break down the big lists into smaller lists (the recursive function) and the other is a function that takes **two** sorted, and returns back **one** sorted function. The first function is recursive and the second is not. People usually define the first as mergeSort, and the second as merge (or stitch).

```javascript
const mergeSort = (nums) => {
  // base case
  if (nums.length < 2) {
    return nums;
  }

  const length = nums.length;
  const middle = Math.floor(length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);

  // merge takes two sorted lists and returns one sorted list
  return merge(mergeSort(left), mergeSort(right));
};

const merge = (left, right) => {
  const results = [];

  // go until one list runs outs
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      // shift removes the first element in an array and returns it
      // it's like .pop() for the front
      results.push(left.shift());
    } else {
      results.push(right.shift());
    }
  }

  // either left or right will be empty so you can safely concat both
  return results.concat(left, right);
};
```

## Resources

#### General
Most of these concepts are from here: https://btholt.github.io/complete-intro-to-computer-science/

#### Algorithms

visual algorithms - https://visualgo.net/en

##### Big O resources

more educational - https://web.mit.edu/16.070/www/lecture/big_o.pdf
cheat sheet - https://www.bigocheatsheet.com/
