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
### Thông tin phiên bản
Ở bài hướng dẫn này, mình dùng:
- React Native bản 0.61
- React Navigation bản 4.x

### Coding
#### init - config
Đầu tiên, tạo app React Native, cmd lệnh quen thuộc:
> react-native init DemoCompexNavigation

Tiếp theo, cài `react-navigation`, cmd lệnh:
> npm i react-navigation --save

Cài `react-navigation-tabs` để dùng Bottom Navigator:
> npm i react-navigation-tabs --save

Cài thêm các package bổ sung:
> npm i react-native-gesture-handler react-native-reanimated react-native-vector-icons --save

Sau khi cài xong, check dependencies trong `package.json`
```
  "dependencies": {
    "react": "16.9.0",
    "react-native": "0.61.3",
    "react-navigation": "4.0.10"
    "react-navigation-tabs": "^2.5.6"
  }
```
_*Note: phiên bản có thể khác nhau tùy thuộc vào thời gian._

**Cấu trúc navigation:** với app trong bài này, hình dung cấu trúc navigation như sau
```
- BottomTab
	- Home Screen
	- List Screen
    	- Item Screen
    	- Drawer
```

Tạo thư mục `components` chứa các component Home, List, Item:
- Home.js

```javascript
import React, { Component } from 'react';
import { View, Text } from 'react-native';

export default class Home extends Component {
  constructor(props) {
    super(props);
    this.state = {
    };
  }

  render() {
    return (
      <View>
        <Text> Home Screen </Text>
      </View>
    );
  }
}
```

- List.js

```javascript
import React, { Component } from 'react';
import { View, Text, TouchableOpacity } from 'react-native';

export default class List extends Component {
  constructor(props) {
    super(props);
    this.state = {
    };
  }

  _navigate() {
      //code navigate to Item screen
  }

  render() {
    return (
      <View>
        <Text> List Screen </Text>
        <TouchableOpacity
        onPress={() => {
            this._navigate();
        }}>
            <Text>Navigate to Item screen</Text>
        </TouchableOpacity>
      </View>
    );
  }
}
```

- Item.js

```javascript
import React, { Component } from 'react';
import { View, Text } from 'react-native';

export default class Item extends Component {
  constructor(props) {
    super(props);
    this.state = {
    };
  }

  render() {
    return (
      <View>
        <Text> Item Screen with Drawer </Text>
      </View>
    );
  }
}
```

Và `index.js` để dễ truy xuất components:
```javascript
import Home from './Home';
import Item from './Item';
import List from './List';

export {
    Home,
    Item,
    List
}

```

OK, Giờ là phần code navigation, nhìn phần cấu trúc ở trên mình sẽ cho App container là BottomTabNavigator (để bottom tab bao bọc toàn bộ), mở `App.js` và code như sau:
```javascript
import React from 'react';
import { createAppContainer } from 'react-navigation';
import { createBottomTabNavigator } from 'react-navigation-tabs';
import { Home, List, Item } from './components';

const IndexNavigator = createBottomTabNavigator({
  'Home': Home,
  'List': List
}, {
  defaultNavigationOptions: ({ navigation }) => ({
    tabBarIcon: ({ focused, horizontal, tintColor }) => {
      const { routeName } = navigation.state;
      let iconName;
      if (routeName === "Home") {
        iconName = `md-home`;
      } else if (routeName === "List") {
        iconName = `md-list-box`;
      }
      return <Ionicons name={iconName} size={25} color={tintColor} />;
    }
  })
});

const App = createAppContainer(IndexNavigator);

export default App;
```

Kết quả run trên máy ảo:

Tiếp theo, ở màn hình **List Screen** khi ấn vào dòng chữ _Navigate to Item screen_ sẽ chuyển đến màn hình **Item Screen** và cũng ở màn hình này chúng ta có **Drawer**.

Trong hàm `_navigate` ở List.js, thêm đoạn code navigate đến Item Screen:
```javascript
  _navigate() {
      //code navigate to Item screen
      // Dùng props navigation 
      this.props.navigation.navigate('Item');
  }
```
