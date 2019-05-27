# 2.1-1
<pre>
1. 31, 41, 59, 26, 41, 58  
       ^  
2. 31, 41, 59, 26, 41, 58  
           ^  
3. 31, 41, 59, 26, 41, 58  
  <------------^  
4. 26, 31, 51, 59, 41, 58  
          <--------^  
5. 26, 31, 41, 51, 59, 58  
                  <----^  
6. 26, 31, 41, 51, 58, 59
</pre>

# 2.1-2
```
INSERTION-SORT(A)
1 for j = 2 to A.length
2     key = A[j]
3     // Insert A[j] into the sorted sequence A[1..j-1]
4     i = j-1
5     while i>0 and A[i]<key
6         A[i+1] = A[i]
7         i = i-1
8     A[i+1]=key
``` 

# 2.1-3
```
LINEAR-SEARCH(A, v)
1 for i = 1 to A.length
2     if v = A[i]
3         return i
4 return NIL
```

**Loop Invariant**: At the start of each iteration of the for loop of lines 1-3, either the element A\[i\] equals to the value v or not.

**Initialization**: When i is assigned with 1, the program compare A\[i\] with value v. It is true for A\[i\] that it is either equals to v or not.

**Maintenance**: After the `if` statement in line 2 comparing A\[i-1\] with v, the program execute the next iteration of `for` loop of lines 1-3. That is, comparing A\[i\] with v. The same condition holds for A\[i\].

**Termination**: The function is terminated by either the `return` expression in line 3 when the condition of the `if` statement in line 2 is met that A\[i\] equals to v or the `return` expression in line 4 since no element in array A equals to v. As a result, either an index of array A which represent the location in A where element of A equals to v or a special value NIL representing that there is no such value v exists in array A is returned. 

# 2.1-4
**Adding two n-bit binary interger**:

**Input**: Two n-element arrays A and B representing two n-bit binary integers  
**Output**: A (n+1)-element array C which stores the result of adding two n-bit binary integers represented by arrays A and B

```
BINARY-SUM(A, B, C)
1  carry_over = 0
2  for i = n+1 downto 2
3      j = i-1
4      if carry_over+A[j]+B[j] = 3
5          C[i] = 1
6      elseif carry_over+A[j]+B[j] = 2
7          C[i] = 0
8      else
9          C[i] = carry_over+A[j]+B[j]
10         carry_over = 1
11 if carry_over = 1
12     C[1] = 1
```
