---
published: true
layout: post
author: ker
categories: tutorial
tags:
  - NodeJS
  - Angular
  - MongoDB
image: assets/images/11.jpg
description: Xây dựng web app confession với NodeJS và AngularJS
featured: true
title: Xây dựng web confession với NodeJS và AngularJS
---
Trong series này chúng ta sẽ viết 1 trang web hoạt động như confession sử dụng back-end là NodeJS và front-end là AngularJS, nào cùng bắt đầu thôi!
## Chuẩn bị kiến thức
Đây là 1 bài viết code project thực tế nên mình không giải thích nhiều đến các kiến thức chuyên về NodeJS hay AngularJS nên trước khi xem bài này bạn nên có kiến thức cơ bản về 2 công nghệ trên, cụ thể:
- Kiến thức nền cơ bản về NodeJS, AngularJS.
- Cài đặt NodeJS trên máy.
- Tìm hiểu về mongoDB - package mongoose (chúng ta sẽ dùng sever databse trên mongo atlas).

Các kiến thức có thể tìm trên google, nếu bạn tự tin với khả năng vừa đọc vừa hiểu (hoặc tìm hiểu) thì vẫn tiếp tục được nhé.
### Website confession là gì?
website confession hoạt động như các trang confession trên facebook: cho người dùng nhập vào nội dung confession ở chế độ ẩn danh và đăng lên trên web cho người khác xem. Vậy sơ qua chúng ta sẽ tạo 1 nơi cho người dùng nhập nội dung và sau đó lưu trữ nó ở databse, khi muốn xem tất cả confession thì get dữ liệu từ database ra thôi.
### Tạo thư mục project
Để tạo project mới: `npm init`

Cấu trúc thư mục project như sau:
- HÌNH ẢNH

Chúng ta sẽ cài đặt 1 số package cần thiết: `express`, `ejs`, `morgan`, `body-parser`, `mongoose`.
## Code back-end với NodeJS
Đầu tiên chúng ta code ở file `app.js`, config 1 số thứ cơ bản và start server:
```javascript
var express = require("express");
var bodyparser = require("body-parser");
var morgan = require("morgan"); //log các request đến thay vì dùng middleware
var app = express();
var port = process.env.PORT || 3000; //set PORT

app.use("/assets", express.static(__dirname + "/public"));
app.use(bodyparser.json());
app.use(bodyparser.urlencoded({extended:true}));
app.use(morgan("dev"));

app.set("view engine", "ejs");

app.get("/", function(req, res) {
  	res.send("Hello NodeJS!");
});

app.listen(port, function() {
    console.log("App listening on port" + port);
});
```
Các bạn hãy truy cập vào `localhost:3000` nếu không có lỗi xảy ra các bạn sẽ thấy dòng "Hello NodeJS!", tiếp tục nào!

Tiếp theo chúng ta sẽ tạo 1 view để trả về trang web cho user, chúng ta sẽ dùng `ejs`, tạo 1 file **home.ejs** trong mục **view** như sau:
```javascript

```
