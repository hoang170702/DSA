# STRING

## 1. String trong java lưu ở đâu 
````
- Lưu trong string pool (heap)
````

````
- string tối ưu memory dựa vào cơ chế reuse literal

ví dụ:
String A = "ABC"
String B = "ABC"
-> chỉ có 1 Object được sinh ra

Vậy khi nào 2 Object được sinh ra ?
String A = new String("ABC")
String B = new String("ABC")
````

## 2. == vs equals khác gì nhau
````
- Đối với "==" thì sẽ so sánh địa chỉ memory (reference)
- Đối với .equals thì sẽ so sánh giá trị / nội dung

ví dụ:
String A = "ABC" 
String B = "ABC" 
A == B //true
A.equals(B) //true 
-> cùng ô nhớ, nên so sánh == đúng

String A = new String("ABC")
String B = new String("ABC")
A == B //false
A.equals(B) //true 
-> khác ô nhớ nên so sánh == sai


Vậy các trường hợp Integer thì thế nào ? 
Integer A = 127
Integer B = 127 
A == B //true
A.equals(B) //true

Integer A = 128
Integer B = 128 
A == B //false
A.equals(B) //true
-> Java cache sẵn địa chỉ ô nhớ Integer từ: -128 -> 127, nên nếu so sánh vượt quá 127 thì == sẽ sai
````

## 3. Vì sao String được thiết kế immutable
````
Security - String dùng trong: Password, Token, File path, URL -> nếu cho sửa thì attacker sẽ tấn công dễ dàng vào hệ thống.

Thread-safe - nếu chạy 100 luồng, string sẽ tự động tạo ra 100 obj khác nhau, không cần lo lắng về luồng này sẽ chứa chứ liệu của luồng kia.

HashCode - nếu string có thể thay đổi dữ liệu thì chuỗi hash có thể bị thay đổi ngay khi vừa hash xong.
````

## 4. Các cách kiểm tra Anagram
````
Anagram là N chuỗi, có cùng ký tự và số lần xuất hiện, nhưng sắp xếp thứ tự khác nhau

"listen" ↔ "silent"
"triangle" ↔ "integral"
"race" ↔ "care

1️⃣: Sort rồi so sánh
2️⃣: Đếm tần suất (HashMap)
3️⃣: Frequency Array (tối ưu nhất cho lowercase) 

-> làm bài tập leetcode 242
````


## 5. Reverse string có bao nhiêu cách
````
Reverse string là đảo ngược chuỗi
"abcd" ↔ "dcba"

1️⃣ Two Pointers
2️⃣ StringBuilder.reverse()
3️⃣ Stack

-> làm bài tập leetcode 344
````

## 6. Cách kiểm tra Palindrome
````
Palindrome là chuỗi string đọc xuôi, ngược đều giống nhau
"madam"
"racecar"
"level"

1️⃣ Two Pointers

-> làm bài tập leetcode 125
````

# Lý thuyết hệ thống - STRING CORE
## String Traversal

### Two Pointers Pattern
````
- dùng 2 con trỏ, duyệt từ 2 đầu cho đến khi hết mảng
````
### Frequency count
````
- duyệt không quan tâm thứ tự, mục đích là tần suất xuất hiện của ký tự
````

### Sliding window
````
- duyệt theo một "cửa sổ", bao phủ một đoạn liên tiếp của chuỗi, sau đó trượt "cửa sổ" để duyệt và xử lý dữ liệu
````

## Độ phức tạp của String

````
- Truy Cập    -> Access char   -> O(1) 
-> lý do O(1), truy cập bằng index thẳng vào giá trị cần tìm, ko cần lặp

- So sánh     -> Compare       -> O(n)
-> lý do O(n), phải lọc so sánh từng kí tự của hai chuỗi

- Nối chuối   -> Concat        -> O(n)
-> lý do O(n), do nếu cộng 2 chuỗi con lại với nhau, sẽ phải lọc qua từng kí tự, rồi sau đó đưa chuỗi vừa cộng qua một ô nhớ mới

- Chuỗi con   -> Substring     -> O(n)
-> lý do O(n), phải lọc qua từng kí tự, cũng là copy từng kí vào một mảng mới 
````


# Bài tập
````
Problem 242 — Valid Anagram
LeetCode 344
LeetCode 125
Longest substring
````








