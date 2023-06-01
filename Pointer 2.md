https://ctf.infosecptit.club/files/94c7ae871a3a70eb3f05e771c02889cc/pointer2.c?token=eyJ1c2VyX2lkIjo0NywidGVhbV9pZCI6bnVsbCwiZmlsZV9pZCI6MzF9.ZG-Fmg.8kOHOIEey0uglMAQnSdPm0DMVVU

1. đạon code: 
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int fuzz(char *);
int main(int argc, char **argv)
{
   printf("Let's see if you passed the right flag...\n");
   if (strlen(*(argv + 1)) == 32)
      if (!fuzz(*(argv + 1)))
         printf("Wrong Direction.");
      else if (!strncmp(*(argv + 1), "302753d5b52596eb75b8", 0x14))
         if (!strncmp(*(argv + 1) + 20, "9c11cc30e5c7", 12))
            printf("Here is your flag : ISP{%s}", *(argv + 1));
         else
            printf("Try again.");
      else
         printf("Try again.");
   else
      printf("Try again.");
}
int fuzz(char *key)
{
   char char1[10], char2[10], char3[10], char4[10];
   memset(char1, 0, 10);
   memset(char2, 0, 10);
   memset(char3, 0, 10);
   memset(char4, 0, 10);

   strncpy(char1, key, 8);
   strncpy(char2, key + 8, 8);
   strncpy(char3, key + 16, 8);
   strncpy(char4, key + 24, 8);

   memset(key, 0, 32);

   strcat(key, char3);
   strcat(key, char1);
   strcat(key, char4);
   strcat(key, char2);

   return 1;
}
```
2. giải thích
- đoạn code check 1 chuỗi argv[1] có độ dài 32 kí tự 
- sau 1 loạt thao tác thì nó check 20 kí tự đầu của chuỗi có bằng "302753d5b52596eb75b8" hay ko
- nếu bằng thì hceck tiếp 12 kí tự sau có bằng "9c11cc30e5c7" hay ko
- nếu bằng thì in ra chuỗi

3. vậy flag là: ISP{302753d5b52596eb75b89c11cc30e5c7}
