---
author: atuanlab
date: 20-04-2024
email: ng.atuanlab.yt@gmail.com
---

# [2024] [PICOCTF] [FORENSIC] SCAN SUPRISE

## 1. THÔNG TIN CHUNG 
### Tác giá và mô tả chung  
- Tác giả: Jeffery John
- Mô tả chung 
    - I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?
    - You can download the challenge files


### Gợi ý 
- QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
- Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
- If you don't have access to a phone, you can also use zbar-tools to convert an image to text


## 2. TÓM TẮT QUÁ TRÌNH 
1. Tải và giải nén tập tin "challenge.zip"
2. Sử dụng tool để đọc nội dung qrcode
    - Sử dụng `zbarimg`
3. Thu thập nội dung của cờ

## 3. CHI TIẾT QUÁ TRÌNH 
### Tải và giải nén tập tin "challenge.zip"

Bạn cũng có thể kết nối đến "Instance" của pico nhưng mình thấy thì tải tập tin "challenge.zip" sẽ thu được một tập png là cờ. Dùng phần mềm đọc nội dung của mã qr là có thể thu được nội dung của cờ

Tải tập tin bằng `wget`

```           
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ wget https://artifacts.picoctf.net/c_atlas/1/challenge.zip
--2024-04-20 12:15:26--  https://artifacts.picoctf.net/c_atlas/1/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 108.157.38.22, 108.157.38.105, 108.157.38.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|108.157.38.22|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 731 [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip 100%     731  --.-KB/s    in 0s         

2024-04-20 12:15:27 (19.3 MB/s) - ‘challenge.zip’ saved [731/731]

                                                       
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ ls -alh     
total 16K
drwxr-xr-x 2 kali kali 4.0K Apr 20 12:15 .
drwxr-xr-x 3 kali kali 4.0K Apr 20 04:25 ..
-rw-r--r-- 1 kali kali  731 Mar 11 19:50 challenge.zip
```

Giải nén tập tin bằng `unzip`: `unzip challenge.zip`

```            
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ unzip challenge.zip 
Archive:  challenge.zip
   creating: home/ctf-player/drop-in/
 extracting: home/ctf-player/drop-in/flag.png  
                                                       
┌──(kali㉿kali)-[~/Desktop/New Folder]
└─$ tree
.
├── challenge.zip
└── home
    └── ctf-player
        └── drop-in
            └── flag.png

4 directories, 2 files
```

Nội dung thu được một tập tin hình ảnh PNG chứa một mã QR là nội dung của cờ

### Đọc nội dung của mã QR

Mình sẽ sử dụng `zbarimg` để đọc nội dung của mã QR
- Có thể tải bằng: `sudo apt install zbar-tools`

Sử dụng `zbarimg` để xem nội dung của mã QR: `zbarimg flag.png `

```
└─$ zbarimg flag.png 
QR-Code:picoCTF{p33k_@_b00_3f7cf1ae}
scanned 1 barcode symbols from 1 images in 0.02 seconds
```

## 4. THU THẬP CỜ 
Nội dung của cờ (flag): `picoCTF{p33k_@_b00_3f7cf1ae}`

## 5. TÀI LIỆU THAM KHẢO 
- https://www.baeldung.com/linux/read-qr-codes

