# 2.2-1
![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5E3%29)

# 2.2-2
```
SELECTION-SORT(A)
1  for i = 1 to n-1
2      // find the smallest element in subarray A[i..n]
3      smallest_value = A[i]
4      smallest_index = i
4      for j = i+1 to n
5          if A[j] < smallest_value
6              smallest_value = A[j]
7              smallest_index = j
8              
9      // swap value of A[i] and A[smallest]
10     A[smallest_index] = A[i]
11     A[i] = smallest_value
```

**Loop Invariant**: At the start of each iteration of the `for` loop of line 1-11, the subarray A[1..i-1] consisting of the i-1 smallest numbers of array A is in sorted order.

Since the loop invariant holds when the `for` loop terminates, we can tell that the subarray A[1..n-1] consists of the n-1 smallest numbers of array A and is in sorted order. Hence, the nth element of array A is the largest element of array A. Given the last element of array A is the largest element of array A as well as subarray A[1..n-1] is in sorted order, the array A as a whole is in sorted order.

**Best-case running time**: ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5E2%29)

**Worst-case running time**: ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5E2%29)

# 2.2-3
On the average, half elements of the input sequence need to be checked.  
On the worst-case, the whole input sequence needs to be checked.

**Average-case running time**: ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%29)

**Worst-case running time**: ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%29)

# 2.2-4
If only consider the best-case running time, a possible way might be add a hard coded part to check the state of input that if input itself are in the state of output. For example, in sorting problems, if the desired output is non-decreasing array and the input is already sorted that way, we can reduce the best-case running time from O(n) to O(1) using hard coded checking part.
