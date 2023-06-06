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
- độ dài chuỗi là bọi của 8
*. Binary Addition: 
- cộng bthg: 1 + 1 = 11
*. Integer Storage Sizes:
- đơ
