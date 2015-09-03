<img src="https://slack-files.com/files-tmb/T02QZ38QK-F0A3GHW2U-402f4a89bf/screenshot_1_360.png">
###Quy trình hoạt động
  + Bước 1 : Client sẽ phải xác thực với Keystone để nhận token ( AuthN lần 1 ) 
  + Bước 2 : Glance mang token hỏi lại Keystone để xác định Client đó có được phép làm việc với Glance không và nếu được thì sẽ làm việc với phần nào ( AuthZ lần 1 )
  + Bước 3 : Khi Client có đủ quyền thì sẽ được dùng đến Glance Store Drivers, tuy nhiên Glance Store Drivers sẽ AuthN lần 2 ( kiểm tra list user trong database ), và AuhtZ lần 2 ( kiểm tra các role trong file json.policy ) 
