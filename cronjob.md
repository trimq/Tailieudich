# Làm sao để thêm Cron jobs trong Linux

# Mục lục:
- [1. Giới thiệu](#1)
- [2. Câu lệnh crontab](#2)
- [3. Các loại file cấu hình cron](#3)
- [4. Làm sao để sử dụng phép tính](#4)
- [5. Sử dụng strings đặc biệt để tiết kiệm thời gian](#5)
- [6. Thông tin thêm về thư mục /etc/crontab và /etc/cron.d/*](#6)
- [7. Backup cronjob](#7)
- [8. Tài liệu tham khảo](#8)

=========================================================

<a name="1"></a>
## 1. Giới thiệu
- Cron job được sử dụng là lệnh về lịch trình để thực hiện theo định kỳ. Có thể chỉnh sửa lệnh và script lặp lại trong khoảng thời gian đã được đặt trước.

- Cron là 1 công cụ hữu ích trong Linux, dịch vụ cron chạy nền và liên tục kiểm tra thư mục /etc/crontab file và /etc/cron.*/. Nó cũng check thư mục /var/spool/cron/

<a name="2"></a>
## 2. Câu lệnh crontab
- Crontab là câu lệnh dùng để cài đặt, hủy cài đặt hoặc liệt kê các bảng (file cấu hình cron) 

- Mỗi người sử dụng có thể có file crontab của riêng mình. Cần phải sử dụng lệnh crontab để chỉnh sửa hoặc thiết lập cronjob của riêng mình

<a name="3"></a>
## 3. Các loại file cấu hình cron
- <b>Crontab hệ thống Linux/Unix</b>: Thường được sử dụng bởi dịch vụ hệ thống và công việc quan trọng đòi hỏi phải có quyền root

- <b>Crontab người dùng</b>: Người dùng có thể cài đặt công việc của mình bằng cách sử dụng crontab command. Trường thứ 6 là câu lệnh để chạy và tất cả các lệnh chạy như người dùng tạo crontab

#### Để chỉnh sửa file crontab thực hiện câu lênh như sau:

```sh
crontab -e
```

- Cú pháp của crontab (mô tả các trường)

```sh
1 2 3 4 5 /path/to/command arg1 arg2
OR
1 2 3 4 5 /root/ntp_sync.sh
```

Trong đó:
<ul>
<li>1: Phút (0-59)</li>
<li>2: Giờ (0-23)</li>
<li>3: Ngày (0-31)</li>
<li>4: Tháng (0-12 [12 == December])</li>
<li>5: Ngày trong tuần(0-7 [7 hoặc 0 == chủ nhật])</li>
<li>/path/to/command – Script or command name to schedule</li>
</ul>

```sh
* * * * * command to be executed
– – – – –
| | | | |
| | | | —– Day of week (0 – 7) (Sunday=0 or 7)
| | | ——- Month (1 – 12)
| | ——— Day of month (1 – 31)
| ———– Hour (0 – 23)
————- Minute (0 – 59)
```

Ví dụ:

```sh
## run backupscript 5 minutes 1 time ##
*/5 * * * * /root/backupscript.sh

## Run backupscript daily on 1:00 am ##

0 1 * * * /root/backupscript.sh

## Run backup script monthly on the 1st of month 3:15 am ##

15 3 1 * * /root/backupscript.sh
```

<a name="4"></a>
## 4. Làm sao để sử dụng phép tính
- Dấu hoa thị (*): Nhà điều hành có thể quy định tất cả giá trị có thể có trong 1 trường. Ví dụ 1 dấu hoa thị trong trường giờ sẽ tương đương với mỗi giờ hoặc dấu hoa thị trong trường tháng sẽ tương đương với mỗi tháng

- Dấu phẩy (,): Dấu này chỉ ra 1 danh sách các giá trị. Ví dụ: “1,5,10,15,20, 25”.

- Dấu gạch ngang (-): Dấu này xác định 1 loạt các giá trị. Ví dụ "5-15" days ==> tương đương với "5,6,7,8...,15"

- Dấu ngăn cách (/): Xác định 1 bước giá trị. Ví dụ "0-23/" có thể sử dụng trong các trường giờ để xác định lệnh thực hiện trong các trường giờ khác nhau. Bước này cũng được cho phép sau dấu (*). Ví dụ ban muốn nói mỗi 2 giờ chỉ cần sử dụng "*/2"


<a name="5"></a>
## 5. Sử dụng strings đặc biệt để tiết kiệm thời gian
Sử dụng các chuỗi đặc biệt sau để tiết kiệm thời gian

| Special string | Ý nghĩa |
|----------------|---------|
| @reboot | Khởi động 1 lần lúc bắt đầu |
| @yearly | Khởi động 1 lần 1 năm, “0 0 1 1 *” |
| @annually	| tương đương với @yearly |
| @monthly | Khởi động 1 lần 1 tháng, “0 0 1 * *” |
| @weekly | Khởi động 1 lần 1 tuần, “0 0 * * 0” |
| @daily | Khởi động 1 lần 1 ngày, “0 0 * * *” |
| @midnight | Tương tự @daily |
| @hourly | Khởi động 1 lần 1 giờ, “0 * * * *” |

Ví dụ: 
```sh
#### Run ntpdate command every hour ####

@hourly /path/to/ntpdate
```

<a name="6"></a>
## 6. Thông tin thêm về file /etc/crontab và /etc/cron.d/*
- /etc/crontab là 1 hệ thống crontab file. Thường chỉ được sử dụng bởi người dùng root hoặc daemons để cấu hình hệ thống. Tất cả người dùng cá nhân phải sử dụng lệnh crontab để cài đặt và chỉnh sửa công việc được mô tả ở trên. /var/spool/cron/ hoặc /var/cron/tabs/ là thư mục cho người dùng sử dụng file crontab. Nó cần được backup với thư mục home

- Thư mục crontab điển hình:

```sh
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/
# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```


<a name="7"></a>
## 7. Backup cronjob

```sh
# crontab -l > /path/to/file

# crontab -u user -l > /path/to/file

```


<a name="8"></a>
## 8. Tài liệu tham khảo
- https://www.unixmen.com/add-cron-jobs-linux-unix/




