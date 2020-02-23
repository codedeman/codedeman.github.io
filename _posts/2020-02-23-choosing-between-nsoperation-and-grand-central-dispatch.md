---
layout: post
title: Chọn cái nào NSOpertion và GDC trong IOS 
categories: ios developer 
comment: 0
---
Xin chào mọi nguời dạo gần đây mình nhận được góp ý của một expert trong nghề góp ý về bài viết của mình để bài viết của mình chất lượng hơn, cảm ơn anh Linh, sau lần góp ý đó mình mới nhận ra được mình đang thiếu sót nhiều chỗ, trong những bài viết tới mình sẽ cố gắng cải thiện để đem đến cho bạn đọc bài viết với nội dung đầy đủ cũng như  trong bài viết này chúng ta sẽ tìm hiểu về sự khác biệt của **NSOperation** và **GDC** tại sao đã có 1 thằng để dùng rồi lại sinh ra thêm thằng kia để làm gì bài viết hôm nay chúng ta cùng khám phá nhé 

## Sự khác biệt của NSOperation 

**GDC** viết tắt của Grand Central Dispatch là một api nó ở  mức độ thấp nhất  được dựa vào nền tảng của **C** tương tác trực tiếp với Unix 
**NSOperation** là một class của **ObjectiveC** nó ở mức độ cao hơn so  với  **GDC**
## Lợi ích của NSOperation 

Ngoài việc **NSOperation** được xây dựng  trên tầng  GCD, ngoài ra nó còn được  cung cấp những tính năng  mà  mà GDC  không có.  Có một vài lợi ích làm **NSOperation** là sự lựa chọn tuyệt vời hơn so với **GDC**



## Life cycle NSOperation 
![](https://imgur.com/llUvCp1)
vòng đời của của NSOperation gồm có các trạng thái sau pending-ready-executing-finish 

Tất cả các trạng thái trên có thể nhảy vào cancel state 


## Dependencies 

Trong **NSOpertion** hộ trợ **dependencies**  không giới hạn số que thực hiện.  Có thể thực thi các task theo một trình tự nhất định 

## Oserable 
NSOperation and NSoperation que classes có rất nhiều giá trị để có thể observed sử dụng KVO (Key Value Observing) đây là một trong mà bạn muốn quan sát các trạng thái của một **operation** hoặc operation que 

## Pause Cancel Resume 
Một trong những điểm lợi hại của **NSOperation**  có thể tạm dừng, huỷ, tiếp tục 
khi bạn sử dụng **GCD** bạn không kiểm soát sâu được   các task thực thi  **NSOperation** có thể kiểm soát được vòng đời của operation 


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


**GDC** Thì thường dùng cho nhưng tác vụ đơn giản 

## Kết luận 

Trong bài viết này chúng ta vừa khám phá điểm lợi và bất lợi của **GDC** và **NSOperation**  Api  rõ ràng rằng có thể kết hợp cả 2 công nghệ là sự lựa chọn trong hầu hết các dự án 

