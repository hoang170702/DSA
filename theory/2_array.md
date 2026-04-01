# ARRAY & SLIDING WINDOW

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

-> quy trình add:
1. thực hiện kiểm tra size nếu >= capacity thì sẽ thực hiện resize -> lúc này độ phức tạp là O(n) vì cần copy sang mảng mới
2. nếu size < capacity thì thực hiện add vào mảng 
    -> lúc này có 2 trường hợp:
        -> nếu add vào cuối -> độ phức tạp chỉ là O(1)
        -> nếu add vào index ->  độ phức tạp sẽ là O(n) vì cần dịch các phần tử ra sau thêm một ô
    -> nhớ rằng delete trong mảng cũng y như vậy
````





