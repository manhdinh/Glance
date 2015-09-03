<li>Khi thêm một image vào Glance phải định nghĩa disk_format và container format cho Image Disk Virtual Machine </li>

#1.Disk Format 
Là định dạng của ổ đĩa máy ảo

Bạn có thể set theo những định dạng sau đây
<ul>

- raw
 + Là định dạng image không có cấu trúc. 
 + Khi khởi tạo một máy ảo có disk format là raw thì dung lượng của file disk sẽ đúng bằng dung lượng của ổ đĩa máy ảo bạn đã tạo
- vhd
 + Là định ổ đĩa chung được sử dụng bởi một số virtual machine monitor VMWare, Xen, Microsoft, VirtualBox...
- vmdk
 + Một định dạng khác của ổ đĩa được hỗ trợ bởi nhiều virtual machine monitor  
- vdi
 + Một định dạng được hỗ trợ bởi VirtualBox và QEMU Emulator
- iso 
 + Một định dạng lưu trữ cho nội dung dữ liệu của đĩa quan (CDROM ..) 
- QCOW2
 + Một định dạng được QEMU Emulator phát triển nó có thể tự động tăng bộ nhớ (Máy ảo dùng bao nhiêu file có dung lượng bấy nhiêu).
 + Hỗ trợ copy-on-write (Một kỹ thuật snapshot trong KVM được ứng dụng trong Openstack). Khi khởi tạo máy ảo mới sẽ dựa vào disk này rồi snapshot thành một máy mới.

#2.Container Format 
Chứa thông tin định dạng ổ đĩa ảo mô tả phần cứng ổ đĩa đó sử dụng. Khi một máy ảo được boot lên nó sẽ thông qua file này để xem những phần cứng nào nó sẽ sử dụng(card mạng, disk location...)

- bare
 + Biểu thị không có container và disk format cho disk
- ovf
 + Là định dạng ovf container. Mô tả các thuộc tính của máy ảo. Nó viết dựa trên định dạng XML
- ova 
 + OVA là một file ovf được đóng gói
- aki
 + Được lưu ở Glance là Kernel Image của Amazon
- ari
 + Được lưu ở Glance là Ramdisk Image của Amazon
- ami
 + Được lưu ở Glance là Machine Image của Amazon
