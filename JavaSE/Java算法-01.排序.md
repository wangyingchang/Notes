常用排序算法
![](https://i.imgur.com/I4DWYUi.png)

----------


####（1）冒泡排序 Bubble Sort
	/**
	 * 冒泡排序
	 * @param arr 需要排序的数组 
	 */
	public void bubbleSort(int[] arr){//int[] arr = {48,62,63,826,73,48,12,66,19,30};
		for(int i= 0;i<arr.length;i++){
			for(int j = 0;j<arr.length-1;j++){
				if(arr[j]  > arr[j+1]){
					int temp;
					temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}				 
			}
			System.out.print(arr[i]  + ",");
		}
	}

----------

####（2）插入排序 Insert Sort
     /**
	 * 插入排序
	 * @param arr 需要排序的数组 
	 */
	public static void insertSort(int[] arr){  
        int length=arr.length; //数组长度  
        int j;               //当前值的位置  
        int i;               //指向j前的位置  
        int key;             //当前要进行插入排序的值  
		//61,19,56,67,6,66,50,34,37,3
        //从数组的第二个位置开始遍历值  
        for(j=1;j<length;j++){  
            key=arr[j];  
            i=j-1;  
            //a[i]比当前值大时，a[i]后移一位,空出i的位置，好让下一次循环的值后移  
            while(i>=0 && arr[i]>key){  
                arr[i+1]=arr[i]; //将a[i]值后移  
                i--;         //i前移  
            }//跳出循环(找到要插入的中间位置或已遍历到0下标)  
            arr[i+1]=key;    //将当前值插入  
        }  
    }  

----------


####（3）选择排序 Select Sort
     /**
	 * 选择排序
	 * @param arr 需要排序的数组 
	 */
	 public static void selectSort(int[] arr) {  
	        if (arr == null || arr.length <= 0) {  
	            return;  
	        }  
		//int[] arr = {48,62,63,826,73,48,12,66,19,30}
	        for (int i = 0; i < arr.length; i++) {  
	            int min = i; /* 将当前下标定义为最小值下标 */  
	  
	            for (int j = i + 1; j < arr.length; j++) {  
	                if (arr[min] > arr[j]) { /* 如果有小于当前最小值的关键字 */  
	                    min = j; /* 将此关键字的下标赋值给min */  
	                }  
	            }  
	            if (i != min) {/* 若min不等于i，说明找到最小值，交换 */  
	                int tmp = arr[min];  
	                arr[min] = arr[i];  
	                arr[i] = tmp;  
	            }  
	        }  
	    }  

----------

####（4）归并排序 Merge Sort
 	/**
	  * 归并排序 
	  * @param a 需要排序的数组
	  * @param s 第一个有序表的起始下标 
	  * @param m 第二个有序表的起始下标 
	  * @param t 第二个有序表的结束下标 
	  *  
     */  
	 public static void merge(int[] arr, int s, int m, int t) {  
		  int[] tmp = new int[t - s + 1];  
		  
		  int i = s, j = m, k = 0;  
		  while (i < m && j <= t) {  
		   if (arr[i] <= arr[j]) {  
		    tmp[k] = arr[i];  
		    k++;  
		    i++;  
		   } else {  
		    tmp[k] = arr[j];  
		    // sum += (j - i) - (j - m);  
		    j++;  
		    k++;  
		   }  
		  }  
		  while (i < m) {  
		   tmp[k] = arr[i];  
		   i++;  
		   k++;  
		  }  
		  
		  while (j <= t) {  
		   tmp[k] = arr[j];  
		   j++;  
		   k++;  
		  }  
		  
		  System.arraycopy(tmp, 0, arr, s, tmp.length);  
	} 

----------

####（5）快速排序 Quick Sort
     /**
	  * 获得基础的下标
	  * @param arr 需要排序的数组
	  * @param low 数组待排序的最小的下标
	  * @param high 数组待排序的最大的下标
	  * @return 返回中轴值（该值大于左边值，小于右边值）
	  */
	  public static  int getMiddle(int[] arr,int low,int high){
        int temp = arr[low];// temp = 12 = arr[0]
        while(low <high){// 0<1
            while(low <high && arr[high] > temp){//0<1  && 14>12
                high--;//h  = 0
            }
            arr[low] = arr[high]; // a[0] = a[0];
            while(low <high && arr[low] <=temp){//
                low++;
            }
            arr[high] = arr[low];//a[0] = a[0]
        }
        arr[low] = temp;//a[0] = 12
        return low;//0
    }

    public  static void quickSort(int[] arr,int low, int high){
        if(low <high){//0,1
            //将数组一份为二
            int middle = getMiddle(arr, low, high);
    
            System.out.println("middle = " + middle);
            //左边进行递归 快速排序
            quickSort(arr,low,middle -1);
            //右边进行递归 快速排序
            quickSort(arr,middle + 1,high);
        }
    }
    
    //再次封装，对外调用  12，14
    public static void quick(int[] arr){
        if(arr.length  >0)
            quickSort(arr, 0, arr.length -1);
    }

