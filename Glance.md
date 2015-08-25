#I.Kiến trúc tổng quan về Glance
<li>Glance Project cung cấp dịch vụ nơi mà người dung có thẻ upload và tìm ra những data hiện có mà có thể được sử dụng với những dịch vụ khác.( Image và metadata )</li>
<li>Dịch vụ Glance image bao gồm việc tìm, ghi và lấy lại những file image của VM.Glance có 1 RESTful API có thể nhận yêu cầu của VM image metadata cũng như lấy lại file image thật.
<li>VM image có sẵn thông qua Glance có thể được lưu trữ ở trong nhiều chỗ khác nhau từ những file hệ thống đơn giản tới object-storage systems như là Swift project.</li>
Glance được viết với những thiết kế sau :
<ul>
<li>Component based architecture : nhanh chóng add những behavior mới</li>
<li>Highly available : Chia những khối lượng công việc quan trọng.</li>
<li>Fault tolerant : Quy trình được độc lập để tránh các sự cố.</li>
<li>Recoverable : Hỏng hóc có thể dễ dàng chuẩn đoán,sửa lỗi và khắc phục.</li>
<li>Open standard : Thực hiện than chiếu cho community-driven api
</ul>
Mô hình kiến trúc của Glance
http://docs.openstack.org/developer/glance/_images/architecture.png
<li>A client - any application that uses Glance server.</li>
<li>REST API - exposes Glance functionality via REST.</li>
<li>Database Abstraction Layer (DAL) - an application programming interface which unifies the communication between Glance and databases.</li>
<li>Glance Domain Controller - middleware that implements the main Glance functionalities: authorization, notifications, policies, database connections.</li>
<li>Glance Store - organizes interactions between Glance and various data stores.
Registry Layer - optional layer organizing secure communication between the domain and the DAL by using a separate service.</li>
