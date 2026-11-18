# SECURITY_PRIVACY_CHECKLIST — NHÓM 24 — TRACK B

## Phạm vi

Checklist áp dụng cho phần nhóm bổ sung chức năng "Ước lượng trước khi tính đúng".

Các thành phần starter nằm ngoài phạm vi sửa đổi theo B-07 gồm:
- Các route `/api/auth/*`.
- Các route `/api/teacher/*`.
- Toàn bộ `server/auth.js`.

## 1. Dữ liệu và quyền riêng tư (B-11)

| # | Hạng mục | Trạng thái | Bằng chứng / ghi chú |
|---|---|---|---|
| 1 | Sử dụng dữ liệu câu hỏi mẫu phục vụ kiểm thử | Cần xác nhận | Đối chiếu `data/seed.json` |
| 2 | Không đưa thông tin cá nhân thật vào dữ liệu kiểm thử và tài liệu nộp | Cần xác nhận | Rà soát repository và thư mục submissions |
| 3 | Không commit token, API key, mật khẩu thật hoặc file `.env` | Cần xác nhận | Rà soát file và lịch sử Git |
| 4 | Không kết nối cơ sở dữ liệu production hoặc dịch vụ thật | Cần xác nhận | Kiểm tra cấu hình môi trường |
| 5 | Log và tài liệu AI-use không chứa PII hoặc secret | Cần xác nhận | Rà soát log và `AI_USE.md` |
| 6 | Fork công khai không chứa dữ liệu nhạy cảm | Cần xác nhận | Rà soát trước Freeze |

## 2. Ranh giới an toàn miền (B-07)

| # | Hạng mục | Trạng thái | Bằng chứng / ghi chú |
|---|---|---|---|
| 7 | Không sửa `server/auth.js` và các route bị giới hạn | Đã đối chiếu một phần | Kiểm tra lại diff với starter gốc |
| 8 | Không làm thay đổi hành vi của 4 dạng câu hỏi cũ | Cần xác nhận | Đối chiếu mã nguồn và test hồi quy |
| 9 | API không để lộ đáp án trước khi nộp | Cần xác nhận | Kiểm tra API và phản hồi thực tế |
| 10 | Logic chấm điểm được xử lý phía máy chủ | Cần xác nhận | Đối chiếu `server/estimate.js` và API |
| 11 | Không sử dụng LLM để sinh hoặc chấm đáp án khi chạy ứng dụng | Cần xác nhận | Rà soát mã nguồn |
| 12 | Kiểm tra thứ tự xử lý và dữ liệu gửi lên API | Cần xác nhận | Đối chiếu API và các trường hợp kiểm thử |

## 3. Kiểm tra đầu vào và injection

| # | Hạng mục | Trạng thái | Bằng chứng / ghi chú |
|---|---|---|---|
| 13 | Kiểm tra dữ liệu đầu vào của chức năng ước lượng | Cần xác nhận | Đối chiếu logic trong `server/estimate.js` |
| 14 | Từ chối dữ liệu không hợp lệ | Đã kiểm thử một phần | Kiểm tra `tests/` |
| 15 | Truy vấn cơ sở dữ liệu sử dụng tham số hóa | Cần xác nhận | Rà soát các truy vấn mới |
| 16 | Kiểm tra cách hiển thị dữ liệu động để hạn chế XSS | Cần xác nhận | Rà soát JavaScript phía frontend |
| 17 | Thông báo lỗi không tiết lộ thông tin nội bộ | Cần xác nhận | Kiểm tra phản hồi API |

## 4. Rủi ro còn tồn tại

- Chưa xác nhận có cơ chế giới hạn tần suất gọi API.
- Các cấu hình mặc định của starter cần được rà soát trước khi triển khai công khai.
- Cần quét secret tự động trên lịch sử Git trước khi Freeze.
- Cần kiểm tra các thay đổi so với starter để bảo đảm tuân thủ B-07.

## 5. Việc cần xác nhận trước Freeze

- [ ] Quét secret trên lịch sử Git của fork.
- [ ] Rà soát lịch sử commit và PR để tránh công khai thông tin cá nhân không cần thiết.
- [ ] Đảm bảo không có file cơ sở dữ liệu `.db` bị commit.
- [ ] Đối chiếu các file và route với starter gốc.
- [ ] Kiểm tra lại các API và kết quả kiểm thử.
- [ ] Kiểm tra CI trên GitHub.

## 6. Kết luận

Nhóm đã triển khai chức năng ước lượng và thực hiện kiểm thử trên môi trường phát triển.

Các hạng mục bảo mật và quyền riêng tư cần được tiếp tục rà soát, xác nhận bằng mã nguồn, kết quả kiểm thử và lịch sử Git trước khi bàn giao chính thức.