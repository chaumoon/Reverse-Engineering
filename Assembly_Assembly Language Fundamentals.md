Assembly Language Fundamentals <ng tắc cơ bản of nn assembly><br>
I. Basic Language Elements <các phần tử cơ bản of nn assembly><br>
1. First Assembly Language Program
- 1 chg trình ez:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/676694b2-c20e-4e64-aa8d-63d5bd8b5895)<br>

- có 1 thủ tục chính (PROC) tên là "main"
- dòng 2: di chuyển giá trị 5 vào thanh ghi EAX
- dòng 3: cộng giữa giá trị hiện tại of EAX và 6, kết quả lưu vào EAX
- dòng 5: lệnh INVOKE gọi hàm ExitProcess để kết thúc chg trình<br>
*. Adding a Variable<br>
- lưu kết quả phép cộng vào biến sum:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/a9b40d4f-36ce-49b5-b7af-b0e418653eae)<br>

- biến sum đc khai báo ở dòng 2 vs kích thc 32 bit, use từ khóa word 
- từ khóa hoạt động tg tự kiểu dữ liệu, chỉ xác định kích thc
- các chỉ thị .code, .data là các segments -> có đoạn mã và đoạn dữ liệu

2. Integer Literals <số ng hằng><br>
- số nguyên hằng = dấu + 1 or nh chữ số + kí tự cơ số tùy chọn:<br>

      [{+ | - }] digits [ radix ]<br>

- [có hay ko cx đc] {phải có}
- bảng giá trị hệ cơ số:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/fd363e6c-7ba3-4d78-9bf4-3053363c9a88)<br.

- số ng hằng thập lục phân bắt đầu = chữ cái phải có số 0 ở đầu để tránh trình biên dịch hiểu nó là 1 định danh

3. Constant Integer Expressions <biểu thức số ng hằng><br>
- mỗi biểu thức phải đánh giá thành 1 số ng, can đc lưu trữ bs 32 bit
- biểu thức số ng hằng chỉ can đánh giá tại ths điểm biên dịch
- các toán tử số học theo mức độ ưu tiên cao -> thấp:

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/e8b632a8-aaf6-414c-8e92-0e850f45981a)<br>

4. Real Number Literals <số thực>
- biểu diễn dưới dạng số thập phân or thập lục phân:

[sign]integer.[integer][exponent]<br>

    sign {+,-}<br>
    exponent E[{+,-}]integer

5. Character Literals<br>
- 1 hằng kí tự là 1 kí tự duy nhất đặt trong dấu '' or ""
- hằng kí tự đc lưu trữ nội bộ dưới dạng số ng, use chuỗi mã hóa ASCII

6. string literals<br>
- là 1 chuỗi các kí tự (gồm cả khoảng trắng) đc đặt trong dấu '' or ""
- hằng chuỗi ddc lưu trữ dưới dạng chuỗi các byte số ng

7. Reserved words<br>
- các từ dành riêng ko phân biệt hao thg:<br>
. từ viết tắt of các lênh như: MOV, ADD, MUL<br>
. tên đăng kí<br>
. hướng dẫn (directives): cho bt trình dịch ngc cách thức biên dịch chg trình<br>
. Thuộc tính (attributes): cung cấp in4 về kích thc, cách use cho biến và toán hạng<br>
. toán tử: xài trong biểu thức hằng và số<br>
. kí hiệu đc định nghĩa sẵn: @data, trả về giá trị số nguyên hằng số trong quá trình biên dịch
- tìm trong bảng phụ lục A

8. identifiers <định danh><br>
- là tên do lập trình viên chọn, can định danh cho biến, hằng số, ...
- quy tắc tạo định danh:<br>
. can chứa 1 -> 247 kí tự<br>
. ko phân biệt hoa thg<br>
. kí tự đầu ko đc là số<br>
. ko đc trùng vs từ khóa<br>
- can lm nó phân biệt hoa thg bằng cách thêm -Cp vào dòng lệnh khi chạy chhg trình

9. directives <hướng dẫn><br>
- nó ko thực thi trong time chạy, nhưng cho phép bạn định nghĩa biến, macros, thủ tục
- can gán tên cho đoạn nhớ và thực hiện quản lí
- chúng ko phân biệt hoa thg
- vd: Directive DWORD cho biết trình dịch assembler để dành không gian trong chương trình cho một biến doubleword. Trong khi đó, lệnh MOV được thực thi trong thời gian chạy, sao chép nội dung của myVar vào thanh ghi EAX:

      myVar DWORD 26<br>
      mov eax,myVar
      
- các trình dịch assemble khác nhau có tập directive khác nhau<br>
*. Defining Segments <định nghĩa đoạn><br>
- directive: định nghĩa phân chg trình or đoạn 
- .DATA:<br>
       .data<br>
- .CODE: xác định vùng chứa lệnh can thực thi:<br>
       .code<br>
- .STACK: vùng chg trình chứa runtime stack và thiết lập kích thc of nó:<br>
       .stack 100h<br>
- xem tại phụ lục A

10. instructions<br>
- 




