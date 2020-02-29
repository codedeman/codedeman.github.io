
---
layout: post
title: Chọn cái nào NSOpertion và GDC trong IOS 
categories: ios developer
thumbnail:https://www.iosdevlog.com/assets/images/wwdc/2015/226/1.png
---
> Xin chào mọi nguời dạo gần đây mình nhận được góp ý của một anh leader team mobile  góp ý về bài viết của mình chia sẻ, cảm ơn anh rất nhiều, sau lần góp ý đó mình mới nhận ra được mình đang thiếu sót nhiều chỗ, trong những bài viết tới mình sẽ cố gắng cải thiện để đem đến cho bạn đọc bài viết với nội dung đầy đủ và chất lượng nhất .>
## Giới thiệu 
Nhắc đến các ứng dụng  IOS nhiều người sẽ nghĩ đến độ mượt mà của nó. Là 1 IOS dev chuyên nghiệp ngoài việc tránh code leak memory làm thế nào để tối ưu hoá bộ nhớ của hệ thống  
Concurrency((xử lý đồng thời) là một khái niệm xử lý nhiều thứ xảy ra cùng một lúc. Cùng với sự phát triển của chip xử lý đa lõi và sự thật là số lõi của mỗi bộ xử lý sẽ ngày càng tăng lên, các nhà phát triển phải tận dụng lợi thế của chúng. Mặc dù các hệ điều  hành có thể chạy nhiều tác vụ song song, nhưng hầu hết chúng là chương trình chạy ngầm, và  thực hiện các tác vụ yêu cầu ít thời gian liên tục, nên nếu một ứng dụng có rất nhiều tác vụ  việc quản lý tốt tài nguyên của hệ thống sẽ giúp hệ thống chạy mượt hơn đỡ giật lag hơn 

Việc sử dụng concurrency trong lập trình iOS là không hề khó, bởi vì Apple đã cung cấp cho lập trình viên các API để chúng ta dễ dàng thao tác sử dụng. Trong bài viết này, tôi xin giới thiệu về Grand Central Dispatch và NSOperation, 2 API thông dụng nhất giúp chúng ta quản lý concurrency một cách đơn giản và dễ dàng. tại sao lại sinh ra 2 thằng để làm gì  trong  bài viết hôm nay chúng ta cùng khám phá nhé 

## II Sự khác biệt của NSOperation 

**GDC** viết tắt của Grand Central Dispatch là một api nó ở  mức độ thấp nhất  được dựa vào nền tảng của **C** tương tác trực tiếp với Unix  các que thực hiện theo cơ chế FIFO [chi tiết GCD](https://techtalk.vn/concurrent-programming-with-gcd-in-swift-3-part-1.html)

**NSOperation** là một class của **ObjectiveC** nó được xây dựng tầng bên trên của  **GDC**
**NSOperation**  nó không giống như **GCD**nó không theo cơ chế theo thứ tự FIFO đây là một số điểm khác biệt 
1. Không theo FIFO: trong operation queues, bạn có thể set độ ưu tiên thực hiện  cho operations, và bạn có thể thêm dependencies giữa các operations nó có nghĩa là bạn có thể xác định một số operations sẽ chỉ được thực hiện sau khi hoàn thành operations khác. Đấy là lý do mà nó không theo cơ chế FIFO 

2. Operation queue chỉ xử lý theo kiểu concurrent queue mà không xử lý theo kiểu serial queue của GCD. Để xử lý theo kiểu serial queue, chúng ta tạo các ràng buộc cho các operation.

3. Operation queue là kiểu hướng đối tượng, mỗi operation queue là một instance của lớp NSOperationQueue, và mỗi task là một instance của lớp NSOperation.
*NSOperation cần được phân bổ trước khi chúng có thể được sử dụng và huỷ bỏ khi không cần dùng nữa. Mặc dù đây là một quá trình được tối ưu hoá cao, nhưng nó vẫn chậm GDC*
## III Lợi ích của NSOperation 
Ngoài việc **NSOperation** được xây dựng  trên tầng  GCD, ngoài ra nó còn được  cung cấp những tính năng  mà  mà GDC  không có.  Có một vài lợi ích làm **NSOperation** là sự lựa chọn tuyệt vời hơn so với **GDC**
### Life cycle NSOperation 
![](https://i.imgur.com/llUvCp1.png)
vòng đời của của NSOperation gồm có các trạng thái sau pending-ready-executing-finish 

Bạn có thể huỷ bất kỳ 1 operation cụ thể nào hoặc tất cả các operations cho bất kỳ hàng đợi nào. Operation có thể bị huỷ bỏ trước khi thêm vào queue. Việc huỷ bỏ có thể được thực hiện bằng cách gọi phương thức **cancel()** trong NSOperation class. Khi bạn cancel bất cứ 1 operation nào sẽ có ba tình huống sẽ xảy ra một trong số chúng 

+ Operation đã kết thúc. Trong trường hợp này phương thức **cancel** không có tác dụng gì 
+ 	Operation đang được thực hiện. Trong trường hợp này hệ thống sẽ không buộc operation ngừng lại nhưng thay vào đó thuộc tính bị huỷ sẽ được set thành true 
+ Operation ở trong hàng đợi chờ được thực thi. Trong trường hợp này operation sẽ không được thực hiện 

### Dependencies 

Trong **NSOpertion** hộ trợ **dependencies**  không giới hạn số que thực hiện.  Có thể thực thi các task theo một trình tự nhất định như (serial ) mà không cần phải xác định các que như GCD.Trong GCD, nếu muốn task chạy tuần tự, chúng ta phải gán task vào serial queue, và gán vào concurrent queue nếu muốn chạy đồng thời. Đối với GCD, chúng ta có thể tạo sự phụ thuộc bằng cách gán task vào serial queue, nhưng sử dụng operation queue ưu việt hơn hẳn dùng GCD.

``` swift

var queue = OperationQueue()
let operation1 = BlockOperation {
  let urlString = URL(string: self.imageUrl[0])
  guard  let data = try? Data(contentsOf: urlString!) else {return}
  
  OperationQueue.main.addOperation {
    self.imageView1.image = UIImage(data: data)
  }
  
}

operation1.completionBlock = {
  print("Operation 1 completed")
}

let operation2 = BlockOperation {
  let urlString = URL(string: self.imageUrl[0])
  guard  let data = try? Data(contentsOf: urlString!) else {return}
  
  OperationQueue.main.addOperation {
    self.imageView2.image = UIImage(data: data)
  }
  
}

operation2.completionBlock = {
  print("Operation 2 completed")

}

operation2.addDependency(operation1)

queue.addOperations([operation1,operation2], waitUntilFinished: true)

```

### Observable 
NSOperation and NSoperation que classes   có  một số thuộc tính có thể observed sử dụng KVO (Key Value Observing)  Đây là một lợi ích quan trọng khác nếu bạn muốn theo dõi trạng thái của một hàng đợi hoạt động hoặc hoạt động


### Pause Cancel Resume 
Một trong những điểm lợi hại của **NSOperation**  có thể tạm dừng, huỷ, tiếp tục 
khi bạn sử dụng **GCD** bạn không kiểm soát sâu được   các task thực thi  **NSOperation** có thể kiểm soát được vòng đời của operation 
### Thay đổi độ ưu tiên 
Cũng giống GDC  các concurrent queue với độ ưu tiên khác nhau, do đó chúng ta phải xác định độ ưu tiên của task trước rồi gán vào queue tương ứng. Đối với operation queue, chúng ta có thể thay đổi độ ưu tiên cho các task một cách dễ dàng sau khi gán task vào operation queue. Điều này là không thể đối với GCD.

Độ ưu tiên của operation được định nghĩa qua enum:
``` swift 
  public enum NSOperationQueuePriority : Int {
      case VeryLow
      case Low
      case Normal
      case High
      case VeryHigh
  }

```
Trong đó, VeryHigh có độ ưu tiên cao nhất và thấp nhất là VeryLow

### Control 
**NSOperation** cũng có được nhiều lợi ích khác, ví dụ như bạn có thể thêm số queue mà bạn muốn hoạt động song song 
``` swift 
maxConcurrentOperationCount = 1
```
Là số operation que  có thể hoạt động song song. Nếu  không để số que cụ thể mà sử dụng  mặc định, thì nó sẽ theo tài nguyên mà hệ thống cho phép, lúc đó có thể thực hiện nhiều task cùng một lúc 
 
## Vậy nên dùng thằng nào 

Theo như Apple khuyên thì chúng ta nên dùng thằng nào có mức độ cao nhất đó chính là **NSOperation**  thay vì **GDC** trừ khi bạn cần làm gì đó mà **NSOperation** không hỗ trợ 
Một operation có thể có dependencies vào một operartion khác nó là một tính năng hữu ích mà GCD không có nếu bạn cần thực thi một vài task theo một thứ tự cụ thể thì operation là một giải pháp tốt 

GDC Thì thường dùng cho nhưng tác vụ đơn giản, điểm lợi thế của **GDC** được dựa trên ngôn ngữ **C** nên nhanh hơn so với **NSOperation** 	


## Kết luận 

Trong bài viết này chúng ta vừa khám phá  sự khác biệt hai api là  **GDC** và **NSOperation**    rõ ràng rằng có thể kết hợp cả 2 công nghệ là sự lựa chọn trong hầu hết các dự án, và tuỳ theo mục đích sử dụng của bạn.  Bài viết này không thiếu sót mong mọi người góp ý giúp mình để lại bình luận phía giới bài việt hoặc mail trực tiếp cho mình [phamtrungkien@gmail.com]

## Tham khảo nguồn 
[Apple](https://developer.apple.com/documentation/foundation/nsoperationqueue)

[appcoda](https://www.appcoda.com/ios-concurrency/)

[techtalk](https://techtalk.vn/concurrent-programming-with-gcd-in-swift-3-part-1.html)

[Concurrency Programming Guide
](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091)
[WDC 2015](https://developer.apple.com/videos/play/wwdc2015/226/)
