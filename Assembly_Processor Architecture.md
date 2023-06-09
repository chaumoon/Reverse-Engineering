PROCESSOR ARCHITECTURE <KIẾN TRÚC BỘ XỬ LÝ OR KIẾN TRÚC VI XỬ LÝ><br>

I. General Concepts<br>

1.  Basic Microcomputer Design <br>
- mô tả thiết kế cơ bản của 1 máy tính vi mô giả định:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/fd4e538b-d300-4e50-910e-30ba14201f12)<br>

- đơn vị xử lý trung tâm (CPU): ns các phép tính diễn ra, bao gồm một số lượng giới hạn các vị trí lưu trữ được gọi là thanh ghi, một đồng hồ tần số cao, một đơn vị điều khiển và một đơn vị logic và phép tính.<br>
• Đồng hồ đồng bộ hóa các hoạt động bên trong của CPU với các thành phần hệ thống khác.<br>
• Đơn vị điều khiển (CU) phối hợp các bước thực hiện các hướng dẫn máy tính.<br>
• Đơn vị logic và phép tính (ALU) thực hiện các phép tính số học như cộng và trừ, và các phép toán logic như AND, OR và NOT.<br>
- CPU nối vs mt thông qua các chân, hầu hết các chân nối vs bus dữ liệu, bus điều khiển và bus địa chỉ
- đơn vị lưu trữ nhận dữ liệu từ CPU,  chuyển dữ liệu từ bộ nhớ truy cập ngẫu nhiên (RAM) vào CPU, và chuyển dữ liệu từ CPU vào bộ nhớ
- các chg trình lưu trữ trong bộ nhớ phải dc sao chép vafp CPU trc khi chúng can thực thi, các hg dẫn của chg trình sao chép 1-1 or 1 lần 1 nhóm
- BUS:<br>
. là 1 gr dây song2 xài để chuyển dữ liệu từ phần này của máy sang phần kia<br>
. gồm 4 loại: <br>
bus dữ liệu: chuyển dữ liệu và hướng dẫn giữa CPU và bộ nhớ<br>
bus I/O: chuyển dữ liệu giữa CPU và các thiết bị nhập/xuất của hệ thống<br>
bus điều khiển: use tín hiệu nhị phân đồng bộ hóa hoạt động của thiết bị k.nối vs bus hệ thống<br>
bus địa chỉ: chứa địa chỉ of hg dẫn và dữ liệu khi chúng thực thi chuyển dữ liệu giữa CPU và bộ nhớ<br>
- CLOCK:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/f3747126-5490-4471-ab3b-f33dc3839a74)<br>

. hoạt động liên quan đến CPU và bus hệ thống đc đồng bộ = 1 clock nội pulsing vs tốc độ ko đổi<br>
. đơn vị time: machine cycle or clock cycle- là time cần cho 1 xung đồng hồ hoàn chỉnh<br>
. độ dài of chu kì = nghịch đảo tốc độ của đồng hồ<br>
. 1 hg dẫn mt cần ít nhất 1 clock, các hg dẫn yêu cầu truy cấp bộ nhớ thg có các chu kì clock gla trạng thái chowf do sự khác bt về tốc độ CPU, bus hệ thống và mạch nhớ<br>

2. Instruction Execution Cycle <chu kì thực thi hg dẫn><br>
- thực thi 1 lệnh máy cần qua chuỗi bc gla chu kì thực thi lệnh. 
- giải sử thanh ghi con trỏ lệnh chứa địa chỉ of lệnh mà chúng ta muốn thực thi. các bc: <br>
. B1: CPU lấy lênh từ hàng đợi lệnh, sau đó tăng con trỏ lệnh lên<br>
. B2: CPU giải mã lệnh bằng cách xem xét mẫu bit nhị phân của nó. Mẫu bit này có thể tiết lộ rằng lệnh có các toán hạng (giá trị đầu vào).<br>
. B3: CPU lấy các toán hạng <nếu có> từ các thanh ghi và bộ nhớ, đôi khi liên quan đến các phép tính địa chỉ.<br>
. B4: CPU thực thi lệnh, sử dụng toán hạng, cập nhật một số cờ trạng thái như Zero, Carry và Overflow.<br>
. B5: CPU lưu kết quả thực thi vào toán hạng đó trong bộ nhớ.<br>
-> đơn giản là: lấy -> giải mã -> thực thi<br>
- sơ đồ khối luồng dữ liệu bên trong CPU:

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/aea8227b-a068-4ce2-82b1-69b0d9525851)<br>

- mối quan hệ giữa các thành phần tg tác trong suốt chu kì:<br>
. Để đọc lệnh chương trình từ bộ nhớ, một địa chỉ được đặt trên bus địa chỉ<br>
. bộ điều khiển bộ nhớ đặt mã yêu cầu lên bus dữ liệu, làm cho mã có sẵn bên trong bộ nhớ cache mã. Giá trị của con trỏ lệnh xác định lệnh sẽ được thực thi tiếp theo<br>
. Lệnh được phân tích bởi bộ giải mã lệnh, gây ra việc gửi các tín hiệu số phù hợp đến bộ điều khiển, điều phối các đơn vị ALU (Arithmetic Logic Unit - Đơn vị tính toán và logic) và đơn vị số dấu chấm động (floating-point unit).<br>
. bus điều khiển chuyển tín hiệu sử dụng đồng hồ hệ thống để điều phối việc truyền dữ liệu giữa các thành phần khác nhau của CPU<br>

3. Reading from Memory<br>
- máy tính đọc bộ nhớ chậm hơn truy cập vào thanh ghi nội bộ
- thông qua 4 bc:<br>
. B1: Đặt địa chỉ của giá trị bạn muốn đọc lên bus địa chỉ<br>
. B2: Kích hoạt (thay đổi giá trị của) chân RD (read) của bộ xử lý<br>
. B3: Chờ một chu kỳ đồng hồ để các chip bộ nhớ phản hồi<br>
. B4: Sao chép dữ liệu từ bus dữ liệu vào toán hạng đích<br>
- 1 bc thg yêu cầu 1 chu kì clock, thanh ghi of CPU thg chỉ cần truy cập 1 chu kì clock duy nhất
- giảm time đoạc và ghi vào bộ nhớ -> lưu trữ các lệnh và dữ liệu đã được sử dụng gần đây nhất trong bộ nhớ tốc độ cao được gọi là bộ nhớ cache
- can tìm thấy dữ liệu trong cache -> cache hit, ko tìm thấy -> cache miss
- bộ nhớ cache có 2 loại: 
. bộ nhớ cache cấp 1 (cache chính): lưu trữ ngay trên CPU<br>
. bộ nhớ cache cấp 2 (cache phụ): chậm hơn 1 chút và đc kết nối vs CPU = 1 bus dữ liệu tốc độ cao<br>
-> chúng hoạt động cùng nhau theo 1 cách tối ưu<br>
- cache nhanh vì nó xây dựng từ chip bộ nhớ (RAm tĩnh)

4. Loading and Executing a Program<br>
- quá trình tải và thực thi chg trình:
. B1: Hệ điều hành (OS) tìm kiếm tên tệp chương trình trong thư mục đĩa hiện tại <ko thấy -> tìm kiếm trong danh sách thư mục đã định trước (gọi là đường dẫn) cho tên tệp>, ko thấy -> hiện thông báo lỗi<br>
. B2: lấy thông tin cơ bản về tệp chương trình từ thư mục đĩa: kích thước tệp và vị trí vật lý trên ổ đĩa<br>
. B3: xác định vị trí bộ nhớ tiếp theo có sẵn và tải tệp chương trình vào bộ nhớ, cấp phát một khối bộ nhớ cho chương trình và nhập thông tin về kích thước và vị trí của chương trình vào một bảng (thường được gọi là bảng miêu tả), có thể điều chỉnh giá trị của các con trỏ trong chương trình để chứa địa chỉ của dữ liệu chương trình<br>
. B4: thực thi lệnh máy đầu tiên của chương trình (điểm vào), gán một số định danh quy trình (process ID) cho quy trình đó, được sử dụng để theo dõi nó trong quá trình chạy.<br>
. B5: Quy trình chạy tự động, hệ điều hành theo dõi quá trình thực thi và đáp ứng các yêu cầu tài nguyên hệ thống<br>
. B6: quy trình kết thúc, nó sẽ bị xóa khỏi bộ nhớ<br>

II. 32-Bit x86 Processors<br>

1. Modes of Operation<br>
- mô tả về các chế độ:<br>
*. Protected Mode<br>
- tất cả các chỉ thị và tính năng đều có sẵn
- chương trình được cung cấp các khu vực bộ nhớ riêng được gọi là các đoạn (segments)
- bộ xử lý ngăn chặn các chương trình truy cập vào bộ nhớ ngoài các đoạn được gán cho chúng<br>

*. Virtual-8086 Mode<br>
- để bộ xử lí can thục thi chg trình ở môi trg an toàn 
- can thực thi nh phiên ảo-8086 riêng biệt cùng một lúc

*. Real-Address Mode<br>
- triển khai môi trường lập trình của một bộ xử lý Intel sớm với một số tính năng bổ sung
- hữu ích nếu một chương trình yêu cầu truy cập trực tiếp vào bộ nhớ hệ thống và các thiết bị phần cứng

*. System Management Mode - SMM<br>
- cung cấp cho hệ điều hành một cơ chế để triển khai các chức năng: quản lý năng lượng và bảo mật hệ thống
- đc triển khai bằng cách tùy chỉnh bộ xử lý cho một cấu hình hệ thống cụ thể

2. Basic Execution Environment <mt thực thi cơ bản><br>
*. Address Space<br>
- một tác vụ hoặc chương trình có thể truy cập không gian địa chỉ tuyến tính lên đến 4 GBytes
- vi xử lý P6, một kỹ thuật gọi là địa chỉ vật lý mở rộng cho phép địa chỉ tới tổng cộng 64 GBytes bộ nhớ vật lý
- chương trình ở chế độ địa chỉ thực chỉ có thể truy cập vào một phạm vi 1 MByte
- Nếu bộ xử lý đang ở chế độ bảo vệ và chạy nhiều chương trình trong chế độ ảo-8086, mỗi chương trình có khu vực bộ nhớ riêng của riêng nó với dung lượng 1 MByte

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/b3b3c73b-66ff-4720-8aff-7e0f5410060d)<br>

*. Basic Program Execution Registers <thanh ghi thực thi chg trình cơ bản><br>
- Thanh ghi là các vị trí lưu trữ tốc độ cao ngay bên trong CPU, được thiết kế để truy cập với tốc độ cao hơn so với bộ nhớ thông thường
- Có 8 thanh ghi dùng chung, 6 thanh ghi đoạn (segment registers), 1 thanh ghi cờ trạng thái của bộ xử lý (EFLAGS), 1 con trỏ chỉ thị (EIP).
- General-Purpose Registers <thanh ghi use chung>:<br>
. xài cho phép tính toán và di chuyển dữ liệu<br>
. VD: 16 bit thấp của thanh ghi EAX có thể được truy cập bằng tên gọi AX<br>
  
![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/b3651173-8850-4958-9929-367ca1afad7f)<br>
  
. Một phần của một số thanh ghi có thể được truy cập như các giá trị 8 bit<br>
. tg tự vs EAX, EBX, ECX và EDX<br>
  
  ![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/714c1418-5d0b-4b95-a390-2caeecb7bfd6)<br>

. các thanh ghi còn lại chỉ can truy cập bằng cách sử dụng tên 32 bit hoặc 16 bit<br>
  
  ![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/303dc463-ae9a-499d-b16d-772c559cad59)<br>
  
- Specialized Uses <br>
. EAX: tự động được sử dụng bởi các lệnh nhân và chia, gla thanh ghi tích lũy mở rộng<br>
. CPU: tự động sử dụng ECX làm bộ đếm vòng lặp<br>
. ESP: sử dụng để địa chỉ dữ liệu trên ngăn xếp (một cấu trúc bộ nhớ hệ thống), ít được sử dụng cho các phép tính thông thường hoặc chuyển dữ liệu, gla thanh ghi trỏ ngăn xếp mở rộng<br>
. ESI và EDI: được sử dụng bởi các lệnh truyền dữ liệu tốc độ cao, gọi là thanh ghi chỉ số nguồn mở rộng và thanh ghi chỉ số đích mở rộng<br>
. EBP: được xài bởi ngôn ngữ cấp cao để tham chiếu các tham số hàm và biến cục bộ trên ngăn xếp, Không nên sử dụng cho các phép tính thông thường hoặc chuyển dữ liệu trừ khi ở mức độ lập trình nâng cao, gọi là thanh ghi trỏ khung mở rộng.<br>
  
- Segment Registers <thanh ghi đoạn><br>
. trong real-address mode: 16 bit chỉ định địa chỉ cơ sở của các khu vực bộ nhớ được chỉ định trước có tên gọi là đoạn (segments)<br>
. protected mode: các thanh ghi đoạn giữ các con trỏ tới bảng mô tả đoạn (segment descriptor tables)<br>
. Một số đoạn chứa các chỉ thị chương trình (code), những đoạn khác chứa biến (data), và một đoạn khác được gọi là đoạn ngăn xếp (stack segment) chứa biến cục bộ của hàm và các tham số của hàm<br>
  
- Instruction Pointer (EIP): thanh ghi chỉ thị, chứa địa chỉ của chỉ thị tiếp theo sẽ được thực thi, Một số chỉ thị máy tính cập nhật giá trị của EIP, dẫn đến chương trình nhảy tới vị trí mới
  
- EFLAGS Register: EFLAGS (just Flags) là một thanh ghi chứa các bit nhị phân riêng lẻ, điều khiển hoạt động của CPU hoặc phản ánh kết quả của một số hoạt động của CPU. Một số chỉ thị kiểm tra và điều khiển từng cờ xử lý riêng lẻ.
  
-> cờ đc đặt khi nó = 1, xóa khi nó = 0<br>
  
- Control Flags<br>
. điều khiển hoạt động của CPU<br>
. Các chương trình có thể đặt các bit riêng lẻ trong thanh ghi EFLAGS để điều khiển hoạt động của CPU<br>
  
- Status Flags<br>: phản ánh kết quả của các phép toán số học và logic được thực hiện bởi CPU<br>
. Carry flag (CF): thiết lập khi kết quả của một phép toán số học không dấu quá lớn để chứa vào đích<br>
. Overflow flag (OF): thiết lập khi kết quả của một phép toán số học có dấu quá lớn hoặc quá nhỏ để chứa vào đích<br>
. Sign flag (SF): thiết lập khi kết quả của một phép toán số học hoặc logic tạo ra một kết quả âm<br>
. Zero flag (ZF):  thiết lập khi kết quả của một phép toán số học hoặc logic tạo ra kết quả = 0<br>
. Auxiliary Carry flag (AC):  thiết lập khi một phép toán số học gây ra việc nhớ từ bit 3 sang bit 4 trong một toán hạng 8-bit<br>
. Parity flag (PF): thiết lập nếu byte có độ trọng nhỏ nhất trong kết quả chứa một số chẵn các bit 1. Ngược lại, nếu không chứa số bit 1 chẵn, PF sẽ được xóa, thg đc use để check lỗi<br>
  
*. MMX Registers <đăng kí MMX><br>
- cải thiện hiệu suất của bộ xử lý Intel khi thực hiện các ứng dụng đa phương tiện và truyền thông tiên tiến
- Tám đăng ký MMX 64-bit hỗ trợ các lệnh đặc biệt được gọi là SIMD (Single-Instruction, Multiple-Data - Một Lệnh, Nhiều Dữ Liệu)
- hoạt động song song trên các giá trị dữ liệu chứa trong các đăng ký MMX
- tên của các đăng ký MMX thực tế là các bí danh của các đăng ký giống nhau được sử dụng bởi đơn vị dấu chấm động<br>

*. XMM Registers<br>
- 8 đăng ký 128-bit gọi là đăng ký XMM, được sử dụng bởi các tiện ích mở rộng SIMD dành cho bộ chỉ thị
- Floating-Point Unit (FPU): <br>
. thực hiện phép tính dấu chấm động tốc độ cao<br>
. FPU đã được tích hợp vào chip bộ xử lý chính<br>
. Có tám đăng ký dữ liệu dấu chấm động trong FPU, được đặt tên là ST(0), ST(1), ST(2), ST(3), ST(4), ST(5), ST(6) và ST(7)<br>
  
  ![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/2d8accda-dacb-4116-aec2-2f7fd87de42a)<br>
  
3. x86 Memory Management <quản lí bộ nhớ x86><br>
*. real-address mode<br>
- chỉ có thể truy cập được 1 MByte bộ nhớ, từ hexa 00000 đến FFFFF<br>
- chỉ có thể chạy một chương trình tại một thời điểm, nhưng có thể tạm thời ngắt chương trình đó để xử lý các yêu cầu từ các thiết bị ngoại vi<br>
- chương trình ứng dụng được phép truy cập vào bất kỳ vị trí bộ nhớ nào, bao gồm cả các địa chỉ được liên kết trực tiếp với phần cứng hệ thống<br>
- Hệ điều hành MS-DOS chạy trong chế độ địa chỉ thực, và Windows 95 và 98 cũng có thể khởi động vào chế độ này<br>

*. protected mode<br>
- có thể chạy nhiều chương trình cùng một lúc<br>
- Mỗi quá trình (chương trình đang chạy) được gán một tổng cộng 4 GByte bộ nhớ<br>
- Mỗi chương trình có thể được gán một khu vực bộ nhớ riêng, và các chương trình bị ngăn không vô tình truy cập vào mã và dữ liệu của nhau<br>
- MS-Windows và Linux chạy trong chế độ bảo vệ<br>

*. virtual-8086 mode<br>
- máy tính chạy trong chế độ bảo vệ và tạo ra một máy ảo-8086 với không gian địa chỉ riêng 1 MByte, giả lập một máy tính 80x86 chạy trong chế độ địa chỉ thực<br>
- có thể chạy nhiều cửa sổ như vậy cùng một lúc, và mỗi cửa sổ được bảo vệ khỏi các tác động từ các cửa sổ khác<br>
- Một số chương trình MS-DOS mà trực tiếp tham chiếu đến phần cứng máy tính sẽ không chạy trong chế độ này dưới Windows NT, 2000 và XP<br>

III. 64-Bit x86-64 Processors<br>
- tính năng cơ bản:<br>
. Nó tương thích ngược với tập lệnh x86.<br>
. Địa chỉ có độ dài 64 bit, cho phép không gian địa chỉ ảo có kích thước là 264 byte. Trên các thiết kế chip hiện tại, chỉ có 48 bit thấp nhất được sử dụng<br>
. Nó có thể sử dụng thanh ghi tổng quát 64 bit, cho phép các lệnh có toán hạng số nguyên 64 bit<br>
. Nó sử dụng tám thanh ghi tổng quát nhiều hơn so với x86<br>
. Nó sử dụng không gian địa chỉ vật lý 48 bit, hỗ trợ lên đến 256 terabyte RAM<br>
- khi chạy trong chế độ 64-bit nguyên bản, các bộ vi xử lý này không hỗ trợ chế độ thực 16-bit hoặc chế độ ảo-8086<br>

1. 64-Bit Operation Modes<br>
- Kiến trúc Intel 64 giới thiệu một chế độ mới được gọi là IA-32e<br>
- gồm hai chế độ con: chế độ tương thích và chế độ 64-bit

*. Compatibility Mode <chế độ tg thích><br>
- các ứng dụng hiện có 16-bit và 32-bit thường có thể chạy mà không cần biên dịch lại
- Windows 16-bit (Win16) và DOS sẽ không chạy trên phiên bản 64-bit của Microsoft Windows
- Windows 64-bit không có một tiến trình máy ảo DOS để tận dụng khả năng của bộ xử lý chuyển sang chế độ ảo-8086
  
*. 64-Bit Mode<br>
- bộ xử lý chạy các ứng dụng sử dụng không gian địa chỉ tuyến tính 64-bit
- Chế độ này cho phép sử dụng các toán tử hướng 64-bit
  
2. Basic 64-Bit Execution Environment <Môi trường thực thi cơ bản 64-bit><br>
- khác biệt quan trọng nhất so với các bộ xử lý 32-bit là:<br>
. Mười sáu thanh ghi 64-bit dùng cho mục đích tổng quát (trong chế độ 32-bit chỉ có tám thanh ghi dùng cho mục đích tổng quát)<br>
. Tám thanh ghi dùng cho dấu phẩy động 80-bit<br>
. Một thanh ghi cờ trạng thái 64-bit có tên là RFLAGS (chỉ sử dụng 32 bit thấp hơn)<br>
. Một con trỏ lệnh 64-bit có tên là RIP<br>
. Tám thanh ghi MMX 64-bit<br>
. Mười sáu thanh ghi XMM 128-bit (trong chế độ 32-bit, chỉ có tám thanh ghi như vậy)<br>

*. General-Purpose Registers <thanh ghi use cho aim tổng quát><br>
- kích thc toán hạng mặc định à 32 bit và có 8 thanh ghi đa năng
- thêm tiền tố REX (mở rộng thanh ghi) vào mỗi chỉ thị, các toán hạng can dài 64 bit và 16 thanh ghi đa năng 
- có all thanh ghi giống như ở chế độ 32 bit + 8 thanhh ghi đánh số từ R8 đến R15
  
 ![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/ad65ad24-4523-42ab-9734-8448568d633e)<br>
  
- một số chi tiết cần lưu ý:<br>
. 1 chỉ thị đơn ko thể truy cập cùng lúc 1 thanh ghi byte cao như AH, BH, CH, DH và đông thời truy cập byte thấp of 1 trong các thanh ghi byte ms (như DIL)<br>
. thanh ghi EFLAGS 32 bit đc thay bởi thanh ghi RFLAGS 64 bit ở chế độ 64 bit, chúng share 32 bit thấp như nhau và 32 bit cao of RFLAGS ko đc xài<br>
. Các cờ trạng thái là giống nhau ở cả chế độ 32 bit và 64 bit.<br>
  

