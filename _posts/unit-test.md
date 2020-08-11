---
# layout: post
title:  Unit test  
categories:  interview
---
Ứng dụng hoặc bất kì sản phẩm nào trước khi đến tay người dùng, đều phải trải qua 1 quá trình test cẩn thận. Khi nói về test nhiều người sẽ nghĩ người tester sẽ ngồi hàng giờ kiểm tra từng màn hình, từng nút bấm  để phát hiện ra điều bất thường và  báo lại cho nhà phát triển, trong bài viết này mình muốn chia sẻ một chủ đề mà thời gian vừa qua mình tìm hiểu  đó là testing, cụ thể trong bài này mình sẽ nói về unit test 

![](https://docs-assets.developer.apple.com/published/20b3426c34/93cc7b80-dd57-423d-be85-f937da693ec3.png)



## Unit testing là gì ? 
Unit test  là một trong những khái niệm căn bản nhẩt của test, là một automation test  chạy và xác thực từng dòng code, tổng thể là function truyền vào tham số và kiểm tra kết quả mong đợi 

## XCtesting 
Là một công cụ có khác năng viết test nhiều mức độ trừu tượng, là một giải pháp tốt để testing  kết hợp được nhiều kiểu test để tối đa hoá lơi ích từ mỗi loại 

## Lợi ích của Unit test 
Unittest hữu ích khi làm việc với codebase lớn, khi  dự án phải làm việc với nhiều dev khác tiết kiệm thời gian thay đổi chỉnh sửa chức năng mà không sợ ảnh hưởng  đến code của ông khác 
Hạn chế bug 
## Setup và Teardown
**Setup** là phương thức khởi tạo các phương thức test
**TearDown** là phương thức clean sau mỗi phương thức hoàn thành  thực thi theo cơ chế LIFO 

