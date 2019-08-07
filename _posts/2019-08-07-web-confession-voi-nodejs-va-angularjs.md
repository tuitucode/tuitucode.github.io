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
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Home</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  <link href="/assets/css/custom.css" rel="stylesheet" type="text/css">
  <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>

  <style>    
    /* Set black background color, white text and some padding */
    footer {
      background-color: #555;
      color: white;
      padding: 15px;
    }
  </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">iConfession</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
      
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a class="nav-link" href="#">Home<span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item dropdown">
              <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Dropdown
              </a>
              <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                <a class="dropdown-item" href="#">Action</a>
                <a class="dropdown-item" href="#">Another action</a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#">Something else here</a>
              </div>
            </li>
            <li class="nav-item">
              <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
            </li>
          </ul>
          <form class="form-inline my-2 my-lg-0">
            <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
          </form>
        </div>
      </nav>
  
<div class="container noidung">    
  <div class="row">
      <div class="col-md-6 offset-md-3">
          <div class="col-md-12">
              <div class="card">
                  <div class="card-body" style="padding: 0">
                          <textarea class="form-control input-lg p-text-area" name="text" id="dataIn" rows="2" placeholder='Bạn có ý tưởng gì?' maxlength="200"></textarea>                        
                  </div>
                  <div class="card-footer">
                    <span>Mail: </span><input class="noidungpost" type="text" placeholder="abc@mail.com"> 
                    <button class="btn btn-primary pull-right">Gửi</button>
                  </div>
              </div> 
                    <div class="card noidung">
                        <div class="card-header">
                          #1
                        </div>
                        <div class="card-body">
                          <span>confession đầu tiên</span>
                        </div>
                        <div class="card-footer">
                          <span>Mail liên hệ: test@mail.com</span>
                        </div>
                    </div>                
          </div>
      </div> 

</div>

<footer class="container-fluid text-center noidung">
  <p>Footer Text</p>
</footer>
</body>
</html>

```
