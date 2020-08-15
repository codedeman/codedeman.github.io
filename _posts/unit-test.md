---
# layout: post
title:  Unit test  
categories:  interview
---
Ứng dụng hoặc bất kì sản phẩm nào trước khi đến tay người dùng, đều phải trải qua 1 quá trình test cẩn thận. Khi nói về test nhiều người sẽ nghĩ người tester sẽ ngồi hàng giờ kiểm tra từng màn hình, từng nút bấm  để phát hiện ra điều bất thường và  báo lại cho nhà phát triển,thường một ứng dụng lớn thì đội tester sẽ mất rất nhiều thời gian để kiểm thử từng chức năng, thậm chí sau đó dev có thể  thay đổi code và sau đó tất cả các việc test của tester sẽ phải bắt đầu lại khá mất thời gian 
Vì lý do đấy nhiều công ty đang bắt đầu viết automation test cho  project của họ, hình ảnh phía giới biểu thị các loại test  
![](https://docs-assets.developer.apple.com/published/20b3426c34/93cc7b80-dd57-423d-be85-f937da693ec3.png)

Tính từ giới kim tự tháp đầu tiên là Unit test, sau đó đến Integration Test và cuối cùng là UI test 

## Unit testing là gì ? 
Unit test  là một trong những khái niệm căn bản nhẩt của automation test  chạy và xác thực mã nguồn, hiểu một cách đơn giản là  là function truyền vào tham số và kiểm tra kết quả mong đợi đầu ra, nó đơn giản mà nhanh 

## Integration test 
Tương tự như Unit test nhưng nó sẽ có thể cover rộng hơn so với unittest 
Mục tiêu của interaction là cài thiện chất lượng của phần mềm 

## UI test 
là bước cuối cùng của automation test là testing chạy lậu nhất so với hai thằng còn lại, nó có khả năng gi lại những tương tác của user lên giao diện và chuyển nó thành mã nguồn 

Trong bài viết này mình muốn chia sẻ một chút hiểu biết của mình  về unit test 

## Lợi ích của Unit test 
Unittest hữu ích khi làm việc với codebase lớn, khi  dự án phải làm việc với nhiều dev khác tiết kiệm thời gian thay đổi chỉnh sửa chức năng mà không sợ ảnh hưởng  đến code của ông khác  hạn chế bug phát sinh, mình đã từng đau khổ khi maintain các dự án cũ nhưng không có unittest kết quả là sửa tính năng này, thì lại hỏng tính năng kia vì các tính năng đều liên quan đến nhau nên code có unittest thì sẽ gíup bạn gỉai quyết vấn đề này 


## XCtesting 
Là một công cụ có khác năng viết test nhiều mức độ trừu tượng, là một giải pháp tốt để testing  kết hợp được nhiều kiểu test để tối đa hoá lơi ích từ mỗi loại 

Một unit test sẽ test 1 case cụ thể, và trong một phương thức thường sẽ có 4 bước 
1 Setup 
</br>
Khởi tạo classs mà bạn muốn test 
</br>
2 Execution 
</br>
    Gọi những phương thức ở trong class 
</br>
3 Expection 
</br>
    Kiểm kết quả mong đợi của kết quả trả về 
4 Clean up 
## Setup và Teardown
**Setup** là phương thức khởi tạo các phương thức test
</br>
**TearDown** là phương thức clean sau mỗi phương thức hoàn thành  thực thi theo cơ chế LIFO 


Chúng ta có test case  đơn giản như sau
Case 1  nhập vào một số chia hết cho 2 
</br>
Setup:Tạo một function nhập vào 1 số chia hết cho 2 
</br>
Execution:chạy function 
</br>
Expection: trả về True
</br>

Case 2 nhập vào một số không chia hết cho 2 

Setup:Tạo một function nhập vào 1 số không chia hết cho 2 
</br>
Execution:chạy function 
</br>
Expection: trả về False
</br>


Bây giờ chúng ta sẽ chuyển đoạn mã giả trên thành code nào, đầu tiên khi tạo project chúng ta sẽ tích vào Unittest nhé 

<br>
<img src="https://i.imgur.com/wjiS1II.png"  width=80% />
<br>


``` Swift
  func sumArray(nums:[Int]) ->Int {
    var sum:Int!
    for num in nums {
      if (num%2 != 0) {
      sum = num+num
      }
    }
    return sum
  }
```


``` Swift
  func testSum()  {
    let sums = [2,2,3,5]
    XCTAssertEqual(sut.sumArray(nums: sums), 8)
  }
```
## Kết luận
Bài viết này mình đã giới thiệu cho các bạn những khái niệm căn bản nhất của testing, và chúng ta cũng ta cũng đã thử viết 1 unit test căn bản, hy vọng bài viết của mình sẽ hữu ích cho bạn khi mới tiếp cận đến unit test, trong bài viết sắp tới mình sẽ chia sẻ cho các bạn về UI test, mọi ý kiến đóng góp mong các bạn gửi về địa chỉ ![]phamtrungkiendev@gmail.com or bình luận phía giới của bài viết này nhé!

Bài viết tham khảo của 

