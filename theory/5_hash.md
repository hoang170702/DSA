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
hash spreading (XOR)
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

### 3.2 Hash Spreading
````
-> Sau khi tính ra 96354

Làm tiếp bước thiếp theo spreading -> hash = h ^ (h >>> 16); 
-> đi trộn bit, 96354 sẽ chuyển qua 1 dãy 32 bit

Từ dãy 32 bit đó, ta lấy 16 bit đầu (dịch sang phải 16 bit) đi XOR với 16 bit cuối 

````

````
Ví dụ:

Giả sử:
    h = 96354
    Đổi sang nhị phân:
        96354 = 00000000 00000001 01111000 01100010

    Tách ra:
        High 16 bit 00000000 00000001
        Low 16 bit 01111000 01100010
````

````
Bước 1: Dịch phải 16 bit (h >>> 16)

Kết quả: 00000000 00000000 00000000 00000001

vì: 00000000 00000001 01111000 01100010
khi thực hiện (>>>>> 16 bit)

sẽ thành: 00000000 00000000 00000000 00000001
````

````
Bước 2: XOR
Công thức : hash = h ^ (h >>> 16)

Lấy: 00000000 00000001 01111000 01100010 (h)

XOR với: 00000000 00000000 00000000 00000001 (h >>> 16)

Quy tắc XOR:
0 ^ 0 = 0
0 ^ 1 = 1
1 ^ 0 = 1
1 ^ 1 = 0
````

````
Thực hiện:

00000000 00000001 01111000 01100010

00000000 00000000 00000000 00000001
-----------------------------------

00000000 00000001 01111000 01100011

Kết quả: 96355
````

###  3.3 Capacity
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

### 3.4 Vấn đề thật sự (bước tiếp theo sau hashCode)
````
Ta có: 
hashCode sau khi trộn = 96355
capacity = 16 / 32 / 64 / 128 ...
````

````
HashMap cần biến: 96355

thành index hợp lệ: 0 → capacity - 1

Ví dụ 
-> nếu capacity = 16: index phải từ 0 → 15
-> Nếu capacity = 32: index phải từ 0 → 31

-> Tiếp tục đến với bước tiếp theo sau khi hiểu XOR và Capacity trong Hash
````
### 3.5 Bucket Index (Tính ra vị trí HashMap lưu object)
````
hash sau khi spreading = 96355
capacity default = 16


HashMap cần biến: 96355
thành:  bucket[0]
        bucket[1]
        ...
        bucket[15]
````

````
HashMap dùng: index = (capacity - 1) & hash;

Ví dụ:

capacity default = 16

thì: capacity - 1 = 15

Đổi sang nhị phân: 15 = 0000 1111

Thực hiện phép AND:
hash = 96355 -> 00000000 00000001 01111000 01100011
(capacity - 1) = 15 -> 00000000 00000000 00000000 00001111

-> Theo công thức (capacity - 1) & hash
-> ta có 
    00000000 00000001 01111000 01100011
    AND
    00000000 00000000 00000000 00001111

=   00000000 00000000 00000000 00000011 = 3 -> lưu vào bucket index 3

````

````
Tìm hiểu thêm, vì sao % (index = hash % capacity;) cũng có thể tính ra đc index chính xác, nhưng lại không được dùng, mà lại dùng AND ?
````

## 4.Hash Collision 








