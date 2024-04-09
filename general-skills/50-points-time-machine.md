---
author: atuanlab
date: 09-04-2024
---

# [2024][PICOCTF] [50 POINTS] TIME MACHINE

## 1. THÔNG TIN CHUNG 

### Tác giả và mô tả
- Tác giả: Jeffery John
- Mô tả (nguyên gốc - tiếng anh): 
    - What was I last working on? I remember writing a note to help me remember ...
    - You can download the challenge files.

### Gợi ý 
- Read the chapter on Git from the picoPrimer here.
- The cat command will let you read a file, but that won't help you here!
- When committing a file with git, a message can (and should) be included.


## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
Quá trình thực hiện bao gồm
- Tải tập tin "challenge.zip"
- Giải nén tập tin "challenge.zip": unzip challenge.zip
- Dùng lệnh `git log` 
- Thu thập nội dung của cờ


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Tải tập tin "challenge.zip"

Dùng lệnh `wget` để tải tập tin "challenge.zip"

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_titan/162/challenge.zip
--2024-04-09 07:05:58--  https://artifacts.picoctf.net/c_titan/162/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.128, 108.157.38.105, 108.157.38.22, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17739 (17K) [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100%  17.32K  71.6KB/s    in 0.2s        

2024-04-09 07:06:00 (71.6 KB/s) - ‘challenge.zip’ saved [17739/17739]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh       
total 28K
drwxr-xr-x 2 kali kali 4.0K Apr  9 07:06 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali  18K Mar 11 20:36 challenge.zip

```


### Giải nén tập tin "challenge.zip"

Sử dụng `unzip` để giải nén tập tin 
- `unzip challenge.zip`
- Nếu chưa có unzip thì có thể tải bằng: `sudo apt install unzip`

Kết quả thu được thư mục "drop-in"
```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh 
total 32K
drwxr-xr-x 3 kali kali 4.0K Apr  9 07:08 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali  18K Mar 11 20:36 challenge.zip
drwxr-xr-x 3 kali kali 4.0K Mar 11 20:07 drop-in
```

Có thể dùng `tree` hay `tree -a` để hiển thị danh sách các tập tin trong thư mục "drop-in"
```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ tree -a
.
├── challenge.zip
└── drop-in
    ├── .git
    │   ├── branches
    │   ├── COMMIT_EDITMSG
    │   ├── config
    │   ├── description
    │   ├── HEAD
    │   ├── hooks
    │   │   ├── applypatch-msg.sample
    │   │   ├── commit-msg.sample
    │   │   ├── fsmonitor-watchman.sample
    │   │   ├── post-update.sample
    │   │   ├── pre-applypatch.sample
    │   │   ├── pre-commit.sample
    │   │   ├── pre-merge-commit.sample
    │   │   ├── prepare-commit-msg.sample
    │   │   ├── pre-push.sample
    │   │   ├── pre-rebase.sample
    │   │   ├── pre-receive.sample
    │   │   └── update.sample
    │   ├── index
    │   ├── info
    │   │   └── exclude
    │   ├── logs
    │   │   ├── HEAD
    │   │   └── refs
    │   │       └── heads
    │   │           └── master
    │   ├── objects
    │   │   ├── 25
    │   │   │   └── 16effb8d70e33bdd0023629b164a77225e1ec2
    │   │   ├── 43
    │   │   │   └── 246218ab4fc7b30e9a9dff073e012316851469
    │   │   ├── 71
    │   │   │   └── 2314f105348e295f8cadd7d7dc4e9fa871e9a2
    │   │   ├── info
    │   │   └── pack
    │   └── refs
    │       ├── heads
    │       │   └── master
    │       └── tags
    └── message.txt

18 directories, 26 files

```

### Dùng `git log` 
Theo mô tả thì tác giả sử dụng "git" cho chương trình nên có thể sử dụng `git log` để xem lại lịch sử những lần "commit"

```
┌──(kali㉿kali)-[~/Desktop/New Folder/drop-in]
└─$ git log          
commit 712314f105348e295f8cadd7d7dc4e9fa871e9a2 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:26 2024 +0000

    picoCTF{t1m3m@ch1n3_e8c98b3a}

```

May mắn một điều là tác giả có ghi chú luôn nội dung của cờ nên có lẽ không cần phải làm gì nhiều nữa.

## 4. THU THẬP NỘI DUNG CỜ 
- Nội dung của cờ: `picoCTF{t1m3m@ch1n3_e8c98b3a}
`

## 5. TÀI LIỆU THAM KHẢO
- https://primer.picoctf.org/#_git_version_control