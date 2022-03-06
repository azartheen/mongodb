- Updating Fields with "updateOne()", "updateMany()" and "$set" ?
- Updating Multiple Fields with "$set" ?

- ...updateOne({name: "Manuel", {$inc: {age: 1}, $set: {isSporty: false}}}) - Tăng / Giảm giá trị với $inc

- "$min", "$max" và "$mul" ?

- ...updateMany({isSporty: true}, {$unset: {phone: ""}}) - Loại bỏ Field (giá trị của Field trong câu lệnh không quan trọng)

- ...updateMany({}, {$rename: {age: "totalAge"}}) - Đổi tên Field

- ...updateOne({name: "Maria}, {$set: {age: 29,...}}, {upsert: true}) - Nếu tồn tại Document, thực hiện thao tác cập nhật. Nếu không tồn tại Document, chèn Document mới với những giá trị được xác định

- ...updateMany({hobbies: {$elemMatch: {title: "Sports", frequency: {$gte: 3}}}}, {$set: {"hobbies.$.highFrequency": true}}) - Cập nhật Matched Array Elements (Matched Element đầu tiên)

- ...updateMany({totalAge: {$gt: 30}}, {$inc: {"hobbies.$[].frequency": -1}}) - Cập nhật All Array Elements

- ...updateMany({"hobbies.frequency": {$gt: 2}}, {$set: {"hobbies.$[el].goodFrequency": true}}, {arrayFilter: [{"el.frequency": {$gt: 2}}]}) - Tìm & Cập nhật Specific Fields

- ...updateOne({name: "Maria"}, {$push: {hobbies: {$each: [{title: "Good Wine", frequency: 1}, {title: "Hiking", frequency: 2}], $sort: {frequency: -1}, $slice: 1}}}) - Thêm Elements vào Arrays (toàn bộ Array sau khi thêm Element được sắp xếp dựa trên 1 Field xác định với $sort; $slice xác định số lượng Element muốn thêm vào Array)

- ...updateOne({name: "Maria"}, {$pull: {hobbies: {title: "Hiking"}}}) - Loại bỏ Elements khỏi Arrays
- ...updateOne({name: "Chris}, {$pop: {hobbies: [1|-1]}}) - Loại bỏ Elements cuối cùng (với 1) hoặc đầu tiên (với -1) khỏi Arrays

- "$addToSet" ?
