---
author: atuanlab
date: 09-04-2024
---

# [2024] [PICOCTF] [75-POINTS] COLLABORATIVE DEVELOPMENT

## THÔNG TIN CHUNG 

### Tác giả và mô tả 
- Tác giả: Jeffery John
- Mô tả (nguyên bản - tiếng anh)
    - My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?
    - You can download the challenge files


### Gợi ý 
- git branch -a will let you see available branches
- How can file 'diffs' be brought to the main branch? Don't forget to git config!
- Merge conflicts can be tricky! Try a text editor like nano, emacs, or vim.


## TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
Quá trình thực hiện
- Tải và giải nén tập tin "challenge.zip"
- Sử dụng `git log` để xem lịch sử 
- Sử dụng `git branch` để xem các branch hiện có
- Dùng `git checkout` vào mỗi branch để thu thập từng thành phần của cờ
    - `git checkout feature/part-1`
    - `git checkout feature/part-2`
    - `git checkout feature/part-3`
- Nối các thành phần lại sẽ thu được nội dung của cờ


## CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Tải và giải nén tập tin "challenge.zip"

Dùng `wget` để tải tập tin

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_titan/178/challenge.zip
--2024-04-09 08:05:14--  https://artifacts.picoctf.net/c_titan/178/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.100, 108.157.38.105, 108.157.38.22, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 24640 (24K) [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100%  24.06K   104KB/s    in 0.2s        

2024-04-09 08:05:15 (104 KB/s) - ‘challenge.zip’ saved [24640/24640]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh 
total 36K
drwxr-xr-x 2 kali kali 4.0K Apr  9 08:05 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali  25K Mar 11 20:36 challenge.zip
```

Dùng `unzip` để giải nén tập tin 
- Dùng lệnh: `unzip challenge.zip`
- Nếu chưa có thì tải qua lệnh: `sudo apt install unzip`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ unzip challenge.zip 
Archive:  challenge.zip
   creating: drop-in/
   creating: drop-in/.git/
   creating: drop-in/.git/branches/
  inflating: drop-in/.git/description  
   creating: drop-in/.git/hooks/
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
  inflating: drop-in/.git/hooks/commit-msg.sample  
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sample  
...
```

Có thể dùng `tree -a` để xem các thư mục theo dạng hình cây

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ tree -a       
.
├── challenge.zip
└── drop-in
    ├── flag.py
    └── .git
        ├── branches
        ├── COMMIT_EDITMSG
        ├── config
        ├── description
        ├── HEAD
        ├── hooks
        │   ├── applypatch-msg.sample
        │   ├── commit-msg.sample
        │   ├── fsmonitor-watchman.sample
        │   ├── post-update.sample
        │   ├── pre-applypatch.sample
        │   ├── pre-commit.sample
        │   ├── pre-merge-commit.sample
        │   ├── prepare-commit-msg.sample
        │   ├── pre-push.sample
        │   ├── pre-rebase.sample
        │   ├── pre-receive.sample
        │   └── update.sample
        ├── index
        ├── info
        │   └── exclude
        ├── logs
        │   ├── HEAD
        │   └── refs
        │       └── heads
        │           ├── feature
        │           │   ├── part-1
        │           │   ├── part-2
        │           │   └── part-3
        │           └── main
        ├── objects
        │   ├── 05
        │   │   └── db9e274ff691e0f9fb492403b570629eb80aa9
        │   ├── 22
        │   │   └── 58a0f267d57e8b6025e2a020b77fac7a553c92
        │   ├── 43
        │   │   └── e44dd37ba0c0adc3d78d0b85d699859ec8d75c
        │   ├── 4f
        │   │   └── 136da027f9a97032d53dd5f667dd6c7852737c
        │   ├── 65
        │   │   └── 5c7bfebe9c221369ab00ac7374d0d4bd4d62a9
        │   ├── 6e
        │   │   └── 17fb3a35364b4f9bb8bef8b5e6a5af2d3e7dfa
        │   ├── 77
        │   │   └── d6ceca6fe23b57d88cf16f20003e10d6715690
        │   ├── 7a
        │   │   └── b4e25c0cd108374b2275fdb1fcdf635e591833
        │   ├── 8e
        │   │   └── ea0627726fc363246015cb4c7e927e70286e87
        │   ├── b9
        │   │   └── 32e8c048154a46d224cd7691c99dc8cb88164a
        │   ├── d1
        │   │   └── f3407cee4479c075997b497fa290ca636fe258
        │   ├── dd
        │   │   └── f6fd2129098bf677ac010259a2a642060aea47
        │   ├── info
        │   └── pack
        └── refs
            ├── heads
            │   ├── feature
            │   │   ├── part-1
            │   │   ├── part-2
            │   │   └── part-3
            │   └── main
            └── tags

29 directories, 41 files

```

Như thường lệ thì tập tin "flag.py" cũng không thu thập được nội dung gì nhiều.

### Sử dụng `git log` và `git branch`

Sử dụng `git log` thì chỉ thu được lần hiển thị duy nhất cho "commit" nên cũng không có gì nhiều 

```
       
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git log             
commit 2258a0f267d57e8b6025e2a020b77fac7a553c92 (HEAD -> main)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:54 2024 +0000

    init flag printer
```

Ngược lại thì dùng `git branch` thì lại có 3 dạng branch khác nhau. Tên hiển thị lại chia thành 3 phần, linh tính mách bảo thì nối 3 thành phần đó lại sẽ được nội dung của cờ.

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git branch
  feature/part-1
  feature/part-2
  feature/part-3
* main

```

### Dùng `git checkout` vào các branch

Sử dụng `git checkout` để truy cập lại những branch khác nhau cho tập tin "flag.py"

Dùng cho branch "feature/part-1" thì thu được một phần nội dung của cờ 

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git checkout feature/part-1

Switched to branch 'feature/part-1'
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat flag.py 
print("Printing the flag...")
print("picoCTF{t3@mw0rk_", end='')   
```

Thực hiện tương tự cho "feature/part-2"

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git checkout feature/part-2 
Switched to branch 'feature/part-2'
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat flag.py 
print("Printing the flag...")

print("m@k3s_th3_dr3@m_", end='')  
```

Và cuối cùng là cho branch "feature/part-3"

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git checkout feature/part-3 
Switched to branch 'feature/part-3'
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ cat flag.py   
print("Printing the flag...")

print("w0rk_6c06cec1}")
```

Kết hợp 3 thành phần ấy lại sẽ thu được nội dung của cờ (tinh thần của làm việc nhóm, mỗi người nắm giữ một chìa khóa dẫn đến thành công)

## THU THẬP NỘI DUNG CỦA CỜ 
Nội dung của cờ: `picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_6c06cec1}`


## TÀI LIỆU THAM KHẢO 
