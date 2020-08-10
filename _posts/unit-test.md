---
# layout: post
title:  Unit test  
categories:  interview
---
Xin chào tất cả các bạn cũng một thời gian dài rồi mình chưa có viết blog nào, trong bài viết này mình muốn chia sẻ một chủ đề mà thời gian vừa qua mình tìm hiểu  đó là testing 




## Unit testing là gì ? 
Unit test  là một trong những khái niệm căn bản nhẩt của test, là một automation test là một bước trong những bước căn bản của test  chạy và xác thực từng dòng code, tổng thể là function truyền vào tham số và kiểm tra kết quả mong đợi 

## Lợi ích của Unit test 
Unittest hữu ích khi làm việc với codebase lớn, khi  dự án phải làm việc với nhiều dev khác tiết kiệm thời gian thay đổi chỉnh sửa chức năng mà không sợ ảnh hưởng  đến code của ông khác 
Hạn chế bug 
## Setup và Teardown
**Setup** là phương thức khởi tạo các phương thức test
**TearDown** là phương thức clean sau mỗi phương thức hoàn thành  thực thi theo cơ chế LIFO 

