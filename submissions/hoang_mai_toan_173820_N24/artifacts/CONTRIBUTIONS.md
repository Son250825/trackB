# CONTRIBUTIONS – Nhóm N24

**Dự án:** Vườn Toán Lớp 3  
**Track:** B – Phát triển tính năng bài tập ước lượng  
**Số thành viên:** 3

## 1. Phân công công việc

| Thành viên | Vai trò | Công việc phụ trách |
|---|---|---|
| Lead-BE | Backend | Phát triển logic xử lý bài tập ước lượng trong `server/estimate.js`; tích hợp API chấm điểm và lưu kết quả trong `server/api.js`; phối hợp xử lý dữ liệu trong database. |
| Dev-FE | Frontend | Phát triển giao diện bài tập ước lượng trong `public/exercise.html`; xử lý nhập đáp án, chuyển câu hỏi, kiểm tra dữ liệu đầu vào và hiển thị kết quả trong `public/assets/js/pages/exercise.js`. |
| Dev-TEST | Testing & Documentation | Xây dựng các bài kiểm thử cho logic, API và giao diện trong thư mục `tests/`; kiểm tra các trường hợp hợp lệ và không hợp lệ; hỗ trợ viết tài liệu và cấu hình CI. |

## 2. Đóng góp chi tiết

| Thành viên | Nội dung đóng góp | Bằng chứng |
|---|---|---|
| Thành viên 1 | Xây dựng chức năng chấm điểm bài tập ước lượng; xử lý dữ liệu đáp án; tích hợp lưu kết quả bài làm. | Commit/PR: [Bổ sung] |
| Thành viên 2 | Xây dựng giao diện làm bài; xử lý nhập khoảng dưới, khoảng trên và đáp án; hiển thị phản hồi cho học sinh. | Commit/PR: [Bổ sung] |
| Thành viên 3 | Viết kiểm thử tự động; kiểm tra các trường hợp biên; hỗ trợ hoàn thiện tài liệu và quy trình CI. | Commit/PR: [Bổ sung] |

## 3. Cross-review

Các thành viên phối hợp kiểm tra chéo phần việc của nhau trước khi hoàn thiện:

| Người kiểm tra | Phần việc được kiểm tra | Nội dung |
|---|---|---|
| Thành viên 1 | Frontend | Kiểm tra dữ liệu gửi từ giao diện có đúng định dạng backend yêu cầu không. |
| Thành viên 2 | Backend | Kiểm tra kết quả chấm điểm và phản hồi trả về có phù hợp với giao diện không. |
| Thành viên 3 | Backend và Frontend | Kiểm tra các trường hợp đầu vào, kết quả chấm điểm và tính ổn định của chức năng. |

## 4. Chuẩn bị bảo vệ

Mỗi thành viên cần nắm được:

- Thành viên 1: Cách hoạt động của `server/estimate.js`, API chấm bài và cơ chế lưu kết quả.
- Thành viên 2: Cách giao diện hiển thị câu hỏi, nhận đáp án và gửi dữ liệu lên server.
- Thành viên 3: Cách viết và chạy kiểm thử bằng `npm test`, ý nghĩa của từng nhóm test và quy trình CI.

Các thành viên đều cần hiểu luồng hoạt động tổng thể của tính năng, không chỉ phần việc cá nhân.

## 5. Sử dụng công cụ AI

Nhóm có sử dụng ChatGPT để hỗ trợ giải thích mã nguồn, gợi ý cách triển khai, tìm lỗi, xây dựng kiểm thử và hoàn thiện tài liệu.

Các thành viên có trách nhiệm tự kiểm tra, chạy thử, hiểu và chịu trách nhiệm với phần nội dung được đưa vào sản phẩm. Chi tiết việc sử dụng AI được trình bày trong `AI_USE.md`.