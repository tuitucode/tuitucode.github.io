---
published: true
layout: post
author: ker
categories: tutorial
tags:
  - Firebase
  - Flutter
image: null
description: Giải quyết các vấn đề nảy sinh trong khi code Flutter với Firebase
featured: false
title: Flutter Problem Guide
---
Hi~! Bài viết này hướng dẫn cách khắc phục các lỗi mình từ gặp khi trải nghiệm Flutter.
### Flutter x Firebase
Các vấn đề xảy ra khi sử dụng FlutterFire
#### #Problem 1
**Mô tả lỗi:** D8: Cannot fit requested classes in a single dex file...

**Cách fix:**

Trong `project/app/build.gradle` thêm:
```javascript
defaultConfig {
    ...

    multiDexEnabled true //<- Dòng này
}
...

dependencies {
    ...

    implementation 'com.android.support:multidex:1.0.3' //<- Dòng này
}
```

Nếu vẫn chưa khắc phục được, đảm bảo minSdkVersion trong android/app/build.gradle ở version 21 (mặc định là 16).


