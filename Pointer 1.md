https://ctf.infosecptit.club/files/db539380e7d7c672c7fcce6cd5372f3d/pointer1.c?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6MzB9.ZG8Drw.AKjU1cONqrqcYQF_6De9fXpcAeU

1. mở file ta có: 
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int check_key(char *);
int sthIdontknow(char, char);
int main(void)
{
    char *usrInp;
    printf("Key? ");
    usrInp = (char *)malloc(33);
    scanf("%s", usrInp);
    int len = strlen(usrInp);
    if (len == 32)
    {
        int (*check)(char *) = check_key;
        if (check(usrInp))
        {
            printf("Correct key.\n");
            printf("Flag is: flag{%s}\n", usrInp);
        }
        else
            printf("Wrong key.\n");
    }
    else
        printf("Invalid.\n");
    free(usrInp);
    return 0;
}
int check_key(char *key)
{
    char sth[] = "pearldarkk";
    char mySth[] = {0x45, 0xd, 0x50, 0x1c, 0x5d, 0xa, 0x46, 0x2d, 0x5e, 0x1f, 0x44, 0x17, 0x54, 0x2d, 0x6, 0x11, 0x54, 0x6, 0x34, 0x7, 0x41, 0xe, 0x52, 0x2d, 0x19, 0x16, 0x3e, 0x1, 0x6, 0x5a, 0x1c, 0x56};
    void *c1 = sth, *c2 = key;
    while (c2 < key + 1 && !(sthIdontknow(*(char *)(c1 + (((char *)c2 - key) % 0xA)), *(char *)c2) ^ *mySth))
    {
        c2 = (char *)c2 + 1;
        ++*mySth;
    }
    if (c2 == key + 1)
        return 1;
    return 0;
}
int sthIdontknow(char b, char k)
{
    char b2;
    for (size_t i = 0; i < 8; ++i)
    {
        if (((b >> i) & 1) == ((k >> i) & 1))
            b2 = ((1 << i) ^ -1) & b & 255;
        else
            b2 = ((1 << i) & 255) | b;
        b = (char)b2;
    }
    return b;
}
```
đoạn code yêu cầu nhập vào 1 key dài 32 kí tự để check key và sau đó in ra flag nếu đúng
2. phân tích hàm con:
```
int sthIdontknow(char b, char k)
{
    char b2;
    for (size_t i = 0; i < 8; ++i)
    {
        if (((b >> i) & 1) == ((k >> i) & 1))
            b2 = ((1 << i) ^ -1) & b & 255;
        else
            b2 = ((1 << i) & 255) | b;
        b = (char)b2;
    }
    return b;
}
```
- hàm này thao tác với 2 kí tự b và k
```
if (((b >> i) & 1) == ((k >> i) & 1))
            b2 = ((1 << i) ^ -1) & b & 255;
```
dịch phải b, và k i bit sau đó & 1 để lấy bit cuối cùng, kiểm tra nếu chúng bằng nhau ta sẽ tính giá trị b2
((1 << i) ^ -1) & b & 255: 1 dịch trái i bit sau đó ^ -1 để lấy đảo các bit
sau đó & b & 255: giữ nguyên các bit khác nhau của b và k chỉ đảo bit thứ i thành 0
```
else
            b2 = ((1 << i) & 255) | b;
```
giữ nguyên các bit khác nhau của b và k chỉ đảo bit thứ i thành 1
=> hàm trả về 0 khi b, k giống nhau
=> *(char *)(c1 + (((char *)c2 - key) % 0xA)) = *(char *)c2) ^ *mySth)
3. do đó ta viết code để tìm ra key như sau:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int sthIdontknow(char, char);
int main(void)
{
   char sth[] = "pearldarkk";
   char mySth[] = {0x45, 0xd, 0x50, 0x1c, 0x5d, 0xa, 0x46, 0x2d, 0x5e, 0x1f, 0x44, 0x17, 0x54, 0x2d, 0x6, 0x11, 0x54, 0x6, 0x34, 0x7, 0x41, 0xe, 0x52, 0x2d, 0x19, 0x16, 0x3e, 0x1, 0x6, 0x5a, 0x1c, 0x56};
   void *c1 = sth;
   char c2;
   for (int i = 0; i < 32; i++)
   {
      char x = *(char *)(c1 + i % 10);
      c2 = char(x ^ mySth[i]);
      printf("%c", c2);
   }
   return 0;
}
```
key là: 5h1n1n'_5t4r5_ju5t_l1k3_ur_sm1l3
4. ném key lại vào đoạn code ban đầu ta có flsg là: flag{5h1n1n'_5t4r5_ju5t_l1k3_ur_sm1l3}
