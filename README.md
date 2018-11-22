# QuickSort
以int[]为例，利用java实现数组的快速排序--快排

    public class Main {
    public static void main(String[] args){
        int[] test = {34,56,45,67,24,68,33,56,88};
        QuickSortArray array = new QuickSortArray(test);
        int[] tested = array.quickSort( 0, test.length - 1);
        for(int i = 0 ; i < tested.length ; i ++){
            System.out.print(tested[i]+ "   ");
        }
    }
   }
       /*利用快排实现排序;
       利用三数中值分割法找到合适的pivot，将其移至最后不进行排序，利用partition找到合适的位置,
       交换至合适位置，对两边继续交换，知道只剩一个点;
       注意在开始partition前，left在 i - 1，right在pivot处*/
       
     public class QuickSortArray {
    int[] ints;
    QuickSortArray(int[] ints){
        this.ints = ints;
    }
    public int[] quickSort(int i , int j){
        return quickSort(ints, i , j );
    }
    public int[] quickSort(int[] ints , int i , int j){
        int k = findPivot(i , j );
        swap(ints , k , j);//将pivot放在最后面，不进行排序
        int m = partition(i -1 , j );
        swap(ints, j , m);
        if(m - i > 1)quickSort(ints, i , m - 1);
        if(j - m > 1)quickSort(ints, m + 1 , j );
        return ints;
    }
    //利用三数中值分割法找到其中合适的pivot
    //Median-of-Three Partitioning
    private int findPivot(int i , int j){
        if( ints[i] > ints[( i + j) / 2])
            swap(ints , i , ( i + j) / 2);
        if(ints[i] > ints[j])
            swap(ints , i , j);
        if(ints[(i + j) / 2] > ints[j])
            swap(ints , (i + j) / 2 , j);

        return (i + j ) / 2 ;
    }
    //实现交换  √
    public void swap(int[] ints, int low , int high){
        int tmp = ints[low];
        ints[low] = ints[high];
        ints[high] = tmp;
    }
    private int partition(int i , int j ) {
        //对  i 与 j 之间的元素进行处理
        //对于整体而言，i 是 初始元素 - 1，j 是 pivot 前面的一个元素
        int m = j;
        do {
            while (ints[++i] < ints[m]){}//不满足小于pivot时跳出，得到i
            while ( j != 0 &&ints[--j] > ints[m]){}//不满足大于pivot时跳出，得到j
            swap(ints, i ,j );
        }while (i < j);
        swap(ints, i , j );
        return i;//此时pivot所在位置为i，返回得到i
    }
    }

