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
                          <textarea class="form-control input-lg p-text-area" name="text" id="dataIn" rows="2" placeholder='Bạn muốn nói gì?' maxlength="200"></textarea>                        
                  </div>
                  <div class="card-footer">
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
                        </div>
                    </div>                
          </div>
      </div> 

</div>

<footer class="container-fluid text-center noidung">
  <p>Web Confession</p>
</footer>
</body>
</html>
```
Chúng ta cũng tạo thêm 1 file **custom.css** trong thư mục **public/css** để tùy chỉnh css cho trang home:
```css
.noidung {
    margin-top: 20px;
}

.pull-right {
    float: right!important;
}

.noidungpost {
    border: 1px solid #ced4da;
    border-radius: .25rem;
    padding: 5px;
}
```
Mình đã link custom.css trên vào sẵn trong home.ejs, nếu bạn muốn đổi tên file css thì vào home.ejs đổi luôn nhé!

Ngoài ra mọi file ở thư mục **public** khi bạn muốn link vào (như js, css) thì phải thay public thành assets trong đường dẫn (như trong home.ejs).

Đổi phần trả về khi get vào "/" ở file app.js như sau:

		res.render("home");
        
OK chạy lại server bạn sẽ thấy được giao diện confession mà mình đã tạo và render thông qua ejs.
- HÌNH ẢNH

### Kết nối đến MongoDB Atlas với mongoose
#### Thiết lập ở MongoDB Atlas
Tiếp theo chúng ta sẽ kết nối đến database, ở đây mình dùng MongoDB trên Atlas. Đầu tiên các bạn hãy tạo 1 tài khoản trên [MongoDB Atlas](https://www.mongodb.com/)

- HÌNH ẢNH

Sau khi có tài khoản, đăng nhập vào và tiến hành tạo database: **ATLAS** -> **Clusters** -> **Collections** -> **Create Database**.

- Database name (tên database): confession
- Collection name (giống như đặt tên bảng ở SQL): confess

- HÌNH ẢNH

Khác với SQL, NoSQL không buộc chúng ta phải cho biết trước các thuộc tính trong collection (như table của SQL).

Tiếp đến chúng ta sẽ cần chuỗi kết nối để web tiến hành truy cập đến, chuỗi kết nối có dạng

		mongodb+srv://<username>:<password>@cluster0-hquon.mongodb.net/
        
Để có được user và password, bạn vào phần **SECURITY** -> **Database Access** sau đó nhập username và password bạn muốn tạo vào, phần User Privileges các bạn chọn cái đầu hoặc thứ 2 cũng được. Vì thông tin này quan trọng và cần ghi nhớ, mình sẽ tạo file **config.json** (trong config) để lưu trữ nó lại dưới dạng như sau:
```javascript
{
    "username": <username>,
    "password": <password>
}
```
OK sau khi có file json, chúng ta tạo tiếp function để trả về chuỗi kết nối - **db.js**
```javascript
var configValues = require("./config");

module.exports = {
    AccessDatabase: function () {

        return `mongodb+srv://${configValues.username}:${configValues.password}@cluster0-hquon.mongodb.net/`;
    }
}
```
Tiếp theo là phần code trong web.
#### Thiết lập thao tác database từ web
Tạo file indexModel.js trong **api** -> **model** để config model cho database như sau:
```javascript
var mongoose = require("mongoose");

var Schema = mongoose.Schema;

var indexSchema = new Schema( {
    noidung : String,
    stt: Number,
})

var Confess = mongoose.model("iconfession", indexSchema, "confess");

module.exports = Partner;
```
Chúng ta định nghĩa 1 hàng dữ liệu được lưu với các trường `stt`, `noidung`. Nếu bạn nghĩ "làm thế nào để đặt stt làm khóa chính khi viết như vậy?" thì câu trả lời là 2 trường mình tạo đều không để làm khóa chính, khóa chính mặc định sẽ được tạo ra ở trường `_id`. Vậy tạo sao không lấy nó làm số thứ tự luôn? Vì trường `_id` tạo ra 1 dãy  kí tự rất "lộn xộn" chứ không phải bắt đầu từ số 0 và hiện tại mình cũng chưa tìm ra cách convert nó sang kiểu dễ nhìn nên mình tạo trường `stt`. Tiếp tục nào!

Tạo file indexController.js trong **api** -> **controller** để tạo các function tương tác (RESTful API):
```javascript
var confess = require("../model/indexModel");

function getListConfess(res) {
    confess.find().sort('-stt').find(function (err, ret) {
        if (err) {
            res.status(500).json(err);
        }
        else {
            res.json(ret);
        }
    })
}

module.exports = function (app) {
    //định nghĩa RESTful API

    //get list Confession
    app.get("/api/confessions", function (req, res) {
        getListPartner(res);
    });

    //Create Confession
    app.post("/api/confession", function (req, res) {

        var post = {
            noidung: req.body.noidung,
            stt: 0,
        };

        confess
        .estimatedDocumentCount()
        .then(count => {
            post.stt = count + 1;
            confess.create(post, function (err, ret) {
                if (err) {
                    throw err;
                }
                else {
                    getListConfess(res);
                }
            })
        })
        .catch(err => {
    //handle possible errors
        });
    });
}
```
Các bạn chú ý đoạn code mình dùng estimatedDocumentCount(), đây là function trả về số lượng dòng dữ liệu có trong collection. Mình sử dụng promise để hứng giá trị trả về (lưu trong biến count) sau đó +1 để tạo ra stt tiếp theo cho confess. Bạn có thể tìm hiểu thêm về estimatedDocumentCount và promise trên google.
### AngularJS
Back-end đã xong! Giờ chúng ta sẽ code phần front-end với AngularJS, đầu tiên tạo app.js trong public -> main như sau
```javascript
var app = angular.module("app.confess", ["xeditable", "ngSanitize"]);

app.controller("indexController", ['$scope', 'servConfess', function ($scope, servConfess) {

    $scope.appName = "iConfession";
    $scope.ConfessionList = [];

    //load data from API
    servConfess.getConfess().success(function (data) {
      
        // hiện cách dấu xuống dòng chính xác khi binding
        data.forEach(function(obj) {
            obj.noidung = obj.noidung.replace(/[\n\r]/g, '<br>');
        });

        $scope.ConfessionList = data;
    })

    $scope.formData = {};

    $scope.createConfess = function () {
        var confess = {
            noidung : $scope.formData.noidung,
        }

        servConfess.createConfess(confess).success(function (data) {
            $scope.ConfessionList = data;
            $scope.formData.noidung = "";
        })

    }
}]);
```
Tiếp theo là tạo service đặt tên là servConfess.js trong pulic -> main ->services với nội dung
```javascript
var app = angular.module("app.confess");

app.factory("servConfess",["$http",function($http) {
    return {
        getConfess : function() {
            return $http.get("/api/confessions");
        },
        createConfess : function(data) {
            return $http.post("/api/confession",data);
        }
    }
}])
```
Cuối cùng chúng ta chỉnh sửa lại file home.ejs như sau
```html
<!DOCTYPE html>
<html lang="en" ng-app="app.confess">
<head>
  <title>Home</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  <link href="/assets/css/custom.css" rel="stylesheet" type="text/css">
  <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
  <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/angular-xeditable/0.9.0/js/xeditable.min.js"></script>
  <script src="https://code.angularjs.org/1.0.3/angular-sanitize.js"></script>
  <script src="/assets/main/app.js"></script>
  <script src="/assets/main/services/servFinder.js"></script>

  <style>    
    /* Set black background color, white text and some padding */
    footer {
      background-color: #555;
      color: white;
      padding: 15px;
    }
  </style>
</head>
<body ng-controller="indexController">

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">{{ appName }}</a>
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
                          <textarea class="form-control input-lg p-text-area" name="text" id="dataIn" rows="2" placeholder='Bạn có ý tưởng gì?' maxlength="200" ng-model="formData.noidung"></textarea>                        
                  </div>
                  <div class="card-footer">
                    <button class="btn btn-primary pull-right" ng-disabled="!formData.noidung" ng-click="createConfess()">Gửi</button>
                  </div>
              </div> 
                    <div class="card noidung" ng-repeat="find in confessionList">
                        <div class="card-header">
                          #{{find.stt}}
                        </div>
                        <div class="card-body">
                          <span ng-bind-html="find.noidung"></span>
                        </div>
                        <div class="card-footer">
                        </div>
                    </div>                
          </div>
      </div> 

</div>

<footer class="container-fluid text-center noidung">
  <p>Web Confession</p>
</footer>

</body>
</html>
```
Xong rồi ~! Các bạn refresh lại trang web và thưởng thức thành quả nhé