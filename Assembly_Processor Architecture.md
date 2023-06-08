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
3. 
