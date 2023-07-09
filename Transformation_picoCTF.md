- Description
- I wonder what this really is... enc ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)]
- https://mercury.picoctf.net/static/0d3145dafdc4fbcf01891912eb6c0968/enc
- Hints 
- You may find some decoders online

1. dòng code: ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])
- đưa 2 kí tự liên tiếp của flag về số
- sau đó dùng ép kiểu đưa lại về char
- kết quả được lưu vào enc: 灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸弲㘶㠴挲ぽ

2. ta code đoạn code giải mã nó:

```
chau = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸弲㘶㠴挲ぽ"
for i in chau:
    check = 0
    for j in range(1, 257):
        for k in range (1, 257):
            t = (j<<8)+k
            x = ord(i)
            if t==x:
                print(chr(j), chr(k), sep = "", end = "")
                check=1
                break
        if check==1:
            break
```

3. flag: picoCTF{16_bits_inst34d_of_8_26684c20}
