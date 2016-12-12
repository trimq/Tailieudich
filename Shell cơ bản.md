# Làm quen với Linux Shell Script

# Mục lục:
- [1. Unix shell là gì?](#1)
- [2. Các loại Shell](#2)
	- [2.1 Bourne shell](#21)
	- [2.2 C Shell](#22)
	- [2.3 Fish](#24)
	- [2.4 Bourne-Again Shell](#24)
- [3. Shell script là gì](#3)
- [4. Làm sao để viết shell script](#4)
- [5. Điều kiện trước tiên](#5)
- [6. Viết shell script đầu tiên của bạn](#6)
- [7. Tài liệu tham khảo](#7)

=================================

Bài viết này cho những người chưa có 1 cái nhìn cụ thể và chưa biết rõ về shell script. Đến cuối series này, bạn có thể sẽ viết được shell script cho tất cả những trường hợp có thể. Trong hướng dẫn này bạn sẽ biết shell script là gì, viết và thực thi shell script đầu tiên của mình

<a name="1"></a>
## 1. Unix shell là gì?
- Unix shell thường được gọi là Shell là 1 dòng lệnh diễn dịch được sinh ra trong hệ điều hành Unix/Linux

- Người dùng tương tác trực tiếp với shell bằng 1 hay 1 loạt các dòng lệnh

- Tất cả các shell hiện nay đều hỗ trợ sẵn các kí hiệu, pipes, các biến, phép lặp, điều kiện hoạt động, câu lệnh thay thế với tài liệu thích hợp

- Một ngôn ngữ shell cơ bản có thể hiểu như giao diện kết nối người dùng tới hệ điều hành

<a name="2"></a>
## 2. Các loại Shell
Có nhiều các loại shell khác nhau, Bourne shell và C shell là 2 loại được sử dụng rộng rãi, Infact Bourne Shell được sử dụng như mã hóa với một số tính năng thêm vào

<a name="21"></a>
### 2.1 Bourne shell
sh hay còn gọi là đường dẫn chuẩn của Bourne trong hệ thống Linux là /bin/sh. Được viết bởi Stephen Bourne. Nó rất nổi tiếng với rất nhiều bản phân phối sh thông dụng/ đường dẫn cứng cho các loại shell khác

<a name="22"></a>
### 2.2  C Shell
csh hay còn gọi là C shell được viết bởi Billy Joy. C shell được phân phối rộng rãi bởi BSD Unix. Được giới thiệu với nhiều tính năng để thực hiện nhiệm vụ tương tác với aliases, lịch sự, điều khiển. Được viết hoàn toàn bởi C, phiên bản ổn định là 6.19

<a name="23"></a>
### 2.3 Fish
Nó thay đổi các người dùng tương tác với Shell linux với các tính năng như Universal Variables (biến Universal), Helpful Error Messages (thông báo lỗi), Tab Completion (tab hoàn thành), Syntax highlighting (highlighting cú pháp), Smart terminal and clipboard handling, tìm kiếm lịch sự command. Phien bản ổn định là 2.2.0

<a name="24"></a>
### 2.4 Bourne-Again Shell
Đây là Shell mặc định trên hầu hết những bản phân phối Linux hiện nay (và MAC OS). Nó được viết như 1 phần dự án GNU. Được viết hầu hết bằng ngôn ngữ C. Phiên bản ổn định là 4.3.42

#### Các loại shell khác:
- Debian Almquist shell aka dash
- Korn Shell aka ksh
- Z shell aka zh
- Busybox, etc


<a name="3"></a>
## 3. Shell script là gì?
- Shell script là 1 chương trình được thiết kế để diễn dịch Linux shell. Một shell script có thể sử dụng cho một loạt các nhiệm vụ như thực hiện các chương trình, thao tác với file, thiết lập môi trường...

- Với người quản trị Linux thì shell script có thể được sử dụng để tự động hóa việc lặp đi lặp lại hàng ngày các nhiệm vụ như backup, khôi phục file. 

- Shell script cho phép người dùng có thể cho phép nhiều lệnh tự động thực hiện thay vì phải nhập từng lệnh một bằng tay. Tùy vào yêu cầu mà bạn có thể sử dụng output của 1 command như là input của các command khác. Tất cả được xác định trong 1 shell script

==> Shell script rất quan trọng cho quản trị viên nhằm tiết kiệm thời gian và tài nguyên

<a name="4"></a>
## 4. Làm sao để viết shell script
- Bạn có thể sử dụng gedit, vi/vim, Emacs để viết shell script. Không nên sử dụng IDE

- Để thực hiện đơn giản, sử dụng gedit (được cài đặt mặc định trên các bản phân phối linux hiện nay), nó rất quan trọng để bắt đầu các dòng code dưới đây

```sh
#!/bin/bash
```

- Kí tự "#!" được gọi là công việc thực hiện

- Phần sau là /bin/bash chỉ dẫn để chạy chương trình bin/bash. Có thể thay thế /bin/bash với shell path của bạn. 

- Có thể viết command ở sau kí tự "#", shell sẽ bỏ qua mọi thứ sau "#"

- Lưu shell với đuôi".sh"

- Một shell cần phân quyền để chạy, thường sử dụng chmod 755

```sh
$ chmod 755 YOUR_SCRIPT.sh
```

<a name"5"></a>
## 5 .Điều kiện trước tiên
- Cần có 1 linux box, hoặc cài hệ điều hành Linux hoặc sử dụng môi trường ảo hóa trên Window

- Tất cả các script/command phải thực hiện trên các bản phân phối của Linux do vậy không nên có sự tranh chấp tại đây, chọn bản phân phối phù hợp với bạn nhất

- Có kiến thức cơ bản về hệ điều hành Linux và các câu lệnh

- Không bao giờ được sử dụng IDE. Thay vào đó sử dụng vi/vim hoặc gedit

- Thực hiện theo tất cả các phần của văn bản và không thoát khỏi bất kỳ

<a name="6"></a>
## 6. Viết shell script đầu tiên của bạn
Mở gedit và viết những dòng code dưới đây (không copy-paste)

```sh
#!/bin/bash
echo "Hello Unixmen Community!"
```

- echo là 1 câu lệnh Linux được sử dụng để in ra dòng "Hello Unixmen Community!" trên đầu ra tiêu chuẩn

- Sau khi thực hiện xong, lưu lại ví dự như `my_first_program.sh`. Để nó được thực thi phải làm như sau

```sh
$ chmod 755 my_first_program.sh
```

- Để chạy được ta sử dụng như sau

```sh
$ ./my_first_program.sh
```

#### Viết chương trình shell thứ 2.

```sh
#!/bin/bash
echo "Hey there! What is your name?"
read a;
echo "Hey $a! what is your Favorite Linux Community?"
read b; echo -e "That's Nice to know @$a that $b is your favorite Linux 
Community.\n How many years of experience you have in Linux?" read c; echo 
"That's great. Keep Connected to Unixmen $a. The fun has just started."
```

-  echo “Hey there! What is your name?” là in dòng in ra. Input của “What is your name?” được lưu trong biến a. Lệnh đọc sẽ đọc từ mô tả của file 

- echo “Hey $a! what is your Favorite Linux Community?” là dòng in ra. Input của “what is your Favorite Linux Community?” được lưu trong biến b. Tương tự với `echo` hay `read` khác trong script

<a name="7"></a>
## 7. Tài liệu tham khảo:
https://www.unixmen.com/starting-with-linux-shell-scripting/


 






