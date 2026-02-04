# STRING

## String trong java lưu ở đâu 
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

## == vs equals khác gì nhau
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






