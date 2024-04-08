---
---

# 

## 1. TỔNG QUAN NỘI DUNG 
### Tác giả
- Tác giả: Jeffery John
### Mô tả nội dung 
Using a Secure Shell (SSH) is going to be pretty important. Additional details will be available after launching your challenge instance
### Quá trình thực hiện 
- Sử dụng Terminal để truy cập SSH bằng lệnh 


## 2. QUÁ TRÌNH THỰC HIỆN 
### Truy cập SSH bằng lệnh 
- Sử dụng lệnh :
`ssh -p 52571 ctf-player@titan.picoctf.net `

- Kết quả hiển thị thu được nội dung của cờ

```
┌──(kali㉿kali)-[~/Desktop]
└─$ ssh -p 52571 ctf-player@titan.picoctf.net  
The authenticity of host '[titan.picoctf.net]:52571 ([3.139.174.234]:52571)' can't be established.
ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:52571' (ED25519) to the list of known hosts.
ctf-player@titan.picoctf.net's password: 
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_8306c99d}
Connection to titan.picoctf.net closed.
```

## 3. THU THẬP CỜ (FLAG)
- Nội dung cờ thu thập được: `picoCTF{s3cur3_c0nn3ct10n_8306c99d}`

## 4. TÀI LIỆU THAM KHẢO 
- https://linux.die.net/man/1/ssh
