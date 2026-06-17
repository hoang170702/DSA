# SORT 

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
- Sau mỗi vòng lặp, phần tử lớn nhất được đẩy về cuối
- Average: O(n²)
- Worst: O(n²)
- Best: O(n) nếu có early stop
- Space: O(1)
- Stable: Có
````

````
for(int i=0;i<n-1;i++){
    for(int j=0;j<n-i-1;j++){
        if(arr[j] > arr[j+1]){
            swap(arr,j,j+1);
        }
    }
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
for(int i=0;i<n-1;i++){
    int min=i;

    for(int j=i+1;j<n;j++){
        if(arr[j]<arr[min]){
            min=j;
        }
    }

    swap(arr,i,min);
}
````

##  3.Insertion Sort
````
- Chia mảng thành:
    + Bên trái: đã sort
    + Bên phải: chưa sort

- Lấy từng phần tử từ bên phải
- Chèn vào đúng vị trí trong phần đã sort

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
for(int i=1;i<n;i++){
    int key = arr[i];
    int j = i - 1;

    while(j >= 0 && arr[j] > key){
        arr[j+1] = arr[j];
        j--;
    }

    arr[j+1] = key;
}
````


