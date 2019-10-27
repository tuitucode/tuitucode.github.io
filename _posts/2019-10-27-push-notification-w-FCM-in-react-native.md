---
published: true
layout: post
author: ker
categories: tutorial
tags:
  - FCM
  - react-native
  - push-notification
image: assets/images/11.jpg
description: >-
  Hướng dẫn push notification trên android bằng FCM (Firebase Cloud Messaging)
  với React Native
featured: false
title: Push notification với Firebase Cloud Messaging trong React Native
---
Hi~! Nhân lúc làm app với React Native và Firebase nên trong bài viết này mình sẽ hướng dẫn các bạn cách đẩy thông báo (push notification) sử dụng FCM (Firebase Cloud Messaging) đồng thời cũng giải đáp một số thắc mắc mà mình mắc phải (và mình nghĩ đa số ai cũng sẽ gặp) khi code, nào bắt đầu thôi!
### Push notification là gì?
Push Notification là một dạng tin nhắn đơn giản xuất hiện cùng với thông báo của hệ thống hoặc giống như tin nhắn bật lên -tuỳ thuộc vào nền tảng.
Định nghĩa khá đơn giản và bạn chắc cũng đã gặp rất nhiều khi sử dụng smartphone, dưới đây là hình ảnh về nó:
	- Ảnh

Tiếp theo chúng ta cùng tìm hiểu 1 chút về lịch sử ra đời của nó.
#### Lịch sử phát triển
- 6/2019: Apple ra mắt Apple Push Notification Service (APNs), dịch vụ push notification đầu tiên.
- 5/2010: Google phát hành dịch vụ riêng: Google Cloud to Device Messaging (C2DM).
- 5/2013: Google giới thiệu ‘rich notification’. Rich notification có thể chứa ảnh, các nút hành động – giúp người dùng thực hiện hành động ngay lập tức từ notification: phát nhạc, mở ứng dụng,…
9/2014: Apple thêm các nút tương tác. Các nút này cho phép người dung gửi phản hồi ngay lập tức cho nhà xuất bản ứng dụng, ngay sau đó ra mắt push notification trên Apple Watch.

Và phần quan trọng nhất: nó dùng để làm gì?
#### Lợi ích
Push Notification cung cấp sự tiện lợi và nhiều giá trị cho người dùng. Ví dụ người dùng có thể nhận được:
- Kết quả bóng đá và tin tức ngay trên màn hình khóa.
- Các thông báo từ ứng dụng khác (thông báo tin nhắn đến, bài viết mới,...).

Còn về phía nhà xuất bản ứng dụng:
- Cách để nói chuyện trực tiếp với người dùng.
- Không bị cho vào spam như mail, tăng tỉ lệ tương tác.
- Nhắc nhở người dùng sử dụng ứng dụng cho dù ứng dụng có được mở hoặc không.
- Quảng cáo, thông báo cho người dùng.

Đến đây chắc các bạn cũng nắm được push notification là gì rồi đúng không? Vậy tiếp theo chúng ta sẽ dùng FCM để push notification trên Android và iOS, còn vì sao lại dùng FCM? Đương nhiên bạn có nhiều lựa chọn khác như OneSignal nhưng hiện tại mình đang làm app theo phong cách rất 'firebase' nên mình chơi luôn của nó :) Cho bạn này chưa biết về Firebase thì tiếp theo là vài phút quảng cáo...
### Firebase là gì?
Firebase là một dịch vụ hệ thống backend được Google cung cấp sẵn cho ứng dụng Mobile của bạn, với Firebase bạn có thể rút ngắn thời gian phát triển, triển khai và thời gian mở rộng quy mô của ứng dụng mobile mình đang phát triển. Hỗ trợ cả 2 nền tảng Android và IOS, Firebase mạnh mẽ, đa năng, bảo mật và là dịch vụ cần thiết đầu tiên để xây dưng ứng dụng với hàng triệu người sử dụng. Link trang chủ: [Firebase](firebase.com "link đến firebase")

Hiện tại dịch vụ mà Firebase cung cấp rất nhiều nên bạn có thể tha hồ vọc vạch, với Firebase việc bạn cần làm chỉ là tập trung code cho tốt phía client thôi.
	- Ảnh

Với bài viết này chúng ta sẽ cùng vọc Cloud Messaging - nằm trong nhóm Grow, nó là...
### Firebase Cloud Messaging
Tóm gọn trong 3 dòng súc tích:
- Firebase Cloud Messaging(FCM) là phiên bản mới của Google Cloud Messaging(GCM). 
- Đây là một giải pháp nhắn tin đám mây đa nền tảng. 
- Bạn có thể sử dụng Firebase Cloud Messaging cho bất kỳ loại thiết bị người dùng cuối nào bao gồm iOS, Android hoặc thậm chí Web mà không mất phí.
#### Tính năng chính
FCM cung cấp cho chúng ta 3 tính năng chính như sau:
- Gửi tin nhắn thông báo (notification messages) hoặc tin nhắn dữ liệu (data messages).
- Mục tiêu gửi tin nhắn đa dạng: 1 thiết bị cụ thể, 1 nhóm các thiết bị hoặc thiết bị đăng kí theo chủ đề.
- Gửi tin nhắn từ app đến server.

Tổng quan về cách thức hoạt động:
	- Ảnh

Cụ thể hơn, chúng ta có 3 cách làm sau:
	- Ảnh 1
	- Ảnh 2
	- Ảnh 3
    
Phần lý thuyết đã xong, Giờ hãy bật Editor lên và code thôi!
### Coding
Tổng quan 1 chút: mình sẽ dùng React Native bản 0.6 để code app và FCM bản 20.0 để push notification.


