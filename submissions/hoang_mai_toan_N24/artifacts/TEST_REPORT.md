
# TEST REPORT – Nhóm 24

## 1. Thông tin chung

- **Dự án:** Vườn Toán Lớp 3
- **Track:** Track B – Ước lượng trước khi tính đúng
- **Nhóm:** 24
- **Lệnh kiểm thử:** `npm.cmd test`
- **Tổng số test:** 52
- **Kết quả:** 52 PASS, 0 FAIL

## 2. Phạm vi kiểm thử

Kiểm thử chức năng ước lượng phép nhân và phép chia trong bảng 7, bao gồm:

- Xử lý và kiểm tra dữ liệu đầu vào.
- Kiểm tra đáp án ước lượng và đáp án chính xác.
- Tính điểm và phân loại kết quả.
- Kiểm tra API lấy câu hỏi và nộp bài.
- Kiểm tra lưu kết quả làm bài.
- Kiểm tra giao diện nhập đáp án và phản hồi lỗi.

## 3. Các nhóm kiểm thử

| Nhóm kiểm thử | File | Số lượng |
|---|---|---:|
| Logic | `tests/estimate.test.js` | Cần xác nhận |
| API | `tests/estimate-api.test.js` | Cần xác nhận |
| UI | `tests/estimate-ui.test.js` | Cần xác nhận |
| **Tổng** | | **52** |

## 4. Kết quả kiểm thử

Kết quả chạy `npm.cmd test` tại môi trường phát triển:

- Tổng số test: 52
- Thành công: 52
- Thất bại: 0

Tất cả các test trong lần chạy được ghi nhận đều thành công.

## 5. Kiểm thử các trường hợp biên

Các trường hợp cần được đối chiếu với test thực tế:

- Dữ liệu đầu vào không phải số.
- Giá trị âm hoặc số thập phân.
- Cận dưới lớn hơn hoặc bằng cận trên.
- Khoảng ước lượng không chứa đáp án chính xác.
- Đáp án chính xác không hợp lệ.
- Người dùng bỏ trống một hoặc nhiều trường.
- Nộp bài và lưu kết quả.

## 6. Kết luận

Bộ kiểm thử hiện tại ghi nhận 52/52 test thành công tại môi trường phát triển.

Kết quả này xác nhận các trường hợp được bao phủ bởi bộ test hoạt động đúng. Việc kiểm thử trên GitHub Actions và các môi trường khác sẽ được thực hiện trước khi hoàn tất Pull Request.
