---
published: true
layout: post
author: ker
categories: tutorial
tags:
  - react-navigation
  - react-native
  - complex navigation in react-native
image: assets/images/fcm.jpg
description: >-
  Bài viết này hướng dẫn các bạn tạo complex navigation với stacks, tabs
  (bottom) và Drawers trong app React Native
title: 'Kết hợp Stacks, Tabs và Drawers của React Navigation 4.x trong React Native'
---
Bonjour! Cùng đi tiếp với series về React Native, hôm nay chúng ta sẽ build 1 app kết hợp các loại navigator bao gồm: Stacks, Tabs và Drawers. App không có tính năng gì đặc biệt chủ yếu để các bạn hiểu cách sử dụng các loại navigator này với nhau thôi, nào let's go!
### Goal - Mục tiêu
Mục tiêu là hoàn thành 1 app như video dưới:

Để tìm hiểu thêm về React Navigation các bạn tham khảo tại ĐÂY
### Config - Thiết lập
Ở bài hướng dẫn này, mình dùng:
- React Native bản 0.61
- React Navigation bản 4.x

### Coding
Đầu tiên, tạo app React Native, cmd lệnh quen thuộc:
> react-native init DemoCompexNavigation

