- Database, Collection, Document sẽ được tạo ngầm (tự động) khi bắt đầu lưu trữ dữ liệu => Đơn giản

- mongod - Chạy MongoDB Server
- mongod --port x - Chạy MongoDB Server tại Port x
- mongo - Kết nối với MongoDB Server
- mongo --port x - Kết nối với MongoDB Server tại Port x

- show dbs - Hiển thị danh sách Database
- show collections - Hiển thị danh sách Collection trong Database hiện tại
- use <db_name> - Chuyển sang Database db_name (Nếu không tồn tại sẽ được tạo khi bắt đầu chèn dữ liệu)
- db.<collecion_name>.insertOne({}) - Chèn 1 Document vào Collection collection_name

- JSON Data: Cấu trúc giống 1 JS Object, nhưng Key Name cần được đặt trong ""
- Document mới được chèn vào Collection sẽ tự động được gán 1 Unique Id với kiểu dữ liệu ObjectId tại trường "\_id"
- db.<collecion_name>.find() - Hiển thị toàn bộ Document trong Collection
- db.<collecion_name>.find().pretty() - Hiển thị toàn bộ Document trong Collection (được định dạng để dễ đọc hơn)

- MongoDB thực chất lưu trữ BSON (Binary Data)
- Khi thêm Document, Key Name có thể bỏ qua "", miễn là không chứa khoảng trắng
- Các Document trong cùng một Collection không nhất thiết phải có cùng 1 Schema (các trường có thể bị thiếu, khác,...)
- Có thể gán giá trị cho trường "\_id" thủ công, nhưng cần đảm bảo giá trị đó là duy nhất

- Filter có dạng: {field_name: field_value}
- $ - Đánh dấu một Reserved Word trong MongoDB
- $set - Mô tả thay đổi trong câu lệnh updateOne

- db.fightData.find({distance: {$gt: 10000}})
- db.<collecion_name>.findOne() - Hiển thị 1 Document đầu tiên trong Collection thỏa mãn điều kiện

- update() - Có thể không sử dụng $set. Khi không sử dụng $set, ghi đè (thay thế) Document với giá trị được sử dụng để cập nhật, chỉ giữ nguyên \_id

- it - Hiển thị thêm kết quả từ câu lệnh find()
- find() trả về một Cursor
- Cursor - Object đặc biệt cho phép duyệt qua từng khối Document kết quả thay vì toàn bộ Document
- Mặc định, find() chỉ hiển thị tối đa 20 Document đầu tiên
- db.<collecion_name>.find().toArray() - Chuyển tất cả Document thành 1 Array
- db.<collecion_name>.find().forEach((x) => {printjson(x)}) - Hiển thị tất cả Document
- pretty() chỉ hoạt động với Cursor (do đó findOne() không thể sử dụng pretty() vì không trả về Cursor,...)

- Projection - Cho phép tùy chọn giới hạn những field cần thiết trong kết quả trả về để tránh những thông tin từ những field không cần thiết
- db.<collecion_name>.find({}, {field_name: [0|1]})
- Mặc định, \_id luôn được trả về. Có thể loại bỏ \_id trong kết quả trả về bằng cách đặt giá trị Projection cho \_id là 0

- Embedded Document - Giới hạn 100 Levels of Nesting và tối đa 16MB / Document

- Có thể tìm kiếm trong Array với chỉ 1 giá trị có thể xuất hiện trong Array đó - db.<collecion_name>.find({hobbies: "sports"}) (hobbies: ["sports", "cooking"])
- Để truy cập Nested Object cần sử dụng "" - db.<collecion_name>.find({"status.description": "on-time"})
