- Transaction - Success Together or Fail Together!

- Session - Request được nhóm một cách logic (nguyên lý tương tự SQL)

- const session = db.getMongo().startSession() - Tạo Session
- session.startTransaction() - Tạo Transaction
- Do Something...
- session.commitTransaction() - Commit Changes
- session.abortTransaction() - Rollback Changes
- Nếu trong quá trình thực thi các tác vụ có lỗi xảy ra, MongoDB sẽ tự động Rollback để trở về trạng thái trước khi Session bắt đầu (Success Together or Fail Together!)
