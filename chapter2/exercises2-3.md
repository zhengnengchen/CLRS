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

Base case: When n=2, T(n) = T(2) = 2lg2 = 2*1 = 2

Inducive step: For an arbitrary k, if T(k) = 2T(k/2)+k = k lgk, then T(k+1) = 2T((k+1)/2)+k+1 = 
