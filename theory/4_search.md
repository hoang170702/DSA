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
Mid: Phần tử ở giữa 
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