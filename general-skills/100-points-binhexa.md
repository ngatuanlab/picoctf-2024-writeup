---
author: atuanlab
date: 10-04-2024
---

# [2024] [PICOCTF] [100-POINTS] BINHEXA

## 1. THÔNG TIN CHUNG 
### Tác giả và mô tả 
- Tác giả: Nana Ama Atombo-Sackey
- Mô tả chung 
    - How well can you perfom basic binary operations?
    - Additional details will be available after launching your challenge instance.


### Gợi ý 

## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Truy cập bằng lệnh `nc`
- Trả lời các câu hỏi liên quan đến phép toán nhị phân 
- Chuyển đổi kết quả câu số 6 thành Hexa 
- Thu thập nội dung của cờ 



## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Truy cập bằng `nc`
Khởi chạy nội dung bằng nhấn "Launch Instance". Bài này thì cũng khá đơn giản do chỉ trả lời các câu hỏi liên quan đến phép toán trên nhị phân và kết thúc là nội dung của cờ 

Truy cập bằng lệnh: `nc titan.picoctf.net 64914` (Port có thể thay đổi)

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc titan.picoctf.net 64914

Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.

Binary Number 1: 11111000
Binary Number 2: 00111111


Question 1/6:
Operation 1: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result: ^C
```

### Trả lời các câu hỏi liên quan
Nội dung các câu hỏi liên quan đến các phép toán trên mã nhị phân. Mình thấy có thể dùng các phần mềm online để làm cho tiện

Các phần mềm như:
- [Binary Calculator](https://www.calculator.net/binary-calculator.html?number1=10011011&c2op=x&number2=00010111&calctype=op&x=Calculate)
- [RapidTables](https://www.rapidtables.com/convert/number/binary-to-hex.html)
- [
Bitwise Converter | Bitwise Calculator
](http://easyonlineconverter.com/converters/bitwise-calculator.html): Mình thì dùng cái này là chính

Một cái thú vị là nội dung câu hỏi có thể khác nhau theo thứ tự nhưng nội dung thì tương tự nhau

Câu hỏi 01: Kết quả của phép dịch bit sang phải của số 2

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc titan.picoctf.net 64914

Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.

Binary Number 1: 11110111
Binary Number 2: 11101000


Question 1/6:
Operation 1: '>>'
Perform a right shift of Binary Number 2 by 1 bits .
Enter the binary result: 1110100
Correct!
```

Câu hỏi 02: Kết quả của phép toán "+" đối với 2 số Number 1 và Number 2

```
Question 2/6:
Operation 2: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result: 111011111
Correct!
```

Câu hỏi 03: Kết quả của phép dịch 1 Bit sang trái của số 1

```
Question 3/6:
Operation 3: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
Enter the binary result: 111101110
Correct!
```

Câu hỏi 04: Kết quả của phép toán "|" của 2 số Number 1 và Number 2

```
Question 4/6:
Operation 4: '|'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11111111
Correct!
```

Câu hỏi 05: Kết quả của phép toán "&" (tức phép toán AND) với 2 số Number 1 và Number 2

```
Question 5/6:
Operation 5: '&'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11100000
Correct!
```

Câu 06: Kết quả của phép nhân "*" của 2 số Number 1 và Number 2

```
Question 6/6:
Operation 6: '*'
Perform the operation on Binary Number 1&2.
Enter the binary result: 1101111111011000
Correct!

```

Cuối cùng thì chỉ cần chuyển kết quả của câu hỏi cuối cùng (dạng binary) thành dạng Hex và có thể thu được nội dung của cò

```
Enter the results of the last operation in hexadecimal: dfd8

Correct answer!
The flag is: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_aeaf4b09}
```

### Phần mềm chuyển đổi của mình 

Mình cũng có viết một chương trình Python đơn giản cho việc thực hiện các phép toán nhị phân và chuyển đổi số từ Binary qua Hex

Source Code 
```
a = int(input("Nhap NUMBER_01: "), 2)
b = int(input("nhap NUMBER_02: "), 2)

print ("Phep + (a+b) = " + bin(a+b)[2:])
print ("Phep & (a&b) = " + bin(a&b)[2:])
print ("Phep | (a|b) = " + bin(a|b)[2:])

print ("Phep SHILFTS LEFT (1 << 1) = " + bin(a<<1)[2:])
print ("Phep SHILFTS LEFT (2 << 1) = " + bin(b<<1)[2:])
print ("Phep SHILFTS RIGHT (1 >> 1) = " + bin(a>>1)[2:])
print ("Phep SHILFTS RIGHT (2 >> 1) = " + bin(b>>1)[2:])
print ("Phep * (a*b) = " + bin(a*b)[2:])

input("Nhan ENTER để tiếp tục chuyển HEX")
c = input("Nhap so chuyen HEX: ")
print ("HEX là: " + hex(int(c,2))[2:])
```

Ví dụ như bài trên, nhận 2 số Number 01 và Number 02 
- Number 01: 11110111
- Number 02: 11101000

Kết quả thực thi
```
C:\Users\anhtuan\Desktop\python-binhexa>python test.py
Nhap NUMBER_01: 11110111
nhap NUMBER_02: 11101000
Phep + (a+b) = 111011111
Phep & (a&b) = 11100000
Phep | (a|b) = 11111111
Phep SHILFTS LEFT (1 << 1) = 111101110
Phep SHILFTS LEFT (2 << 1) = 111010000
Phep SHILFTS RIGHT (1 >> 1) = 1111011
Phep SHILFTS RIGHT (2 >> 1) = 1110100
Phep * (a*b) = 1101111111011000
Nhan ENTER để tiếp tục chuyển HEX
Nhap so chuyen HEX: 1101111111011000
HEX là: dfd8
```

## 4. THU THẬP NỘI DUNG CỦA CỜ 
Nội dung của cờ: `picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_aeaf4b09}
`


## 5. TÀI LIỆU THAM KHẢO 
- https://www.calculator.net/binary-calculator.html?number1=10011011&c2op=x&number2=00010111&calctype=op&x=Calculate
- https://www.rapidtables.com/convert/number/binary-to-hex.html
- http://easyonlineconverter.com/converters/bitwise-calculator.html

