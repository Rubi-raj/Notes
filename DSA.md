# Data Structures and Algorithm 📈

* **Purpose of using DSA** - Less Time and Less memory and Efficient
* **Algorithm** - Means following certain steps.

## What is Time Complexity?⏱️

Measure of how the running time of an algorithm increases with the size of the input data.

<img height="300" width="300" src="https://adrianmejia.com/images/time-complexity-examples.png"/>

## Big O Notation

* **O(1)** : Constant Time
* **O(log n)** : Logarithmic Time
* **O(n)** : Linear Time
* **O(n log n)** : Linearithmic Time
* **O(n<sup>2</sup>)** : Quadratic Time
* **O(2<sup>n</sup>)** : Exponential Time
* **O(n!)** : Factorial Time

## Searching Algorithms
* Linear Search
* Binary Search

### Linear Search

* **Sequential** scanning of each element.
* Time complexity: **O(n)**

```java
int linearSearch(int[] nums, int target) {
	for (int i = 0; i < nums.length; i++) {
		if (nums[i] == target) {
			return i;
		}
	}
	return -1;
}
```

### Binary Search

* Divide array exactly `(1/2)` then searching the target element.
* **Rule:** Array should be **sorted**.
* Find mid of an array **mid=(start + end) / 2**
* Each step cuts the search space in half, so time complexity is **O(log n)**

```java
int binarySearch(int[] nums, int target) {
	int start = 0;
	int end = nums.length - 1;
	while (start <= end) {
		int mid = (start + end) / 2;
		if (nums[mid] == target) {
			return mid;
		} else if (target > nums[mid]) {
			start = mid + 1;
		} else {
			end = mid - 1;
		}
	}
	return -1;
}
```

## Sorting Algorithms

* Bubble Sort
  * ❌Efficient ✅Simple to Understand.
  * Swapping two element from beginning, until it got sorted.
  * Time Complexity **O(n<sup>2</sup>)**