- mongod --auth - Chạy MongoDB Server với tùy chọn Authentication
- db.auth("username", "password") - Login
- mongo -u username -p password --authenticationDatabase db_name - Login
- Khi chưa có User nào trong hệ thống, được phép tạo 1 User duy nhất với quyền Admin
  use admin
  db.createUser({user: "username", pwd: "password", roles: ["userAdminAnyDatabase"]})

- db.logout() - Log out
- Mặc định, User được gán với Database nào sẽ chỉ có quyền thực hiện những thao tác tương ứng trong Database đó

- db.updateUser("appdev", {roles: ["readWrite", {role: "readWrite", db: "blog"}]}) - Cập nhật Role và Database mà User có quyển thao tác
- db.getUser("username") - Hiển thị thông tin User
