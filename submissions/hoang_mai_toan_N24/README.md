# Vườn Toán Lớp 3 – Ước lượng trước khi tính đúng

## 1. Thông tin bài nộp

- **Track:** Track B – Vườn Toán Lớp 3: Ước lượng trước khi tính đúng
- **Nhóm:** Nhóm 24
- **Tên thư mục bài nộp:** `vuontoan-nhom24`

## 2. Thành viên

| Alias | Vai trò |
|---|---|
| Lead-BE | Leader |
| Dev-FE | Member |
| Dev-TEST | Member |

## 3. Giới thiệu sản phẩm

Vườn Toán Lớp 3 là ứng dụng hỗ trợ học sinh lớp 3 rèn luyện kỹ năng ước lượng trước khi thực hiện phép tính chính xác.

Trong phần bài tập ước lượng, học sinh cần đưa ra khoảng giá trị hợp lý cho kết quả, sau đó nhập đáp án chính xác. Hệ thống kiểm tra câu trả lời và phản hồi kết quả để giúp học sinh tự đánh giá khả năng ước lượng của mình.

## 4. Chức năng đã triển khai

- Hiển thị danh sách câu hỏi ước lượng.
- Cho phép học sinh nhập cận dưới và cận trên của khoảng ước lượng.
- Kiểm tra dữ liệu đầu vào, không chấp nhận dữ liệu không hợp lệ.
- Cho phép học sinh nhập kết quả chính xác sau khi hoàn thành khoảng ước lượng hợp lệ.
- Chấm điểm câu trả lời ở phía máy chủ.
- Lưu kết quả bài làm và điểm số vào hệ thống.
- Hiển thị phản hồi sau khi nộp bài.

## 5. Cách tính điểm

Mỗi câu hỏi có tổng điểm tối đa là 5 điểm:

- 3 điểm nếu khoảng ước lượng hợp lý.
- 2 điểm nếu kết quả chính xác đúng.

Việc đánh giá khoảng ước lượng dựa trên quy tắc được triển khai trong hệ thống.

## 6. Công nghệ sử dụng

- Node.js
- Express
- SQLite
- HTML, CSS, JavaScript
- Node.js Test Runner

## 7. Cài đặt và chạy chương trình

### Yêu cầu

- Node.js
- npm

### Cài đặt thư viện

```bash
npm ci