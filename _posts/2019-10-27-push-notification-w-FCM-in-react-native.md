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
- 5/2010: Google phát hành dịch vụ riêng: Google Cloud to Device Messaging (C2DM)
- 5/2013: Google giới thiệu ‘rich notification’. Rich notification có thể chứa ảnh, các nút hành động – giúp người dùng thực hiện hành động ngay lập tức từ notification: phát nhạc, mở ứng dụng,…
9/2014: Apple thêm các nút tương tác. Các nút này cho phép người dung gửi phản hồi ngay lập tức cho nhà xuất bản ứng dụng, ngay sau đó ra mắt push notification trên Apple Watch
