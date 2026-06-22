# HASH

## 1.Thuật ngữ
````
Key: Dữ liệu dùng để tìm kiếm giá trị trong HashMap.
hashCode: Là một số nguyên được tạo ra từ Key.
Bucket: Là vị trí lưu dữ liệu bên trong HashMap.
capacity: Sức chứa của mảng
````

## 2.Hash là gì?
````
Hash là quá trình biến đổi dữ liệu bất kỳ
thành một số nguyên cố định.

Object
↓
hashCode()
↓
Integer
````

````
Ví dụ:
"ABC".hashCode()

Kết quả:
64578
````

## 3.HashMap hoạt động thế nào?

````
Key
↓
hashCode()
↓
hash spreading
↓
index = (n - 1) & hash
↓
bucket[index]
↓
Node(key, value)
````

###  3.1 Phân tích hashCode, "lõi" của toàn bộ hash

````
hashCode() là gì?

-> Trong HashMap, key không được đưa trực tiếp vào mảng.
````

````
Ví dụ:
map.put("abc", 100);
````

````
HashMap cần trả lời câu hỏi: Nên để ("abc", 100) ở vị trí nào trong table?

Nhưng "abc" là object/string, không thể dùng trực tiếp làm index.

Vì vậy Java gọi: int h = key.hashCode();
-> hashCode() trả về một số nguyên int
````

````
Ví dụ:
"abc".hashCode() = 96354

-> Nhưng 96354 vẫn chưa phải index.

-> Vì index của mảng phải nằm trong range: 0 → capacity - 1 ??? vầy thì làm sao để tính ra index ??? -> đây chỉ là bước đầu của hashcode, theo dõi tiếp bước sau
````

###  3.2 Capacity

