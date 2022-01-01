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

## Data Structures
### What is a data structure? 
A data structure is an arrangement of data, you can define a way that you interact with this data and the way it is arranged in memory. Some data structures are continuous blocks of memory, in which they are located next to eachother (like an array). You have ordered data structures, hierarchical which have parent child relationships, or complex relationships. You can model real world things with data, but you need to structure it properly so that you can do particular operations on that data structure. 

Think of the DOM, you interact with it all the time but it really at its core is a tree. If you had performance issues and bottlenecks, knowing how you are traversing something will greatly help performance. 

Here are some common data structures and what they are used for. 

| Data Structure   | Common Uses         |
| ------------ | --------------- |
| Arrays & Strings         | ordered data, words        |
| Hash Tables    | optimization |
| Linked Lists | data insert/delete |
| Stackes/Queues       | creative aux DS          |
| Trees, Heaps        | hierchal data       |
| Graphs        | complex relationships      |

## Stacks and Queues
Stacks and queues are very similar to eachother. They are an ordered data structure that have opinions about the order in which things can be inserted and removed. These pretty much underly everything that you do.

For a stack, imagine it like a stack of plates. You stack them on top of eachother, and you take the last one out when removing it. Stacks store items in a last in, first out order (LIFO).

For a queue, think of waiting in line for something. You would stack it up, but always take from the bottom. A stack stores items in a first in, first out order (FIFO).

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
Trees are another way to structure data. A binary search tree has to be in a sorted order, just like a binary search does. At its core, a tree is very similar to a LinkedList. You have nodes. Those nodes have values and pointers to other nodes. Unlike a LinkedList which only has one next pointer (or maybe a next and previous) trees can have many pointers. This hiearchy is important to remember, as one node splits into two, and that splits in the same pattern from there. A binary tree will have two children at most. 

So we have one node that is the root. That node can have a left child and a right child. It can have both, one, or neither. Every node has a value. Both children are nodes just like the root: they can 0-2 children as well and will always have a value (there are no nodes without values.) Every value in a node's left tree is smaller than its value and every node in its right tree is larger than its value. Values that are equal can go either way, just be consistent. In the example below, everything below 8 has to live on the left side, everything above has to be on the right. You need to make sure you understand this concept and are able to notice it in your code, otherwise it does not fit as a binary search tree (it could be another though). Notice how it is consistent, if the number is higher than the last it goes to the right, if smaller it does to the left.

The average case scinario of lookups in the tree are log(n). A place that uses trees for lookups are database indexes, so if you get IDs from MondoDB, and want an index, it will build a tree out of all of your ideas and have pointers to other IDs. Maybe not binary but certainly a tree. In production these are not very common to see, because searching a tree can take longer than other tree methods. 

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
## AVL Tree
AVL tree is a self balancing tree, but like a binary tree it is almost never used in production. We are just using these as easy examples to explain trees. Most of the concepts are similar to the binary tree, except when adding to an AVL tree, you do this thing called a balancing. A balancing allows you to make sure you have a balanced tree. 

The basic idea for rebalncing, is that if one side of tree gets too heavy (i.e. the max height of one of its children is two more than the max height of the other child) then we need to perform a rotation to get the tree back in balance. A time you want to use self balancing trees and not just AVL, is when you have huge amounts of data (like 1000 things not 100), and you need to find things very quickly. You are willing to sacrifice add performance, and delete performance, for extreme searchability.  

#### Single Rotation
https://user-images.githubusercontent.com/48197040/147845156-430d5c5c-205f-4951-9f1d-0cc3ccad261d.mp4

There is a generalized formula you can use for rotations, in which you essentially use in a single or double rotation. Here is a generalized formula for a right rotation (if you ever implement a left just mirror this). The real main goal of a rotation is to make a tree flatter so searching is faster.

1. swap the values of nodes A and B
2. make node B the left child of node A
3. make node C the right child of node A
4. move node B's right child to its left child
(in this case they're both null)
5. make node A's _original_ left child
(which was null in this case) the left child of node B
6. update the heights of all the nodes involved

#### Double Rotation
A double rotation, is when the child is branched but rather than all on one side, it will go in a pattern like right, left, right. You need to rotate it one time left, then right to balance it (or vice versa depending on what is implemented). 

https://user-images.githubusercontent.com/48197040/147845705-c35c5bc4-1360-4bc7-b92d-9036fd782a62.mp4

```javascript
class Tree {
  constructor() {
    this.root = null;
  }
  add(value) {
    if (!this.root) {
      this.root = new Node(value);
    } else {
      this.root.add(value);
    }
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
    this.height = 1;
  }
  add(value) {
    if (value < this.value) {
      // go left

      if (this.left) {
        this.left.add(value);
      } else {
        this.left = new Node(value);
      }
      if (!this.right || this.right.height < this.left.height) {
        this.height = this.left.height + 1;
      }
    } else {
      // go right

      if (this.right) {
        this.right.add(value);
      } else {
        this.right = new Node(value);
      }
      if (!this.left || this.right.height > this.left.height) {
        this.height = this.right.height + 1;
      }
    }
    this.balance();
  }
  balance() {
    const rightHeight = this.right ? this.right.height : 0;
    const leftHeight = this.left ? this.left.height : 0;

    if (leftHeight > rightHeight + 1) {
      const leftRightHeight = this.left.right ? this.left.right.height : 0;
      const leftLeftHeight = this.left.left ? this.left.left.height : 0;

      if (leftRightHeight > leftLeftHeight) {
        this.left.rotateRR();
      }

      this.rotateLL();
    } else if (rightHeight > leftHeight + 1) {
      const rightRightHeight = this.right.right ? this.right.right.height : 0;
      const rightLeftHeight = this.right.left ? this.right.left.height : 0;

      if (rightLeftHeight > rightRightHeight) {
        this.right.rotateLL();
      }

      this.rotateRR();
    }
  }
  rotateRR() {
    const valueBefore = this.value;
    const leftBefore = this.left;
    this.value = this.right.value;
    this.left = this.right;
    this.right = this.right.right;
    this.left.right = this.left.left;
    this.left.left = leftBefore;
    this.left.value = valueBefore;
    this.left.updateInNewLocation();
    this.updateInNewLocation();
  }
  rotateLL() {
    const valueBefore = this.value;
    const rightBefore = this.right;
    this.value = this.left.value;
    this.right = this.left;
    this.left = this.left.left;
    this.right.left = this.right.right;
    this.right.right = rightBefore;
    this.right.value = valueBefore;
    this.right.updateInNewLocation();
    this.updateInNewLocation();
  }
  updateInNewLocation() {
    if (!this.right && !this.left) {
      this.height = 1;
    } else if (
      !this.right ||
      (this.left && this.right.height < this.left.height)
    ) {
      this.height = this.left.height + 1;
    } else {
      //if (!this.left || this.right.height > this.left.height)
      this.height = this.right.height + 1;
    }
  }
  serialize() {
    const ans = { value: this.value };
    ans.left = this.left === null ? null : this.left.serialize();
    ans.right = this.right === null ? null : this.right.serialize();
    ans.height = this.height;
    return ans;
  }
}
```
## Traversals
Trees are an essential part of storing data, or at computer scientists like to refer them as, data structures. Among their benefits is that they're optimized to be searchable. Occasionally you need to serialize the entire tree into a flat data structure (a tree into an array). You can do that with traversals.

## Depth First Traversal
There are different ways you can traverse a tree. The first one to talk about is the preoder traversal. The basic gist is that for each of the nodes, you process the node (in our case, save it to an array since we're serializing this tree,) then process the left subtree and then the right tree. In preorder traversal, you process the node, then recursively call the method on the left subtree and then the right subtree.

In inorder traversal, you first recursively call the method on the left tree, then process the node, and then call the method on the right tree.

Postorder traversal, you recursively call the method on the left subtree, then the left subtree, then you process the node. 

It all depends on what you're doing on which of these you use. For a sorted list out of a BST, you'd want to use inorder. If you're making a deep copy of a tree, preorder traversal is super useful since you'd copy a node, and then add its left child and then its right tree. Postorder would be useful if you're deleting a tree since you'd process the left tree, then the right, and only after the children had been deleted would you delete the node you're working on.

<img src="https://btholt.github.io/complete-intro-to-computer-science/static/8333499546d84a58751a5a12a8f34e9b/533c1/bst.png" height="300" width="300" />

```javascript
const preorderTraverse = (node, array) => {
  if (!node) return array;
  array.push(node.value);
  array = preorderTraverse(node.left, array);
  array = preorderTraverse(node.right, array);
  return array;
};

const inorderTraverse = (node, array) => {
  if (!node) return array;
  array = inorderTraverse(node.left, array);
  array.push(node.value);
  array = inorderTraverse(node.right, array);
  return array;
};

const postorderTraverse = (node, array) => {
  if (!node) return array;
  array = postorderTraverse(node.left, array);
  array = postorderTraverse(node.right, array);
  array.push(node.value);
  return array;
};
```
## Breadth First Traversal
Breadth-first isn't recursive processing of subtrees like depth-first. Instead we want to process one layer at a time. Using the tree above, we want the resulting order to [8, 3, 10, 1, 6, 14, 4, 7, 13]. In other words, we start at the root, and slowly make our way "down" the tree. 

The way we accomplish this is using our old friend, the queue. A queue is an array that the first thing you into is the first thing you get out of it (FIFO, first in first out, as opposed a stack which is first in last out, FILO.) Another way of thinking about it is that if you call dequeue on a queue, the item that has been in there the longest is the one that comes out.

What you should do to achieve this, is process the node, then add the left child to the queue and then add the right child to the queue. After that, we'll just dequeue an item off of the queue and call our function recursively on that node. You keep going until there's no items left in the queue. The benefit of using a breadth first traversal is nearness from one node to another. It ends up being the more useful of traversals. You can traverse this recursively or iteratively. 

```javascript
// recursive
const breadthFirstTraverse = (queue, array) => {
  if (!queue.length) return array;
  const node = queue.shift();
  array.push(node.value);
  if (node.left) queue.push(node.left);
  if (node.right) queue.push(node.right);
  return breadthFirstTraverse(queue, array);
};

// iterative
const breadthFirstTraverse2 = (queue, array) => {
  if (!queue.length) return array;

  while (queue.length) {
    const node = queue.shift();
    array.push(node.value);
    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }

  return array;
};
```

## Heap Sort
A heap is an array that represents a tree data structure and has to be sorted in a particular way to represent that tree. Priority queues are often represented as heaps and often those two terms are used interchangeably even if the the priority queue is implemented a different way. They are often used in things like priority queues, like network stacks. 

A priority queue is a normal queue that when you queue something it has a priority associated with it. Things that are higher priority are dequeued first. Think of your Internet traffic and how it handles data packets. If you're both syncing your Dropbox and watching Netflix, the Netflix packets would be higher priority because if you drop those the video stutters whereas the Dropbox stuff can happen whenever and you'd never notice. This would be well modeled as a priority queue. And those are usually stored as heaps.

There are many different types of heaps but the one that will be talked about is a binary heap. A binary heap translates to a binary tree, similar to the binary search trees that we covered earlier.

Some differences between a binary search tree and a binary heap are: 
• A binary heap is an array; a BST is made up of node objects (typically.)
• In a BST, there is a strict order where a left child is always smaller than the parent and the right node is always     greater. This is not true of a binary heap. The only guarantee of binary heap is the parent is greater than the         children, there are no guarantees between sibling nodes.
• Similar to the above point, if you do an in-order traversal of a BST, you'll get a sorted list. This does not work in   a binary heap.
• A binary heap is a "complete binary tree." This means it's as compact as possible. All the children of each node are     as full as they can be and left children are filled out first. This is not true of a BST: they can be sparse.

Binary heaps come in two falvors: max heaps and min heaps. We'll be dealing with max heaps (which help you find the greatest number in the heap) but you can imagine that if you flip all the comparisons you'd have a min heap (which helps you find the smallest number.)

This is why a priority queue is often a binary heap: it's very easy to tell the largest number in a binary heap. None of the other is guaranteed, but once you dequeue (or take the next element off) it's easy to find the next item in the queue. In fact, that's how heapsort works: you construct an internal priority queue and then remove an item at a time and stick it at the end and then find the next largest item in the priority queue; rinse and repeat.

The way to represent a binary tree as an array is that for any index of an array n, its left child is stored at 2n + 1; and its right child is at 2n + 2. The root node will always be at 0. That means the root node's left child is at 1 and right child is at 2. 1's left child is at 3 and right is at 4.

One thing to note in this kind of heap, is that the largest number has to be the root of the array. 

<img src="https://btholt.github.io/complete-intro-to-computer-science/static/38d462612230f54d41456fd320ab8eaf/6af66/heap.png" width="300px" height="300px"/>

Once you construct a heap, removing an item from it is done in constant time since you need to find the next largest node to move to the root. This process is typically called heapify. In order to construct a max heap, you run heapify starting at the middle of the array and work backwards to the root. You don't need to do it from the end because heapify will inherently look at those nodes.

So the process of heapsort is
•  Make the array a max heap
•  To make a max heap, you'll run have to heapify on the first half of the array, going backwards. Your loop will looking something like this: for (let i =            Math.floor(array.length / 2) - 1; i >= 0; i--)
•  Loop over the array / max array, dequeuing the root node (which will give you the largest item) and swapping that with last item in the array
•  After dequeuing each item, run heapify again (same function we used to create the heap) once to find the next root node
•  Next loop you'll dequeue the root node and swap it with the second-to-last item in the array and run heapify again.
•  Once you've run out of items to dequeue, you have a sorted array! Let's see what that looks like.

A situation where a heap sort could be useful in the real world, is where memory is a concern, but you still need an nlog(n) sort, and you need to be able to handle sorted lists, reverse sorted lists, and randomly sorted lists, with no guarantee of how your data will look when coming in. With the caveat that quick sort would be better really. 

```javascript
const heapSort = (array) => {
  array = createMaxHeap(array);
  for (let i = array.length - 1; i > 0; i--) {
    swapPlace(0, i, array);
    heapify(array, 0, i);
  }
  return array;
};

const swapPlace = (index1, index2, array) => {
  let temp = array[index1];
  array[index1] = array[index2];
  array[index2] = temp;
  return array;
};

const createMaxHeap = (array) => {
  for (let i = Math.floor(array.length / 2) - 1; i >= 0; i--) {
    heapify(array, i, array.length);
  }
  return array;
};

const heapify = (array, index, heapSize) => {
  const left = 2 * index + 1;
  const right = 2 * index + 2;

  let largestValueIndex = index;

  if (heapSize > left && array[largestValueIndex] < array[left]) {
    largestValueIndex = left;
  }

  if (heapSize > right && array[largestValueIndex] < array[right]) {
    largestValueIndex = right;
  }

  if (largestValueIndex !== index) {
    swapPlace(index, largestValueIndex, array);
    heapify(array, largestValueIndex, heapSize);
  }
};
```
## Graphs
A graph essentially is a tree without a root. You just have a node that is connected to other notes, whereas a tree has hierarchy (where a root is has children, which has children).

Graphs are all about modeling relations between many items. For example, think of Facebook's Social Graph. I'm friends with you and you're friends with me. But you're also friends with six hundred other people which is about five hundred fifty too many. Those people in turn also have too friends. But many of my friends are your friends, so the connections aren't linear, they're … well, they're graph-like.

In the Facebook example, each person would be a node. A node represents some entity, much like a row in an SQL database. Every so-called "friendship" would be called an edge. An edge represents some connection between two items. In this case, our Facebook friendship is bidirectional: if I'm friends with you then you're friends with me. Twitter would be an example of a unidirectional edge: just because I follow you doesn't mean you follow me.

## Resources
#### General
Most of these concepts are from here: https://btholt.github.io/complete-intro-to-computer-science/

#### Algorithms

Visual Algorithms - https://visualgo.net/en

##### Big O resources

https://web.mit.edu/16.070/www/lecture/big_o.pdf
https://www.bigocheatsheet.com/
