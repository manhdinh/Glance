#I.Giới thiệu về Glance.
<ul>
Glance cung cấp lưu trữ và truy vấn các virtual disk image. Glance được thiết kế để là một dịch vụ độc lập sử dụng cho việc tổ chức lưu trữ image, tuy nhiên khi kết hợp với Nova và Swift, nó cung cấp giải pháp end-to-end cho việc quản lí các disk image cho hạ tầng cloud.
</ul>
#II.Kiến trúc tổng quan về Glance
<li>Glance Project cung cấp dịch vụ nơi mà người dung có thẻ upload và tìm ra những data hiện có mà có thể được sử dụng với những dịch vụ khác.( Image và metadata )</li>
<li>Dịch vụ Glance image bao gồm việc tìm, ghi và lấy lại những file image của VM.Glance có 1 RESTful API có thể nhận yêu cầu của VM image metadata cũng như lấy lại file image thật.
<li>VM image có sẵn thông qua Glance có thể được lưu trữ ở trong nhiều chỗ khác nhau từ những file hệ thống đơn giản tới object-storage systems như là Swift project.</li>
Glance được viết với những thiết kế sau :
<ul>
<li>Component based architecture : nhanh chóng add những behavior mới</li>
<li>Highly available : Chia những khối lượng công việc quan trọng.</li>
<li>Fault tolerant : Quy trình được độc lập để tránh các sự cố.</li>
<li>Recoverable : Hỏng hóc có thể dễ dàng chuẩn đoán,sửa lỗi và khắc phục.</li>
<li>Open standard : Thực hiện than chiếu cho community-driven api.</li>
</ul>
Mô hình kiến trúc của Glance
<ul>
http://docs.openstack.org/developer/glance/_images/architecture.png
</ul>
<ul>
http://ilearnstack.files.wordpress.com/2013/04/glance.png?w=300&h=300
</ul>

Glance-API : chiu trách nhiệm nhận các API calls cho việc truy xuất, lưu trữ image...
<ul> 
<li> Store image: POST/image : lưu trữ image và sau đó trả về metadata của image</li>
<li> Dowload image: GET/image/<id>: lấy image được chỉ thị bởi <id> </li>
<li> Update image: PUT/image/<id>: cập nhật metadata hoặc dữ liệu xác định cụ thể bởi <image> </li>
<li> Delete image: DELETE/image/<id>: xóa image cụ thể bởi <id> </li>
<li> List image: GET/image: trả về id, name, disk_format, container_format …..</li>
<li> Image details: HEAD/image/<id>: trả về toàn bộ metadata của image xác định bởi <id></li>
</ul>
Glance-registry : Lưu trữ processes và lấy về các metadata về image( size, type...)
<ul>
Glance-database: Database lưu trữ về các image metadata
</ul>
<ul>
Glance-stores: Thành phần lưu trữ image: có thể sử dụng file system, S3, Swift...
</ul>
