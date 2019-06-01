# 2.3-1
> Using Figure 2.4 as a model, illustrate the operation of merge sort on the array A = <3, 41, 52,26, 38, 57, 9, 49>

<pre>
                  sorted sequence
               ----------------------
              | 3 9 26 48 41 49 52 57|
               ----------------------
                /       merge      \
       ----------                  ----------
      |3 26 41 52|                |9 38 49 57|
       ----------                  ----------
      /  merge   \                 /  merge \
   ----          -----         -----        ----
  |3 41|        |26 52|       |38 57|      |9 49|
   ----          -----         -----        ----
 / merge \     / merge \     / merge \    / merge \
 -       --   --       --   --       --   -       --
|3|     |41| |52|     |26| |38|     |57| |9|     |49|
 -       --   --       --   --       --   -       --
                  initial sequence
</pre>

# 2.3-2
> Rewrite the MERGE procedure so that it does not use sentinels, instead stopping once either array L or R has had all its elements copied back to A and then copying the remainder of the other array back into A

```
MERGE(A, p, q, r)
1  n1 = q-p+1
2  n2 = r-q
3  let L[1..n1] and R[1..n2] be new arrays
4  for i = 1 to n1
5      L[i] = A[p+i-1]
6  for j = 1 to n2
7      R[j] = A[q+j]
8  i = 1
9  j = 1
10 k = p
11 while i <= n1 and j <= n2
12     if L[i] <= R[j]
13         A[k] = L[i]
14         i = i+1
15     elif A[k] = R[j]
16          j = j+1
17     k = k+1
18 while i <= n1
19     A[k] = L[i]
20     i = i+1
21     k = k+1
22 while j <= n2
23     A[k] = R[j]
24     j = j+1
25     k = k+1
```
 # 2.3-3
> Use mathematics induction to show that when n is an exact power of 2, the solution of the recurrence  
> ![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3D%5Cbegin%7Bcases%7D2%26%5Ctext%7Bif%20%7Dn%3D2%2C%5C%5C2T%28%5Cdfrac%7Bn%7D%7B2%7D%29&plus;n%26%5Ctext%7Bif%20%7Dn%3D2%5Ek%5Ctext%7B%2C%20for%20%7Dk%3E1%5Cend%7Bcases%7D)  
> is ![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3Dn%5Clg%7Bn%7D)

Base case: When k=1, ![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3DT%282%5E1%29%3DT%282%29%3D2)

Inducive step: For an arbitrary k where ![equation](https://latex.codecogs.com/svg.latex?k%5Cgeq%201), let's assume that ![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3DT%282%5Ek%29%3D2T%28%5Cdfrac%7Bn%7D%7B2%7D%29&plus;n%3Dn%5Clg%7Bn%7D) is true. Then we have ![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DT%282%5E%7Bk&plus;1%7D%29%26%3DT%282n%29%5C%5C%26%3D2T%28%5Cdfrac%7B2n%7D%7B2%7D%29&plus;2n%5C%5C%26%3D2T%28n%29&plus;4n%5C%5C%26%3D2n%5Clg%7Bn%7D&plus;2n%5C%5C%26%3D2n%28lg%7Bn%7D&plus;1%29%5C%5C%26%3D2n%28%5Clg%7B2n%7D%29%5Cend%7Balign*%7D)  
That is, if the result of ![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3Dn%5Clg%7Bn%7D) holds for all ![equation](https://latex.codecogs.com/svg.latex?k%5Cgeq%201), then the same result holds for ![equation](https://latex.codecogs.com/svg.latex?k&plus;1)

# 2.3-4
> We can express insertion sort as a recursive procedure as follows. In order to sort A\[1..n\], we recursively sort A\[1..n-1\] and then insert A\[n\] into the sorted array A\[1..n-1\]. Write a recurrence for the running time of this recursive version of insertion sort.

![equation](https://latex.codecogs.com/svg.latex?T%28n%29%3D%5Cbegin%7Bcases%7D1%26%5Ctext%7Bif%20%7Dn%3D2%2C%5C%5CT%28n-1%29&plus;n%26%5Ctext%7Bif%20%7Dn%3E2%5Cend%7Bcases%7D)

# 2.3-5
> Referring back to the searching problem (see Exercise 2.1-3), observe that if the sequence A is sorted, we can check the midpoint of the sequence against v and eliminate half of the sequence from further consideraton. The **binary search** algorithm repeats this procedure, halving the size of the remaining portion of the sequence each time. Write pseudocode, either iterative or recursive, for binary search. Argue that the worst-case running time of binary search is ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28%5Clg%7Bn%7D%29).

```
BINARY-SEARCH(A, v, p, q)
1  if p = q
2      if A[p] = v
3          return p
4      else
5          return NIL
6  m = floor( (p+q)/2 )
7  if v <= A[m]
8      return BINARY-SEARCH(A, v, p, m)
9  else
10     return BINARY-SEARCH(A, v, m+1, q)
```

Suppose the array A we are searching has a size of power of 2. Name it n where `n = A.length`. We start the binary search with `BINARY-SEARCH(A, v, 1, n)`. In the worst case, we don't happen to find the value v within A before `p=q`. Instead, we call **BINARY SEARCH** procedure ![equation](https://latex.codecogs.com/svg.latex?%5Clg%7Bn%7D) times until `p=q`. And finally the procedure either return an index or NIL.

Now we can count the exact times each line of procedure is executed:  
the `if`  statement in line 1 determining `p = q` executed ![equation](https://latex.codecogs.com/svg.latex?%5Clg%7Bn%7D&plus;1) times in constant time;  
the `if-else` statement in lines 2-5 executed exactly 1 time in constant time;  
the `floor` function in line 6 computing the midpoint of subarray A\[p..q\] executed ![equation](https://latex.codecogs.com/svg.latex?%5Clg%7Bn%7D) times in constant time; 
the `if-else` statement in lines 7-10 executed ![equation](https://latex.codecogs.com/svg.latex?%5Clg%7Bn%7D) times in constant time.

In summary, the worst-case running time of **binary search** procedure is ![equation](https://latex.codecogs.com/svg.latex?%5Cbegin%7Balign*%7DT%28n%29%26%3Dc_1%28%5Clg%7Bn%7D&plus;1%29&plus;c_2&plus;c_3%5Clg%7Bn%7D&plus;c_4%5Clg%7Bn%7D%5C%5C%26%3D%28c_1&plus;c_3&plus;c_4%29%5Clg%7Bn%7D&plus;%28c_1&plus;c_2%29%5C%5C%26%3D%5Ctheta%28%5Clg%7Bn%7D%29%5Cend%7Balign*%7D)

# 2.3-6
> Observe that the while loop of lines 5-7 of the INSERTION-SORT procedure in Section 2.1 uses a linear search to scan (backward) through the sorted subarray A\[1..j-1\]. Can we use a binary search (see Exercises 2.3-5) instead to improve the overall worst-case running time of insertion sort to ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29).

No. We can find the proper index for A\[j\] to insert in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28%5Clg%7Bn%7D%29) time. But once we inserted A\[j\] into subarray A\[1..j-1\], we have to move all elements on the right of A\[j\] to move to right by one position which still takes ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%29) time.

# 2.3-7
> Describe a ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29)-time algorithm that, given a set S of n integers and another integer x, determines whether or not there exist two elements in S whose sum is exactly x.

By combining **merge sort** and **binary search** procedures to implement a new **two sum** procedure, we have the desired algorithm which has the worst-case running time in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29).

First, sorting set S using **merge sort** procedure. Then for each integer i in set S, finding the value of x-i in the remaining set using **binary search** procedure since we have already sorted the set S. If a value of x-i exists for an integer i in set S, there exist two elements in S whose sum is exactly x. Otherwise, such two elements do not exist in set S.

Sorting set S takes ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29) time. Then we perform n times of **binary search** on a subarray whose size is n-1. This takes ![equation](https://latex.codecogs.com/svg.latex?n%5Ccdot%5Ctheta%28%5Clg%7Bn%7D%29%3D%5Ctheta%28n%5Clg%7Bn%7D%29) time. Overall, our algorithm of **two sum** procedure is in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29).
