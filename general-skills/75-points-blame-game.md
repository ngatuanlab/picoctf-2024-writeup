---
author: atuanlab
date: 09-04-2024
---

# [2024] [PICOCTF] [75-POINT] BLAME GAME

## 1. THÔNG TIN CHUNG 

### Tác giả và mô tả
- Tác giả: Jeffery John
- Mô tả (nguyên bản - tiếng anh)
    - Someone's commits seems to be preventing the program from working. Who is it?
    - You can download the challenge files

### Gợi ý
- In collaborative projects, many users can make many changes. How can you see the changes within one file?
- Read the chapter on Git from the picoPrimer here.
- You can use python3 <file>.py to try running the code, though you won't need to for this challenge.

## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Tải tập tin và giải nén tập tin bằng unzip
- Liệt kê 5 dòng cuối của "git log": `git log --oneline | tail -n 5`
- Nội dung của cờ nằm trong tên của tác giả


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Tải tập tin và giải nén tập tin "challenge.zip"

Tải tập tin "challenge.zip" bằng `wget`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_titan/159/challenge.zip
--2024-04-09 07:25:08--  https://artifacts.picoctf.net/c_titan/159/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.22, 108.157.38.100, 108.157.38.105, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.22|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 293915 (287K) [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100% 287.03K   974KB/s    in 0.3s        

2024-04-09 07:25:10 (974 KB/s) - ‘challenge.zip’ saved [293915/293915]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh 
total 296K
drwxr-xr-x 2 kali kali 4.0K Apr  9 07:25 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali 288K Mar 11 20:36 challenge.zip
```

Giải nén tập tin bằng unzip thì sẽ thu được thư mục "drop-in"
- Dùng `unzip`: `unzip challenge.zip`
- Nếu chưa có thì dùng lệnh để tải: `sudo apt install unzip`

```                                      
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ unzip challenge.zip 
Archive:  challenge.zip
   creating: drop-in/
 extracting: drop-in/message.py      
   creating: drop-in/.git/
   creating: drop-in/.git/branches/
  inflating: drop-in/.git/description  
   creating: drop-in/.git/hooks/
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
  inflating: drop-in/.git/hooks/commit-msg.sample  
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sampl
...
```

Truy cập thư mục "drop-in" thì thu được `message.py` và `.git`
```
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ ls -alh       
total 16K
drwxr-xr-x 3 kali kali 4.0K Mar 11 20:07 .
drwxr-xr-x 3 kali kali 4.0K Apr  9 07:26 ..
drwxr-xr-x 8 kali kali 4.0K Mar 11 20:07 .git
-rw-r--r-- 1 kali kali   22 Mar 11 20:07 message.py

```

Đọc nội dung của tập tin `mesasge.py` thì cũng không thu được thông tin gì nhiều (vì có cái gì đâu để thu thập)

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat message.py 
print("Hello, World!"
```

### Sử dụng `git log` và `git checkout`

Cùng tương tự như bài trước, mình cũng có thể sử dụng `git log` để kiểm tra lịch sử những lần "commit" nhưng vấn đề là có quá nhiều. Một hồi ngồi "Enter" cho hết thì lần thay đổi thứ hai mới có nội dung khác. 

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git log | tail -n 10
Author: picoCTF{@sk_th3_1nt3rn_81e716ff} <ops@picoctf.com>
Date:   Tue Mar 12 00:07:15 2024 +0000

    optimize file size of prod code

commit 3ce5c692e2f9682a866c59ac1aeae38d35d19771
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:15 2024 +0000

    create top secret project

```

Nội dung của cờ nằm trong tên của tác giả (nhân vật xóa đi dấu ")" trong code để tối ưu hóa).

##  4. THU THẬP NỘI DUNG CỦA CỜ 
- Nội dung cờ: `picoCTF{@sk_th3_1nt3rn_81e716ff}`

## 5. TÀI LIỆU THAM KHẢO
- https://primer.picoctf.org/#_git_version_control