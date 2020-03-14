**Heapsort**

min-heap property: value at a node is no more than the values at its children.

max-heap property: value at a node is no less than the values at its children.

框架：
heapSort(int[] num){
  //初始化建立堆，使满足最大堆，第一个元素为最大元素
  buildmaxheap();
  //堆排序
  heapSort();
}

流程：
1. 初始化：建最大堆，buildmaxheap，从末结点的父结点开始，向上建立。循环调用maxheap函数
2. 堆排序：循环，从i = num.length -1 开始，到i = 0结束，i每次减一（即排除末尾元素）。先是一个swap函数调换首末元素，接着调用maxheap为剩余数组排序。

提示：
当前结点索引i，则左子结点为2i+1，右子结点为2i+2

* Java
```Java
public class heapSort{
  //堆排序主函数
  public static void heapsort(int[] num){
    for(int i = num.length - 1; i > 0; i--){
      //调换首末元素
      swap(num, 0, i);
      //对剩余数组排序
      maxHeap(num, 0, i - 1);
    }
  }

  //初始化堆，即建堆
  public static void buildMaxHeap(int[] num, int lastIndex){
    for(int i = (lastIndex - 1) / 2; i >= 0 ; i--){
      maxHeap(num, i, lastIndex);
    }
  }

  //维持与最大堆的性质
  public static void maxHeap(int[] num, int current, int lastIndex){
        int maxChild = 2 * current + 1;//左子结点索引

        if (maxChild > lastIndex)return;//当前为堆末，退出

        if (maxChild <= lastIndex - 1 && num[maxChild] < num[maxChild + 1])maxChild++;

        if (num[maxChild] > num[current]){
            swap(num, current, maxChild);
            maxHeap_recursive(num, maxChild, lastIndex);//继续往下调整堆
        }
  }
  
  //定义交换
  public static void swap(int[] num, int i, int j){
    int temp = num[i];
    num[i] = num[j];
    num[j] = temp;
  }

  //主函数测试
  public static void main(String[] args){
    int[] a = {87, 43, 2, 4, 5, 5, 234, 77, 89, 56};
    //初始化堆
    buildMaxheap(a, a.length - 1);
    //堆排序
    heapSort(a);
    System.out.println(Arrays.toString(a));
  }
}
```