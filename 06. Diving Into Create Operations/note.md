- insert() - Chèn 1 hoặc nhiều Document vào Collection. Không ưu tiên sử dụng

- Ordered Insert - Tất cả Inserted Document được xử lí riêng biệt. Nếu 1 Document Insert thất bại, hủy toàn bộ quá trình Insert với tất cả các Document còn lại nhưng không Rollback những Document đã được Insert trước đó
- db.<collection_name>.insertMany([{...}, {ordered: false}]) - Tùy chỉnh nếu 1 Document Insert thất bại, có thực hiện Ordered Insert hay không. Ordered Insert nếu true, Unorderd Insert (tiếp tục Insert những Document còn lại) nếu false

- WriteConcern - Cấu hình một số tùy chọn cho thao tác ghi dữ liệu (có ghi vào Journal hay không, tùy chỉnh timeout,...)
- Journal ("Todos") - 1 File lưu trữ những thao tác ghi dữ liệu Storage Engine cần thực hiện nhưng chưa được hoàn thành
- { w: 1, j: undefined } - Không ghi vào Journal (nhanh hơn nhưng không đảm bảo an toàn nếu gặp sự cố)
- { w: 1, j: true } - Ghi vào Journal (chậm hơn nhưng đảm bảo an toàn nếu gặp sự cố)
- { w: 1, wtimeout: 200, j: true } - Tùy chỉnh thời gian tối đa dành cho cho 1 thao tác ghi để được chấp nhận là hoàn thành (quá timeout mà chưa hoàn thành, thao tác ghi sẽ được xét là ghi thất bại, mặc dù vẫn có thể ghi thành công trong thời gian lớn hơn timeout)

- w: 0 - Không quan tâm tới kết quả trả về của Database Server (thời gian rất nhanh)

- Atomicity - MongoDB CRUD Operation sẽ được Rollback (KHÔNG có gì được lưu) nếu gặp lỗi, hoặc lưu trữ toàn bộ nếu thành công (áp dụng trên Document Level)

- mongoimport ./data.json -d db_name -c collection_name --jsonArray (đối với 1 Array các Document) --drop (nếu Collection đã tồn tại thì drop và ghi dữ liệu mới; mặc định là append dữ liệu vào Collection đã tồn tại)
