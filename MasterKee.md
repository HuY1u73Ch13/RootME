## Bối cảnh
* Bài này dựa trên CVE-2023-32784, CVE này được phát hiện trong KeePassWordSafe thì KeePassWordSafe là trình quản lý mật khẩu phổ biến cho người dùng Window, Linux, MacOS và cả nhứng người dùng trên thiết bị di động
* Tức là bạn lưu mật khẩu vào keepass ứng dụng này sẽ tạo ra một chuỗi kí tự tạm thời trong bộ nhớ ram để xử lý. Trước bản 2.54 chuỗi này không được xóa ngay lập tức sau khi dùng xong.
* Nên nếu ai đó có thể dump bộ nhớ Ram họ có thể tìm thấy được mật khẩu mà bạn vừa nhập
* Thông qua CVE trên thì tôi làm tìm được `https://github.com/vdohney/keepass-password-dumper` để có thể revert lại mật khẩu của tôi nên tôi đã thử dùng tool này
* `PS C:\Users\Admin\keepass-password-dumper> dotnet "C:\Users\Admin\keepass-password-dumper\bin\Debug\net6.0\keepass_password_dumper.dll" "D:\Downloands\ch45\MasterKee.DMP"`
* Với command trên tôi đã có mật khẩu
* <img width="1004" height="41" alt="image" src="https://github.com/user-attachments/assets/c76b6173-5163-4d4f-bd7f-012d8344fb45" />
* Tuy nhiên thì ký tự đầu tiên chúng ta cần burpforce nó và chúng ta còn file kdbx chúng ta chưa xài.
* 
