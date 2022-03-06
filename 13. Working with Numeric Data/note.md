- Mặc định, Number được lưu trữ dưới dạng 64bit Double khi sử dụng Mongo Shell (bởi vì nó dựa trên JavaScript)

- Kiểu dữ liệu mặc định không phụ thuộc vào MongoDB mà phụ thuộc vào Client (Shell, Node.js, Python,...)

- ...insertOne({age: NumberInt([29|"29"])}) - Sử dụng int32

- Sử dụng giá trị lớn hơn giới hạn lưu trữ của kiểu dữ liệu không gây ra lỗi nhưng giá trị lưu trữ có thể bị sai lệch
- ...insertOne({age: NumberLong("123456789")}) - Sử dụng int64
- Nên sử dụng tham số vào dạng Text để tránh giới hạn về lưu trữ với kiểu dữ liệu 64bit Double mặc định của Mongo Shell

- Lưu ý: Int + Double => Double (khi 1 kiểu dữ liệu tương tác với 1 kiểu dữ liệu khác có thể dẫn đến kết quả bị thay đổi kiểu dữ liệu so với ban đầu)

- Double (64bit) luôn có sự không chính xác nhất định trong lưu trữ giá trị Number with Decimal Place

- ...insertOne({a: NumberDecimal("0.3")}) - Sử dụng Decimal 128bit

- Scale Factor ?
