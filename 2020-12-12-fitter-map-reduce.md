---
layout: post
title:  Fitter Map & Reduce trong IOS 
categories: interview
---

Xin chào các bạn trong bài viết này mình sẽ giới thiệu cho các bạn cách sử các hàm map flatmap rất hữu dụng trong IOS swift  khi xử lý các đối tượng collection 


## Map 

Sử dụng phép xử lý map để lặp duyệt qua từng phần tử trong một collection, đồng thời sử dụng các phép biến đổi để thay đổi giá trị của từng phần tử. Kết quả cuối cùng của phép xử lý map là một mảng các phần tử của collection cũ sau khi áp dụng các phép biến đổi.

Bây giờ  chúng ta tạo một mảng với đối tượng như thế này 
``` swift
struct Devices {
    
    var type:String = ""
    var price:Double = 0.0
    var color:String = ""
}

let iDevices:[Devices] = [Devices(type: "I Mac pro", price: 100.0, color: "Space gray"),Devices(type: "Iphone", price: 10202.0, color: "Black"), ]

,,,

VD Bây giờ chúng ta muốn tính thuế của mỗi sản phẩm nhân 2 lần. Bình thường chúng ta sẽ sử dụng for để duyệt các các phần tử để nhân 2  như thế này 

``` swift 

var taxes:[Double] = []

for tax in iDevices {
    
    taxes.append(tax.price * 2.0)
}
print("taxes result:",taxes)
Output
taxes result [200.0, 20404.0]

```

Trong swift cung cấp cho chúng ta hàm map dể xử lý trường hợp này ngắn gọn hơn 

``` swift 

let result = iDevices.map({ return $0.price * 2.0 })

print("taxes result",result)

Output 
taxes result [200.0, 20404.0]


```

## Fitter 

Sử dụng phép xử lý filter duyệt qua tất cả các phần tử có trong collection và chỉ lấy ra các phần tử thoả mãn điều kiện cho trước và bổ sung vào mảng kết quả. 

VD Bây giờ trong cái mảng  iDevices này  chúng ta muốn tìm ra loại thiết bị Iphone chẳng hạn chúng ta sẽ dùng fitter để lọc ra phần tử mình cần 


``` swift

let myIphone = iDevices.filter({return $0.type == "Iphone"})

print(myIphone)

```

## Reduce 

Phép xử lý reduce được sử dụng để kết hợp tất cả các phần tử trong một collection thành một kết quả đầu ra





