Binary Search

bsearch(x, A, i, j)
Notion: i refers to the start index often i = 0, j refers to the end index, often j = 0.

1. if i > j then return -1;
2. mid = (i + j) / 2;
3. if A[m] = x, then return m;
4. if A[m] < x, then return bsearch(x, A, i, m-1)
5. if A[m] > x, then return bsearch(x, A, m+1, j)

* JAVA
```java
public class bsearch {
    public static void main(String[] args){
        int[] A = {2, 6, 8, 10, 56, 78, 99, 99, 100};
        int x1 = 7;
        int x2 = 78;

        System.out.println(bsearch(x1, A, 0, A.length - 1));
        System.out.println(bsearch(x2, A, 0, A.length - 1));
    }

    public static int bsearch(int x, int[] A, int i, int j){
        if (i > j) return -1;
        int mid = (int) (i + j) / 2;

        if (A[mid] == x) return mid;
        if (A[mid] < x) return bsearch(x, A, mid + 1, j);
        if (A[mid] > x) return bsearch(x, A, i, mid - 1);

        //if not presented
        return -1;
    }
}
```
Time Complexity时间复杂度：
In each recursive call bsearch(...), $T(n) <= T(n/2) + O(1)(T(1) = O(1)$ when we find x or not found)
$T(n) <= T(n/2^k) + K*O(1)$, in the worst case, where $k=logn$, 

$T(n) <= T(1) + logn * O(1)$
      $=O(logn)$