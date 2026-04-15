# ARRAY 

## Có tất cả bao nhiêu loại sort từ dễ đến khó
````
1. Bubble sort
2. Selection sort
3. Insertion sort
4. Mergr sort
5. Quick sort
6. Heap sort
````

## 1. Bubble sort - dễ nhất
````
- So sánh từng cặp liền kề
- Swap nếu sai thứ tự
- Phần tử lớn nhất “nổi lên” cuối
- Độ phức tạp trung bình là O(n2), còn nếu mảng được check early stop và ko cần sort thì O(n)
````

````
public static void main(String[] args) {
        int arr[] = new int[]{3,1,5,3,2,4,7,4323,6};
        int n = arr.length;
        for(int i =0; i< n-1; i++){
            for(int j=0; j< n-1-i;j++){
                if(arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }        
            }
        }
        for(int num: arr){
            System.out.printf("%d-", num);
        } 
    }
````


##  2.Selection Sort
````
- Tìm min -> Đổi lên đầu
- Độ phức tạp trung bình là O(n2)
````

````
public static void main(String[] args) {
        int arr[] = new int[]{3,1,5,3,2,4,7,4323,6};
        int n = arr.length;
        for(int i =0; i< n; i++){
            int minIndex = i;
            for(int j=i+1; j< n;j++){
                if(arr[j] < arr[minIndex]){
                    minIndex = j;
                }
            }
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
        for(int num: arr){
            System.out.printf("%d-", num);
        }
    }
````

##  3.Insertion Sort
````
- Xây sorted array từng bước -> Chèn phần tử vào đúng vị trí
- Độ phức tạp trung bình là O(n2)
- Khi mảng đã sort gần xong hoặc ít index thì độ phức tạp còn O(N)
````


