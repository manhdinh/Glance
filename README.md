# Glance trong OpenStack
##.Vai trò của Glance trong Open Stack
Glance trong OpenStack là một project có nhiệm vụ chính là lưu trữ các file image để tạo instance.Bài viết trình bày [Tổng quan về kiến trúc và cách hoạt động của Glance](https://github.com/manhdinh/Glance/blob/master/Glance.md).
- Khi làm việc với Glance, cần lưu ý và hiểu rõ về 3 phần sau : 
<ul>
  + [Glance Format](https://github.com/manhdinh/Glance/blob/master/Glance%20Disk%20Format.md) : Khi thêm 1 image vào Glance cần phải định nghĩa disk_format và container format cho Image Disk Virtual Machine
  + [Glance Image Cache](https://github.com/manhdinh/Glance/blob/master/Glance%20Image%20Cache.md) : Giúp cho việc lấy file image boot lên máy ảo trở nên nhanh chóng hơn nhờ việc lấy thẳng image trên glance mà ko cần xuống backend.
  + [Glance AuthN and AuthZ](https://github.com/manhdinh/Glance/blob/master/Glance%20AuthN%20and%20AuthZ.md) : Các bước xác thực và ủy quyền trong Glance với KeyStone
  </ul>
