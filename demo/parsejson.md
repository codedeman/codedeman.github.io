Xin chào các nếu là một developer không sớm thì muộn bạn sẽ gặp phải parse json, bài viết này mình xin hướng dẫn mọi người cách parse json bằng  Codable nhé
### Codable là gì 
![WWDC 2017](https://developer.apple.com/videos/play/wwdc2017/212) Apple giới thiệu tính năng mới trong Swift để parse json 
Codable có thể chuyển đổi chính nó vào và ra dạng dữ liệu bên ngoài, Codable  kết hợp Encodable và  Decodable  trong một,  trình biên dịch sẽ cố gắng tự động tổng hợp code yêu cầu encode hoặc decode 

``` swift
typealias Codable = Decodable & Encodable

```

### Codable trong Swift 4 
Trong swift 4, Apple đã giới thiệu 1 cách thức mới để mã hoá và giải mã hoá 
Encodable - dùng cho mã hóa
Decodable - dùng cho giải mã
Codable - dùng cho cả mã hóa và giải mã
Chúng hỗ trợ cả class struct và enum 

### Encodable Protocol

Một  kiểu  có thể mã hóa bản thân nó  thành một dạng dữ liệu để có thể sử dụng bên ngoài (JSON, plist,...). Nó được sử dụng bởi các types có thể được mã hóa.
Nó chứa một phương thức duy nhất:
encode(to:) - Mã hóa giá trị này vào bộ mã hóa đã cho.


### Decodable Protocol
Một loại có thể giải mã hoá bản thân nó thành dữ liệu bên ngoài thành đối tượng được sử dụng trong ứng dụng. Nó được sử dụng bởi loại có thể được giải mã 
Nó cũng chứ một phương thức duy nhất :
init(from:) — Khởi tạo một đối tượng bằng cách giải mã dữ liệu từ bộ giải mã đã cho 


Đầu tiên mọi người có thể xem link [json](("https://api.github.com/search/users?q=dung")) ở đây  **dung** là 1 cái parameter mà mình để  thôi các bạn có thể để bất cứ tên gì mà các bạn muốn  miễn là có data 

### Ví dụ 
Mình có một đoạn json như sau 

```

{
"total_count": 4679,
"incomplete_results": false,
    "items": [
    {
    "login": "dung",
    "id": 384206,
    "node_id": "MDQ6VXNlcjM4NDIwNg==",
    "avatar_url": "https://avatars3.githubusercontent.com/u/384206?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/dung",
    "html_url": "https://github.com/dung",
    "followers_url": "https://api.github.com/users/dung/followers",
    "following_url": "https://api.github.com/users/dung/following{/other_user}",
    "gists_url": "https://api.github.com/users/dung/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/dung/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/dung/subscriptions",
    "organizations_url": "https://api.github.com/users/dung/orgs",
    "repos_url": "https://api.github.com/users/dung/repos",
    "events_url": "https://api.github.com/users/dung/events{/privacy}",
    "received_events_url": "https://api.github.com/users/dung/received_events",
    "type": "User",
    "site_admin": false,
    "score": 145.70857
    },
}


```

### Bước 1 import thư viện 
Đầu tiên chúng ta cần import thư viện thông qua ![cocopods](https://cocoapods.org)

``` 
pod 'Alamofire', '~> 5.0.0-rc.3'

```
### Bước 2 Tạo Model
Chúng ta sẽ tạo 1 file model có tên là  ***User***   kế thừa từ **Codable**

``` swift

import Foundation

struct UserRequest:Codable{
    
    let total_count:Int = 0
    let incomplete_results:Bool
    let items:[User]
}

struct User:Codable{
    let login:String
    let id:Int
    let node_id:String
    let avatar_url:String
 

```
👉🏼Lưu ý các properties trong Model phải trùng khớp với các key value trong JSON data  thì mới parse được json nhé, trong trường hợp mà tên biến trong **Model** mà không trùng với key value trong Json data chúng ta có thể dùng 

``` 
enum CodingKeys: String, CodingKey {
    case totalcount = "total_count"
}
```


### Bước 3 parse json 
👉🏼 Tiếp theo chúng ta tạp 1 file có tên là ***DataService*** trong file này chúng ta sẽ viết 1 class , trong class có chứa 1 closure  

``` swift

import Foundation
import Alamofire
class Dataservice {
    static let intance = Dataservice()
    func fetchData(keyword:String, completion:@escaping(_ user:UserRequest?)->())  {
        AF.request("https://api.github.com/search/users?q=\(keyword)").responseJSON { (response) in
            
            if let error = response.error{
                debugPrint(error.localizedDescription)
                completion(nil)
            }
            
            guard let data = response.data else {return completion(nil)}
            let jsonDecoder = JSONDecoder()
            
            do {
                let person = try jsonDecoder.decode(UserRequest.self, from: data)
                completion(person)
            } catch {
                debugPrint(error.localizedDescription)
                completion(nil)
            }
        }
        
    }
    
    
}

```

### Đoạn code trên làm gì 

👉🏼 Ở đây chúng ta dùng thư viện Alamofire  như mình đã nói ở trên, vì ở đây là phương thức **get** nên chỉ cần dùng **AF.request(url)** là đủ 

``` swift

AF.request("https://api.github.com/search/users?q=\(keyword)").responseJSON { (response) in


```

👉🏼 Ở đây chúng ta sử dụng **JSONEncoder**  để chuyển từ  kiểu **Codable** sang **data**

``` swift 

    let person = try jsonDecoder.decode(UserRequest.self, from: data)

```


Tiếp theo chúng ta sẽ tạo một file cell để hiển thị thông tin lên ***Tabel***  có tên là  **DasboardCell**  trong file này chúng ta muốn hiển thị ảnh cũng như tên 
``` swift


import UIKit

    class DasboardCell: UITableViewCell {

        @IBOutlet weak var avatarImageView: UIImageView!
        @IBOutlet weak var usernameLabel: UILabel!
        
        override func awakeFromNib() {
            super.awakeFromNib()
        }
        
        func configureCell(user:User)  {
            DispatchQueue.main.async {
                
                guard let url = URL(string: user.avatar_url) else { return }
                guard let data = try? Data(contentsOf: url) else {return}
                self.avatarImageView.image = UIImage(data: data)
                self.usernameLabel.text = user.login
                
            }
          
        }

        override func setSelected(_ selected: Bool, animated: Bool) {
            super.setSelected(selected, animated: animated)

            // Configure the view for the selected state
        }
        
    }

```

Trong file **ViewController**  chúng ta sẽ hiển thị dữ liệu lên 1 tableview 

``` swift

//
//  ViewController.swift
//  TestDesignPattern
//
//  Created by Apple on 10/22/19.
//  Copyright © 2019 Apple. All rights reserved.
//

import UIKit


class ViewController: UIViewController {
    
    @IBOutlet weak var userTableView: UITableView!
    var userModel:[User] = []
    
    override func viewDidLoad() {
        super.viewDidLoad()
        userTableView.register(UINib(nibName: "DasboardCell", bundle: nil), forCellReuseIdentifier: "DasboardCell")

        userTableView.delegate = self
        userTableView.dataSource = self
        Dataservice.intance.fetchData(keyword: "b") { (users) in
            self.userModel = users!.items
            self.userTableView.reloadData()
        }
    
    }
}
extension ViewController:UITableViewDelegate,UITableViewDataSource{
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return userModel.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
        guard let cell = tableView.dequeueReusableCell(withIdentifier: "DasboardCell") as? DasboardCell else   {
    
            return DasboardCell()
        }
        let user = userModel[indexPath.row]
        cell.configureCell(user: user)
        
        
        return cell
        
    }
    
    
}
    


```
### Đoạn code trên làm gì 

Ở đây như mình đã nói ở trên bạn có thể truyền vào 1 parameter bất kỳ miễn là có data nhé 

``` swift

Dataservice.intance.fetchData(keyword: "b") { (users) in
           
}

```


Ok h bấm run để  xem kết quả của chúng ta nào 

![](https://imgur.com/a/mTZl1ph)



Bài viết tham khảo nguồn ![](https://www.swiftbysundell.com/basics/codable/)
Mình vừa hướng dẫn các bạn cách bạn json sử dụng **codable**  bài viết này có thể còn nhiều thiếu sót mong các cao nhân góp ý giúp em, để em có thể cải thiện bài viết sau hơn, mọi thông tin góp ý xin gửi về ![phamtrungkiendev@gmail.com]()
