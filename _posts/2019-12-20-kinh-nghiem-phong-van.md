---
published: true
layout: post
author: ker
categories: tutorial
tags:
  - note
  - interview
image: assets/images/fcm.jpg
description: Tổng hợp kinh nghiệp phỏng vấn
title: Kinh nghiệm phỏng vấn
---
Kinh nghiệm phỏng vấn
### PHP
- Constructor có modifier là? 
> **TL:** Public
- POST và GET khác nhau? Dữ liệu gửi lên có mã khóa không?
> Mã hóa bằng giản đồ URL Endcoding.
[Chi tiết So sánh](https://viblo.asia/p/phuong-thuc-get-va-post-aWj53VBYl6m)
- COOKIE và SESSION tại sao phải dùng cả 2?
> Session lưu trên Server, để Server biết Session của Client nào thì cũng đồng thời tạo Cookie tương ứng với Session đó -> Lưu toàn bộ trên Session dẫn đến nặng.
- Đặc tính OOP
> 4 Đặc tính: Kế thừa, đa hình, trừu tượng, đóng gói
- PHP có đa kế thừa không? 
> Không, dùng Traits và Interface
- GIT/GITHUB là gì?
> GIT là hệ thống quản lý phiên bản phân tán, hỗ trợ quản lý code và lịch sử thay đổi
GITHUB là dịch vụ lưu trữ trên web dành cho các dự án có sử dụng hệ thống kei6m3 soát Git revision
- INTERFACE và ABSTRACT khác/ giống ra sao?
> Đã ghi
- Mô hình MVC
> Đã ghi
- Ajax là gì?
> AJAX là chữ viết tắt của Asynchronous JavaScript and XML. Nó là một bộ các kỹ thuật thiết kế web giúp cho các ứng dụng web hoạt động bất đồng bộ – xử lý mọi yêu cầu tới server từ phía sau. 
- Object, Class và Instance khác nhau như thế nào?
> Một bản thiết kế chi tiết cho ngôi nhà giống như là mô tả một class. Tất cả những ngôi nhà được xây dựng dựa trên bản thiết kế đó là những object của class. Một ngôi nhà cụ thể là một instance.
- Có mấy loại Join bảng?
> INNER: Phép giao = lấy phần chung,
OUTER: LEFT: lấy phần trái và phần hơp bên phải, RIGHT ngược lại
FULL OUTER: lấy hết
- Mô tả quá trình từ khi nhập URL vào thanh trình duyệt đến load trang web hoàn chỉnh.
> Đã ghi
- Giải thuật: Sort và Search
> Đã ghi
- Khác nhau giữa DECLARE và DEFINE?
> Đã ghi
- Phân biệt static::method() với self::method()
> `static` gọi phương thức tĩnh ở lớp hiện tại trong khi `selt` gọi phương thức ở lớp cha (nếu có và cho dù lớp con cũng có)
- Magic Method? 
> [Magic Methods](https://dzone.com/articles/9-magic-methods-php-0), Chủ yếu là constructor, destructor và get/set...
- Trait trong PHP
> [Trait](https://viblo.asia/p/lap-trinh-huong-doi-tuong-voi-php-va-nhung-dieu-can-biet-phan-2-Eb85oXq0K2G), có thể có thuộc tính lẫn phương thức
- RESTful API
> RESTful API là một tiêu chuẩn dùng trong việc thết kế các thiết kế API cho các ứng dụng web để quản lý các resource. RESTful là một trong những kiểu thiết kế API được sử dụng phổ biến nhất ngày nay.
- Transaction và Trigger trong SQL
> Trans: [Trans](https://viblo.asia/p/cac-lenh-xu-ly-transaction-trong-sql-Do754kaelM6)
, Trigger: Hiểu đơn giản thì Trigger là một stored procedure không có tham số. Trigger thực thi một cách tự động khi một trong ba câu lệnh Insert, Update, Delete làm thay đổi dữ liệu trên bảng có chứa trigger. 

### Các Design Pattern
- Singleton Pattern
- MVC Pattern
