- Cấu trúc của GeoJSON Data
  key_name: {
  type: "Point|...",
  coordinates: [lng, lat]
  }

- db.places.createIndex({location: "2dsphere"}) - Tạo Geospatial Index

- db.places.find({location: {$near: {$geometry: {type: "Point", coordinates: [lng, lat]}, $maxDistance: 500, $minDistance: 5}}}) - Tìm kiếm những địa điểm gần (với khoảng cách (mét) tối đa và tối thiểu được xác định với $maxDistance và $minDistance) với tọa độ đã chỉ định (kết quả trả về đã được sắp xếp)

- db.places.find({location: {$geoWithin: {$geometry: {type: "Polygon", coordinates: [[p1, p2, p3, p1]]}}}}) - Tìm kiếm những địa điểm nằm trong một khu vực đã chỉ định (cần đặt điểm bắt đầu ở cuối coordinates để tạo 1 Polygon kín) (p1: [lng, lat])

- Cấu trúc của 1 Area
  key_name: {
  type: "Polygon",
  coordinates: [[p1, p2, p3, p1]]
  }
- db.areas.find({area: {$geoIntersects: {$geometry: {type: "Point", coordinates: [lng, lat]}}}}) - Tìm kiếm những Area "giao" với Point (hoặc Area) đã chỉ định

- db.places.find({location: {geoWithin: {$centerSphere: [[lng, lat], radius]}}}) - Tìm kiếm những địa điểm nằm trong bán kính xác định từ 1 điểm (kết quả trả về không được sắp xếp) (cần chuyển đổi giá trị của radius sang radian trước khi thực hiện truy vấn)
