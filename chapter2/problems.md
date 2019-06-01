# 2-1
> Although merge sort runs in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5Clg%7Bn%7D%29) worst-case time and insertion sort runs in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28n%5E2%29) worst-case time, the constant factors in insertion sort can make it faster in practice for small problem sizes on many machines. Thus, it makes sense to **coarsen** the leaves of the recursion by using insertion sort within merge sort when subproblems become sufficiently small. Consider a modification to merge sort in which ![equation](https://latex.codecogs.com/svg.latex?%5Cdfrac%7Bn%7D%7Bk%7D) sublists of length k are sorted using insertion sort and then merged using the standard merging mechanism, where k is a value to be determined.

> a. Show that insertion sort can sort the ![equation](https://latex.codecogs.com/svg.latex?%5Cdfrac%7Bn%7D%7Bk%7D) sublists, each of length k, in ![equation](https://latex.codecogs.com/svg.latex?%5Ctheta%28nk%29) worst-case time.


