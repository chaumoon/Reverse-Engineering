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

II. 
