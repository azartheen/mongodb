- Index - Nguyên lý tương tự với SQL

- db.<collection_name>.explain().find() - Hiển thị thông tin về "Plan" MongoDB sẽ thực hiện với câu lệnh truy vấn
- db.<collection_name>.explain("executionStats").find() - Hiển thị thông tin chi tiết về về "Plan" MongoDB sẽ thực hiện với câu lệnh truy vấn và kết quả sẽ được trả về như thế nào
- db.contacts.createIndex({"dob.age": 1}) - Tạo Index trên Field age nằm trong Field dob của Collection contacts với thứ tự sắp xếp tăng dần (thứ tự giảm dần với -1)
- IXSCAN chỉ trả về Key cùng Pointer tương ứng trong Index thỏa mãn điều kiện. Từ các giá trị này, MongoDB FETCH Document dựa trên Pointer tương ứng

- db.contacts.dropIndex({"dob.age": 1}) - Drop Index
- Trong trường hợp truy vấn phần lớn hoặc toàn bộ Document, Index có thể làm chậm quá trình. Index hiệu quả với những truy vấn với một phần (nhỏ) số lượng Document

- db.contacts.createIndex({"dob.age": 1, gender: 1}) - Tạo Compound Index (Index với nhiều hơn 1 Field, thứ tự các Field quan trọng) (bản chất Compound Index sẽ sắp xếp Key theo các Field với thứ tự lần lượt ngoài cùng từ trái sang trong khai báo)
- Có thể sử dụng Compound Index mà không cần tới tất cả các Field được định nghĩa (chỉ sử dụng các Field theo thứ tự ngoài cùng từ trái sang trong khai báo Compound Index)

- ...find({"dob.age": 35}).sort({gender: 1})
- Có thể sử dụng thứ tự của Key trong Index để tối ưu hóa thao tác sắp xếp các Document tương ứng (với số lượng Document lớn) (một vài trường hợp không thể hoàn thành sắp xếp nếu số lượng Document quá lớn, khi đó sử dụng Index không chỉ tối ưu hóa mà còn đảm bảo có thể hoàn tất thao tác sắp xếp)

- db.<collection_name>.getIndexes() - Hiển thị tất cả Index
- Mặc định, \_id Field được tự động tạo Index

- db.contacts.createIndex({"dob.age": 1}, {unique: true}) - Tạo Index với ràng buộc Unique (những thao tác trên Document vi phạm ràng buộc duy nhất sẽ không được thực thi), đảm bảo Collection chỉ chứa những Document với Field xác định có giá trị duy nhất

- db.contacts.createIndex({"dob.age": 1}, {partialFilterExpression: {gender: "male"}}) - Tạo Partial Index (Partial Index có thể được sử dụng kết hợp với Compound Index)
  (db.contacts.find({"dob.age": {$gt: 60}, gender: "male"}) có thể được hưởng lợi từ việc tạo Partial Index trên)
- Partial Index khác với Compound Index ở việc nó hoạt động trên một phần số lượng Document trong khi Compound Index hoạt động với toàn bộ Document

- MongoDB coi giá trị của các Field không tồn tại như NULL
- Sử dụng Partial Index kết hợp với ràng buộc Unique trong trường hợp muốn có 1 Unique Field nhưng vẫn chấp nhận một số Document không có Field đó hoặc giá trị của Field là NULL

- db.sessions.createIndex({createdAt: 1}, {expireAfterSeconds: 10}) - Tạo Time-To-Live (TTL) Index (chỉ có thể sử dụng với Index cho các Field mang dữ liệu kiểu thời gian (Date,...) và không hoạt động với Compound Index)
- Sau khi Collection thực hiện chèn dữ liệu, TTL Index sẽ kiểm tra toàn bộ Document trong Collection và loại bỏ tất cả Document có giá trị thời gian vượt quá giá trị được xác định với expireAfterSeconds

- Covered Query - Những truy vấn hoàn toàn sử dụng dữ liệu từ Index mà không cần duyệt qua bất kì Document nào (thường là những câu lệnh truy vấn trả về giá trị của 1 hoặc một vài Field đã được tạo Index) => Tốc độ truy vấn nhanh

- MongoDB so sánh phi phí thực hiện mỗi "Approach" truy vấn, từ đó tìm ra "Winning Plan"

- Multi-Key Index - Mỗi Index Value chứa nhiều giá trị
- Multi-Key Index có hiệu quả với truy vấn sử dụng Array Value, Nested Value, Value trong Embedded Document trong Array
- Compound Index chỉ có thể kết hợp với 1 Multi-Key Index (chỉ có thể sử dụng nhiều Multi-Key Index riêng biệt)

- "text" Index - Bản chất là Array chỉ chứa các Key Word. "text" Index giúp tìm kiếm hiệu quả hơn Regex (không phân biệt kí tự hoa - thường)
- db.products.createIndex({description: "text"}) - Tạo "text" Index
- db.products.find({$text: {$search: "awesome book"}}) - Tìm kiếm theo từng từ đơn
- db.products.find({$text: {$search: "\"awesome book\""}}) - Tìm kiếm theo cụm từ

- db.products.find({$text: {$search: "awesome book"}}, {score: {$meta: "textScore"}}) - Hiển thị "score" của các kết quả tìm kiếm
- db.products.find({$text: {$search: "awesome book"}}, {score: {$meta: "textScore"}}).sort({score: {$meta: "textScore"}}) - Sắp xếp các kết quả tìm kiếm theo "score"

- db.products.createIndex({title: "text", description: "text"}) - Tạo Combined "text" Index (thực chất kết hợp Key Word của tất cả các Field được tạo "text" Index)

- db.products.find({$text: {$search: "awesome -book"}}) - Exclude Word với kí tự - trước từ cần Exclude

- db.products.createIndex({title: "text", description: "text"}, {default_language: "english", weights: {title: 1, description: 10}}) - Thay đổi ngôn ngữ mặc định của "text" Index (có ảnh hưởng đến việc lọc Key Word) và thay đổi Weight (trọng số) của các Field được tạo "text" Index
- db.products.find({$text: {$search: "awesome book", $language: "german"}}) - Thay đổi ngôn ngữ tìm kiếm
- db.products.find({$text: {$search: "awesome book", $caseSensitive: true}}) - Tìm kiếm với tùy chọn Case Sensitive

- mongo credit-rating.js - Thực thi 1 File trong Shell
- db.ratings.createIndex({age: 1}, {background: true}) - Thực thi quá trình tạo Index ở Background
