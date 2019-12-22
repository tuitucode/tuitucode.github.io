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
> **TL:** Mã hóa bằng giản đồ URL Endcoding.
- COOKIE và SESSION tại sao phải dùng cả 2?
> **TL:** Session lưu trên Server, để Server biết Session của Client nào thì cũng đồng thời tạo Cookie tương ứng với Session đó -> Lưu toàn bộ trên Session dẫn đến nặng.
- Đặc tính OOP
> 4 Đặc tính: Kế thừa, đa hình, trừu tượng, đóng gói
- PHP có đa kế thừa không? 
> **TL:** Không, dùng Traits và Interface
- GIT/GITHUB là gì?
- INTERFACE và ABSTRACT khác/ giống ra sao?
> Đã ghi
- Mô hình MVC
- Ajax là gì?
- Object, Class và Instance khác nhau như thế nào?
- Có mấy loại Join bảng?
- Mô tả quá trình từ khi nhập URL vào thanh trình duyệt đến load trang web hoàn chỉnh.
- Giải thuật: Sort và Search
- Khác nhau giữa DECLARE và DEFINE?
- Phân biệt static::method() với self::method()
> **TL:** `static` gọi phương thức tĩnh ở lớp hiện tại trong khi `selt` gọi phương thức ở lớp cha (nếu có và cho dù lớp con cũng có)
- Magic Method? 
> **TL:** [Magic Methods](https://dzone.com/articles/9-magic-methods-php-0), Chủ yếu là constructor, destructor và get/set...
- Trait trong PHP
> **TL:** [Trait](https://viblo.asia/p/lap-trinh-huong-doi-tuong-voi-php-va-nhung-dieu-can-biet-phan-2-Eb85oXq0K2G), có thể có thuộc tính lẫn phương thức
- RESTful API
> RESTful API là một tiêu chuẩn dùng trong việc thết kế các thiết kế API cho các ứng dụng web để quản lý các resource. RESTful là một trong những kiểu thiết kế API được sử dụng phổ biến nhất ngày nay.
- Transaction và Trigger trong SQL
### Các Design Pattern
- Singleton Pattern
- MVC Pattern
