# SORT

## Có tất cả bao nhiêu loại sort từ dễ đến khó
````
1. Bubble sort
2. Selection sort
3. Insertion sort
4. Merge sort
5. Quick sort
6. Heap sort
````

## Thuật ngữ
````
Average: Độ phức tạp trung bình
Worst: Trường hợp tệ nhất
Best: trường hợp tốt nhất
Space: Độ phức tạp không gian
Stable: Giữ nguyên thứ tự các phần tử bằng nhau
````

## 1. Bubble sort - dễ nhất
````
- So sánh từng cặp liền kề
- Swap nếu sai thứ tự
- Sau mỗi vòng lặp, phần tử lớn nhất được đẩy về cuối
- Average: O(n²)
- Worst: O(n²)
- Best: O(n) nếu có early stop
- Space: O(1)
- Stable: Có
````

````
for(int i = 0; i < arr.length - 1; i++) {

    // Mỗi vòng lặp sẽ đưa 1 phần tử lớn nhất về cuối mảng
    for(int j = 0; j < arr.length - i - 1; j++) {

        // So sánh 2 phần tử liền kề
        if(arr[j] > arr[j + 1]) {

            // Nếu sai thứ tự thì đổi chỗ
            swap(arr, j, j + 1);
        }
    }

    // Sau vòng lặp này:
    // arr[arr.length - i - 1] đã nằm đúng vị trí
}
````


##  2.Selection Sort
````
- Tìm phần tử nhỏ nhất
- Đổi lên đầu
- Average: O(n²)
- Worst: O(n²)
- Best: O(n²)
- Space: O(1)
- Stable: Không
````

````
for(int i = 0; i < arr.length - 1; i++) {

    // Giả sử phần tử hiện tại là nhỏ nhất
    int min = i;

    // Duyệt phần chưa sort để tìm phần tử nhỏ nhất thực sự
    for(int j = i + 1; j < arr.length; j++) {

        // Nếu tìm thấy phần tử nhỏ hơn
        if(arr[j] < arr[min]) {

            // Cập nhật vị trí phần tử nhỏ nhất
            min = j;
        }
    }

    // Đưa phần tử nhỏ nhất về đầu phần chưa sort
    swap(arr, i, min);
}
````

##  3.Insertion Sort
````
- Chia mảng thành:
    + Bên trái: đã sort
    + Bên phải: chưa sort

- Lấy từng phần tử từ bên phải
- Chèn vào đúng vị trí trong phần đã sort
- TimSort trong java dùng 2 loại sort, trong đó 1 cái là Insertion Sort :) -> tự tìm hiểu lý do và loại còn lại.

Ví dụ:

5 3 4 1

-> 5
-> 3 5
-> 3 4 5
-> 1 3 4 5
````

````
Average: O(n²)

Worst:
Mảng ngược hoàn toàn
5 4 3 2 1
=> O(n²)

Best:
Mảng đã sort sẵn
1 2 3 4 5
=> O(n)

Space: O(1)
Stable: Có
````

````
{
    for(int i=1;i<arr.length;i++){
        // lấy giá trị hiện tại để lưu giữ
        int key = arr[i];
            
        // lấy vị trí giá trị trước đó để so sánh
        int j = i -1;
            
        // check nếu giá trị trước đó > giá trị hiện tại
        while(j >= 0 && arr[j] > key){
            // thực hiện chèn lấy luôn vị trí
            arr[j+1] = arr[j];
               
            // lùi j thêm 1 đơn vị để tiếp tục so sánh vs key, nếu như key vẫn < arr[j] thực hiện vòng lên để chèn tiếp
            j--;
        };
           
        // Chèn key vào vị trí phù hợp trong phần đã sort
        arr[j+1] = key;
}
````


##  4.Merge Sort
````
- Chia để trị
- Divide and Conquer
- Chia đôi liên tục
- Merge lại theo thứ tự
- Hàm sort thứ 2 sau Insertion mà TimSort dùng chính là Merge sort -> tìm hiểu lý do vì sao ko dùng mỗi MergeSort mà phải kết hợp thêm Insertion Sort


Ví dụ:

8 3 4 1
-> 8 3 | 4 1

-> 8 | 3
   4 | 1

-> 3 8
   1 4

-> 1 3 4 8
````

````
- Average: O(n log n)
- Worst: O(n log n)
- Best: O(n log n)
- Space: O(n)
- Stable: Có
````

### Triển khai
````
public static void mergeSort(int[] arr, int left, int right) {

        // Nếu mảng chỉ còn 1 phần tử hoặc không còn phần tử nào thì đã sort
        if (left >= right) {
            return;
        }

        // Tìm điểm giữa để chia mảng thành 2 nửa
        int mid = left + (right - left) / 2;

        // Sort nửa bên trái (đệ quy)
        mergeSort(arr, left, mid);

        // Sort nửa bên phải (đệ quy)
        mergeSort(arr, mid + 1, right);

        // Gộp 2 nửa đã sort lại với nhau
        merge(arr, left, mid, right);
}
````

````
private static void merge(int[] arr, int left, int mid, int right) {

        // Tính số lượng phần tử của mảng bên trái
        int n1 = mid - left + 1;

        // Tính số lượng phần tử của mảng bên phải
        int n2 = right - mid;

        // Tạo mảng tạm để lưu nửa bên trái
        int[] leftArr = new int[n1];

        // Tạo mảng tạm để lưu nửa bên phải
        int[] rightArr = new int[n2];

        // Copy dữ liệu từ mảng gốc sang mảng trái
        for (int i = 0; i < n1; i++) {
            leftArr[i] = arr[left + i];
        }

        // Copy dữ liệu từ mảng gốc sang mảng phải
        for (int j = 0; j < n2; j++) {
            rightArr[j] = arr[mid + 1 + j];
        }

        // i dùng để duyệt mảng trái
        int i = 0;

        // j dùng để duyệt mảng phải
        int j = 0;

        // k dùng để ghi dữ liệu trở lại mảng gốc
        int k = left;

        // So sánh từng phần tử của 2 mảng trái/phải
        while (i < n1 && j < n2) {

            // Nếu phần tử bên trái nhỏ hơn hoặc bằng bên phải
            if (leftArr[i] <= rightArr[j]) {

                // Ghi phần tử bên trái vào mảng gốc
                arr[k] = leftArr[i];

                // Tăng i để qua phần tử tiếp theo của mảng trái
                i++;
            } else {

                // Ghi phần tử bên phải vào mảng gốc
                arr[k] = rightArr[j];

                // Tăng j để qua phần tử tiếp theo của mảng phải
                j++;
            }

            // Tăng k để ghi vào vị trí tiếp theo của mảng gốc
            k++;
        }

        // Nếu mảng trái còn phần tử thì copy hết vào mảng gốc
        while (i < n1) {
            arr[k] = leftArr[i];
            i++;
            k++;
        }

        // Nếu mảng phải còn phần tử thì copy hết vào mảng gốc
        while (j < n2) {
            arr[k] = rightArr[j];
            j++;
            k++;
        }
    }
}
````


## Quick sort
````
Không chia đôi cố định như Merge Sort.
Quick Sort chọn một phần tử gọi là: Pivot

Các số nhỏ hơn pivot -> bên trái

Pivot -> ở giữa

Các số lớn hơn pivot -> bên phải
````

````
B1: 

9 8 3 4 1 5

pivot = 5

Partition lần 1

3 4 1 | 5 | 9 8
        ^
      pivot đã đúng vị trí
````

````
B2:

Tiếp tục sort bên trái

3 4 1

pivot = 1

1 | 4 3
^

Tiếp tục sort bên phải

4 3

pivot = 3

3 | 4
^

Kết quả bên trái

1 3 4

````

````
B3:

Tiếp tục sort bên phải pivot ban đầu

9 8

pivot = 8

8 | 9
^

Kết quả bên phải

8 9

Ghép lại

1 3 4 | 5 | 8 9
````

### Triển khai
````
public static void quickSort(int[] arr, int low, int high){

    if(low < high){

        int pivotIndex = partition(arr, low, high);

        quickSort(arr, low, pivotIndex - 1);

        quickSort(arr, pivotIndex + 1, high);
    }
}
````

````
private static int partition(int[] arr, int low, int high){

    // Chọn phần tử cuối làm pivot
    int pivot = arr[high];

    // Vị trí cuối cùng của nhóm phần tử nhỏ hơn pivot
    int i = low - 1;

    // Duyệt từ đầu đến trước pivot
    for(int j = low; j < high; j++){

        // Nếu phần tử hiện tại nhỏ hơn pivot
        if(arr[j] < pivot){

            i++;

            // Đưa phần tử nhỏ hơn pivot sang bên trái
            swap(arr, i, j);
        }
    }

    // Đưa pivot về đúng vị trí
    swap(arr, i + 1, high);

    return i + 1;
}
````

## Heap Sort
### Heap là gì?
````
Ví dụ:

      9
    /   \
   7     8
  / \   /
 3   1 4

 -> Đây là Max Heap vì Cha luôn >= con
````

````
      1
    /   \
   3     4
  / \   /
 7   8 9
-> Đây là Min Heap vì Cha luôn <= con
````

````
-> Heap Sort dùng Max Heap
````

### Các bước thực hiện
````
Bước 1

Xây Max Heap

        9
      /   \
     8     5
    / \   /
   4  1  3
````

````
Bước 2

Lấy phần tử lớn nhất
-> Đưa về cuối mảng

8 5 3 4 1 | 9
````

````
Bước 3

Heapify lại

        8
      /   \
     4     5
    / \
   3   1
````

````
Bước 4

Lấy max tiếp -> đưa về cuối -> lặp lại
````

````
Kết quả: 1 3 4 5 8 9
````

### Triển khai
````
public static void heapSort(int[] arr){

    int n = arr.length;

    // Xây dựng Max Heap
    for(int i = n / 2 - 1; i >= 0; i--){
        heapify(arr, n, i);
    }

    // Đưa phần tử lớn nhất về cuối mảng
    for(int i = n - 1; i > 0; i--){

        swap(arr, 0, i);

        // Heapify lại phần còn lại
        heapify(arr, i, 0);
    }
}
````

````
private static void heapify(int[] arr, int n, int root){

    int largest = root;

    int left = 2 * root + 1;

    int right = 2 * root + 2;

    if(left < n && arr[left] > arr[largest]){
        largest = left;
    }

    if(right < n && arr[right] > arr[largest]){
        largest = right;
    }

    if(largest != root){

        swap(arr, root, largest);

        heapify(arr, n, largest);
    }
}
````
