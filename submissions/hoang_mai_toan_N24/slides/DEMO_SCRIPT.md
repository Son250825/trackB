# DEMO SCRIPT — NHÓM 24 — TRACK B

**Sản phẩm:** Vườn Toán Lớp 3 – Ước lượng trước khi tính đúng  
**Thời lượng:** Tối đa 7 phút

## 1. Kịch bản demo

| Thời gian | Nội dung | Người phụ trách | Minh chứng |
|---|---|---|---|
| 0:00–0:45 | Giới thiệu bài toán, mục tiêu và phạm vi sản phẩm | Lead-BE | Giao diện tổng quan |
| 0:45–1:45 | Trình bày các quyết định thiết kế quan trọng, cách bổ sung dạng câu hỏi `estimate` mà không ảnh hưởng dạng câu hỏi cũ | Lead-BE | `DECISIONS.md` |
| 1:45–3:15 | Demo quy trình học sinh làm bài: nhập cận dưới, cận trên và kết quả chính xác | Dev-FE | Giao diện bài tập |
| 3:15–4:15 | Demo kiểm tra dữ liệu đầu vào và xử lý trường hợp không hợp lệ | Dev-FE | Giao diện và thông báo lỗi |
| 4:15–5:15 | Trình bày quy tắc chấm điểm: 3 điểm cho ước lượng hợp lý, 2 điểm cho kết quả chính xác | Lead-BE | `server/estimate.js` |
| 5:15–6:15 | Trình bày tích hợp API, lưu kết quả và kiểm thử | Lead-BE | `server/api.js`, `tests/` |
| 6:15–7:00 | Tổng kết chức năng, giới hạn hiện tại và hướng hoàn thiện | Cả nhóm | Slide tổng kết |

## 2. Nội dung vấn đáp cần chuẩn bị

1. Vì sao nhóm bổ sung dạng câu hỏi `estimate` thay vì sửa các dạng câu hỏi cũ?
2. Vì sao phải nhập khoảng ước lượng trước kết quả chính xác?
3. Vì sao chọn khoảng ước lượng hợp lý từ 0,8X đến 1,2X?
4. Cách tính điểm ước lượng và điểm kết quả chính xác?
5. Hệ thống xử lý dữ liệu đầu vào không hợp lệ như thế nào?
6. Vì sao tách logic chấm điểm vào `server/estimate.js`?
7. Đáp án được bảo vệ như thế nào trước khi học sinh nộp bài?
8. Kết quả bài làm được lưu ở đâu?
9. Nhóm đã kiểm thử những trường hợp nào?
10. Nhóm bảo đảm tuân thủ yêu cầu B-07 như thế nào?

## 3. Chuẩn bị trước demo

- [ ] Kiểm tra ứng dụng khởi động thành công.
- [ ] Kiểm tra tài khoản đăng nhập thử nghiệm.
- [ ] Kiểm tra bộ câu hỏi ước lượng.
- [ ] Chuẩn bị câu hỏi và đáp án mẫu.
- [ ] Kiểm tra luồng nhập khoảng ước lượng và kết quả chính xác.
- [ ] Kiểm tra chức năng nộp bài và lưu kết quả.
- [ ] Chuẩn bị tài liệu và mã nguồn cần trình bày.
- [ ] Chạy lại bộ kiểm thử trước demo.
- [ ] Chuẩn bị ảnh chụp màn hình dự phòng.

## 4. Phương án dự phòng

- Lỗi đăng nhập hoặc tải câu hỏi: kiểm tra server, API và dữ liệu mẫu.
- Lỗi nộp bài: kiểm tra kết nối và log server.
- Demo trực tiếp gặp sự cố: sử dụng ảnh chụp màn hình đã chuẩn bị.
- Không đủ thời gian: ưu tiên demo luồng làm bài và giải thích logic chấm điểm.