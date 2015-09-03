Glance image cache
<ul>
<li>Trên glance có thể cấu hình glance image cache là bộ nhớ đệm trong glance để lưu 1 bản sao của image.</li>
<li>Glance image cache giúp cho việc lấy file image boot lên máy ảo trở nên nhanh chóng hơn nhờ việc lấy thẳng image trên glance mà ko cần xuống backend. </li>
<li>Glance image cache được cấu hình trong file glance-api.conf
<ul>
 flavor = keystone+cachemanagement
 </ul>
 </li>
	
<li>Sau khi cấu hình và image được boot lên máy ảo, glance sẽ tự động lưu lại file image đó trong /var/lib/glance/image-cache </li>
<li>Kiểm tra bằng câu lệnh:  glance-cache-manage list-cached</li>
<li>Mỗi file cache có thể cấu hình size tối đa trong glance-cache.conf. Khi bộ nhớ cache đã đầy nó sẽ tự động xóa các cache </li>
