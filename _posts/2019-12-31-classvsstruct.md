---
layout: post
title:  Sự khác biệt giữa struct với class trong IOS 
categories:  interview
---

### IOS fresher thì hỏi gì 
Xin chào các bạn sau vài lần đi phỏng vấn dạo, một trong những câu hỏi căn bản mình được hỏi nhiều nhất đó chính là **struct**  **class**  trong swift khác nhau ở điểm nào,  một câu hỏi tưởng chừng dễ. Nhưng bình thường chúng ta dùng thì cũng chả để ý đến nó  mà dùng nó lung tung 

Đầu tiền trong Swift  **struct** và **class** khác nhau **struct** là kiểu dữ liệu còn **class** là kiểu tham chiếu 

![](https://miro.medium.com/max/1226/1*37Itex_pCsEW62HKKZB6CQ.jpeg)

### Kiểu tham chiếu  và tham trị là gì 
**class** Một ví dụ thực tế là khi bạn làm việc trên google doc bạn chia sẻ cho đồng nghiệp rồi đi ăn, sau khi quay trở lại thì bạn thấy một đống thứ tùm lum thay đổi. Đó là kiểu tham chiếu 
mọi thay đổi  đồng nghiệp của bạn sẽ làm thay đổi tài liệu của bạn 

**struct** Ngược lại bạn đính kèm tài liệu rồi gửi mail or facebook cho đồng nghiệp lúc này sẽ có 2 bản 1 bản của bạn làm còn 1 bản coppy bạn gửi cho đồng nghiệp. Hai  người có thể làm việc độc lập, và sự thay đổi của đồng nghiệp của bạn không làm thay đổi đến tài liệu của bạn, đó là Struct 
Lấy một ví dụ để xem sự khác biệt của nó 

## Bắt tay vào code thử nhé 

``` swift


class Developer {
    
    var firstName : String
    var lastName : String
    var position : String
    
    init(firstName:String,lastName:String,position:String) {
        self.firstName = firstName
        self.lastName = lastName
        self.position = position
    }
}

let dev = Developer(firstName: "Kevin", lastName: "Pham", position: "Junior")

let passedDev = dev
dev.firstName = "JonyB"
passedDev.firstName = "Casey"

print(dev.firstName) // might expect this to print JonnyB
print(passedDev.firstName)  // might expect print Sally



```

 👉🏼 Kết quả sẽ là 
 Casey
 Casey

Vì chúng ta print ***firstName*** ra hai lần nên nó in ra 2 cái **firstname** là Casey mà nó không in ra tên là JonyB

Rồi chúng ta sẽ lấy thêm một ví dụ về **struct** để thấy được sự khác bọt của nó 


``` swift 

struct DevStruct{

    var firstName : String
    var lastName : String
    var position : String
}

var devStruct = DevStruct(firstName: "Kevin", lastName: "Pham", position: "Junior")
var copyDevStruct = devStruct

devStruct.firstName = "Casey"
copyDevStruct.firstName = "Tim"

print(devStruct.firstName)
print(copyDevStruct.firstName)


```
👨‍⚖️ lưu ý ở đây **struct** không cần sử dụng hàm dựng **init()**

👉🏼 lúc này kết quả chúng ta sẽ là 
Casey
Tim


### Khi nào nên dùng **class**  và khi nào nên dùng **struct**

* Chọn Class khi cần thừa kế được dùng nhiều như : UIView, UIViewController.
* Chọn Struct khi không muốn thay đổi property khi đã khởi tạo rồi => đóng gói các dữ liệu đơn giản
* Struct được dùng nhiều trong Swift như : Array, String, Dictionary,Int,Float.
* Struct ngăn ngừa rủ ro bộ nhớ bị đổi khi bạn chuyền 1 instance qua môi trường đa luồng khác nhau.
