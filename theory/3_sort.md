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
