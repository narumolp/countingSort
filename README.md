# Counting sort algorithm
The Counting Sort algorithm is efficient to sort a small collection of integers. For example given input sequence [4, 0, 4, 2, 0, 3, 5, 5], output sequence will be [0, 0, 2, 3, 4, 4 ,5, 5]. Sorting with this algorithm can be done in 3 steps. First we create an array “Counts” containing a key-value histogram of the number of occurrence (counts) of each distinct element in the collection ranging from minimum to maximum elements. Counts’ s index represents the value occur in input array while Counts’s content represent the count of each value from input array. Next we make another array of prefix sum from the numberOfCounts array. The prefixSums array is then used as a look up table to find the correct index against each element of the input array. The final array is the sorted array. 

This playground example is written in Swift 3.0 and it is geared towards helping the reader to understand how the counting sort algorithm works rather than optimizing it’s performance. It provides plenty of comments and print statements to allow the reader to understand the algorithm step by step. 

### Example 

example input_array:  [4, 0, 4, 2, 0, 3, 5, 5]

1) First we create array ‘counts’ with the size of (maxValue - minValue + 1) and initialize it by filling all elements with zeros. e.g 5 - 0 + 1 = 6 our counts array will have a size of 6 and ranges from 0 to 5
```
keys   : [0, 1, 2, 3, 4, 5]
counts : [0, 0, 0, 0, 0, 0]
```
2) Next, we configure the counts array where each value is the count of number of occurrence of each distinct element (key)
e.g number 0 occurs twice, number 1 does not exist in the input array, number 2 occurs once, and so on. 
```
keys   : [0, 1, 2, 3, 4, 5]
counts : [2, 0, 1, 1, 2, 2]
```

```
  let keys = Array(minElement...maxElement)
  for item in inArray {
    counts[idx] += 1
  }
```

 3) Make ‘prefixSums’ array whose element is calculated by following rule
    1. prefixSums[0] = counts[0] , and    
    2. prefixSums[i] = prefixSums[i-1] + count[i]
  
  *Following our example,*
```
keys       = [0, 1, 2, 3, 4, 5]
prefixSums = [2, 2, 3, 4, 6, 8]
```

```
  for idx in 1 ..< counts.count {
    prefixSums[idx] = prefixSums[idx - 1] + counts[idx]
  }
```
4) Finally we can make output (sorted) array: by looking up value in prefixSums array for associated key. Each element in prefixSums array indicates the correct index for each distinct input element representing in keys array. 
e.g looking at our input array, 
first we see number 4, find number 4 in ‘keys’ and we find 6 in ‘prefixSums’, so we put 4 under index 6.
The next number is 0, find number 0 in ‘keys’ and we find 2 in ‘prefixSums’, so we put 0 under index 2. 
The next number is 4, find number 4 in ‘keys’ and we find 6 in ‘prefixSums’, so we put 4 under index 5 (index 6 was already taken)
the next number is 2, find number 2 in ‘keys’ and we find 3 in ‘prefixSums’, so we put 2 under index 3.
```
index:  [1, 2, 3, 4, 5, 6, 7, 8]
sorted: [0, 0, 2, 3, 4, 4 ,5, 5]
```

```
  for idx in 0 ..< inArray.count {
    
    // reading out element from input array (key)
    let key = inArray[idx]

    // get the value by reading out from prefixSums table
    let prefixSumAtIndex = prefixSums[index]
    
    // place our element in sorted array
    // shift down by one because swift array starts at index 0.
    sorted[prefixSumAtIndex - 1] = key
  }
```

### Usage
To run the code, uncomment the call to example1() through example()3 in the bottom of the playground.

### Observation 
Counting sort is more effective when the input array has smaller range of minimum to maximum values than it’s total count. The example in the playground elaborates on this point. For more information on the Counting Sort algorithm see 
https://en.wikipedia.org/wiki/Counting_sort 

