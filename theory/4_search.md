# SEARCH

## Có tất cả bao nhiêu loại search cơ bản
````
1. Linear Search 
2. Binary Search 
3. Lower Bound 
4. Upper Bound
````

## Thuật ngữ
````
Target: Giá trị cần tìm 
Sorted Array: Mảng đã được sắp xếp 
Mid: Vị trí ở giữa khoảng tìm kiếm hiện tại
Left: Biên trái 
Right: Biên phải
````

## 1. Linear Search
### Ý tưởng
````
Duyệt từng phần tử

Tìm thấy thì return

Không thấy thì duyệt tiếp

Ví dụ:

1 3 5 7 9

target = 7

1 -> không

3 -> không

5 -> không

7 -> tìm thấy
````

### Độ phức tạp
````
Average: O(n) 
Worst: Target nằm cuối hoặc không tồn tại => O(n) 
Best: Target nằm đầu => O(1) 
Space: O(1)
````

### Triển khai
````
public static int linearSearch(int[] arr, int target){ 
    for(int i = 0; i < arr.length; i++){ 
        // Nếu tìm thấy target 
        if(arr[i] == target){ 
            return i; 
        } 
    } 
    return -1; 
}
````

## 2. Binary Search

### Điều kiện
````
- Mảng phải được sort trước
- Binary Search hoạt động bằng cách loại bỏ một nửa dữ liệu sau mỗi lần so sánh.
````

### Ý tưởng
````
Thay vì duyệt toàn bộ:

1 3 5 7 9 11 13

Ta lấy giữa:

1 3 5 | 7 | 9 11 13
````

````
Nếu:

target = 9

9 > 7

Loại bỏ nửa bên trái:

9 11 13
````

````
Tiếp tục:

9 | 11 | 13
    ^
9 < 11

Loại bỏ nửa bên phải:

9

Tìm thấy.
````

### Độ phức tạp
````
Average: O(log n) 
Worst: O(log n) 
Best: O(1) 
Space: O(1)
````

### Triển khai
````
public static int binarySearch(int[] arr, int target){
	int left = 0;
	int right = arr.length - 1;
	    
	while(left <= right){
	    int mid = left + (right - left)/2;
	        
	    if(arr[mid] == target){
	        return mid;
	    }
	        
	    if(arr[mid] < target){
	        left = mid + 1;
	    }else{
	        right = mid -1;
	    }
	}
	return -1;
}
````

### Nâng cao
````
- Tự tìm hiểu thêm về Lower Bound, Upper Bound 

-> gợi ý: Liên hệ Database index, khi >=, <= , >, < 
````

## Inteview
````
Câu 1
Tại sao Binary Search nhanh hơn Linear Search?
````

````
Câu 2
Khi nào dùng Binary Search?
````

````
Câu 3

Tại sao dùng:
int mid = left + (right - left) / 2;

thay vì:
int mid = (left + right) / 2;
````

````
Liên hệ thực tế
Binary Search
↓
BST
↓
B-Tree
↓
Database Index
↓
Partition Pruning

Đây là nền tảng cho rất nhiều cơ chế tìm kiếm trong hệ thống backend.
````