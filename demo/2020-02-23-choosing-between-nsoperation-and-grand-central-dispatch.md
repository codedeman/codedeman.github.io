
---
layout: post
title: Chọn cái nào NSOpertion và GDC trong IOS 
categories: ios developer 
---
Xin chào mọi nguời dạo gần đây mình nhận được góp ý của một anh leader, anh góp ý về bài viết của mình để bài viết của mình chất lượng hơn, cảm ơn anh rất nhiều,  sau lần góp ý đó mình mới nhận ra được mình đang thiếu sót nhiều chỗ, trong những bài viết tới mình sẽ cố gắng cải thiện để đem đến cho bạn đọc bài viết với nội dung đầy đủ và chất lượng nhất,

Để tăng trải nhiệm ng
Trong bài viết này chúng ta sẽ tìm hiểu về sự khác biệt của **NSOperation** và **GDC** tại sao đã có 1 thằng để dùng  rồi lại sinh ra thêm thằng kia để làm gì bài viết hôm nay chúng ta cùng khám phá nhé 

## Sự khác biệt của NSOperation 

**GDC** viết tắt của Grand Central Dispatch là một api nó ở  mức độ thấp nhất  được dựa vào nền tảng của **C** tương tác trực tiếp với Unix  thực hiện theo cơ chế FIFO 

**NSOperation** là một class của **ObjectiveC** **GDC**
**NSOPeration**  nó không giống như **GCD**nó không theo cơ chế theo thứ tự FIFO đây là một số điểm khác biệt 
1. Không theo FIFO: trong operation queues, bạn có thể set độ ưu tiên thực hiện  cho operations, và bạn có thể thêm dependencies giữa các operations nó có nghĩa là bạn có thể xác định một số operations sẽ chỉ được thực hiện sau khi hoàn thành sau khi hoàn thành operations khác. Đấy là lý do mà nó không theo cơ chế FIFO 

2. Mặc định chúng hoạt động concurrent , bạn có thể thay đổi nó kiểu serial queues, vẫn còn một cách giải quyết để thực hiện các tác vụ trong hàng đợi hoạt động theo trình tự bằng cách sử dụng các dependencies  giữa các hoạt động.
3. Operation queue là kiểu hướng đối tượng, mỗi operation queue là một instance của lớp NSOperationQueue, và mỗi task là một instance của lớp NSOperation
NSOperation cần được phân bổ trước khi chúng có thể được sử dụng và huỷ bỏ khi không cần dùng nữa. Mặc dù đây là một quá trình được tối ưu hoá cao, nhưng nó vẫn chậm GDC 
## Lợi ích của NSOperation 

Ngoài việc **NSOperation** được xây dựng  trên tầng  GCD, ngoài ra nó còn được  cung cấp những tính năng  mà  mà GDC  không có.  Có một vài lợi ích làm **NSOperation** là sự lựa chọn tuyệt vời hơn so với **GDC**
## Life cycle NSOperation 
![](https://imgur.com/llUvCp1)
vòng đời của của NSOperation gồm có các trạng thái sau pending-ready-executing-finish 

Tất cả các trạng thái trên có thể nhảy vào cancel state 


## Dependencies 

Trong **NSOpertion** hộ trợ **dependencies**  không giới hạn số que thực hiện.  Có thể thực thi các task theo một trình tự nhất định như (serial ) mà không cần phải xác định các que như GCD.Trong GCD, nếu muốn task chạy tuần tự, chúng ta phải gán task vào serial queue, và gán vào concurrent queue nếu muốn chạy đồng thời. Đối với GCD, chúng ta có thể tạo sự phụ thuộc bằng cách gán task vào serial queue, nhưng sử dụng operation queue ưu việt hơn hẳn dùng GCD.

## Oserable 
NSOperation and NSoperation que classes có rất nhiều giá trị để có thể observed sử dụng KVO (Key Value Observing) đây là một trong mà bạn muốn quan sát các trạng thái của một **operation** hoặc operation que 

## Pause Cancel Resume 
Một trong những điểm lợi hại của **NSOperation**  có thể tạm dừng, huỷ, tiếp tục 
khi bạn sử dụng **GCD** bạn không kiểm soát sâu được   các task thực thi  **NSOperation** có thể kiểm soát được vòng đời của operation 
## Thay đổi độ ưu tiên 

Cũng giống GDC  các concurrent queue với độ ưu tiên khác nhau, do đó chúng ta phải xác định độ ưu tiên của task trước rồi gán vào queue tương ứng. Đối với operation queue, chúng ta có thể thay đổi độ ưu tiên cho các task một cách dễ dàng sau khi gán task vào operation queue. Điều này là không thể đối với GCD.

Độ ưu tiên của operation được định nghĩa qua enum:
``` swift 
  

```
Trong đó, VeryHigh có độ ưu tiên cao nhất và thấp nhất là VeryLow

## Control 
**NSOperation** cũng có được nhiều lợi ích khác, ví dụ như bạn có thể thêm số queue mà bạn muốn hoạt động song song 
maxConcurrentOperationCount = 1
Là số operation que  có thể hoạt động song song. Nếu  không để số que cụ thể mà sử dụng  mặc định, thì nó sẽ theo tài nguyên mà hệ thống cho phép, lúc đó có thể thực hiện nhiều task cùng một lúc 
 



## Vậy nên dùng thằng nào 

Theo như Apple khuyên thì chúng ta nên dùng thằng nào có mức độ cao nhất đó chính là **NSOperation** 
Một operation có thể có dependencies vào một operartion khác nó là một tính năng hữu ích mà GCD không có nếu bạn cần thực thi một vài task theo một thứ tự cụ thể thì operation là một giải pháp tốt 

GDC Thì thường dùng cho nhưng tác vụ đơn giản 


## Khi nào sử dụng **NSOperation**

Dependency management  là một thứ tuyệt vời khi sử dụng **NSOperation**, Một operation này có thể phụ thuộc vào một operation khác đó là một tính năng hữu ích mà **GDC** không có,  nếu bạn cần thực hiện một vài task theo thứ tự cụ thể thì **NSOperation** là một giải pháp tốt 

## Khi nào thì dùng **GDC**


Dispatch Queues là cách dễ dàng để thực hiện các task bất đồng bộ, và đô


## Kết luận 

Trong bài viết này chúng ta vừa khám phá điểm lợi và bất lợi của **GDC** và **NSOperation**  Api  rõ ràng rằng có thể kết hợp cả 2 công nghệ là sự lựa chọn trong hầu hết các dự án bài viết này không thiếu sót mong mọi người góp ý giúp mình 

## Tham khảo nguồn 
[appcoda](https://www.appcoda.com/ios-concurrency/)

[techtalk](https://techtalk.vn/concurrent-programming-with-gcd-in-swift-3-part-1.html)

[](https://techblog.vn/concurrency-trong-ios-tim-hieu-ve-grand-central-dispatch-va-nsoperation)
