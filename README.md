Difference-comand-useradd-and-adduser-
======================================

Khái quát về tài khoản trong linux và sự khác nhau giữa 2 cách tạo tài khoản 'useradd' và 'adduser'

Mục lục

1. Khái niệm

2. Các tạo người sử dụng

=========
##### 1. Khái niệm
Linux là một nền tảng sử dụng đa người dùng nên trong Linux có thể tạo nhiều người sử dụng. Mỗi ngưởi sử dụng được đặc chưng bởi một tài khoản đăng nhập hệ thống (account) và một password.

Có 3 loại tài khoản: 
- Siêu tài khoản: root. được gọi là siêu tài khoản vì nó có quyển lực cao nhất, nó có thể can thiệt vào mọi việc trong hệ thống
- Ngưởi sử dụng bình thường: được cấp một tài khoản và password để có thể thực hiện quyền sử dụng trên các hệ thống và bị hạn chế về quyền lực
- Tài khoản nobody: tài khoản này để chạy các chương trình dịch vụ trên hệ thống, tài khoản này không có thư mục home và môi trường shell để làm việc
**Chỉ có tài khoản root mới có thể tạo ra người sử dụng**

<img class="image__pic js-image-pic" src="http://i.imgur.com/rgXIDZx.png" alt="" id="screenshot-image">

- Các khái niệm liên quan:

###### a. Chỉ số UID
UID (User ID) là một số nguyên dương đại diện cho từng người sử dụng. Để xem UID của người sử dụng ta dùng câu lệnh sau

```
# vi /etc/passwd
```
<img class="image__pic js-image-pic" src="http://i.imgur.com/QceCKN0.png" alt="" id="screenshot-image">

###### b. Chỉ số GID
GID (Group ID): Group là một nhóm gồm nhiều tài khoản. Trong Linux có thể tạo ra nhiều group và trong mỗi group chứa một số lượng tài khoản người dùng:
VD: group "congnhan" chứa người dùng là công nhân
    group "vanphong" chứa người dùng làm văn phòng

<img class="image__pic js-image-pic" src="http://i.imgur.com/QceCKN0.png" alt="" id="screenshot-image">

#### 2. Cách tạo người sử dụng

Để có thể tạo được tài khoản trong Linux nhất thiết bạn phải đăng nhập bằng tài khoản root. Xét riêng trường hợp tạo tài khoản trong Linux bằng câu lệnh có 2 cách được sử dụng: useradd và adduser. Tôi sẽ sử dụng cả 2 câu lệnh này để tạo tài khoản và chỉ ra sự khác nhau giữa 2 câu lệnh này.

**Lưu ý: để có thể thấy rõ sự khác nhau giữa hai câu lệnh bạn nên sử dụng Linux có phiên bản là Ubuntu**

###### a. Sử dụng lệnh useradd

Tạo tài khoản:
```
#useradd [option] <Tên tài khoản>
```

*Trong đó:*Trường option bao gồm các tùy chọn

|Tùy chọn | Ý nghĩa |
|---------|---------|
|-p | nhập password cho tài khoản |
|-c | thêm thông tin cho tài khoản |
|-d | chỉ đường dẫn chưa thư mục home của tài khoản, nếu không chỉ định thì mặc định nó sẽ tạo thư mục tại /home |
|-g | chỉ ra nhóm tài khoản muốn thuộc, nếu không chỉ mặc định nó sẽ tạo ra một group để cho tài khoản đó vào |
|-s | xác định shell cho hệ thống, mặc định là /bin/bash |
|-u | xác định chỉ số UID của người dùng |
|-e | có định dạng là yyyy-mm-dd xác định thời gian hệ hạn của tài khoản |
|-f | yyyy-mm-dd xác định số ngày password sẽ vô hiệu hóa khi tài khoản hết hạn |

Đây là một số tùy chọn thường được sử dụng. Ngoài ra nó còn một số các tùy chọn khác nữa, bạn có thể dùng command để biết thêm các tùy chọn khác ` man useradd `.

VD: #useradd -c 'Nguyen Hoai Nam' -d /home/hoainam -e 2014-12-11 -p admin1234 hoainam

###### b. Sử dụng lệnh adduser

```
#adduser <tên tài khoản>
```
Sau khi nhập xong câu lệnh lúc này hệ thống sẽ hiện ra các câu hỏi để bạn có thể nhập vào như thông tin về mật khẩu, tên, địa chỉ nhà, số điện thoại,...kết thúc quá trình hệ thống sẽ hỏi về xác thực nếu bạn cho yes thì  một tài khoản sẽ được tạo với những thông tin bạn khai báo nếu chọn no quá trình tạo tài khoản sẽ hủy

<img class="image__pic js-image-pic" src="http://i.imgur.com/JSFKSIC.png" alt="" id="screenshot-image">

#### 3. Sự khác nhau giữa 2 câu lệnh

  Khi bạn dùng phiên bản Debian tiêu biểu là Ubuntu bạn sẽ thấy rõ sự khác nhau giữa 2 câu lệnh này. Câu lệnh useradd sử dụng tất cả các thông số mà khi người root nhập vào để tạo tài khoản. Còn đối với cách tạo sử dụng câu lệnh adduser hệ thống sẽ tương tác trực tiếp với người tạo để đưa ra các câu hỏi. Qua đó giúp người sử dụng dễ dàng tạo hơn. Còn về quan điểm cá nhân tôi thích các sử dụng useradd hơn vì đơn giản là nó sẽ phát huy được tác dụng khi tôi viết một scrips.
  
  Còn đối với phiên bản như Centos. sự khác nhau ở đây là ít hơn. Lúc đó khi sử dụng adduser hệ thống sẽ tạo luôn một tài khoản và bạn cần thực hiện thêm một số câu lệnh để có thể thêm mật khẩu và thông tin liên quan

#### 4. Một số lệnh liên quan

Đối với nhóm lênh này bạn phải vào tài khoản root để có thể thực hiện được

- Tạo group:
```
#groupadd <Tên group>
```
- Xóa group
```
#groupdel <Tên group>
```
- Xóa tài khoản người dùng
```
#userdel <Tên tài khoản người dùng>
```
- Chỉnh sửa thông tin người dùng
```
#usermod [option] [Nội dung chỉnh sửa] <Tài khoản người dùng>
```
Với trường option và và nôi dụng bạn muốn chỉnh sửa.
VD: Chỉnh sửa lại thư mục home của tài khoản 'hoainam'
```
#usermod -c 'Nguyen Van Nam' hoainam
```

#usermod
- Thay đổi password cho tài khoản người dùng
Đối với câu lệnh passwd bạn có thể thay đổi tài khoản của chính bạn hoặc có thể đăng nhập bằng tài khoản root để thay đổi tài khoản bất kì của người dùng
```
#passwd <Tên tài khoản người dùng>
```
Sau đó hệ thống sẽ hỏi bạn thông tin về password mới

#### 5. Kết luận:

Bài viết ngày hôm nay tôi điêm quan cho các bạn năm lại về các loại tài khoản người dùng trong Linux và tìm hiểu một thông số UID GID và sự khác nhau giữa 2 cách tạo tài khoản trong linux và các vấn đề như chỉnh sửa, xóa đối với tài khoản. Hi vọng các bạn đọc xong bài viết này sẽ reveiw lại kiến thức cũng như bổ sung thêm kiến thức. Thân!!!
Các bạn có thể liên hệ với tôi qua skype `namptit307` để cùng nhau chia sẻ.












