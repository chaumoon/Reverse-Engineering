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
- instruction: 1 câu lệnh đc thực thi khi chg trofnh biên dịch, biên dịch thành byte nn máy, đc tải và thực thi bởi CPU trong time chạy
- gồm 4 phần:<br>
. Label (nhãn): tùy chọn<br>
. Instruction mnemonic (mã gợi nhớ): bắt buộc<br>
. Operand(s) (toán hạng): thg bắt buộc<br>
. Comment: tùy chọn

         [label:] mnemonic [operands] [;comment]<br>

*. Label<br>
- đánh dấu vị trí cho các instruction và dữ liệu
- đặt ngay trc 1 instruction cho bt địa chỉ of instruction đó
- đặt trc biến -> địa chỉ biến
- có 2 loại: <br>

data label: <br>
. định danh vị trí of biến, cung cấp 1 cách thuận tiện để tham chiếu đến biến trong code<br>
. định nghĩa 1 biến tên count: count DWORD 100<br>
. trình biên dịch gán 1 địa chỉ số cho mỗi nhãn, can định nghĩa nh mục data sau 1 nhãn<br>
. VD: array xác định vị trí của số đầu tiên (1024). Các số khác tiếp theo trong bộ nhớ ngay sau đó:<br>

    array DWORD 1024, 2048<br>
          DWORD 4096, 8192<br>
    
. nhãn kết thúc bởi dấu (:)<br>

Code label<br>
. use như aim of câu lệnh nhảy và lặp<br>
. VD: câu lệnh JMP (nhảy) sau chuyển đến vị trí được đánh dấu bởi nhãn có tên là target, tạo thành một vòng lặp:<br>

    target:<br>
        mov ax,bx<r>
        ...<br>
        jmp target<br>
        
. nó can share cùng 1 dòng vs 1 câu lệnh or ở trên 1 dòng riêng biệt:<br>

    L1: mov ax,bx<br>
    L2:<br>
    
*. Instruction Mnemonic<br>
- use để định danh 1 instrcution 
- các mnemonic của instruction trong ngôn ngữ assembly như mov, add và sub cung cấp gợi ý về loại hoạt động mà chúng thực hiện

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/60a2ddd8-c85e-437d-b8c7-3484bca73aaa)<br>

*. Operands<br>
- là 1 giá trị đc use lm đầu vào or đầu ra cho 1 instruction 
- các instruction can có < 3 toán hạng, mỗi toán hạng có thể là một thanh ghi (register), toán hạng bộ nhớ (memory operand), biểu thức số nguyên (integer expression) hoặc cổng vào-ra (input-output port)
- một số toán hạng mẫu:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/18ad3204-4837-4f9a-b02c-550f31ed88d9)<br>

- instruction STC không có toán hạng: stc ; set Carry flag
- Instruction INC có một toán hạng: inc eax ; cộng 1 vào EAX
- Instruction MOV có hai toán hạng: mov count,ebx ; chuyển EBX vào count
- khi các instruction có nh toán hạng -> cái đầu tiên là toán hạng đích (destination operand), casci thứ 2 là toán hạng nguồn (source operand)
- Instruction IMUL có ba toán hạng, trong đó toán hạng đầu tiên là đích, và hai toán hạng tiếp theo là nguồn, được nhân với nhau: imul eax,ebx,5<br>

*. Comments<br>
- trên 1 dòng: bắt đầu = dấu (;)
- trên nh dòng:

      COMMENT + kí tự<br>
          Dòng này là một bình luận.<br>
          Dòng này cũng là một bình luận.<br>
      !<br>
      
*. The NOP (No Operation) Instruction<br>
- chiếm 1 byte trong bộ nhớ, ko thực hiện bất kì công việc nào
- Đôi khi, hướng dẫn này được sử dụng bởi trình biên dịch và trình tổng hợp để căn chỉnh mã thành địa chỉ hiệu quả
- VD: hướng dẫn MOV đầu tiên tạo ra ba byte mã máy. Hướng dẫn NOP căn chỉnh địa chỉ của hướng dẫn thứ ba thành một giới hạn doubleword (bội số chẵn của 4):<br>

       00000000 66 8B C3 mov ax,bx<br>
       00000003 90 nop ; align next instruction<br>
       00000004 8B D1 mov edx,ecx<br>
       
- Các bộ xử lý x86 được thiết kế để tải mã và dữ liệu nhanh hơn từ các địa chỉ doubleword chẵn

II. Example: Adding and Subtracting Integers<br>
1. The AddTwo Program<br>

       1: ; AddTwo.asm - adds two 32-bit integers
       2: ; Chapter 3 example
       3:
       4: .386
       5: .model flat,stdcall
       6: .stack 4096
       7: ExitProcess PROTO, dwExitCode:DWORD
       8:
       9: .code
       10: main PROC
       11: mov eax,5 ; move 5 to the eax register
       12: add eax,6 ; add 6 to the eax register
       13:
       14: INVOKE ExitProcess,0
       15: main ENDP
       16: END main<br>

- dòng 4: ".386" -> xác định đây là chương trình 32bit can truy cập vào thanh ghi và địa chỉ 32bit
- dòng 5 chọn mô hình bộ nhớ của chương trình (flat) và xác định quy ước gọi hàm (gla stdcall) cho các thủ tục
- dòng 6: dành 4096 byte bộ nhớ xài cho ngăn xếp time chạy mà mọi chương trình đều phải có
- dòng 7: khai báo 1 nguyên mẫu (prototype) cho hàm ExitProcess (là 1 dịch vụ chuẩn của windows. nguyên mẫu gồm: tên hàm, từ khóa PROTO, một dấu phẩy và danh sách các tham số đầu vào. Tham số đầu vào cho ExitProcess được đặt tên là dwExitCode, can coi đó là giá trị trả về đc truyền lại cho windows (0 là thành công, !=0 là lỗi). Khi chương trình của bạn đã sẵn sàng kết thúc, nó gọi ExitProcess và trả về một số nguyên để thông báo cho hệ điều hành rằng chương trình của bạn đã hoạt động tốt.
- dòng 16: dùng chỉ thị END đánh dấu dòng cuối đc lắp ráp và xác định điểm nhập chg trình (main). main đc khai báo ở dòng 10 và nó đánh dấu địa chỉ mà chg trình sẽ bắt đầu thực thi<br>

*. A Review of the Assembler Directives: (đánh giá lại các chỉ thị)<br>
- .MODEL: cho bt trình dịch use mô hình bộ nhớ nào:<br>
   ```.model flat, stdcall```<br>
. chg trình 32 bit luôn xài chế độ flat, liên quan đến chế độ bảo vệ của bộ xử lý<br>
. stdcall -> cách trinh =f biên dịch quản lý ngăn xếp trong time chạy khi gọi các thủ tục<br>
- .STACK: cho bt số byte trình biên dịch nên dành cho ngăn xếp trong time chạy of chg trình:<br>
   ```.stack 4096```<br>
. all chg trình hiện đại đều xài 1 ngăn xếp khi gọi các tiểu trình: để lưu trữ các tham số truyền vào, lưu địa chỉ of mã đã gla hàm<br>
. CPU xài địa chỉ này để quay lại khi cuộc gọi hàm kết thúc, trở lại vị trí mà hàm đã đc gọi<br>
. ngăn xếp time chạy can chứa các biến cục bộ - biến đc khai báo bên trong 1 hàm<br>
- .CODE: đánh dấu phần thân mã of chg trình, ns chứa các chỉ thị can thực thi, sau dòng này là khai báo điểm nhập chg trình (main - theo quy ước). điểm nhập: ns câu lệnh đầu tiên mà chg trình sẽ thực thi <br>
   ```.code
       main PROC```<br>
- ENDP: đánh dấu kết thúc của một thủ tục, chg trình tên main -> phải xài tên main<br>
   ```main ENDP```<br>
- END: kết thúc chg trinh và trỏ ts điểm nhập chg trình<br>
   ```END main```<br>
. viết j sau dòng END cx đc vì nó sẽ đc bỏ qua<br>

2. Running and Debugging the AddTwo Program<br>
*. Debugging Demonstration<br>

 ![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/13731d99-db92-4f85-8824-cebbced15209)<br>

*. Customizing the Debugging Interface <tùy chỉnh giao diện gỡ lỗi><br>
- khi chạy chg trình nó sẽ đc khởi chạy bên trong 1 cửa sổ control.
- can mở 1 cửa sổ command pronpt trong thư mục Debug\Bin của dự án và chạy ứng dụng trực tiếp từ dòng lệnh
- nếu lm ddieeefu này -> chỉ thấy k.quả of chg trình bao gồm văn bản đc viết ra cửa sổ control

III. Assembling, Linking, and Running Programs<br>
1. The Assemble-Link-Execute Cycle <chu trình Assemble-Link-Execute><br>
- quá trình chỉnh sửa, lắp ráp, liên kết và thực thi các chg trình ngôn ngữ assembly<br>
. B1: use trình soạn thảo văn bản tạo 1 tệp văn bản tên là source file<br>
. B2: trình biên dịch đọc tệp nguồn và tạo ra tệp object file là phiên bản dịch sang nn máy of chg trình. nó cx tạo ra listing file. nếu có lỗi -> quay về B1 để sửa<br>
. B3: trình liên kết đọc object file và check xem chg trình có chứa các lời gọi tới các thủ tục trong thư viện liên kết hay ko. trình liên kết sao chép các thủ tục cần thiết từ thư viện liên kết + object file -> executable file<br>
. B4: tiện ích nạp hệ điều hành đọc executable file và bộ nhớ và nhảy đến địa chỉ bắt đầu of chg trình trên CPU và chg trình bắt đầu thực thi<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/8e73b188-27d8-4bdb-a8ab-26b83a364731)<br>

2. Listing File<br>
- 1 listing file chứa 1 bản sao của mã nguồn chg trình, vs số dòng, địa chỉ số of mỗi lệnh, các byte mã máy of mỗi lệnh (dưới dạng hệ thập lục phân) và 1 symbol table
- symbol table: chứa tên all định danh (identifiers), các đoạn (segments) và thông tin liên quan

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/d7add1ab-e356-4be9-b3ff-2c6e4a434186)<br>

- dòng 1-7 ko chứa mã thực thi -> sao chép trực tiếp từ tệp nguồn mà ko có j thay đổi
- dòng 9: cho thấy đoạn mã (code segment) bắt đầu tại địa chỉ 00000000 (trong một chương trình 32-bit, địa chỉ hiển thị dưới dạng 8 chữ số thập lục phân). địa chỉ này liên quan đến đầu of vùng bộ nhớ chg trình nhưng sẽ đc chuyển đổi thành bộ nhớ địa chỉ tuyệt đối khi chg trình đc nạp vào bộ nhớ. Khi điều đó xảy ra, chương trình có thể bắt đầu tại một địa chỉ như 00040000h.
- dòng 10, 11: hiển thị địa chỉ bắt đầu là 00000000 vì lệnh thực thi đầu tiên là MOV (dòng 11)
- dòng 11: có 1 số byte thập lục phân xuất hiện giữa địa chỉ và mã nguồn. Các byte này (B8 00000005) đại diện cho lệnh mã máy (B8) và giá trị hằng số 32-bit (00000005) được gán vào thanh ghi EAX bởi lệnh:<br>
   ```11: 00000000 B8 00000005 mov eax,5```<br>
- giá trị B8 (mã hoạt động or opcode): đại diện cho 1 lệnh máy cụ thể di chuyển 1 số nguyên 32bit vào thanh ghi eax
- dòng 12: chứa 1 lệnh thực thi, bắt đầu từ 00000005. vị trí này là 1 khoảng cách 5 byte từ đầu chg trình
- dòng 14: chứa chỉ thị invoke, nó khiến trình biên dịch tạo ra các câu lệnh PUSH, CALL hiện trên dòng 15, 16
- các lệnh máy đc tải vào bộ nhớ dưới dạng 1 chuỗi các giá trị số nguyên, ở đây là hệ 16: B8, 00000005, 83, C006, 6A, 00, EB, 00000000. số cữ số -> số bit (1 số -> 8 bit) -> các lệnh máy có đúng 15 byte
- Phần còn lại của tệp danh sách chứa danh sách các cấu trúc và liên minh, cũng như các thủ tục, tham số và biến cục bộ<br>
  
IV. Defining Data <định nghĩa dữ liệu><br>
1. Intrinsic Data Types <các loại data cố định><br>
2. Data Definition Statement <br>
- 1 Data Definition Statement dành ra bộ nhớ cho 1 biến, vs tên tùy chọn
- cú pháp:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/86418a6b-a490-4dc9-ab4c-6e166238fdf5)<br>

- vd:<br>
   ```count DWORD 12345```<br>
- name: tên tùy chọn gán cho biến phải tuân theo các quy tắc cho các định danh
- Directive: can là bất kì cái nào trong bảng 3-2 và 3-3
- Initializer: ít nhất 1 giá trị khởi tạo đc yêu cầu trong 1 câu lệnh định nghĩa dữ liệu, ngảy cả khi nó là số 0. các giá trị khởi tạo bổ sung đc phân tách bằng dấu ','. nếu muốn để lại biến ko đc khởi tạo *gán 1 giá trị ngẫu nhiên) -> xài kí hiệu '?'

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/2f3475e3-19ca-4c20-b8a3-0819bfb1286a)<br>

3. Adding a Variable to the AddTwo Program<br>
```
      1: ; AddTwoSum.asm - Ví dụ chương 3
      2:
      3: .386
      4: .model flat,stdcall
      5: .stack 4096
      6: ExitProcess PROTO, dwExitCode:DWORD
      7:
      8: .data
      9: sum DWORD 0
      10:
      11: .code
      12: main PROC
      13: mov eax,5
      14: add eax,6
      15: mov sum,eax
      16:
      17: INVOKE ExitProcess,0
      18: main ENDP
      19: END main
```

- can chạy nó trong trình gỡ lỗi = cách đặt 1 điểm dừng (breakpoint) tại dòng 13 và thực hiện từng dòng 1.
- thực hiện xong dòng 15 -> biến sum xem giá trị of nó or mở 1 của sổ Watch (theo dõi)

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/7ef9ad5d-c9f2-440d-8616-6771c2ed57c1)<br>

4. Defining BYTE and SBYTE Data<br>
- BYTE (define byte) và SBYTE (define signed byte): dành chỗ lưu trữ cho 1 or nh giá trị ko dấu or có dấu. mỗi giá trị khởi tạo phải fit vs 8 bit of ko gian lưu trữ<br>
  
      value1 BYTE 'A'      ; character literal
      value2 BYTE 0        ; smallest unsigned byte
      value3 BYTE 255      ; largest unsigned byte
      value4 SBYTE −128    ; smallest signed byte
      value5 SBYTE +127    ; largest signed byte<br>

- 1 giá trị khởi tạo dang dấu '?' khiến biến ko đc khởi tạo <=> nó sẽ đc gán 1 giá trị tại thời điểm chạy:<br>
   ```value6 BYTE ?```<br>
- tên tùy chọn là 1 nhãn đánh dấu vị trí of biến tính từ đầu of đoạn bao bọc nó. VD: nếu value1 nằm ở vị trí offset 0000 trong đoạn dữ liệu và chiếm 1 byte không gian lưu trữ, value2 sẽ tự động nằm ở vị trí offset 0001<br>
   ```value1 BYTE 10h
      value2 BYTE 20h
   ```<br>
- Chỉ thị DB cũng có thể định nghĩa một biến 8 bit, có dấu hoặc không dấu:<br>
   ```
   val1 DB 255 ; byte không dấu
   val2 DB -128 ; byte có dấu
   ```<br>

*. Multiple Initializers <nh giá trị khởi tạo><br>
- nếu có nh giá trị khởi tạo trong cùng 1 định nghĩa dữ liệu, nhãn of nó chỉ tham chiếu đến offset of giá trị khởi tạo đầu tiên<br>
   ```list BYTE 10,20,30,40```<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/3f71367c-9317-4bfc-a955-e6802128aa2a)<br>

- kp all định nghĩa dữ liệu đều yêu cầu nhãn. VD: tiếp tục mảng byte bắt đầu = list<br>
   ```list BYTE 10,20,30,40
           BYTE 50,60,70,80
           BYTE 81,82,83,84```<br>
- 





   




