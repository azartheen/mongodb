- mongod --help - Hiển thị danh sách Command cấu hình MongoDB Server

- mongod --dbpath ./db --logpath ./logs/log.log - Config nơi lưu trữ Data File và Log File

- mongod --fork --logpath ./logs/log.log - Chạy MongoDB Server ở Background (câu lệnh chỉ khả dụng trên MacOS và Linux)
- db.shutdownServer() - Shutdown MongoDB Server

- mongod -f ./bin/mongod.cfg - Chạy MongoDB Server với thiết lập trong Config File

- mongo --help - Hiển thị danh sách Command cấu hình Shell
- mongo -> help - Hiển thị danh sách Command thao tác với Shell
- db.help() - Hiển thị danh sách Command thao tác với Database
- db.<collection_name>.help() - Hiển thị danh sách Command thao tác với Collection
