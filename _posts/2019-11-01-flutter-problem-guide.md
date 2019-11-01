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
**Mô tả lỗi:** _D8: Cannot fit requested classes in a single dex file..._

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

#### #Problem 2
**Mô tả lỗi:** crash app khi dùng chức năng 'sign in with Google' và vài dòng log lỗi có dạng
 > Suppressed: java.lang.NoClassDefFoundError: com.google.android.gms.auth.api.signin.internal.SignInHubActivity
 ...
 
**Cách fix:**
- Đảm bảo minSdkVersion đang ở >= 21 (recommended 23)
- Trong `android/gradle.properties` thêm:
```
android.useAndroidX=true
android.enableJetifier=true
```
- Trong `android/build.gradle` đảm bảo 3 dòng sau:
```
dependencies {
    classpath 'com.android.tools.build:gradle:3.2.1'
    classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    classpath 'com.google.gms:google-services:4.2.0'
}
```
*Note: Ở thời điểm hiện tại phiên bản service 4.3.0 trở lên vẫn chưa ổn định, mặc định project được tạo thời điểm viết bài là 4.3.2

- Chạy 2 lệnh cmd lần lượt là `flutter clean` và `flutter pub upgrade`.

#### #Problem 3
**Mô tả lỗi:** _Android dependency 'androidx.core:core' has different version for the compile (1.0.0) and runtime (1.0.1) classpath. You should manually set the same version via DependencyResolution_

**Cách fix:**
Trong `android/build.gradle` thêm:
```
buildscript {
	...
    dependencies {
        classpath 'com.android.tools.build:gradle:3.2.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath 'com.google.gms:google-services:4.2.0'
    }
	
    //Thêm subprojects này
    subprojects {
        project.configurations.all {
            resolutionStrategy.eachDependency { details ->
                if (details.requested.group == 'androidx.core'
                        && !details.requested.name.contains('androidx') ) {
                    details.useVersion "1.0.1"
                }
            }
        }
    }
    ////////

}
```

#### #Problem 4
**Mô tả lỗi:** itemBuilder có thêm tham số index, lỗi có dạng:
> The argument type 'ChatMessage Function(BuildContext, DataSnapshot, Animation<double>)' can't be assigned to the parameter type 'Widget Function(BuildContext, DataSnapshot, Animation<double>, int)'
  
**Cách fix:** thêm tham số **index** vào anonymous function như sau
```
  itemBuilder: (_, DataSnapshot snapshot, Animation<double> animation, index) {
  }
```

#### Đang cập nhật
Nếu bạn gặp phải lỗi nào khác hoặc giải quyết được 1 lỗi gì khác thì comment bên dưới để giúp đỡ mọi người nhé :')
