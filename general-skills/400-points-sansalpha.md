---
author: atuanlab
date: 11-04-2024
Email: ng.atuanlab.yt@gmail.com
---

# [2024] [PICOCTF] SANSALPHA

## 1. THÔNG TIN CHUNG 
### Tác giả và mô tả chung 
- Tác giả: syreal
- Mô tả chung 
    - The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.
    - Additional details will be available after launching your challenge instance.


### Gợi ý 
- Where can you get some letters?


## 2. TÓM TẮT QUÁ TRÌNH THỰC HIỆN 
- Truy cập SSH bằng thông tin cho sẵn 
- Sử dụng kí hiệu thay thế cho chữ cái 
    - "?": là một chữ ngẫu nhiên (vd: /??? là /bin)
    - "[]": là một trường hợp đặc biệt 
    - "!": là dạng loại trừ một điều kiện
- Dùng kí tự xác định 
    - `/????/??????????/??????/????????`: Path đến flag.txt
    - `/???/???[!_]64`: là dùng `/bin/base64`
- Sử dụng `base64` giải mã và thu được nội dung của cờ


## 3. CHI TIẾT QUÁ TRÌNH THỰC HIỆN 

### Truy cập SERVER bằng SSH

Truy cập SERVER bằng SSH với những thông tin cho sẵn: `ssh -p 53127 ctf-player@mimas.picoctf.net`

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ssh -p 53127 ctf-player@mimas.picoctf.net
The authenticity of host '[mimas.picoctf.net]:53127 ([52.15.88.75]:53127)' can't be established.
ED25519 key fingerprint is SHA256:n/hDgUtuTTF85Id7k2fxmHvb6rrLrACHNM6xLZ46AqQ.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:28: [hashed name]
    ~/.ssh/known_hosts:30: [hashed name]
    ~/.ssh/known_hosts:31: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[mimas.picoctf.net]:53127' (ED25519) to the list of known hosts.
ctf-player@mimas.picoctf.net's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 6.5.0-1016-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

SansAlpha$ ls
SansAlpha: Unknown character detected
SansAlpha$  

```

### Sử dụng kí tự thay cho chữ cái

Một điều thú vị là mình không sử dụng được chữ cái nên các lệnh không thể thực hiện một cách bình thường được. 

Những gì sử dụng được là chữ số và các kí tự đặc biệt 

Mình dùng dấu `/` thì hiển thị như đường dẫn, dùng tiếp `/???` thì chỉ dẫn vào `/bin`

```
SansAlpha$ /
bash: /: Is a directory

SansAlpha$ /???
bash: /bin: Is a directory
```

Thực hiện tương tự nhưng với kí tự là `*/*` thì mình thấy được tập tin chắc là chứa nội dung của cờ 

```
SansAlpha$ */*
bash: blargh/flag.txt: Permission denied
```

Biết được vị trí của cờ (nằm trong `blargh/flag.txt`) giờ thì mình có thể mò được đường dẫn đến cờ đó từ vị trí `/` bằng sử dụng tiếp kí tự `?`

Mặc định như những bài trước cờ có thể nằm trong `root` nhưng do mình thấy tên lạ nên có thể là nằm trong `home`. 

Như vậy thì dùng kết hợp giữa `/` và `?` thì tìm được đường dẫn đến cờ 

```
SansAlpha$ /????/??????????
bash: /home/ctf-player: Is a directory

SansAlpha$ /????/??????????/??????/????????
bash: /home/ctf-player/blargh/flag.txt: Permission denied
```

### Đọc nội dung của cờ 
Ban đầu thì mình có thể dùng `cat` để đọc nội dung nhưng cũng khá khó vì sử dụng mà không dùng chữ là một vấn đề. Nên có thể dùng `base64` đọc nội dung 

Mò ra `base64` thì cũng đơn giản vì `/bin/base64` có thể hiển thị dạng `/???/????64`

Nên có thể dùng cú pháp: `/???/????64 /????/??????????/??????/????????`, hiểu như là `/bin/base64 /home/ctf-player/blargh/flag.txt`

```
SansAlpha$ /???/????64 /????/??????????/??????/????????
/bin/base64: extra operand '/bin/x86_64'
Try '/bin/base64 --help' for more information.
```

Lỗi này xuất hiện là do việc hiển thị tất cả những gì cùng dạng `/???/????64` (tức là còn có `/bin/x86_64`) nên cần phải xác định chính xác mình muốn dùng `base64`

Dùng cú pháp: `/???/???[!_]64` (tức là kí tự thứ 4 phải khác dấu "_")

```
SansAlpha$ /???/???[!_]64 /????/??????????/??????/????????
cmV0dXJuIDAgcGljb0NURns3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV8zNmE2NzRjMH0=
```

Dịch ngược lại mã `base64` sẽ thu được nội dung của cờ

```
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ echo 'cmV0dXJuIDAgcGljb0NURns3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV8zNmE2NzRjMH0=' | base64 -d      

return 0 picoCTF{7h15_mu171v3r53_15_m4dn355_36a674c0} 
```

## 4. THU THẬP NỘI DUNG CỜ 
Nội dung của cờ: `picoCTF{7h15_mu171v3r53_15_m4dn355_36a674c0}`

## 5. TÀI LIỆU THAM KHẢO 
- Cảm ơn bài Writeup của `Altair` đã cho mình ý tưởng thực hiện, [Link](https://medium.com/@niceselol/picoctf-2024-sansalpha-86bbdb58bde6) 
- Cảm ơn bài Writeup của `0xVirtu4l` đã cho mình ý tưởng thực hiện, [Link](https://medium.com/@0xVirtu4l/picoctf-2024-sansalpha-challenge-solve-c754ee1deba4)
