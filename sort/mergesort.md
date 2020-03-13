1、mergseSort

**Problem description**:
Suppose that you are given an unorderd array A[0..n − 1] of n numbers. Mergesort is supposed to return the array A in sorted order.

**Solution & ideas**:
The idea is to apply divide-and-conquer. We first recursively sort A[0..n/2 − 1] and A[n/2..n] independently. This is done by two recursive calls of mergesort on these two subarrays. Afterwards, we merge these two sorted subarrays into one sorted array.  

* Java
```java

public static void mergeSort(int[] A, int start, int end){
    //check if the array contains exactly one element
    if(start >= end) return;
    
    //define a midpoint to divide the array
    int midpoint = start + (start + end) / 2;

    //use two recursive calls to sort the two subarrays
    mergeSort(A, start, midpoint); //sort the left half
    mergeSort(A, midpoint + 1, end); //sort the right half
    merge(A, start, midpoint, end);// merge the two sorted arrays into one

    //sort function
    void merge(int[] A, int start, int midpoint, int end){
        //need a new array to store the sort result
        int[] newArray = new int[end - start + 1];

        //need two pointers p, q, and a index for newArray
        int p = start, q = midpoint + 1, index = 0;

        while(p <= midpoint && q <= end)
        {
            if(A[p] < A[q])newArray[index++] = A[p++];
            else newArray[index++] = A[q++];
        }

        //copy the remaining elements in left or right array into newArray

        while(p <= midpoint)newArray[index++] = A[p++];
        while(q <= end)newArray[index++] = A[q++];
    }

    //copy the sorted array to A
    System.arraycopy(newArray, 0, A, start, end);

}

```
  
    

* Python
```python
def mergesort(A):
    if len(A) <= 1:
        return A

    mid = int(len(A) / 2)

    left = mergesort(A[:mid])
    right = mergesort(A[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    p = 0
    q = 0
    while p < len(left) and q < len(right):
        if left[p] <= right[q]:
            result.append(left[p])
            p += 1
        else:
            result.append(right[q])
            q += 1

    #copy the remaining elements
    result += left[p:]
    result += right[q:]

    return result
```