---
author: atuanlab
date: 10-04-2024
---

# [2024] [PICOCTF] [100-POINTS] BINARY SEARCH

## 1. THÔNG TIN CHUNG 

### Tác giả và mô tả 
- Tác giả: Jeffery John
- Mô tả chung 
    - Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.
    - Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!
    - You can download the challenge files here:

### Gợi ý 
- Have you ever played hot or cold? Binary search is a bit like that.
- You have a very limited number of guesses. Try larger jumps between numbers!
- The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around 500. Can you think of why?

## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Có thể tải tập tin "challenge.zip" để xem Source Code
- Truy cập bằng SSH và nhập Pass theo hướng dẫn
- Đoán các số (này mình làm thì đúng là hên xui thật)
- Đúng số thì thu được nội dung của cờ


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Tải tập tin "challenge.zip"

Có thể tải tập tin bằng `wget`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_atlas/4/challenge.zip  
--2024-04-09 21:58:25--  https://artifacts.picoctf.net/c_atlas/4/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.100, 108.157.38.105, 108.157.38.22, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1041 (1.0K) [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100%   1.02K  --.-KB/s    in 0s          

2024-04-09 21:58:26 (22.9 MB/s) - ‘challenge.zip’ saved [1041/1041]

                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh
total 12K
drwxr-xr-x 2 kali kali 4.0K Apr  9 21:58 .
drwxr-xr-x 3 kali kali 4.0K Apr  8 05:00 ..
-rw-r--r-- 1 kali kali 1.1K Mar 11 19:51 challenge.zip
```

Giải nén tập tin bằng `unzip` và có thể dùng `tree -a` để xem các tập tin và thư mục sau khi giải nén

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ tree -a                        
.
├── challenge.zip
└── home
    └── ctf-player
        └── drop-in
            └── guessing_game.sh

4 directories, 2 files

```

### Chơi thử "guessing.sh"

Cái này thì mình làm đúng là theo hên xui ấy. Nội dung thì sẽ chọn ngẫu nhiên một số từ 1 đến 1000 nhưng nếu xem Code thì thật ra số đúng hiển thị sẽ chỉ từ 1 đến 768


Kết quả của phép toán này thì target (tức là biến cho kết quả) chỉ từ 1 --> 768

```
# Generate a random number between 1 and 1000
target=$(( (RANDOM % 1000) + 1 ))
```

Mình thấy thì có thể bắt đầu từ 500 cũng được nhưng bước nhảy nên lớn một chút (từ 100 đến 200), tăng hay giảm đến khi tìm đúng số. Mình thì làm vài lần đều thu được số ở lần thử thứ 8 hay 9

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ssh -p 57954 ctf-player@atlas.picoctf.net
The authenticity of host '[atlas.picoctf.net]:57954 ([18.217.83.136]:57954)' can't be established.
ED25519 key fingerprint is SHA256:M8hXanE8l/Yzfs8iuxNsuFL4vCzCKEIlM/3hpO13tfQ.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:26: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[atlas.picoctf.net]:57954' (ED25519) to the list of known hosts.
ctf-player@atlas.picoctf.net's password: 
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 300
Lower! Try again.
Enter your guess: 100
Lower! Try again.
Enter your guess: 50
Lower! Try again.
Enter your guess: 20
Lower! Try again.
Enter your guess: 10
Lower! Try again.
Enter your guess: 5
Lower! Try again.
Enter your guess: 2
Higher! Try again.
Enter your guess: 3
Congratulations! You guessed the correct number: 3
Here's your flag: picoCTF{g00d_gu355_ee8225d0}
Connection to atlas.picoctf.net closed.
                                           
```

Kết quả nếu điền đúng số hiển thị sẽ thu được nội dung của cờ.

## 4. THU THẬP NỘI DUNG CỦA CỜ 
Nội dung của cờ: `picoCTF{g00d_gu355_ee8225d0}`

## 5. TÀI LIỆU THAM KHẢO
- https://www.thegamegal.com/2012/03/31/hot-or-cold/