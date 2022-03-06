- Comparison Operator

* $eq - Equal
* $ne - Not Equal
* $gt - Greater Than
* $lt - Lower Than
* $gte - Greater Than or Equal
* $lte - Lower Than or Equal

- Query Embedded Field - db.<collection_name>.find({"rating.average": {$gt: 7}})
- Query Array (By Item) - db.<collection_name>.find({genres: "Drama"}) (tìm những Document có Field là Array chứa Item cần tìm kiếm)
- Query Array (By Array) - db.<collection_name>.find({genres: ["Drama"]}) (tìm những Document chứa Field là Array xác định trong Filter)

- "$in" và "$nin" ?
- "$or" và "$nor" ?
- "$and" ?
- "$not" ?

- $exists - Kiểm tra sự tồn tại của 1 Field

- "$type" ?
- "$regex" ?
- "$expr" ?

- Query Array of Embedded Document - db.<collection_name>.find({"hobbies.title": "Sports"}) (tìm những Document có Field là Array chứa Embedded Document có giá trị của 1 Field được xác định trong Filter) (hobbies: [{title: "Sports", frequency: 2}, {title: "Cooking", frequency: 3}])

- "$size" ?
- "$all" ?
- "$elemMatch" ?

- Cursor - Con trỏ giới hạn số lượng Document trả về tại cùng một thời điểm (trả về Document theo "Batch" chứ không trả về toàn bộ cùng lúc)

- ...find().count() - Trả về số Document tìm kiếm
- const cursor = db.movies.find()
- cursor.next() - Trả vể Document tiếp theo trong Cursor
- cursor.hasNext() - Kiểm tra có Document nào tiếp theo trong Cursor hay không
- cursor.forEach(doc => printjson(doc)) - Lặp qua từng Document trong Cursor

- ...find().sort({"rating.average: 1, runtime: -1"}) - Sắp xếp kết quả trả về trong Cursor (1 <=> asc, -1 <=> desc)

- ...find().skip(x).limit(y) - Bỏ qua x Document và giới hạn y Document trong kết quả trả về

- ...find({}, {name: 1, "rating.average": 1, \_id: 0}) - Projection (xác định Form của dữ liệu trả về)
- \_id luôn được trả về. Có thể set \_id: 0 để không trả về id

- ...find({genres: "Drama"}, {"genres.$": 1})
- ...find({genres: "Drama"}, {genres: {$elemMatch: {$eq: "Horror"}}})

- "$slice" ?
