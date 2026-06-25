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

### 4.1 Collision là gì?
````
Collision xảy ra khi:

Nhiều Key khác nhau
↓
Sau khi hash
↓
Rơi vào cùng Bucket
````

Ví dụ:
````
Key A
↓
hash
↓
bucket[1]
````

````
Key B
↓
hash
↓
bucket[1]
````

````
-> 2 key sau khi hash xong đều vào cùng 1 bucket để lưu object MẶC DÙ A != B

=> Đó là Collision
````

### 4.2 Tại sao Collision luôn xảy ra?

Lý Do:
````
HashMap

capacity = 16

bucket[0]
bucket[1]
...
bucket[15]

Tức là: chỉ có 16 bucket
````

Nhưng:
````
Key có thể là:

"ABC"
"XYZ"
"user01"
"user02"
"user03"
...

Vô hạn
````

Nên:
````
Số Key >> Số Bucket

=> Collision là điều chắc chắn xảy ra.
````

### 4.2.1 Lịch sử phát triển
#### 4.2.1.1 Java 7 xử lý Collision thế nào?
````
Bucket
↓
LinkedList
````

````
bucket[3]

ABC
 ↓
XYZ
 ↓
DEF
 ↓
MNO
````

````
map.get("DEF");

bucket[3]

ABC ? -> không
XYZ ? -> không
DEF ? -> có

-> Complexity: O(n) -> phải đi lọc để tìm đúng key, nếu quá nhiều key vào 1 bucket sẽ rất tốn thời gian dù xài hash
````

#### 4.2.1.2 Java 8 cải tiến gì?
Nếu LinkedList quá dài:
````
ABC
 ↓
XYZ
 ↓
DEF
 ↓
MNO
 ↓
...
````

Lookup sẽ ngày càng chậm:
````
O(n)
````

Nên Java 8 thêm:
````
Red Black Tree
````

Vậy khi nào thì hashmap sẽ biến linkedlist -> Red Black Tree (Treeify) ?

````
Node > 8

và

Capacity >= 64
````


Ví dụ:
````
bucket[3]

A
↓
B
↓
C
↓
D
↓
E
↓
F
↓
G
↓
H
↓
I
````

Chuyển thành:
````
        D
      /   \
     B     G
    / \   / \
   A  C  F  I
         /  /
        E  H
````

Complexity:
````
LinkedList O(n) -> RedBlackTree O(log n)
````


## Interview

````
Câu 1 Tại sao HashMap phải thực hiện: hash = h ^ (h >>> 16); thay vì dùng trực tiếp hashCode()?
````

````
Câu 2 Tại sao HashMap dùng: (capacity - 1) & hash mà không dùng: hash % capacity ?
````

````
Câu 3 Tại sao capacity luôn là lũy thừa của 2? Nếu capacity = 15 hoặc 100 thì chuyện gì xảy ra?
````

````
Câu 4 Hash Collision là gì? Tại sao Collision chắc chắn sẽ xảy ra?
````

````
Câu 5 Java 7 xử lý Collision như thế nào? Nhược điểm?
````

````
Câu 6 Java 8 cải tiến Collision như thế nào? Điều kiện để LinkedList chuyển thành RedBlackTree là gì?
````

````
Câu 7 Tại sao phải thêm điều kiện: Capacity >= 64 mới được Treeify, sao không Treeify lúc capacity = 16 luôn?
````

````
Câu 8 Nếu override equals() thì có cần override hashCode() không? Tại sao?
````

````
Câu 9 equals() có vai trò gì khi xảy ra Collision?
````

````
Câu 10 HashMap dùng hashCode() hay equals() trước? 
Hai hàm này phối hợp với nhau như thế nào khi tìm kiếm một Key?
````

````
Câu 11 Load Factor là gì? Mặc định bằng bao nhiêu? 
````

````
Câu 12 Resize xảy ra khi nào? Resize chỉ copy mảng hay phải tính lại bucket của toàn bộ node?
````

````
Câu 13 HashMap có thread-safe không? Nếu nhiều thread cùng put() thì dùng gì thay thế?
````

````
Câu 14 HashSet hoạt động dựa trên cấu trúc dữ liệu nào? HashSet có lưu Value không?
````

