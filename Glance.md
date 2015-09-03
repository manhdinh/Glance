###I.Giới thiệu về Glance.
  Glance cung cấp lưu trữ và truy vấn các virtual disk image. Glance được thiết kế để là một dịch vụ độc lập sử dụng cho việc   tổ chức lưu trữ image, tuy nhiên khi kết hợp với Nova và Swift, nó cung cấp giải pháp end-to-end cho việc quản lí các disk   image cho hạ tầng cloud.

###II.Kiến trúc tổng quan về Glance
* 1.
* Glance Project cung cấp dịch vụ nơi mà người dung có thẻ upload và tìm ra những data hiện có mà có thể được sử dụng với những dịch vụ khác.( Image và metadata )
* Dịch vụ Glance image bao gồm việc tìm, ghi và lấy lại những file image của VM.Glance có 1 RESTful API có thể nhận yêu cầu của VM image metadata cũng như lấy lại file image thật.
* VM image có sẵn thông qua Glance có thể được lưu trữ ở trong nhiều chỗ khác nhau từ những file hệ thống đơn giản tới object-storage systems như là Swift project.
* Glance được viết với những thiết kế sau :
<ul>
<li>Component based architecture : nhanh chóng add những behavior mới</li>
<li>Highly available : Chia những khối lượng công việc quan trọng.</li>
<li>Fault tolerant : Quy trình được độc lập để tránh các sự cố.</li>
<li>Recoverable : Hỏng hóc có thể dễ dàng chuẩn đoán,sửa lỗi và khắc phục.</li>
<li>Open standard : Thực hiện than chiếu cho community-driven api.</li>
</ul>
Mô hình kiến trúc của Glance

<ul>
<img src="http://ilearnstack.files.wordpress.com/2013/04/glance.png?w=300&h=300" >
</ul>

* Glance-API : chiu trách nhiệm nhận các API calls cho việc truy xuất, lưu trữ image...
<ul> 
<li> Store image: POST/image : lưu trữ image và sau đó trả về metadata của image</li>
<li> Dowload image: GET/image/<id>: lấy image được chỉ thị bởi <id> </li>
<li> Update image: PUT/image/<id>: cập nhật metadata hoặc dữ liệu xác định cụ thể bởi <image> </li>
<li> Delete image: DELETE/image/<id>: xóa image cụ thể bởi <id> </li>
<li> List image: GET/image: trả về id, name, disk_format, container_format …..</li>
<li> Image details: HEAD/image/<id>: trả về toàn bộ metadata của image xác định bởi <id></li>
</ul>
* Glance-registry : Lưu trữ processes và lấy về các metadata về image( size, type...)
<ul>
</ul>
* Glance-database: Database lưu trữ về các image metadata
<ul>
</ul>
* Glance-stores: Thành phần lưu trữ image: có thể sử dụng file system, S3, Swift...
<ul>
</ul>
<ul>
<img src="http://docs.openstack.org/developer/glance/_images/architecture.png" >
</ul>
* Các bước hoạt động:
<ul>
<li>1.Khi có client muốn làm việc với Glance, keystone sẽ xác thực người dùng đó là ai ( AuthN ), khi xác thực đúng thì Client sẽ thực hiện 1 call API thông qua REST API tới Glance Domain Controller ( DGC ) .</li>
<li>2.GDC thực hiện xác nhận quyền của Client với Keystone, sau đó làm việc với Glance DB, các việc này thông qua 3 lớp Auth  Notifier Policy Quota Location DB, Registry Layer và DAL để lấy các metadata về file image cần làm việc.</li>
<li>3.Sau khi xác thực và lấy được thông tin về image cần dùng, Auth  Notifier Policy Quota Location DB sẽ chọc xuống Glance Store, sau khi xác thực người dùng và quyền, Glance Store sẽ trả về file image cần thiết.</li>
</ul>
#III.	Một số lệnh về glance
<ul>
 
<li>1.	glance image-create : Tạo image	 --id <IMAGE_ID> ID
<ul>

			<li>--name <NAME>	Tên của image	
			<li> --store <STORE>		
			<li> --disk-format <DISK_FORMAT>	format disk của image: raw, qcow2, vmdk ……	
			<li> --container-format <CONTAINER_FORMAT>	format Container của image: bare, ami, ovf …..	
			<li>--owner <TENANT_ID>	id của Tennant sở hữu image	
			<li> --size <SIZE>	Kích thước của image data (bytes)	
			<li> --min-disk <DISK_GB>	Size nhỏ nhất của disk mà image cần để boot (gigabytes)	
			<li> --min-ram <DISK_RAM>	Lượng ram nhỏ nhất cần để boot image (megabyts)	
			<li> --location <IMAGE_URL>		
			<li> --file <FILE>	file local chứa disk image được upload trong quá trình tạo	
			<li> --is-public {True,False}	Chọn True = mọi tennant có thể sử dụng image này	
			<li> --is-protected {True,False}	Ngăn chặn image bị xóa	
			<li>--progress	Hiển thị thanh tiến trình tải image lên	
			<li> --human-readable	Hiển thị size image (MB)	
			<li> --copy-from <IMAGE_URL>	Link download image từ mạng	
</ul>
</li>					
<li>2.	glance image-delete : Xóa image	glance image-delete id<id image>	</li>	

<li>3.	glance image-list : In ra danh sách các image	 --name <NAME>	Hiển thị danh sách các image có tên <NAME>

			 --status <STATUS>	Hiển thị danh sách các image có cùng <STATUS>	
			 --container-format <CONTAINER_FORMAT>	Hiển thị danh sách các image có cùng <CONTAINER_FORMAT>	
			 --disk-format <DISK_FORMAT>	Hiển thị danh sách các image có cùng <DISK_FORMAT>	
			 --size-min <SIZE>	Hiển thị danh sách các image có <SIZE> >=	
			 --size-max <SIZE>	Hiển thị danh sách các image có <SIZE> <=	
			 --human-readable	Hiển thị danh sách các image có sử dụng <--human-readable	
			 --page-size <SIZE>		
			 --is-public {True,False}	Hiển thị danh sách các image có cùng --is-public {True,False}	
			 --owner <TENANT_ID>	Hiển thị danh sách các image cùng thuộc 1 <TENANT_ID>	
			 --all-tenants	Hiển thị danh sách tất cả các image ko phân biệt tennant	
<li>4.	glance image-show : Mô tả image cụ thể	<IMAGE>	Tên hoặc id của image	
<li>5.	glance image-update	: Update thông tin image	<IMAGE>	Tên hoặc id của image muốn thay đổi	
			 --name <NAME>D35		
			 --disk-format <DISK_FORMAT>		
			 --container-format <CONTAINER_FORMAT>		
			 --owner <TENANT_ID>		
			 --size <SIZE>		
			 --min-disk <DISK_GB>		
			 --min-ram <DISK_RAM>		
			 --copy-from <IMAGE_URL>		
			 --is-public {True,False}		
			 --is-protected {True,False}		
			 --human-readable		
			 --progress		
<li>6.	glance member-create	: Share image cho 1 tenant	<IMAGE>	Tên hoặc id của image	
			<TENANT_ID>	Id của Tennant add làm member	
			 --can-share	Cho phép Tenant share image	
<li>7.	glance member-delete <IMAGE> <TENANT_ID>	: Remove image được share cho 1 tennant			
<li>8.	glance member-list [--image-id <IMAGE_ID>] [--tenant-id <TENANT_ID>] : Mô tả danh sách các tennant được share image	
			<li>--tenant-id <TENANT_ID>	Lọc kết quả thei Tennant id	</li>
			<li> --image-id <IMAGE_ID>	Lọc kết quả theo image id	</li>


