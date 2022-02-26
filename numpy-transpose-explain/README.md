In this notebook, I will attempt to briefly explain `numpy.transpose()` function and its axis parameters
(that I find them difficult to understand and took me quite some time to wrap my head around)

For an n-dimensional array `a` the axis indices are as follows:  
    `a[0, 1, 2, ..., n-2, n-1]`  
For example, when you say `a[:,0,0]` you tell NumPy that you want element `0,0` on every array/matrix in 0th axis.

The following array `a` has 3 dimensions with the shape of (2, 2, 2)


```python
import numpy as np
a = np.arange(8).reshape(2, 2, 2)
a
```




    array([[[0, 1],
            [2, 3]],
    
           [[4, 5],
            [6, 7]]])



Imagine these numbers are on 2 grids (each grid is a composite of rows and columns),
The first grid is place at the front of the second grid (they are now being layered),
0,1,2,3 are on the 1st layer and 4,5,6,7 are on the 2nd layer.

Now, if I were to assign axis indices, it would be as follows:  
Layer is 0th axis, Row is 1st axis and Column is 2nd axis.

When you `numpy.flatten()` `a`, or change the shape with `numpy.reshape()`,
NumPy will go through each element from highest to lowest axis index.
That means, It will start from `a[0,0,0]` then change column (2nd axis) to get to the next element.
No more column? Then change row, no more row?, then layer.


```python
a.flatten()
```




    array([0, 1, 2, 3, 4, 5, 6, 7])




```python
a.reshape(4, 2)
```




    array([[0, 1],
           [2, 3],
           [4, 5],
           [6, 7]])



Now about `numpy.transpose()`,
This function can change the way NumPy will go through each element.
To use it, first you need to think about which axis you want to go through first.
Let's say, 0th axis (layers) first, then 2nd (column), then 1st (row).
Now put these indices 0, 2, 1 to `numpy.transpose()` parameter.
**BUT WAIT!** You need to put them in a reverse order as follows.


```python
b = a.transpose(1, 2, 0)
b
```




    array([[[0, 4],
            [1, 5]],
    
           [[2, 6],
            [3, 7]]])



Now, when you flatten (or reshape) the array, NumPy will go through the order as you wanted.


```python
b.flatten()
```




    array([0, 4, 1, 5, 2, 6, 3, 7])



For reference to the original array


```python
a
```




    array([[[0, 1],
            [2, 3]],
    
           [[4, 5],
            [6, 7]]])



---
All of these are being explained in more details on the NumPy's documentation. I'm just trying to explain it in short that I think I can understand better.  

Thanks for reading -- Nathan Young (26 February 2022)
