I. Basic Concepts
1. Welcome to Assembly Language
- www.asmirvine.com: có in4 bổ sung, hg dẫn và bài tập
2.  Virtual Machine Concept
- máy hiểu nn L0, ng viết bằng nn L1. có 2 cách để đạt đc điều này:<br>
  . Interpretation: mỗi chỉ thị của L1 -> L0 -> thực thi<br>
  . Translation: toàn bộ L1 -> L0 -> thực thi<br>
- Virtual Machines: là 1 chg trình p.mềm mô phỏng c.năng của 1 m.tính v.lý or<br>
m.tính ảo khác.
- Specific Machines: 

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/aa8e5e74-0bfc-48cd-890f-72287191f28a)<br>

. lv1: phần cứng logic số of máy tính<br>
. lv2: kiến trúc tập lệnh (ISA) là cấp độ đầu tiên mà user có thể viết chương trình.<br>
can g.là nn máy, lệnh thực thi bởi chg trình gắn trong vi xử lý là microprogram<br>
. lv3: nn assembly xuất hiện, dễ dịch sang ISA.<br>
các chg trình nn assembly đc dịch hoàn toàn thành nn máy trc khi thực thi<br>
. lv4: nn lập trình cao cấp như C, C++, Java, chứa các câu lệnh mạnh mẽ được dịch thành nhiều lệnh ngôn ngữ assembly.<br>
 Mã ngôn ngữ assembly được tự động tổng hợp thành ngôn ngữ máy bởi trình biên dịch.<br>
 3. Data Representation
 *. Binary Integers:
 - bit bên trái có trọng số cao nhất (MSB)
 - bit bên phải có trọng số thấp nhất (LSB)

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/057ea971-75b6-4ff8-9fa6-30dbe9cd7d1b)<br>

- số nguyên nhị phân can có hoặc ko có dấu. ko dấu mặc định là dương, số 0 là số dương
- độ dài chuỗi là bọi của 8<br>
*. Binary Addition: 
- cộng bthg: 1 + 1 = 11<br>
*. Integer Storage Sizes:
- đơn vị lưu trữ:<br>
. Byte: 8 bits<br>
. Word: 16 bits<br>
. Doubleword: 32 bits<br>
. Quadword: 64 bits<br>
. kilobyte: 2^10 byte<br>
. megabyte (1 MByte): 2^20 byte<br>
. gigabyte (1 GByte): 2^30 byte<br>
. terabyte (1 TByte): 2640 byte<br>
. petabyte: 2^50 byte<br>
. exabyte: 2^60 byte<br>
. zettabyte: 2^70 byte<br>
. yottabyte: 2^80 byte<br>
*. Hexadecimal Integers:<br>
- số nguyên lớn biểu diễn nhị phân -> khó đọc -> biểu diễn hex<br>
*. Hexadecimal Addition:<br>
- cộng bthg như trong kt.số<br>ư
*. Signed Binary Integers:<br>
- số nguyên âm biểu diễn bằng đảo bù 2, chỉ cần xài phép + vì - -> +
- Để tạo ra đảo bù hai của một số nguyên thập lục phân, đảo ngược tất cả các bit và cộng 1.<br>
đảo ngược các bit của một chữ số thập lục phân = cách trừ chữ số đó vs 15
- chuyển số nhị phân có dấu sang thập phân:<br>
. MSB = 1 -> lấy bù 2 r chuyển bthg<br>
. MSB = 0 -> chuyển bthg<br>
- chuyển số nguyên âm sang nhị/thập lục phân: 
. chuyển trị tuyệt đối của nó sang nhị/thập lục phân<br>
. lấy bù 2<br>
*. Binary Subtraction:<br>
- trừ bthg<br>
4. Boolean Expressions:<br>
- đại số bool: chỉ có true or false
- các toán tử:<br>
. NOT: được ký hiệu là ¬ hoặc ~ hoặc '<br>
. AND: được ký hiệu là ∧ hoặc •<br>
. OR: được ký hiệu là ∨ hoặc |<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/947dccea-0995-4c83-89fa-0c5e3974ce4b)<br>

- quy tắc ưu tiên:<br>

![image](https://github.com/chaumoon/Reverse-Engineering/assets/127403046/985ac4d0-f601-487c-b46e-9a8387e80244)<br>

*. Truth Tables for Boolean Functions <bảng chân trị> <br>
- viết như trong kts ấy<br>

