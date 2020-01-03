---
layout: post
title:  struct với class trong IOS 
categories:  q&a
---

### IOS fresher thì hỏi gì 
Xin chào các bạn sau vài lần đi phỏng vấn dạo một trong những câu hỏi căn bản mình được hỏi nhiều nhất đó chính là Struct Class trong swift khác nhau ở điểm nào,  một câu hỏi tưởng chừng dễ. Nhưng bình thường chúng ta dùng thì cũng chả để ý đến nó  

Đầu tiền trong Swift  Struct và class khác nhau Struct là kiểu dữ liệu còn Class là kiểu tham chiếu 

Kiểu tham chiếu là gì 
Một ví dụ thực tế là khi bạn làm việc trên google doc bạn chia sẻ cho đồng nghiệp rồi đi ăn sau khi quay trở lại thì bạn thấy một đống thứ tùm lum thay đổi. Đó là kiểu tham chiếu 
mọi thay đổi  đồng nghiệp của bạn sẽ làm thay đổi tài liệu của bạn 
(Classs)

Ngược lại bạn đính kèm tài liệu rồi gửi mail or facebook cho đồng nghiệp lúc này sẽ có 2 bản 1 bản của bạn làm còn 1 bản coppy bạn gửi cho đồng nghiệp. Hai  người có thể làm việc độc lập, và sự thay đổi của đồng nghiệp của bạn không làm thay đổi đến tài liệu của bạn, đó là Struct 
Lấy một ví dụ để xem sự khác biệt của nó 









Vậy khi sử dụng  struct khi nào sử dụng class 

Khi nào chọn Class và Struct 
Chọn struct mặc định 
Chọn Class khi muốn tương tác với Objective c 
Sử dụng Class khi muốn kiểm soát tính dữ liệu 


Class và Struct đều hỗ trợ kế thừa nhưng Struct chỉ nhận kế thừa từ 1 protocol 
