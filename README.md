
### Github Task: Search & Sort
In this assignment, you will be given the task to implement a some methods
based on object comparison. One of these tasks will be to implement a
typical sorting algorithm, and as an extra task, implement a binary search algorithm.
We will practice this by using arrays in Java.

#### Requirements
- You should use the same method names as specified below.
- Methods should be appropriately documented and tested (see the testing section)
- You should strive to implement the tests first before you implement the code for the methods. Of course 
this will usually mean that the code will not compile unless you have created the method. A workaround for
this is to simply create the method and just leave it empty (alternatively return a dummy value if it requires
a return). See the method `removeRectanglesLargerThan` in `RectangleArrayProcessor.java`.

It is recommended that you have a look at the [Testing](#testing) section
before starting to implement the methods!

#### Exercises I:
A `Rectangle` class has been provided for you in [`src/Rectangle.java`](src/Rectangle.java). Make
yourself familiar with the source code and note that the `compareTo` method has been overriden so that instances of
 `Rectangle` can be compared by their `area`. Information on Object Ordering and
Comparable can be found
[here](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html).
It's also important to note that we've overridden the `equals` method. According to the method, do we consider 
a `Rectangle` to be the same as another one based on object identity or field values? Hopefully, it 
shouldn't be hard to guess. 


We of course need a way to process `Rectangle`s so therefore you've been given a Java class 
[`src/RectangleArrayProcessor.java`](src/RectangleArrayProcessor.java)`RectangleProcessor`.
 This class will contain your methods.

More specifically, your task is to implement the following methods:
- A method`removeRectanglesLargerThan` that takes a `Rectangle` array and an `int` n and returns an array
containing only the rectangles with a smaller area than n.
- Another method `removeRectanglesLargerThan` (yes, now we're overloading :) ) that takes a `Rectangle` array 
and a `Rectangle` r and returns an array containing only the rectangles with a smaller area than r's area.
- A method `containsSquare` that takes a `Rectangle` array and returns `true` if the array contains a square
or false otherwise.
 - Another method `filterRectanglesWithEqualArea` that takes a `Rectangle` array 
 and a `Rectangle` r and returns an array containing only the rectangles with an area equal to r's area.

You have been provided with a test class for `Rectangle` at [`src/RectangleTest.java`] that
asserts that `Comparable` is correctly implemented. Make sure that it passes
before moving on to other tasks.

> **Assistant's note:** The motivation for using the `Comparable<Rectangle>`
> interface here is simple but perhaps not obvious. The benefit of using it is
> that we can implement generic comparison based algorithms (such as serach and
> sort) that don't actually know what they are comparing by. For the sake of
> keeping complexity down, you will only be implementing algorithms
> specifically for the `Rectangle` class here, but with a small change to the method
> signatures, one could make the algorithms work for _any_ class `T` that
> implements `Comparable<T>` (ask your assistant if you are curious). An
> implication, and huge benefit, of the search/sort not having anything to do
> with the comparison is that if we decide that we want to compare by for
> example height alone, we only need to change `compareTo`!



### Helpful Literature
Study all the following pages from the
[course text](http://www.nada.kth.se/~snilsson/algoritmer/) (online):

- [Hur snabb är datorn?](http://www.nada.kth.se/~snilsson/algoritmer/tid)
- [Algoritmer](http://www.nada.kth.se/~snilsson/algoritmer/algoritmer)

#### Exercise II: Sort and Search

* Choose either the Selection sort or Insertion sort algorithm, as shown below
* In `RectangleArrayProcessor` class, the header for the sorting method
  should be the following:
    * `public void sort(Rectangle[] array)`
* Expected behaviour: list of Rectangle objects will be sorted by increasing area
* You _must_ use `Rectangle.compareTo(Rectangle)` for _all_ comparison operations.

> **Assistant's note:** Notice how the return type is `void`? This gives away
> the fact that these methods sort _in place_. That is to say, they are
> supposed to _mutate_ the argument array/list, instead of returning a copy.

```python
Insertion Sort (A)
------------------
1   for i = 1 to A.length - 1
2       j = i
3       while j > 0 and A[j-1] > A[j]
4           temp = A[j]
5           A[j] = A[j-1]
6           A[j-1] = temp
7           j = j - 1
```
To help you understand how it works, here is a (horribly slow, blame
[Wikipedia](https://en.wikipedia.org/wiki/Insertion_sort)) visualization of
insertion sort:

![Insertion sort gif](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

```python
Selection Sort (A)
------------------
1   for i = 0 to A.length - 1
2       min = i
3       for j = i + 1 to A.length - 1
4           if A[j] < A[min]
5               # minimum element found
6               min = j
7       temp = A[i]
8       A[i] = A[min]
9       A[min] = temp
```
To help you understand how it works, here is a (pretty neat, thank
[Wikipedia](https://en.wikipedia.org/wiki/Selection_sort)) visualization of
selection sort:

![Selection sort gif](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

#### Exercise 3: Sequential Search
Now you will create an iterative sequential search algorithm that **searches
for a Rectangle that is comparably equal to a specified Rectangle**. This will be a 'brute
force' approach that simply iterates through all elements.

* In `RectangleProcessor` class, implement two versions, using both collections and
  arrays, with the following headers:
    * `public int sequentialSearch(Rectangle[] array, Rectangle rectangle)`
    * `public int sequentialSearch(List<Rectangle> list, Rectangle rectangle)`
* Expected behaviour: return index of the first `Rectangle` that has the same area
  as `rectangle`, or -1 if no such `Rectangle` is present.
* You _must_ use `Rectangle.compareTo(Rectangle)` for _all_ comparison operations.

#### Exercise 4: Binary Search
If you assume that the input array/list is sorted, you can use the binary
search algorithm to improve search performance. Create a recursive (or
iterative) version of the binary search algorithm that **searches for a
Rectangle that is comparably equal to a specified Rectangle**.

* In your `RectangleProcessor` class, implement two versions, using both collections
  and arrays, with the following headers:
    * `public int binarySearch(Rectangle[] array, Rectangle rectangle)`
    * `public int binarySearch(List<Rectangle> list, Rectangle rectangle)`
* When testing, be sure to always use sorted lists/arrays as input.
* Expected behaviour: return index of _any_ `Rectangle` that has the same area
  as `rectangle`, or -1 if no such `Rectangle` is present.
* You _must_ use `Rectangle.compareTo(Rectangle)` for _all_ comparison operations.

### Testing
For this week's testing, you've been provided with two test classes.
[`RectangleTest.java`](src/RectangleTest.java), which you do not have to do any more work on,
is just there to make sure that `Comparable<Rectangle>` is correctly implemented.
Make sure to run it before you make your final push. Comparable is the interface which allows
the user to define how an Object should be compared to another Object of the same type.

The second test class, and the one you should work on, is
[`RectangleProcessorTest.java`](src/RectangleProcessorTest.java). You have been given most
test implementations but not all. You should implement all of the test methods
that consist of this single fail statement:

```java
fail("Not implemented");
```

> **Assistant's note:** It is in your own best interests to take the testing
> seriously, as if you properly implement the test class and then pass all of
> the tests, you can be confident that you will not get komplettering on the
> functionality of your code (style issues may still be cause for
> komplettering).

### Grading Criteria
Each week we will communicate grading criteria through the [issue tracker](../../issues/). Grading criteria set the basic standards for a pass, komp or fail, so it is essential you review them each week. These will change over time as your skills develop, so make sure you read the grading criteria issue carefully and tick off all the requirements.
