I. cài môi trường: http://www.masm32.com/download.htm<br>
sau đó tạo project cho nó<br>

II. kiến thức nền tảng:
1. biểu diễn dữ liệu
- chúng ta can biểu diễn dữ liệu dưới dạng: 2, 8, 16, 10
- dù thế nào thì máy cx chỉ lm việc vs nhị phân
- thg thì ng ta sẽ xài bin-> hex
- lm việc vs dữ liệu 32 bit

2. biểu diễn số ng có dấu trong máy tính
- pp dấu lượng: bit đầu tiên bên trái (MSB) lm bit dấu: 0 là (+), 1 là (-)<br>
                có 1 điểm chưa nhất quán là số 0 có 2 cách biểu diễn
- pp bù 1: số dương giữ nguyên, số âm thì bit dấu giữ nguyên, đảo các bit còn lại: số 0 vẫn có 2 cách biểu diễn, <br>
           khó khăn khi máy tính thực hiện các phép toán
- pp bù 2: số dương giữ nguyên, số âm thì lấy bù 1 + 1<br> khắc phục đc cả 2 vấn đề của 2 pp trên -> các máy hiện đại xài
- pp bù 2 vs hệ cơ số 16: vẫn thực hiện như trong nhị phân<br> việc lấy đảo chỉ cần lấy mỗi kí tự hex - 15

3. kích thước lưu trữ
- 1 byte = 8 bit
- 1 word = 16 bit
- 1 doubleword = 32 bit
- 1 quadword = 64 bit

4. biểu diễn xâu
- biểu diễn bằng 1 mảng các giá trị tương ứng trong mã ascii, thg đc viết dưới dạng hex
- xâu “ABC123” có thể hiển thị dưới dạng 41h, 42h, 43h, 31h, 32h, 33h.

5. biểu thức đại số bool
- AND
- OR
- NOT
- XOR

III. các thanh ghi 32 bit
- trong assembly ko có k.niệm biến mà chỉ thao tác vs thanh ghi và bộ nhớ

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/857724e5-9af6-41da-8ece-969df2209d72)<br>

1. thanh ghi đa năng:
- thanh ghi dữ liệu: có 4 thanh ghi dữ liệu

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/c71e9a98-801b-43f3-ad9f-f2ed0e045d33)<br>

*. EAX: thanh ghi tích lũy, xài trong nhập xuất và các lệnh tính toán số học như nhân, chia<br>
*. EBX: thanh ghi cơ sở, đánh dấu địa chỉ, lưu địa chỉ bắt đầu của 1 mảng<br.
*. EDX: thanh ghi dữ liệu, xài trong nhập xuất như EAX<br>
*. ECX: thanh ghi đếm, xài trong vòng lặp đếm số lần lặp<br>

mỗi thanh ghi đc chi thành các đoạn nhỏ hơn như sau:<br>
VD: vs EAX:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/8bd10a40-07f5-40e6-8c38-701724b810e3)<br>

*. nhỉ nhất là 2 thanh ghi 8 bit AH (8 bit cao), AL (8 bit thấp)<br>
*. AH và AL hợp lại thành thanh ghi 16 bit AX <br>
*. AX chứa phần bit thấp của thanh ghi 32 bit EAX<br>
thay đổi giá trị của AH or AL -> giá trị AX thay đổi: AL = 5 -> AX = 5, AH = 5 -> AX = 1280, AL = 5 và AH = 5 -> AX = 1285<br>
chỉ can thay đổi 16 bit thấp AX của EAX còn đổi bit cao -> thủ thuật khác vd dịch trái<br>

- thanh ghi con trỏ: <br>
Có 3 thanh ghi con trỏ là EIP, ESP và EBP. Ba thanh ghi này cũng được chia nhỏ ra 3 thanh ghi 16 nữa là IP, SP và BP.<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/304b3231-6209-4081-b30e-d9fdd7826f7e)<br>

*. EIP và IP: thanh ghi con trỏ lệnh (Instruction Pointer), trỏ ts vị trí lệnh tiếp theo đc thực thi<br> IP kết hợp vs EIP -> địa chỉ chính xác
*. ESP và SP: thanh ghi con trỏ stack (Stack Pointer), trỏ tới định hiện thời của stack, <br>
SP cùng vs thanh ghi SS tham chiếu ts vị trí hiện tại của data or địa chỉ nằm trong program stack<br>
*. EBP và BP: các thanh ghi cơ sở (Base Pointer), tham chiếu đến các biến tham số use trong chg trình con<br>
ta sẽ lm việc vs ESP và EBP hơn là EIP<br>

- thanh ghi chỉ số: đánh số cho các địa chỉ of mảng và xâu or xài trong phép tính số học <br>
ESI và EDI cũng được chia thành các thanh ghi 16 bit SI và DI.<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/78cbb073-11f3-44e0-a9bb-501546137947)<br>

*. ESI và SI: (Source Index) lm địa chỉ nguồn cho các phép toán vs xâu<br>
*. EDI và DI: (Destination Index) lm địa chỉ đích cho các phép toán vs xâu<br>

2. thanh ghi điều khiển
- thanh ghi điều khiển = thanh ghi con trỏ 32 bit + thanh ghi cờ 32 bit (Flags Register)
- assembly ko có cấu trúc if, for, ... -> muốn xài cần kết hợp lệnh ss, lệnh nhảy + giá trị cờ <br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/968e927e-7ab9-41b3-b467-d86af1c3c24b)<br>

- thanh ghi cờ dài 16 bit nma ko phải all bit đều đc use để biểu diễn giá trị cờ:<br>
*. cờ tràn (Overflow Flag - OF): = 1 khi kết quả phép toán có dấu > kích thc of địa chỉ đích<br>
*. Cờ hướng (Direction Flag - DF): định hg trái - phải cho việc di chuyển or ss xâu;<br>
DF = 0 -> trái -> phải và ngc lại
*. Cờ ngắt (Interupt Flag - IF): xác định khi nào các ngắt ngoài như nhập dữ liệu từ bàn phím được xử lý<br>
Khi IF = 1 thì tín hiệu ngắt sẽ được xử lý, ngược lại thì bỏ qua.
*. cờ dừng: hỗ trợ thực thi chương trình theo Single-step mode. <br>
trình debug sẽ đặt giá trị cho TF -> can thực thi từng lệnh 1<br>
*. Cờ dấu (Sign Flag - SF): cho bt kết quả phép toán là âm or dương <br>
giá trị SF phụ thuộc và giá trị bit dấu<br>
*. Cờ không (Zero Flag - ZF): kết quả of phép toán số học or phép ss<br>
ZF = 1 khi k.quả = 0 or ss bằng nhau<br>
*. Cờ nhớ (Carry Flag - CF): chứa giá trị nhớ 0 or 1 of MSB sau khi thực hiện phép toán số học<br>
khi dịch bit (shift) hoặc quay (rotate) -> CF lưu giá trị bit bị đẩy ra cuối cùng<br>
*. Cờ nhớ phụ trợ (Auxiliary Carry Flag - AF): chứa giá trị nhớ khi chuyển từ bit có trọng số 3 lên bit có trọng số 4 <br>
(nhớ từ lower nibble sang high nibble) khi thực hiện phép toán số học.<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/6ce449ac-9f04-4b93-9676-951d87dddc24)<br>

*. Cờ chẵn lẻ (Parity Flag - PF): = 0 khi sl bit 1 là chẵn, = 1 khi sl là lẻ<br>
PF còn được dùng để kiểm tra lỗi.

- DF, IF, TF: là 3 cờ điều khiển; OF, SF, ZF, CF, AF và PF: cờ trạng thái<br>

3. thanh ghi đoạn:
- Một chương trình Assembly được chia thành các đoạn (Segment) chứa dữ liệu, code và stack:<br>
*. Code segment: chứa các mã lệnh thực thi, thanh ghi đoạn code CS chứa địa chỉ start của Code segment<br>
*. Data segment: chứa biến, hằng số, data of chg trình, thanh ghi đoạn dữ liệu DS chứa địa chỉ bắt đầu của Data segment.<br>
*. Stack segment: chứa dữ liệu và địa chỉ trả về của các chương trình con. Các dữ liệu này được lưu trữ theo cấu trúc Stack.<br>
Thanh ghi đoạn stack SS chứa địa chỉ bắt đầu của Stack segment.<br>
*. ngoài ra còn có các thanh ghi đoạn ES (Extra Segment Register), FS và GS cung cấp các phân đoạn bổ sung cho việc lưu trữ dữ liệu<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/9d06401e-9143-4430-9996-f137aa0e40cc)<br>

- để xác định chính xác địa chỉ của 1 dữ liệu hoặc 1 lệnh thuộc phân đoạn, cần có thêm giá trị offset.<br>
-  Địa chỉ thực tế sẽ được tính bằng cách cộng thêm giá trị offset vào địa chỉ đầu phân đoạn.<br>
