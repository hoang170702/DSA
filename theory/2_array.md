# ARRAY 
## 1. ArrayList lưu dữ liệu kiểu gì?
````
Dùng mảng động (dynamic array)
````

## 2. Khi add vượt capacity thì chuyện gì xảy ra?
````
-> Resize (grow array) -> Tạo mảng mới lớn hơn -> Copy dữ liệu cũ sang

-> resize sẽ tăng newCapacity = oldCapacity + (oldCapacity >> 1) = old * 1.5

-> tại sao là 1.5 mà ko phải 2 ? -> vì khi x2 lên thì sẽ tốn memory, 1.5 là đủ cân bằng giữa memory và số lần resize
````

## 3. Complexity của add()
````
| Operation         | Complexity |
| ----------------- | ---------- |
| add() bình thường | O(1)       |
| add() khi resize  | O(n)       |

-> add() có amortized O(1)
-> quy trình add:
1. thực hiện kiểm tra size nếu >= capacity thì sẽ thực hiện resize -> lúc này độ phức tạp là O(n) vì cần copy sang mảng mới
2. nếu size < capacity thì thực hiện add vào mảng 
    -> lúc này có 2 trường hợp:
        -> nếu add vào cuối -> độ phức tạp chỉ là O(1)
        -> nếu add vào index ->  độ phức tạp sẽ là O(n) vì cần dịch các phần tử ra sau thêm một ô
    -> nhớ rằng delete trong mảng cũng y như vậy
````

## 4. Initial capacity
````
new ArrayList()
-> KHÔNG tạo mảng ngay
-> chỉ khi add phần tử đầu tiên mới allocate (default = 10)
````


## INTERVIEW
````
Câu 1 Array và ArrayList và List khác nhau thế nào?
````

````
Câu 2 Tại sao ArrayList get(index) là O(1)?
````

````
Câu 3 Tại sao add(index) là O(n)?
````

````
Câu 4 ArrayList có thread-safe không?
````

````
Câu 5 
new ArrayList<>(1000) 
có tạo sẵn 1000 object không?
````

````
Câu 6 ArrayList và LinkedList nên dùng khi nào?
````

````
Câu 7 Capacity và Size khác nhau thế nào?
````




