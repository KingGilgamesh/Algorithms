**Quicksort**

The idea is to use an element x from A[0..n-1] to partition A[0..n-1] into two parts A[0..j] and A[j+1..n-1] such that :
* Each element in A[0..j] is at most x
* Each element in A[j+1..n-1] is at least x

Afterwards, apply two quicksort recursively to sort A[0..j] and A[j+1..n-1]

* Quicksort(A, p: start, q:end)
Notion: A[p..r]
1. if r < p, then return
2. Pick a pivot from A[p..r] //usually a random choice
3. q = partition(A, p, r) //A is partitioned into two subarrays A[p..q] and A[q+1..r]
4. Quicksort(A, p, q)
5. Quicksort(A, q+1, r)

* Partition(A, p, r)
1. Suppose that i $\in$ [p,r] is picked to be the index of the pivot
2. x = A[i], exchange A[p] and A[i], i = p - 1; j = r + 1
3. repeat:  
   a. Repeat i++ until A[i] >= x
   b. Repeat j++ until A[j] <= x
   c. if i >= j, return j
   d. Swap A[i] and A[j]

* Java
```java
public class QuickSort{
    public static void main(String[] args){
        int[] A = {10, 7, 8, 9, 1, 5, 100, 38, 56,56,5,8};
        quicksort(A);
        System.out.println(Arrays.toString(A));
    }

    //just to convenient input
    public static void quicksort(int[] A){
        quicksort(A, 0, A.length() - 1);
    }

    //sort the given array
    public static void quicksort(int[] A, int p, int r){
        if(r < p) return;

        int pivotIndex = partition(A, p, r); //get the index of the partition

        //two recursive calls
        quicksort(A, p, pivotIndex);
        quickksort(A, pivotIndex+1, r);

    }

    //return an integer of the partition index
    public static int partition(int[]A, int p, int r){
        //choose the first element as pivot, if not the first, 
        //swap the index with the current first element
        int pivot = A[p];
        int low = p + 1;//index for forward search
        int high = r;//index for backward search

        while(high > low){
            //search forward from left
            while(high >= low && A[low] <= pivot)low++;//stops when finds element in the left subarray bigger than pivot, and should make change

            while(high >= low && A[high] > x)high++;//stops when finds element in the right subarray smaller than pivot, and should make change with A[low]

            //swap the two disordered elements
            if(high > low){
                int temp = A[high];
                A[high] = A[low];
                A[low] = temp;
            }

            //up to now, the array is sorted in such a manner that A[pivot, ...sorted part...]
            //so the next thing is to find the position
            //where the pivot should belong to
            while(high > low && A[high] >= pivot)high--;

            //swap pivot with A[high], and high could be the index of p(first index)
            if(pivot > A[high]){
                A[p] = A[high];
                A[high] = pivot;
                return high;
            }
            else return p;


        }
    }
}
```