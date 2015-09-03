# Glance trong OpenStack
##Vai trò của Glance trong Open Stack
Glance trong OpenStack là một project có nhiệm vụ chính là lưu trữ các file image để tạo instance.Khi kết hợp với Nova và Swift, Glance có thể cung cấp giải pháp end-to-end cho việc quản lí các disk image cho hạ tầng cloud.
##.[Kiến trúc tổng quan về Glance](https://github.com/manhdinh/Glance/blob/master/Glance.md)
- 1.Mô hình kiến trúc của Glance
<img src="https://camo.githubusercontent.com/98e3755c1fc01a71fd2a499845839a3df501cd0f/687474703a2f2f696c6561726e737461636b2e66696c65732e776f726470726573732e636f6d2f323031332f30342f676c616e63652e706e673f773d33303026683d333030">
+ Glance-API : chiu trách nhiệm nhận các API calls cho việc truy xuất, lưu trữ image...
+ Glance-registry : Lưu trữ processes và lấy về các metadata về image( size, type...)
+ Glance-database: Database lưu trữ về các image metadata
+ Glance-stores: Thành phần lưu trữ image: có thể sử dụng file system, S3, Swift...
- 2.Cách thức hoạt động trong Glance
<img src="https://camo.githubusercontent.com/052568e3b0e91d7e956624c97c7ae167d1895cec/687474703a2f2f646f63732e6f70656e737461636b2e6f72672f646576656c6f7065722f676c616e63652f5f696d616765732f6172636869746563747572652e706e67">
+ 1.Khi có client muốn làm việc với Glance, keystone sẽ xác thực người dùng đó là ai ( AuthN ), khi xác thực đúng thì Client sẽ thực hiện 1 call API thông qua REST API tới Glance Domain Controller ( DGC ) .
+ 2.GDC thực hiện xác nhận quyền của Client với Keystone, sau đó làm việc với Glance DB, các việc này thông qua 3 lớp Auth Notifier Policy Quota Location DB, Registry Layer và DAL để lấy các metadata về file image cần làm việc.
+ 3.Sau khi xác thực và lấy được thông tin về image cần dùng, Auth Notifier Policy Quota Location DB sẽ chọc xuống Glance Store, sau khi xác thực người dùng và quyền, Glance Store sẽ trả về file image cần thiết.
- Khi làm việc với Glance, cần lưu ý và hiểu rõ về 3 phần sau : 
<ul>
  + [Glance Format](https://github.com/manhdinh/Glance/blob/master/Glance%20Disk%20Format.md) : Khi thêm 1 image vào Glance cần phải định nghĩa disk_format và container format cho Image Disk Virtual Machine
  + [Glance Image Cache](https://github.com/manhdinh/Glance/blob/master/Glance%20Image%20Cache.md) : Giúp cho việc lấy file image boot lên máy ảo trở nên nhanh chóng hơn nhờ việc lấy thẳng image trên glance mà ko cần xuống backend.
  + [Glance AuthN and AuthZ](https://github.com/manhdinh/Glance/blob/master/Glance%20AuthN%20and%20AuthZ.md) : Các bước xác thực và ủy quyền trong Glance với KeyStone
  </ul>
