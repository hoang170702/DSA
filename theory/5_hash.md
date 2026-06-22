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

-> Vì index của mảng phải nằm trong range: 0 → capacity - 1 
??? vầy thì làm sao để tính ra index ??? 
-> đây chỉ là bước đầu của hashcode, theo dõi tiếp bước sau
````

###  3.2 Capacity
````
Khi bạn khởi tạo 1 hashMap mới: new HashMap<>();

-> default capacity là 16

Nhưng capacity có thể là:
new HashMap<>(32);
new HashMap<>(64);
new HashMap<>(100);

-> nếu bạn không thích những con số là lũy thừa của 2 như: 16, 32, 64 ... .Bạn hoàn toàn có thể thay bằng những con số khác, nhưng hashMap sẽ chỉnh capacity nội bộ thành lũy thừa của 2 gần phù hợp.

new HashMap<>(10)  -> capacity thực tế thường là 16
new HashMap<>(17)  -> capacity thực tế thường là 32
new HashMap<>(100) -> capacity thực tế thường là 128

Vì HashMap muốn capacity dạng: 2^k
````

### 3.3 Vấn đề thật sự (bước tiếp theo sau hashCode)
````

````

