# 排序算法

### 1.冒泡排序

**算法描述**：

- 比较相邻的元素。如果第一个比第二个大，就交换它们两个
- 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数
- 针对所有的元素重复以上的步骤，除了最后一个
- 重复直到结束

``` c++
function bubbleSort(arr)
{
    int len=arr.size();
    for(int i=0;i<len-1;i++)   //外循环
    {
        for(int j=0;j=len-1-i;j++)  //内循环
        {
            if(arr[j]>arr[j+1])    //相邻元素对比
            {
                int temp=arr[j];  //交换
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
    }
    return arr;
}
```

**算法分析**：所有元素都没按顺序，则内外循环都为O(n),总为O(n²)。

​                       最好情况，所有元素已按顺序排序，只需要内循环一次即可，为O(n)。

​                       平均为：O(n²)。



### 2.快速排序

算法描述：

- 选第一个元素作为基准数，分别从数组的两端进行扫描，设low、high
- 先从尾端扫描，若比基准数大，则high-1，反之则将high的位置赋值给low的位置，low+1
- 再从前端扫描，若比基准数小，则low+1，反之则将low位置赋值给high，high-1
- 不断循环，直至low==high结束循环

``` c++
void quick_sort(int arr[], int low, int high)
{
    if(low<high)
    {
        int i,j,index;
        i=low;
        j=high;
        index=arr[i];
        while(i<j)
        {
            while(i<j && arr[j]>index)  j--;// 从右向左找第一个小于x的数
            if(i<j)
                a[i++]=a[j];
            while(i < j && a[i] < x)    i++; // 从左向右找第一个大于x的数
            if(i < j)
                a[j--] = a[i];
            
        }
        a[i] = x;
        quick_sort(arr, low, high-1); /* 递归调用 */
        quick_sort(arr, low+1, high); /* 递归调用 */
    }
}
```



**算法分析**:快速排序在所有元素都有序的情况下，为最坏的时间复杂度，是O(N²)。在所有元素都无序的情况下，时间复杂度为O(n).平均的时间复杂度是O(N*lgN)。

### 3.插入排序

算法描述：

- 从第一个元素开始排序
- 取出下一个元素，从已排好序列中从后向前扫，小则前进，大则尾插
- 重复

```c++
function insertionSort(arr)
{
    int len=arr.size();
    int pre,curr;
    for(int i=1;i<len;i++)
    {
        pre=i-1;
        curr=arr[i];
        while(pre>0 && arr[pre]>curr)   //若已排序元素大于新元素，则后移
        {
            arr[pre+1]=arr[pre];
            pre--;
        }
        arr[pre]=curr;   //找到合适位置，插入
    }
    return arr;
}
```

**算法分析**：插入排序在实现上，通常采用in-place排序（即只需用到O(1)的额外空间的排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

### 4.选择排序

**算法描述**：

- 初始状态:无序区为R[1..n]，有序区为空
- 第i趟排序(i=1,2,3…n-1)开始时，当前有序区和无序区分别为R[1..i-1]和R(i..n）。该趟排序从当前无序区中-选出关键字最小的记录 R[k]，将它与无序区的第1个记录R交换，使R[1..i]和R[i+1..n)分别变为记录个数增加1个的新有序区和记录个数减少1个的新无序区
- n-1趟结束，数组有序化了

```c++
function selectionSort(arr)
{
    int len=arr.size();
    int index,temp;
    for(int i=0;i<len-1;i++)
    {
        index=i;
        for(int j=i+1;j<len;j++)
        {
            if(arr[j]<arr[index])  //寻找最小的数
            {
                index=j;    //将索引给index
            }
        }
        temp=arr[i];
        arr[i]=arr[index];
        arr[index]=temp;
    }
    return arr;
}
```

**算法分析**：表现最稳定的排序算法之一，因为无论什么数据进去都是O(n2)的时间复杂度，所以用到它的时候，数据规模越小越好。唯一的好处可能就是不占用额外的内存空间了吧。



### 5.堆排序

**算法描述**：

- 将元素构成大顶堆，初始为无序状态
- 将堆顶元素R[1]与最后一个元素R[n]交换，此时得到新的无序区(R1,R2,……Rn-1)和新的有序区(Rn),且满足R[1,2…n-1]<=R[n]
- 于交换后新的堆顶R[1]可能违反堆的性质，因此需要对当前无序区(R1,R2,……Rn-1)调整为新堆，然后再次将R[1]与无序区最后一个元素交换，得到新的无序区(R1,R2….Rn-2)和新的有序区(Rn-1,Rn)。不断重复此过程直到有序区的元素个数为n-1，则整个排序过程完成

```c++
function buildMaxHeap(arr) 
{  // 建立大顶堆
    len = arr.length;
    for(int i = Math.floor(len/2); i >= 0; i--)//从第一个非叶子结点从下至上，从右至左调整结构
    {
        heapify(arr, i);
    }
}
function heapify(arr, i)
{    // 堆调整
    int left = 2 * i + 1,
        right = 2 * i + 2,
        largest = i;
 
    if(left < len && arr[left] > arr[largest]) 
    {
        largest = left;
    }
 
    if(right < len && arr[right] > arr[largest]) 
    {
        largest = right;
    }
 
    if(largest != i) //调整堆结构+交换堆顶元素与末尾元素
    {
        swap(arr, i, largest);//将堆顶元素与末尾元素进行交换
        heapify(arr, largest);//重新对堆进行调整
    }
}
function swap(arr, i, j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
 
function heapSort(arr) 
{
    buildMaxHeap(arr);
 
    for(int i = arr.length - 1; i > 0; i--) 
    {
        swap(arr, 0, i);
        len--;
        heapify(arr, 0);
    }
    return arr;
}
```



**算法分析**：堆排序是一种选择排序，整体主要由构建初始堆+交换堆顶元素和末尾元素并重建堆两部分组成。其中构建初始堆经推导复杂度为O(n)，在交换并重建堆的过程中，需交换n-1次，而重建堆的过程中，根据完全二叉树的性质，[log2(n-1),log2(n-2)...1]逐步递减，近似为nlogn。所以堆排序时间复杂度一般认为就是O(nlogn)级。




