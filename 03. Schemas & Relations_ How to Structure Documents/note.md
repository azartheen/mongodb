- Mặc định, Shell sử dụng Floating Point Number (Floating Point Number với độ chính xác thấp, không phải kiểu dữ liệu NumberDecimal)
- ObjectId được mã hóa để có thể sắp xếp theo thời gian Document được khởi tạo

- db.dropDatabase() - Drop Database hiện tại
- db.<collection_name>.drop() - Drop Collection collection_name
- ...insertOne({..., foundingDate: new Date(), insertedAt: new Timestamp()})
- db.stats() - Hiển thị thông tin về Database hiện tại

- var var_name = ... - Khai báo biến

- n:n Relation không nhất thiết phải sử dụng "Intermediate Table"

- Embedded Document thường được sử dụng trong 1:1, 1:n Relation; Reference thường được sử dụng trong n:n Relation

- $lookup - Joining Collection

- Schema Validation - Tạo ra 1 Schema cho Collection. Dựa trên Schema có thể Accept hoặc Reject thao tác Insert hoặc Update nếu không tuân thủ Schema đã định nghĩa

- db.runCommand({...}) - Thực thi Command trong Shell
