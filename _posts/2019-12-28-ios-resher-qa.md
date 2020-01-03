---
layout: post
title:  Khi nào thì viewWillAppear, viewDidAppear, viewDidLoad, viewWillDisappear thực sự gọi trong IOS 
categories: q&a
---

![](https://topdev.vn/nha-tuyen-dung/wp-content/uploads/2019/03/fpt-software-image-4.jpg)
### IOS fresher thì hỏi gì 
Một vài tháng trước mình đã quyết định apply vào một công ty công nghệ có tên là 👨🏻‍💻 không tiện nói tên. Sau một tuần thì mình nhận được kết quả công ty ofer cho mình với mức lương là hơn ******* triệu, nó không quá cao , cũng không hẳn là quá thấp đối với mình một sinh viên mới ra trường  Bên cạnh đó mình  cũng phải  làm 1 bài test liên quan đến IOS dù sao thì mình cũng đã pass qua được vòng phỏng vấn,  nên mình sẽ chia sẻ mình được hỏi những gì trong lúc phỏng vấn 

Trước khi bắt đầu vào phỏng vấn anh leader có hỏi mình một câu khá đơn giản viewWillAppear, viewDidAppear, viewDidLoad, viewWillDisappear, and viewDidDisappear  những cái đấy khi nào sẽ chạy trước, nếu bạn là 1 IOS developer chẳng chẳng còn xa lạ đến func này, nhưng có nhiều người khi làm còn không để ý đến nó 

### Tạo 1 project để xem nó chạy thế nào ?
project mà chúng ta tạo sẽ là singleview application, như bình thường chúng ta vẫn làm, Sau đó chúng ta sẽ viết các function như hình bên giới 

![](https://lh6.googleusercontent.com/WIuFTBF8lugmnTGYQ687Wa3uypMSPSbyazyieyN_hTKMB7F1ZZIY5SoXP9XbnMcB0_Vm9F7_4V2fhlCxdIfr8m6L9FCbDnHplhkTjoNOavKYmposLjsxFzeUPIhYZ0XpMxVIivKS)

Bước tiếp theo chúng ta sẽ đặt một số  breakpoint để xem nó chạy như thế nào 

Bum kết quả sẽ được hiện thị như hình bên giới 
![](https://lh3.googleusercontent.com/GPtLGalY0Sya_AjZ3yO-ks9hLmwxD-uWwHTkyoDziPrpdqqXk_Ph-EQ-fCdd9orYOCOYdNf2CjxnoWpA-dsYEw5jldxEL3l7udhB0pF33fJh545P89I05e7yjIwrPULPl06iLCjy)

Bạn có thể nhìn thấy thự tự chạy sẽ là 

1 viewDidLoad
2 viewWillApear
3 viewDidApear
4 viewWillDidDisappear
5 viewDidDisappea

### Tổng kết 

1 viewDidLoad  sẽ được chạy đầu tiên nó được gọi chỉ khi controller load view  viewDidLoad chỉ làm 1 lần, bạn nên những thứ mà chỉ làm một lần trong ViewdidLoad , ví dụ như set Text hoặc Label
2 viewWillApear sẽ được gọi trước khi view được thêm vào, nó luôn xảy ra sau viewDidLoad và được gọi bất cứ khi nào view được hiển thị 

4viewWillDidDisappear được gọi trước khi bạn bấm chuyển màn hình 

5 viewDidDisappear được gọi sau khi bạn chuyển đến màn hình khác 

Mong rằng bài biết sẽ hữu ích đối với các bạn fresher  sắp phòng vấn hay đang chuẩn bị đi phỏng vấn trong thời gian tới 

mọi đóng góp xin gửi về email cho mình tại địa chỉ [phamtrungkiendev@gmail.com]()

