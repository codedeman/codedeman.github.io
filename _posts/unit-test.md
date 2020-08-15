---
# layout: post
title:  Unit test  
categories:  interview
---
Ứng dụng hoặc bất kì sản phẩm nào trước khi đến tay người dùng, đều phải trải qua 1 quá trình test cẩn thận. Khi nói về test nhiều người sẽ nghĩ người tester sẽ ngồi hàng giờ kiểm tra từng màn hình, từng nút bấm  để phát hiện ra điều bất thường và  báo lại cho nhà phát triển,thường một ứng dụng lớn thì đội tester sẽ mất rất nhiều thời gian để kiểm thử từng chức năng, thậm chí sau đó dev có thể  thay đổi code và sau đó tất cả các việc test của tester sẽ phải bắt đầu lại 
Vì lý do đấy nhiều công ty đang bắt đầu viết automation test cho  project của họ, hình ảnh phía giới biểu thị các loại test  
![](https://docs-assets.developer.apple.com/published/20b3426c34/93cc7b80-dd57-423d-be85-f937da693ec3.png)

Tính từ giới kim tự tháp đầu tiên là unit test, sau đó đến Integration Test và cuối cùng là UI test 

## Unit testing là gì ? 
Unit test  là một trong những khái niệm căn bản nhẩt của automation test  chạy và xác thực từng dòng code, tổng thể là function truyền vào tham số và kiểm tra kết quả mong đợi 

## Integration test 


## UI test 
là bước cuối cùng của automation test là testing chạy lậu nhất so với hai thằng còn lại, nó có khả năng gi lại những tương tác của user lên giao diện và chuyển nó thành mã nguồn 



trong bài viết này mình muốn chia sẻ một chủ đề mà thời gian vừa qua mình tìm hiểu  đó là testing, cụ thể trong bài này mình sẽ nói về unit test 




## XCtesting 
Là một công cụ có khác năng viết test nhiều mức độ trừu tượng, là một giải pháp tốt để testing  kết hợp được nhiều kiểu test để tối đa hoá lơi ích từ mỗi loại 

## Lợi ích của Unit test 
Unittest hữu ích khi làm việc với codebase lớn, khi  dự án phải làm việc với nhiều dev khác tiết kiệm thời gian thay đổi chỉnh sửa chức năng mà không sợ ảnh hưởng  đến code của ông khác 
Hạn chế bug 

Một unit test sẽ test 1 case cụ thể, và trong một phương thức thường sẽ có 4 bước 
1 Setup 
    Khởi tạo classs mà bạn muốn test 
2 Execution 
    Gọi những phương thức ở trong class 
3 Expection 
    Kiểm kết quả mong đợi của kết quả trả về 
4 Clean up 

## Setup và Teardown
**Setup** là phương thức khởi tạo các phương thức test
**TearDown** là phương thức clean sau mỗi phương thức hoàn thành  thực thi theo cơ chế LIFO 

