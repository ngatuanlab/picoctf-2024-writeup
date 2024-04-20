---
author: atuanlab
date: 20-04-2024
Contact: ng.atuanlab.yt@gmail.com
---

# [2024] [PICOCTF] [50-POINTS] INTERENCDEC

## 1. THÔNG TIN CHUNG 
### Tác giả và mô tả chung 
- Tác giả: NGIRIMANA Schadrack
- Mô tả chung 
    - Can you get the real meaning from this file.
    - Download the file here.

### Gợi ý 
- Engaging in various decoding processes is of utmost importance

## 2. TÓM TẮT QUÁ TRÌNH 
- Tải tập tin "enc_flag"
- Giải mã nội dung tập tin: dùng `base64` và `caesar`



## 3. CHI TIẾT QUÁ TRÌNH 
### Tải nội dung tập tin "enc_flag"
Sử dụng `wget` để tải tập tin "enc_flag"

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_titan/110/enc_flag
--2024-04-20 00:34:08--  https://artifacts.picoctf.net/c_titan/110/enc_flag
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.22, 108.157.38.100, 108.157.38.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.22|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 73 [application/octet-stream]
Saving to: ‘enc_flag’

enc_flag      100%      73  --.-KB/s    in 0s          

2024-04-20 00:34:09 (110 MB/s) - ‘enc_flag’ saved [73/73]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh 
total 12K
drwxr-xr-x 2 kali kali 4.0K Apr 20 00:34 .
drwxr-xr-x 3 kali kali 4.0K Apr 14 04:26 ..
-rw-r--r-- 1 kali kali   73 Mar 11 20:36 enc_flag

```

Đọc nội dung tập tin "enc_flag" bằng `cat`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ cat enc_flag 
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzJhMnd6TW1zeWZRPT0nCg==

```

Nội dung thu được là một chuỗi kí tự mà mình nghĩ là đã được mã hóa 

### Giải mã nội dung 

Để ý một chút chuỗi được mã hóa có kết thúc bằng kí tự "==" nên có thể là được mã hóa bằng `base64` nên có thể dùng `base64` để giải mã 

Sử dụng lệnh để giải mã: `base64 -d`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ echo "YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzJhMnd6TW1zeWZRPT0nCg==" | base64 -d 

b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg2a2wzMmsyfQ=='
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ echo "d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg2a2wzMmsyfQ==" | base64 -d
wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2}  
```

Chuỗi thu được có dạng tương tự như nội dung của cờ (tức là cùng cú pháp và có thể là độ dài cũng sẽ tương tự) nên mình đoán là họ đang dùng một dạng mã hóa làm thay đổi nội dung của các kí tự (một dạng mã hóa giống caesar - đổi kí tự theo n) 

Mình dùng một phần mềm online là "CacheSleuth"
- Link: [CacheSleuth](https://www.cachesleuth.com/multidecoder/)

Kết quả thu được là tại n = 7 của mã hóa Ceasar thì thu được nội dung của cờ 




## 4. THU THẬP NỘI DUNG CỜ 
Nội dung của cờ: `picoCTF{caesar_d3cr9pt3d_86de32d2}`


## 5. TÀI LIỆU THAM KHẢO 
- https://www.cachesleuth.com/multidecoder/
- https://en.wikipedia.org/wiki/Base64
- https://www.base64decode.org/