# 2-1 Insertion sort on small arrays in merge sort
> Although merge sort runs in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5Clg%7Bn%7D%29) worst-case time and insertion sort runs in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5E2%29) worst-case time, the constant factors in insertion sort can make it faster in practice for small problem sizes on many machines. Thus, it makes sense to **coarsen** the leaves of the recursion by using insertion sort within merge sort when subproblems become sufficiently small. Consider a modification to merge sort in which n/k sublists of length k are sorted using insertion sort and then merged using the standard merging mechanism, where k is a value to be determined.

> a. Show that insertion sort can sort the n/k sublists, each of length k, in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28nk%29) worst-case time.

For each sublist in size of k, insertion sort can sort it in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28k%5E2%29) time and there are n/k of such sublists. Hence, the total time to sort n/k sublists in size of k is ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28k%5E2%29%5Ccdot%20n/k%3D%5CTheta%28k%5E2%5Ccdot%20n/k%29%3D%5CTheta%28nk%29)

> b. Show how to merge the sublists in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5Clg%28n/k%29%29) worst-case time.

We can firstly merge every two sublist into one larger sublist using the standard **merge** procedure. That is, merge n/k sublists into n/(2k) sublists. Repeating this step by merge every two sublists into one until there is only one list that is the original list. According to Figure 2.5, there are ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Clg%28n/k%29&plus;1) levels of recurrence. Each level takes ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n/2%5Eik%29%5Ccdot2%5E%7Bi-1%7Dk%3D%5CTheta%28n/2%29) time to merge every two sublists into one. Thus, the overall time to merge all sublists into one original list is ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n/2%29%5Ccdot%28%5Clg%28n/k%29&plus;1%29%3D%5CTheta%28n%5Clg%28n/k%29%29)

> c. Given that the modified algorithm runs in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28nk&plus;n%5Clg%28n/k%29%29) worst-case time, what is the largest value of k as a function of n for which the modified algorithm has the same running time as standard merge sort, in terms of ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta)-notation?

Given the worst-case running time of **merge sort** is ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5Clg%7Bn%7D%29). We have ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28nk&plus;n%5Clg%28n/k%29%29%3D%5CTheta%28n%5Clg%7Bn%7D%29). Since the modification requires ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20k%20%3E%201) to be meaningful, we can ignore the ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20n%5Clg%28n/k%29) part on LHS because ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20k%20%3E%201) makes ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20n%5Clg%28n/k%29%5Cll%20n%5Clg%7Bn%7D). This gives us ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20nk%3Dn%5Clg%7Bn%7D%5Cto%20k%3D%5Clg%7Bn%7D).

> d. How should we choose k in practice?

Given the result calculated in previous. We should choose k to be the nearest integer of ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Clg%7Bn%7D) where n is the size of array to be sorted.

# 2-2 Correctness of bubblesort
> Bubblesort is a popular, but inefficient, sorting algorithm. It works by repeatly swapping adjacent elements that are out of order.
> ```
> BUBBLESORT(A)
> 1 for i = 1 to A.length-1
> 2     for j = A.length downto i+1
> 3         if A[j] < A[j-1]
> 4             exchange A[j] with A[j-1]
> ```
> a. Let A' denote the output of BUBBLESORT(A). To prove that BUBBLESORT is correct, we need to prove that it terminates and that  
> ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20A%27%5B1%5D%5Cleq%20A%27%5B2%5D%5Cleq%5Ccdots%5Cleq%20A%27%5Bn%5D%5Cqquad%282.3%29)  
> where n = A.length. In order to show that BUBBLESORT actually sorts, what else do we need to prove?

Besides the algorithm terminates and outputs a sorted array, we need to prove that each element in the output is in a distinct position in the original array. That is, the algorithm sort original array instead of something else.

> b. State precisely a loop invariant for the **for** loop in lines 2-4, and prove that this loop invariant holds. Your proof should use the structure of the loop invariant proof presented in this chapter.

**Loop invariant**: At the start of each iteration of the inner **for** loop of lines 2-4, the element A\[j\] is the smallest element of subarray A\[j..A.length\].

**Initialization**: Prior to the first iteration of the loop, we have j = A.length, so that the subarray A\[j..A.length\] contains only one element which is A\[A.length\]. This element is trivially the smallest element of a subarray contains only itself.

**Maintenance**: The **if** statement in lines 3-4 will perform a swap between A\[j\] and A\[j-1\] if A\[j\] if smaller. No swap will be performed if A\[j\] is large. As a result, after the execution of lines3-4, A\[j-1\] will always be the smaller element of A\[j\] and A\[j-1\]. Then the next iteration of inner **for** loop starts with j is decremented. Now j becomes j-1 and A\[j-1\] is smaller than A\[j\] and all other elements in subarray A\[j..A.length\]. That is, A\[j-1\] is the smallest element of subarray A\[j-1..A.length\] which maintains the loop invariant.

**Termination**: At termination, j = i. By the loop invariant, the element A\[i\] is the smallest element of subarray A\[i..A.length\].

> c. Using the termination condition of the loop invariant proved in part (b), state a loop invariant for the **for** loop in lines 1-4 that will allow you to prove inequality (2.3). Your proof should use the structure of the loop invariant proof presented in this chapter.

**Loop invariant**: At the start of each iteration of the outer **for** loop of lines 1-4, the subarray A\[1..i-1\] contains the i-1 smallest elements of array A in sorted order.

**Initialization**: Prior to the first iteration of the loop, we have i = 1, so that the subarray A\[1..i-1\] is empty. This empty subarray contains the i-1 = 0 smallest elements of A and hence is in sorted order trivially.

**Maintenance**: The inner **for** loop of lines 2-4 starts with the last element of array A. It keeps exchanging smaller element to one position previous. Sometimes, this exchange is skipped since current element is large than the previous element. Once it finds the smallest element in subarray A\[i..A.length\], this element will be exchanged all the way to A\[i\]. That is, the smallest element in subarray A\[i..A.length\] is now in the position of A\[i\] which is the front of subarray A\[i..A.length\]. Then a next iteration of the outer **for** loop starts. Given that subarray A\[1..i-1\] contains the i-1 smallest elements of array A and A\[i\] contains the smallest element of remaining subarray, new subarray A\[1..i\] contains the i smallest elements of array A in sorted order.

**Termination**: At termination, i = A.length. By the loop invariant, the subarray A\[1..A.length-1\] contains the A.length-1 smallest elements of A in sorted order. This suggests that element A\[A.length\] is the largest element of array A and in the last position of array A. So we can conclude that the whole array A is sorted.

> d. What is the worst-case running time of bubblesort? How does it compare to the running time of insertion sort?

In the worst-case, the array A is in descending order. Then for each iteration of the **for** loop of lines 2-4, the **if** condition is to be determined and the exchange is to be performed. Suppose the swap operation can be performed in constant time, we have

![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DT%28n%29%26%3D%5Csum_%7Bi%3D1%7D%5En%5Csum_%7Bj%3Di&plus;1%7D%5Enc_1%5C%5C%26%3D%5Csum_%7Bi%3D1%7D%5En%28n-i%29c_1%5C%5C%26%3D%5Csum_%7Bi%3D1%7D%5En%28nc_1-ic_1%29%5C%5C%26%3D%5Csum_%7Bi%3D1%7D%5Ennc_1-%5Csum_%7Bi%3D1%7D%5Enic_1%5C%5C%26%3Dc_1n%5E2-%5Cdfrac%7B%28n&plus;1%29n%7D%7B2%7Dc_1%5C%5C%26%3D%5Cdfrac%7B1%7D%7B2%7Dc_1n%5E2-%5Cdfrac%7B1%7D%7B2%7Dc_1n%5C%5C%26%3D%5CTheta%28n%5E2%29%5Cend%7Balign*%7D)

# 2-3 Correctiness of Horner's rule
> The following code fragment implements Horner's rule for evaluating a polynomial  
> ![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DP%28x%29%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn%7Da_kx%5Ek%5C%5C%26%3Da_0&plus;x%28a_1&plus;x%28a_2&plus;%5Ccdots&plus;x%28a_%7Bn-1%7D&plus;xa_n%29%5Ccdots%29%29%5Cend%7Balign*%7D),  
> given the coefficients ![equation](https://latex.codecogs.com/svg.latex?a_0%2Ca_1%2C%5Ccdots%2Ca_n) and a value for x:
> ```
> 1  y = 0
> 2  for i = n downto 0
> 3      y = a_i+x*y
> ```
> a. In terms of ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta)-notation, what is the running time of this code fragment for Horner's rule?

Suppose the multiplication and summation operations in line 3 takes constant time to execute. We have the worst-case running time as  
![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DT%28n%29%26%3D%5Csum_%7Bi%3D0%7D%5En%28c_1&plus;c_2%29%5C%5C%26%3D%28c_1&plus;c_2%29n&plus;%28c_1&plus;c_2%29%5C%5C%26%3D%5CTheta%28n%29%5Cend%7Balign*%7D)

> b. Write pseudocode to implement the naive polynomial-evaluation algorithm that computes each term of the polynomial from scratch. What is the running time of this algorithm? How does it compare to Hoener's rule?

```
NAIVE-POLYNOMIAL-EVALUATION(x, A)
1  y = 0
2  // evaluate each term
3  for i = A.length downto 0
4      x_term = 1
5      // evaluate x^k
6      for j = 1 to i
7          x_term = x_term*x
8      y = y+A[i]*x_term
```

The running time of naive polynomial-evaluation algorithm is  
![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DT%28n%29%26%3D%5Csum_%7Bi%3D0%7D%5En%28%5Csum_%7Bj%3D1%7D%5Eic_1&plus;c_2%29%5C%5C%26%3D%5Csum_%7Bi%3D0%7D%5En%28c_1i&plus;c_2%29%5C%5C%26%3D%5Cdfrac%7B%28n&plus;1%29n%7D%7B2%7Dc_1&plus;%28n&plus;1%29c_2%5C%5C%26%3D%5Cdfrac%7B1%7D%7B2%7Dc_1n%5E2&plus;%28%5Cdfrac%7B1%7D%7B2%7Dc_1&plus;c_2%29n&plus;c_2%5C%5C%26%3D%5CTheta%28n%5E2%29%5Cend%7Balign*%7D)

The naive polynomial-evaluation algorithm is in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5E2%29) while Horner's rule can be run in linear time.

> c. Consider the following loop invariant:
>
> > At the start of each iteration of the **for** loop of lines 2-3, ![equation](https://latex.codecogs.com/svg.latex?y%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-%28i&plus;1%29%7Da_%7Bk&plus;i&plus;1%7Dx%5Ek).
>
> Interpret a summation with no terms as equaling 0. Following the structure of the loop invariant proof presented in this chapter, use this loop invariant to show that, at termination, ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20y%3D%5Csum_%7Bk%3D0%7D%5Ena_kx%5Ek).

**Interpretation**: At the start of ith iteration of the **for** loop of lines 2-3, the subarray A\[i+1..n\] has been evaluated as a polynomial with degree of n-(i+1). That is, ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20y%3DA_%7Bi&plus;1%7D&plus;A_%7Bi&plus;2%7Dx&plus;A_%7Bi&plus;3%7Dx%5E2&plus;%5Ccdots&plus;A_%7Bn-1%7Dx%5E%7Bn-%28i&plus;1%29-1%7D&plus;A_nx%5E%7Bn-%28i&plus;1%29%7D).

**Initialization**: Prior to the first iteration of the loop, we have i = n, so that the subarray A\[i+1..n\] is empty. Since the subarray is empty, the coefficients of all terms of polynomial are 0. Thus, y = 0.

**Maintenance**: To see that each iteration maintains the loop invariant, let us first suppose that j = i-1. Then given that at the start of ith iteration of the **for** loop of lines 2-3, the subarray A\[i+1..n\] has been evaluated as a polynomial with degree of n-(i+1). After calculating ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20y%20%3D%20a_i&plus;xy) as in line 3, A\[i\] is evaluated into new polynomial and we have  
![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7Dy%26%3DA_i&plus;x%28A_%7Bi&plus;1%7D&plus;A_%7Bi&plus;2%7Dx&plus;%5Ccdots&plus;A_%7Bn-1%7Dx%5E%7Bn-%28i&plus;1%29-1%7D&plus;A_nx%5E%7Bn-%28i&plus;1%29%7D%29%5C%5C%26%3DA_i&plus;A_%7Bi&plus;1%7Dx&plus;A_%7Bi&plus;2%7Dx%5E2&plus;%5Ccdots&plus;A_%7Bn-1%7Dx%5E%7Bn-i-1%7D&plus;A_nx%5E%7Bn-i%7D%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-i%7DA_%7Bk&plus;i%7Dx%5Ek%5Cend%7Balign*%7D)  
This is the end of the ith iteration as well as the start of next iteration. That is, the subarray A\[i..n\] is evaluated as a polynomial with degree of n-i and in next iteration, A\[j\], which is also A\[i-1\], is going to be evaluated. We replace i in the equation from loop invariant with j to see if the equation still holds  
![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7Dj%26%3Di-1%5C%5Cy%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-i%7Da_%7Bk&plus;i%7Dx%5Ek%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-i&plus;1-1%7Da_%7Bk&plus;i-1&plus;1%7Dx%5Ek%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-%28i-1%29-1%7Da_%7Bk&plus;j&plus;1%7Dx%5Ek%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-j-1%7Da_%7Bk&plus;j&plus;1%7Dx%5Ek%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5E%7Bn-%28j&plus;1%29%7Da_%7Bk&plus;j&plus;1%7Dx%5Ek%5Cend%7Balign*%7D)  
Observing the fact that the same results holds for j where j is decremented from i. We can tell that the loop invariant holds for next iteration.

**Termination**: At termination, i = -1. By the loop invariant, the subarray A\[i+1..n\], which is A\[0..n\], has been evaluated as a polynomial with degree of n. The polynomial is  
![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cbegin%7Balign*%7Dy%26%3Da_0&plus;a_1x&plus;a_2x%5E2&plus;%5Ccdots&plus;a_%7Bn-1%7Dx%5E%7Bn-1%7D&plus;a_nx%5En%5C%5C%26%3D%5Csum_%7Bk%3D0%7D%5Ena_kx%5Ek%5Cend%7Balign*%7D)

> d. Conclude by arguing that the given code fragment correctlyt evaluates a polynomial characterized by the coefficients ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20a_0%2Ca_1%2C%5Ccdots%2Ca_n).

Since the loop invariant is proved that at termination, we have ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20y%3D%5Csum_%7Bk%3D0%7D%5Ena_kx%5Ek). We can rewrite the summation in the form of polynomial as we did in previous part. Thus, the polynomial is correctly evaluated by a set of coefficients ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20a_0%2Ca_1%2C%5Ccdots%2Ca_n).

# 2-4 Inversions
> Let A\[1..\] be an array of n distinct numbers. If i < j and A\[i\] > A\[j\], then the pair (i,j) is called an **inversion** of A.
> a. List the five inversions of the array (2,3,8,6,1).

(2,1), (3,1), (8,6), (8,1), (6,1)

> b. What array with elements from the set {1,2,...,n} has the most inversions? How many does it have?

A sorted array in descendent order with all elements from the set {1,2,...,n} has the most inversions. It has ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%28n-1%29&plus;%28n-2%29&plus;%5Ccdots&plus;2&plus;1%3D%5Csum_%7Bi%3D1%7D%5E%7Bn-1%7Di%3D%5Cdfrac%7Bn%28n-1%29%7D%7B2%7D) pairs of inversions.

> c. What is the relationship between the running time of insertion sort and number of inversions in the input array? Justify your answer.

The running time of insertion sort and number of inversions in the input array are positively related. Because the number of inversions is number of swap performed in insertion sort.

> d. Give an algorithm that determines the number of inversions in any permutation on n elements in ![equation](https://latex.codecogs.com/svg.latex?%5Cinline%20%5CTheta%28n%5Clg%7Bn%7D%29) worst-case time. (*Hint*: Modify merge sort.)

First, we implement a **MERGE** procedure that works as **MERGE** procedure in merge sort. Our new **MERGE** procedure calculates the number of inversion among two subarray A\[p..q\] and A\[q+1..r\]:

```
MERGE(A, p, q, r)
1  inv = 0
2  i = p
3  j = q+1
4  for k = p to r
5      if A[i] <= A[j]
6          i = i+1
7      else
8         inv = inv+(q-i+1)
9         j = j+1
10 return inv
```

Then, we implement a **MERGE-INVERSION** that combine results from **INVERSION** procesure:

```
MERGE-INVERSION(A, p, q)
1  if p < r
2      q = floor((p+r)/2)
3      left = MERGE-INVERSION(A, p, q)
4      right = MERGE-INVERSION(A, q+1, r)
5      current = MERGE(A, p, q, r)
6      return left+right+current
```
