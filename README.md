# Glance
Tổng quan về kiến trúc và cách hoạt động của Glance.3 phần cần chú ý trong Glance: 
  + Glance Disk Format : Khi thêm 1 image vào Glance cần phải định nghĩa disk_format và container format cho Image Disk Virtual Machine
  + Glance Image Cache : Giúp cho việc lấy file image boot lên máy ảo trở nên nhanh chóng hơn nhờ việc lấy thẳng image trên glance mà ko cần xuống backend.
  + Glance AuthN and AuthZ : Các bước xác thực và ủy quyền trong Glance với KeyStone
