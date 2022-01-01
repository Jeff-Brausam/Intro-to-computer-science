# Intro to Computer Science

As a self taught developer I find these concepts difficult to grasp, so these notes are really just to help me understand.
The goal of this is provide a stronger foundation and understanding of computer science and algorithms. This is all coming from a 
web developer standpoint, so solutions are written in Javascript.

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
If it uses recursion, it is usually logarithmic (because you are splitting the work in half each cycle).
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

Human time is almost always more valuable than computer time. Readability is generally better than optimization. Only try to optimize as you hit scaling problems.

## Algorithms

Note: There are probably better and more optimized ways of solving these algorithms. These are just written in ways to more easily disect what the algorithm is doing.

## Iterative Sorts

#### Bubble Sort

The bubble sort algorithm does this: Go through each number individually in a list, and assess whether or not the number on the left is bigger or smaller, if it is bigger the two numbers switch places. 

This algorithm is really never used, if ever in the real world. 

<img src="https://btholt.github.io/complete-intro-to-computer-science/e164c2436ed5486ed13e54135a1d009a/bubblesort.gif" alt="bubble sort" width="300" height="200" />

```javascript 
const BubbleSort = (nums) => { 
   let swapped = false; 
   do { 
     swapped = false; 
     for (let i = 0; i < nums.length; i++) { 
      if (nums[i] > nums[i + 1]) { 
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

<img src="https://btholt.github.io/complete-intro-to-computer-science/e1c75fd04db2c886c086edd156ba5ff2/insertionsort.gif" alt="" width="200" height="300" />


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

##### When would you use an insertion sort over a quick/merge sort?
The case in which you would use an insertion sort is when a list is pretty close to already being sorted. But if it isn't, then something like merge or quick sort would be better.

## Recursion
The point of recursion is to break down a problem, into smaller problems, until you have a problem that you can solve.
Rather than using loops, you instead are having the function call itself until solved.
  
The tradeoff is readability vs performance. Frequently but not always an iterative solution will be faster and more efficent as the problem scales. Realizing these patterns is extremely important, as you will see the concept of recursion in merge and quick sorts. 

Recursion consists of two things: a base case - a case where the problem is defined as complete, and a recursive call - a call to the same function, until it solves itself.

Here are some common examples:

```javascript 
const fibonacci = (n) => {
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
const nestedAdd = (array) => {
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
const factorial = (n) => {
  if (n >= 1) return;
  return n * factorial(n - 1);
}
```
## Recursive Sorts
### Merge Sort 
Merge sort is a sort that recursively divides the set into groups of at most two, then recursively sorts each half. It compares each number one at a time, moving the smallest number to the left of the pair. 

So we need two functions. One is the first function to break down the big lists into smaller lists (the recursive function) and the other is a function that takes **two** sorted, and returns back **one** sorted function. The first function is recursive and the second is not. People usually define the first as mergeSort, and the second as merge (or stitch).
 
Most javascript engines live v8 will use merge sort under the hood for the .sort method. Some other engines use quick sort.  

<img src="https://btholt.github.io/complete-intro-to-computer-science/a29c0dd0186d1f8cef3c5ebdedf3e5a3/mergesort.gif" alt="" width="300" height="200" />

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
### Quick Sort
The basic gist of a quick sort, is that you take the last element in the list and call that the pivot. Everything that's smaller than the pivot gets put into a "left" list and everything that's greater get's put in a "right" list. You then call quick sort on the left and right lists independently (hence the recursion.) After those two sorts come back, you concatenate the sorted left list, the pivot, and then the right list (in that order.) The base case is when you have a list of length 1 or 0, where you just return the list given to you.

Something important to note, is the number you use as a pivot does not go into either array. It is just used as a reference to essentially create less comparisons.

Sorted lists, or reverse sorted lists are actually a disaster for quick sort because of this pivot. There are other versions to mitigate around this, like using quicksort 3. 

<img src="https://btholt.github.io/complete-intro-to-computer-science/static/4a14b48b386ca8457bbbef9063a27135/804b2/quicksort-diagram.png" alt="recursion" height="700px" width="400px" />

```javascript
const quickSort = (nums) => {
  if (nums.length < 2) {
    return nums;
  }
  
  let pivot = nums[nums.length - 1];
  
  let left = []
  let right = []
  
  for (let i = 0; i < nums.length - 1; i++){
    if(nums[i] < pivot){
      left.push(nums[i])
    } else {
      right.push(nums[i])
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```



## Non-Comparison Sorts
### Radix Sort

Radix sort is an sorting algorithm that sorts data with integer keys by grouping the keys by individual digits that share the same significant position and value (place value). There are no actual number compares with this kind of algorithm (no if one number is greater than the other). It is just simply checking from the furthest right digit, sorting those it into buckets (an array that holds and 10 arrays, one for each digit 0-9), then dequeueing it back the next 10s place until it loops through all of the numbers. 

Radix sort is useful when you start dealing with huge numbers such as 50,000, but if it something like 500, other sorting algorithms would be more efficent.

https://user-images.githubusercontent.com/48197040/147708321-fbb68800-f952-4944-9280-ddde7e19988f.mp4


```javascript
function getDigit(number, place, longestNumber) {
  const string = number.toString();
  const size = string.length;

  const mod = longestNumber - size;
  return string[place - mod] || 0;
}

function findLongestNumber(array) {
  let longest = 0;
  for (let i = 0; i < array.length; i++) {
    const currentLength = array[i].toString().length;
    longest = currentLength > longest ? currentLength : longest;
  }
  return longest;
  /* 
   Alternatively you can do this 
   let largest = Math.max(...array).toString().length; 
      return largest;
   */
}

function radixSort(array) {
  const longestNumber = findLongestNumber(array);

  const buckets = new Array(10).fill().map(() => []); // make an array of 10 arrays

  for (let i = longestNumber - 1; i >= 0; i--) {
    // Enqueue into the buckets
    while (array.length) {
      const current = array.shift();
      buckets[getDigit(current, i, longestNumber)].push(current);
    }
    // Dequeue from the buckets
    for (let j = 0; j < 10; j++) {
      while (buckets[j].length) {
        array.push(buckets[j].shift());
      }
    }
  }

  return array;
}
```
## Binary Search
Binary search is an algorithm that takes a **sorted** list, and an item and does something similar to this situation. Say you have a phonebook and you are looking for a name. Rather than going a page at a time (linear or simple search, like a for loop), you'll open the book more or less to the middle (or say you do, for argument's sake.) From there, if the name you're looking for is smaller/earlier in the alphabet, you'll go halfway to the smaller/earlier side of the book, and so-on-and-so-forth, keeping going halfway until eventually you land on the name you're looking for. 

```javascript
const BinarySearch = (sortedlist, item) => {
  let low = 0;
  let high = sortedlist.length - 1;

  while (low <= high) {
    let middle = low + high;
    let guess = sortedlist[middle];

    if (guess == item) {
      return Math.floor(middle);
    }
    if (guess > item) {
      high = middle - 1;
    } else {
      low = middle + 1;
    }
  }

  return null;
};
```

## Arrays
## Array List
This is actually a bit of a moot point for JavaScript developers: we have normal arrays and no choice beyond anything in the matter. In other languages, however, there are multiple types of array and you choose which one you need based on the sort operations you intend on doing on that array. Lets say there is no such thing as an array in Javascript. We only have one thing: objects. So we'd need to implement the array numbering ourselves. But not just that, we'd have to implment adding numbers, removing numbers, getting numbers, etc. 

Array list struggles when it comes to having to add something in the middle, or deleting items off the array, because then everything else has to shift. They are good though for things you have to do a lot of lookups on, or addition (adding things to the end). This is to implement a dynamic array.

```javascript
class ArrayList {
  constructor() {
    this.length = 0;
    this.data = {};
  }
  push(value) {
    this.data[this.length] = value;
    this.length++;
  }
  pop() {
    const ans = this.data[this.length - 1];
    delete this.data[this.length - 1];
    this.length--;
    return ans;
  }
  get(index) {
    return this.data[index];
  }
  delete(index) {
    const ans = this.data[index];
    this._collapseTo(index);
    return ans;
  }
  _collapseTo(index) {
    for (let i = index; i < this.length; i++) {
      this.data[i] = this.data[i + 1];
    }
    delete this.data[this.length - 1];
    this.length--;
  }
  serialize() {
    return this.data;
  }
}
```
## Linked List
LinkedList is made of a bunch of nodes that point to the next one in the list. Every node in a LinkedLists has two properties, the value of whatever is being store and a pointer to the next node in the list. These nodes will not be sequential in memory, meaning we don't get the easy lookups but the advantage is that adding things is easy since we don't have to do the compacting we had to do with ArrayList.

The main thing that gives LinkedList an advantage over ArrayList, is that the inserts and deletes work great. It is ideal when you're doing a lot of writes and deletions. In general, ArrayList tends to be the most generally useful because the lookup speed is so helpful, but LinkedLists definitely have their place.

There are variations of LinkedList, called the Double LinkedList. Rather then just having a forward, it also has a previous. You really never have to worry about these in Javascript because arrays are quite optimized, but in other languages like C or Java it could make a pretty big difference. With Linkedlists you do better with memory since you do not have to define it, but ArrayLists require you to define it.

```javascript
class LinkedList {
  constructor() {
    this.tail = this.head = null;
    this.length = 0;
  }
  push(value) {
    const node = new Node(value);
    this.length++;
    if (!this.head) {
      this.head = node;
    } else {
      this.tail.next = node;
    }
    this.tail = node;
  }
  pop() {
    if (!this.head) return null;
    if (this.head === this.tail) {
      const node = this.head;
      this.head = this.tail = null;
      return node.value;
    }
    const penultimate = this._find(
      null,
      (value, nodeValue, i, current) => current.next === this.tail
    );
    const ans = penultimate.next.value;
    penultimate.next = null;
    this.tail = penultimate;
    this.length--;
    return ans;
  }
  _find(value, test = this.test) {
    let current = this.head;
    let i = 0;
    while (current) {
      if (test(value, current.value, i, current)) {
        return current;
      }
      current = current.next;
      i++;
    }
    return null;
  }
  get(index) {
    const node = this._find(index, this.testIndex);
    if (!node) return null;
    return node.value;
  }
  delete(index) {
    if (index === 0) {
      const head = this.head;
      if (head) {
        this.head = head.next;
      } else {
        this.head = null;
        this.tail = null;
      }
      this.length--;
      return head.value;
    }

    const node = this._find(index - 1, this.testIndex);
    const excise = node.next;
    if (!excise) return null;
    node.next = excise.next;
    if (!node.next.next) this.tail = node.next;
    this.length--;
    return excise.value;
  }
  test(search, nodeValue) {
    return search === nodeValue;
  }
  testIndex(search, __, i) {
    return search === i;
  }
  serialize() {
    const ans = [];
    let current = this.head;
    if (!current) return ans;
    while (current) {
      ans.push(current.value);
      current = current.next;
    }
    return ans;
  }
}

class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```
## Trees
## Binary Search Tree
Trees are another way to structure data. Binary search tree has to be in a sorted order just like a binary search does. At its core, a tree is very similar to a LinkedList. You have nodes. Those nodes have values and pointers to other nodes. Unlike a LinkedList which only has one next pointer (or maybe a next and previous) trees can have many pointers. This hiearchy is important to remember, as one node splits into two, and that splits in the same pattern from there. A binary tree will have two children at most. 

So we have one node that is the root. That node can have a left child and a right child. It can have both, one, or neither. Every node has a value. Both children are nodes just like the root: they can 0-2 children as well and will always have a value (there are no nodes without values.) Every value in a node's left tree is smaller than its value and every node in its right tree is larger than its value. Values that are equal can go either way, just be consistent. In the example below, everything below 8 has to live on the left side, everything above has to be on the right. You need to make sure you understand this concept and are able to notice it in your code, otherwise it does not fit as a binary search tree (it could be another though). Notice how it is consistent, if the number is higher than the last it goes to the right, if smaller it does to the left.

The average case scinario of lookups in the tree are log(n). A place that uses trees for lookups are database indexes, so if you get IDs from MondoDB, and want an index, it will build a tree out of all of your ideas and have pointers to other IDs. Maybe not binary but certainly a tree.

<img src="https://btholt.github.io/complete-intro-to-computer-science/static/8333499546d84a58751a5a12a8f34e9b/533c1/bst.png" width="300px" height="300px" />

```javascript
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (this.root === null) {
      this.root = new Node(value);
    } else {
      let current = this.root;
      while (true) {
        if (current.value > value) {
          // go left

          if (current.left) {
            current = current.left;
          } else {
            current.left = new Node(value);
            break;
          }
        } else {
          // go right
          if (current.right) {
            current = current.right;
          } else {
            current.right = new Node(value);
            break;
          }
        }
      }
    }
    return this;
  }
  toJSON() {
    return JSON.stringify(this.root.serialize(), null, 4);
  }
  toObject() {
    return this.root.serialize();
  }
}

class Node {
  constructor(value = null, left = null, right = null) {
    this.left = left;
    this.right = right;
    this.value = value;
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    return ans;
  }
}
```

## Resources
#### General
Most of these concepts are from here: https://btholt.github.io/complete-intro-to-computer-science/

#### Algorithms

Visual Algorithms - https://visualgo.net/en

##### Big O resources

https://web.mit.edu/16.070/www/lecture/big_o.pdf
https://www.bigocheatsheet.com/
