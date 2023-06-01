[# Reverse-Engineering](https://ctf.infosecptit.club/files/e69162348febb6abe405334e422e07cb/BasicRev.c?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6NTR9.ZG5E8g.ESGpwQ84eg82eG1jj1lWl3GsOUc

1. đọc code:
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define ull long long
#define ui unsigned int

int main(int argc, char *argv[])
{
    if (argc != 5)
    {
        printf("Oh no!");
        exit(1);
    }
    else
    {
        ull first = atoi(argv[1]);
        if (first != 0xcafe)
        {
            printf("you are wrong, sorry.\n");
            exit(2);
        }
        char s[11] = {0123, 0164, 0064, 0122, 0142, 0165, 0103, 0153, 065, 0137};
        char tmp[11] = {};
        strncpy(tmp, argv[2], 11);
        for (int i = 0; i < strlen(tmp); ++i)
        {
            if (tmp[i] != s[i])
            {
                printf("No no no!");
                exit(3);
            }
        }
        ui second = atoi(argv[4]);
        if (second % 5 == 3 || second % 17 != 8)
        {
            printf("ha, you won't get it!\n");
            exit(4);
        }
        if (strcmp("ISPCTF{", argv[3]))
        {
            printf("so close, dude!\n");
            exit(5);
        }

        ui hash = first * 31337 + (second % 17) * 11 + strlen(argv[3]) - 1615810207;

        char flag[25] = {};
        strcat(flag, strlwr(argv[3]));
        strcat(flag, argv[2]);
        strcat(flag, itoa(hash, tmp, 16));
        strcat(flag, "}");

        printf("Brr wrrr grr\nGet your flag: ");
        puts(flag);
    }
    return 0;
}
```

2. code trên có nội dung:
- check argc != 5 -> thoát, nếu argc = 5 thì tiếp tục
- tiếp theo có biến first = atoi(argv[1]), nếu first != 0xcafe -> thoát => first = 0xcafe
- strncpy(tmp, argv[2], 11): gán 11 kí tự cảu argv[2] vào tmp, nếu tmp khác s -> thoát => tmp = s
- second = atoi(argv[4]), second % 5 == 3 || second % 17 != 8: => second % 5 != 3 và second % 17 = 8
- strcmp("ISPCTF{", argv[3]): so sánh chuỗi nếu argv[3] != ISPCTF{ -> thoát => argv[3] = ISPCTF{
- hash = first * 31337 + (second % 17) * 11 + strlen(argv[3]) - 1615810207: thay (second % 17) = 8

3. đoạn code đc sửa lại như sau: 
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define ull long long
#define ui unsigned int

int main(int argc, char *argv[])
{
   ull first = 0xcafe;
   char s[11] = {0123, 0164, 0064, 0122, 0142, 0165, 0103, 0153, 065, 0137};
   char tmp[11] = {};
   for (int i = 0; i < 11; ++i)
      tmp[i] = char(s[i]);
   ui hash = first * 31337 + 8 * 11 + 7 - 1615810207;
   char flag[25] = {};
   strcat(flag, "ispctf{");
   strcat(flag, tmp);
   strcat(flag, itoa(hash, tmp, 16));
   strcat(flag, "}");
   printf("Brr wrrr grr\nGet your flag: ");
   puts(flag);
   return 0;
}
```
4. flag: ispctf{St4RbuCk5_c0ffee})
