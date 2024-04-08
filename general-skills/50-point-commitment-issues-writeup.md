---
author: atuanlab
---

# [picoCTF2024] [50 ppoint] Commitment Issues

## 1. TỔNG QUAN NỘI DUNG 
### Thông tin chung 
- Author: Jeffery John
- Description: I accidentally wrote the flag down. Good thing I deleted it! You download the challenge files.

### Gợi ý 
- Version control can help you recover files if you change or lose them
- Read the chapter on Git from the picoPrimer
- You can 'checkout' commits to see the files inside them


## 2. QUÁ TRÌNH THỰC HIỆN 
Các bước thực hiện 
- Tải và giải nén tập tin `challenge.zip`
- Sử dụng `git log` và `git checkout`
- Thu thập nội dung của cờ

## 3. CHI TIẾT THỰC HIỆN 
### Tải nội dung File "challenge.zip"
Có thể dùng wget để tải tập tin về máy 

```
wget https://artifacts.picoctf.net/c_titan/76/challenge.zip
```

Kết quả thu được sau khi dùng lệnh `wget`
```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_titan/76/challenge.zip
--2024-04-08 05:00:37--  https://artifacts.picoctf.net/c_titan/76/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.22, 108.157.38.105, 108.157.38.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.22|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19201 (19K) [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100%  18.75K  79.2KB/s    in 0.2s        

2024-04-08 05:00:39 (79.2 KB/s) - ‘challenge.zip’ saved [19201/19201]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh
total 28K
drwxr-xr-x 2 kali kali 4.0K Apr  8 05:00 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali  19K Mar 11 19:49 challenge.zip

```

Giải nén tập tin "challenge.zip" bằng `unzip`
```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ unzip challenge.zip 
```

Kết quả thu được sau khi sử dụng lệnh `unzip`
```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh 
total 32K
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:18 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali  19K Mar 11 19:49 challenge.zip
drwxr-xr-x 3 kali kali 4.0K Mar  9 16:10 drop-in

```

Đọc nội dung tập tin "message.txt" thì thu được nội dung 

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ ls -alh 
total 16K
drwxr-xr-x 3 kali kali 4.0K Mar  9 16:10 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:18 ..
drwxr-xr-x 8 kali kali 4.0K Mar  9 16:10 .git
-rw-r--r-- 1 kali kali   11 Mar  9 16:10 message.txt
                                                       
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat message.txt 
TOP SECRET

```

### Sử dụng `git log` và `git checkout`
Theo gợi ý thì có thể kiểm soát những phiên bản khác nhau của những lần "commit" để có thể khôi phục lại nội dung của File sau hoặc trước khi chỉnh sửa

- Dùng `git log` để xem lại lịch sử 
- Dùng `git checkout` để chuyển đổi những nhánh (branch) và phục hồi File từ phiên bản cũ

Kết quả sử dụng `git log` thu được lịch sử những lần "commit" cùng với thông điệp

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git log 
commit a6dca68e4310585eac3b5c9caf0f75967dfe972c (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:06 2024 +0000

    remove sensitive info

commit e720dc26a1a55405fbdf4d338d465335c439fb3e
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:06 2024 +0000

    create flag
```

Như vậy thì trong lần "commit" đầu tiên thì tạo nội dung của cờ nhưng trong lần "commit" tiếp theo thì sẽ xóa những thông tin nhạy cảm (có thể là nội dung của cờ).

Sử dụng `git checkout` để phục hồi nội dung của "mesage.txt"

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git checkout e720dc26a1a55405fbdf4d338d465335c439fb3e
Note: switching to 'e720dc26a1a55405fbdf4d338d465335c439fb3e'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at e720dc2 create flag

```

Truy cập lại nội dung của file `message.txt` thì sẽ thu thập được nội dung của cờ

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat message.txt 
picoCTF{s@n1t1z3_7246792d}

```

## 4. THU THẬP CỜ (FLAG)
- Cờ thu thập: `picoCTF{s@n1t1z3_7246792d}`


## 5. TÀI LIỆU THAM KHẢO 
- https://xuanthulab.net/lenh-git-checkout-git-switch-git-restore-de-chuyen-nhanh-va-phuc-hoi.html
- https://primer.picoctf.org/#_git_version_control