---
author: atuanlab
date: 10-04-2024
---

# [2024] [PICOCTF] [200-POINTS] ENDIANNESS

## 1. THÔNG TIN CHUNG 

### Tác giả và mô tả chung 
- Tác giả: Nana Ama Atombo-Sackey
- Mô tả chung 
    - Know of little and big endian?



### Gợi ý 
- You might want to check the ASCII table to first find the hexadecimal representation of characters before finding the endianness.
- Read more about how endianness here

## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Có thể tải tập tin "Source" về tham khảo mã nguồn của chương trình 
- Sử dụng các trình để đổi
    - [CyberChef](https://gchq.github.io/CyberChef/#recipe=To_Hex('None',0)): ASCII <-> HEX
    - [save-editor](https://www.save-editor.com/tools/wse_hex.html): chuyển Big <-> Small Endian
- Đổi cụm từ cho sang HEX, từ đó là Big Endian
- Dùng trình chuyển Big Endian thành Little Endian
- Thu thập nội dung của cờ


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Tổng quan về "Big Endian" và "Little Endian"

Bài này thì hơi mới một chút vì khác niệm về "Big Endian" và "Small Endian" thì trước giờ mình chưa nghe đến. Một hồi tìm hiểu thì đó là sắp xếp các byte dùng để đọc (read) hay ghi (write) một từ vào bộ nhớ máy tính. Cụ thể thì: 
- Big Endian: MSB (Most significant byte) lưu trữ ở trước hay cho địa chỉ bộ nhớ thấp hơn
- Little Endian: LSB (Least significant byte) lưu trữ trước hay ở một địa chỉ bộ nhớ thấp hơn

Theo mình thiểu đơn giản thì:
- Big Endian: lưu trữ sắp xếp từ Trái -> Phải từ vị trí đầu tiên
- Small Endian: lưu trữ ngược lại, từ Phải -> Trái từ vị trí đầu tiên

Ví dụ: mình có chuỗi là 0x11223344 (dạng Hex). Như vậy thì LSB là 0x44 và MSB là 0x11. Giả sử lưu tr ữ vào địa chỉ bộ nhớ là 100, 101, 102 và 103

| Địa chỉ | 100 | 101 | 102 | 103 |
| --- | --- | --- | --- | --- | 
| Big Endian | 0x11 | 0x22 | 0x33 | 0x44 |
| Small Endian | 0x44 | 0x33 | 0x22 | 0x11

### Sử dụng trình để chuyển đổi 

Đầu tiên thì truy cập `nc` vào Instance đã cho: `nc titan.picoctf.net 61227`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc titan.picoctf.net 61227
Welcome to the Endian CTF!
You need to find both the little endian and big endian representations of a word.
If you get both correct, you will receive the flag.
Word: zbbln
Enter the Little Endian representation: ^C
```

Như ví dụ mà mình hiểu thì khi chuyển cụm từ cho (trường hợp này là `gqvmn`) thành HEX sẽ có dạng `6771766d6e` và đó cũng là `Big Endian`. Có thể sử dụng trình chuyển đổi `Big Endian` thành `Little Endian` (đổi vị trí ngược lại của nhau)
- Little Endian: `6E 6D 76 71 67`
- Big Endian: `67 71 76 6d 6e`

Nhập nội dung theo yêu cầu

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc titan.picoctf.net 61227
Welcome to the Endian CTF!
You need to find both the little endian and big endian representations of a word.
If you get both correct, you will receive the flag.
Word: gqvmn
Enter the Little Endian representation: 6E6D767167
Correct Little Endian representation!
Enter the Big Endian representation: 6771766d6e
Correct Big Endian representation!
Congratulations! You found both endian representations correctly!
Your Flag is: picoCTF{3ndi4n_sw4p_su33ess_817b7cfe}
```

Nhập các nội dung sẽ thu được nội dung của cờ 

## 4. THU THẬP NỘI DUNG CỦA CỜ 
Nội dung của cờ: `picoCTF{3ndi4n_sw4p_su33ess_817b7cfe}`

## 5. TÀI LIỆU THAM KHẢO 
- Cảm ơn tác giả `noamgariani11` đã gợi ý cho mình thực hiện bài Wirteup này
    - [Link - endianness.md](https://github.com/noamgariani11/picoCTF-2024-Writeup/blob/main/General%20Skills/endianness.md)
- https://levelup.gitconnected.com/little-endian-and-big-endian-74ab6441b2a7
- https://embetronicx.com/tutorials/p_language/c/little-endian-and-big-endian/
