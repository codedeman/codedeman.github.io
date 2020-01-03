Xin chào  các bạn  ios developer   bài viết này mình xin hướng dẫn mọi người cách parse json bằng  Codable nhé
### Swift Codable là gì 
![WWDC 2017](https://developer.apple.com/videos/play/wwdc2017/212) Apple giới thiệu tính năng mới trong Swift để parse json 


Codable  kết hợp Encodable và  Decodable  trong một 

trình biên dịch sẽ cố gắng tự động tổng hợp code yêu cầu encode hoặc decode

Như chúng ta đã biết Codable đã được thêm vào ở Swift4.
Thực tế thì việc Encode, Decode không phải chỉ JSON mới có thể làm được. ở Foundation cũng đã có PropertyListEndcoder , PropertyListDecoder.
Ngoài ra, việc sử dụng một Protocol Decoder Encoder độc lập , với lợi ích mà Codable mang lại , chúng ta có thể tuỳ ý xử lý biến đổi dữ liệu một cách an toàn.

Vì vậy mà hôm nay để hiểu hơn về cơ chế hoạt động của Decoder, chúng ta hãy cùng thực hiện thử decode file CSV (có dấu phẩy phân biệt giữa các data) nhé.
Cách làm của tôi đó là vừa tham khảo phần code JSONEncoder/Decoder PlistEncoder/Decoder đã có vừa viết dần dần code xử lý file CSV.

Để đơn giản hoá file code, những tính năng mở rộng hay những phần xử lý nằm ngoài ví dụ đều được giản lược đi. Vì vậy chúng ta có thể nhìn kết cấu phần Decoder một cách dễ dàng và đơn giản hơn.

At WWDC 2017, Apple has introduced the new feature in Swift to parse JSON without any pain using Swift Codable protocol. There is talk available to watch on Whats New in Foundation, you can watch about this new featured from 23 min onwards. Basically, this protocol has the combination of Encodable and Decodable protocol that can be used to work with JSON data in both directions. In summary, Swift Codable protocol has offered following things to us.
* Sử dụng  Codable
Using Codable, we can model JSONObject or PropertyList file into equivalent Struct or Classes by writing very few lines of code. We don’t have to write the constructor for the properties in the objects. It’s all handed by Codable. We just need to extend our model to conform to the Codable, Decodable or Encodable protocol.

Đầu tiên mọi người có thể xem link [json](("https://api.github.com/search/users?q=dung")) ở đây  **dung** là 1 cái parameter mà mình để  thôi các bạn có thể để bất cứ tên gì mà các bạn muốn 


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
Điều đầu tiên bạn cần phải biết 

### Bắt đầu parse json nào 
Đầu tiên chúng ta cần import thư viện thông qua ![cocopods](https://cocoapods.org)

``` 
pod 'Alamofire', '~> 5.0.0-rc.3'

```

Chúng ta sẽ tạo 1 file model có tên là  ***User***   

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
Lưu ý các properties trong Model phải trùng khớp với các key value trong JSON data.



👉🏼 Tiếp theo chúng ta tạp 1 file có tên là ***DataService** trong file này chúng ta sẽ viết 1 class , trong class có chứa 1 closure  

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
Chúng ta sẽ tạo một file cell để hiển thị thông tin lên ***Tabel***  có tên là  **DasboardCell** 
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

Trong file **ViewController**



Bài viết này có thể còn nhiều thiếu sót mong các cao nhân góp ý giúp em, để em có thể cải thiện bài viết sau hơn, mọi thông tin góp ý xin gửi về ![phamtrungkiendev@gmail.com]()
