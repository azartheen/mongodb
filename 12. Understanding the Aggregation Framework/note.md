"Aggregation Framework" - Xây dựng 1 "Pipeline of Step" thực thi trên Data lấy từ Collection và trả về Output ở Form cần sử dụng

- db.persons.aggregate([ { $match: {gender: "female"} } ]) - Tạo Aggregation Framework với $match Stage (lọc Document theo Filter)
- Aggregation Framework vẫn có thể tận dụng Index trong lọc Document
- Aggregation Framework trả về 1 Cursor

- { $group: { _id: { state: "$location.state" }, totalPersons: { $sum: 1 } } }
- $group Stage - Nhóm dữ liệu theo 1 hoặc một số Field
- \_id - Khai báo các Field sử dụng để nhóm dữ liệu (luôn là tham số đầu tiên)
- Có thể thêm Key vào kết quả trả về với tham số thứ hai sử dụng "Aggregation Function" ($sum,...)
- $group "accumulate data" - Từ nhiều Document, $group sẽ chỉ trả về 1 kết quả (với "Aggregation Function" tương ứng với mỗi loại thao tác)
- "$location.state" - Kí tự $ thể hiện tham chiếu đến Field trong Input Document

- { $sort: { totalPersons: -1 } }
- $sort Stage - Sắp xếp kết quả trả về từ Stage trước đó

- $project ?

- Có thể sử dụng 1 loại Stage nhiều lần trong cùng 1 Aggregation Framework
- {
  $convert: {
  input: '$location.coordinates.longitude',
  to: 'double',
  onError: 0.0,
  onNull: 0.0
  }
  } - Chuyển đổi kiểu dữ liệu với $convert

- { $toDate: '$dob.date' } - Convert Shortcut

- $isoWeekYear ?
- $group vs $project ?

- { $group: { _id: { age: "$age" }, allHobbies: { $push: "$hobbies" } } } - Thêm Elements vào Newly Created Arrays

- $unwind ?

- { $group: { _id: { age: "$age" }, allHobbies: { $addToSet: "$hobbies" } } } - Loại bỏ Duplicate Values

- { $project: { _id: 0, examScore: { $slice: ["$examScores", 2, 1] } } } - Sử dụng Projection với Arrays sử dụng $slice

- { $size: "$examScores" } - Lấy độ dài của Array

- $filter ?

- { $first: "$name" } - Lấy giá trị đầu tiên
- { $max: "$score" } - Lấy giá trị lớn nhất dựa trên 1 Field

- $bucket ?

- { $skip: 10 } - $skip Stage bỏ qua một số lượng Document trả về
- { $limit: 10 } - $limit Stage giới hạn số lượng Document trả về

- { $out: "collectionName" } - $out Stage chèn Document trả về vào 1 Collection (đã tồn tại hoặc không tồn tại)
