
# REQUIREMENTS — Track B: Vườn Toán Lớp 3 — Tính năng luyện tập ước lượng

- **Nhóm:** N24
- **Phiên bản:** 1.0
- **Phạm vi:** Bổ sung dạng câu hỏi ước lượng vào hệ thống Vườn Toán Lớp 3.
- **Nguyên tắc:** Sử dụng dữ liệu tổng hợp (synthetic), chấm điểm bằng quy tắc xác định, không sử dụng LLM để sinh hoặc chấm đáp án.

## 1. Tổng quan và mục tiêu

Dự án bổ sung dạng bài tập "Ước lượng kết quả" vào hệ thống học tập Vườn Toán Lớp 3.

Thay vì chỉ yêu cầu học sinh nhập kết quả chính xác, dạng bài mới cho phép học sinh đưa ra một khoảng ước lượng gồm cận dưới, cận trên và kết quả chính xác của phép tính.

Mục tiêu:
- Giúp học sinh rèn luyện khả năng ước lượng kết quả phép tính.
- Tích hợp dạng bài mới vào luồng học tập hiện có.
- Chấm điểm tự động ở phía máy chủ.
- Phản hồi rõ ràng về kết quả ước lượng và kết quả chính xác.
- Lưu kết quả làm bài để phục vụ theo dõi tiến độ học tập.

## 2. Phạm vi thực hiện

### 2.1. Trong phạm vi

- Bổ sung dạng câu hỏi mới có `type = estimate`.
- Xây dựng bộ câu hỏi tổng hợp về phép nhân và phép chia bảng 7.
- Cung cấp tối thiểu 12 câu hỏi có thể tái tạo.
- Cho phép học sinh nhập:
  - Cận dưới của khoảng ước lượng (`lower`).
  - Cận trên của khoảng ước lượng (`upper`).
  - Kết quả chính xác (`exact`).
- Kiểm tra tính hợp lệ của dữ liệu đầu vào.
- Chấm điểm ở phía máy chủ.
- Hiển thị phản hồi sau khi nộp bài.
- Lưu câu trả lời, điểm số và tiến độ vào database.
- Bổ sung kiểm thử tự động cho logic, API và giao diện.

### 2.2. Ngoài phạm vi

- Thay đổi hệ thống xác thực và phân quyền.
- Thay đổi cơ chế quản lý phiên đăng nhập.
- Thay đổi tài khoản mẫu.
- Thay đổi cấu hình triển khai hệ thống.
- Kết nối hệ thống với dữ liệu học sinh hoặc giáo viên thật.
- Thay đổi các dạng câu hỏi cũ không liên quan đến tính năng ước lượng.
- Mở rộng sang các nội dung học tập khác ngoài phạm vi được giao.

## 3. Quy tắc nghiệp vụ

Nguồn xử lý và chấm điểm: `server/estimate.js`.

### 3.1. Cấu trúc dữ liệu đáp án

Đáp án của câu hỏi được lưu theo định dạng:

`kết_quả_chính_xác|cận_dưới_cho_phép-cận_trên_cho_phép`

Ví dụ:

`14|11-17`

Trong đó:
- `14`: kết quả chính xác.
- `11`: cận dưới cho phép.
- `17`: cận trên cho phép.

### 3.2. Kiểm tra dữ liệu đầu vào

Các giá trị học sinh nhập phải đáp ứng:
- Là số nguyên không âm.
- Cận dưới nhỏ hơn cận trên.
- Các trường bắt buộc phải có giá trị hợp lệ.
- Khoảng ước lượng phải chứa kết quả chính xác.
- Các giá trị nằm trong giới hạn cho phép của đáp án.

Dữ liệu không hợp lệ không được tính là câu trả lời đúng.

### 3.3. Quy tắc xác định ước lượng hợp lý

Gọi:
- `E`: kết quả chính xác.
- `L`: cận dưới học sinh nhập.
- `U`: cận trên học sinh nhập.
- `Min`: cận dưới cho phép của câu hỏi.
- `Max`: cận trên cho phép của câu hỏi.

Ước lượng được xem là hợp lý khi:

`L < U`

`Min ≤ L ≤ E ≤ U ≤ Max`

Quy tắc được thực hiện bằng code, không phụ thuộc vào đánh giá chủ quan hoặc mô hình AI.

### 3.4. Quy tắc chấm điểm

Mỗi câu hỏi có điểm tối đa là 5 điểm.

- Ước lượng hợp lý: 3 điểm.
- Kết quả chính xác đúng: 2 điểm.
- Không đạt điều kiện của phần nào thì không nhận điểm phần đó.

Tổng điểm câu hỏi là tổng điểm của hai thành phần.

Ví dụ:

| Ước lượng | Kết quả chính xác | Điểm |
|---|---|---:|
| Hợp lý | Đúng | 5 |
| Hợp lý | Sai | 3 |
| Không hợp lý | Đúng | 2 |
| Không hợp lý | Sai | 0 |

### 3.5. Phản hồi kết quả

Hệ thống cần phân biệt:
- Ước lượng hợp lý.
- Ước lượng chưa hợp lý.
- Kết quả chính xác đúng.
- Kết quả chính xác chưa đúng.

Phản hồi được xây dựng dựa trên kết quả chấm điểm của máy chủ.

## 4. Acceptance Criteria và truy vết (B-01 đến B-12)

| Mã | Tiêu chí nghiệm thu | Cách đáp ứng | Bằng chứng |
|---|---|---|---|
| B-01 | Tích hợp vào luồng học hiện có, không phải trang demo riêng | Tích hợp dạng bài ước lượng vào hệ thống bài học và luyện tập hiện có | `exercise.html`, `exercise.js`, `curriculum-view.js` |
| B-02 | Có ít nhất 12 câu hỏi synthetic, có thể tái tạo | Bổ sung 12 câu hỏi trong bộ dữ liệu seed | `data/seed.json` |
| B-03 | Quy tắc tạo và chấm điểm rõ ràng, tất định, kiểm thử được | Xây dựng module xử lý riêng, quy định rõ điều kiện ước lượng và cách tính điểm | `server/estimate.js`, `tests/estimate.test.js` |
| B-04 | API không trả đáp án trước khi học sinh nộp bài | API lấy câu hỏi không công khai trường đáp án chính xác | `server/api.js`, `tests/estimate-api.test.js` |
| B-05 | Máy chủ chấm điểm và lưu kết quả; dữ liệu không mất khi tải lại | Tích hợp chấm điểm với API nộp bài, lưu câu trả lời và kết quả vào database | `server/api.js`, `server/db.js` |
| B-06 | Phản hồi phân biệt ước lượng hợp lý và kết quả chính xác | Trả về kết quả từng thành phần và phản hồi tương ứng | `server/estimate.js`, `exercise.js` |
| B-07 | Không sửa các thành phần được bảo vệ | Không thay đổi `server/auth.js`, session, tài khoản mẫu và cấu hình deployment | Kiểm tra Git diff và kiểm thử hồi quy |
| B-08 | Có kiểm thử normal, boundary, invalid và scoring | Bổ sung kiểm thử logic, API và giao diện | `tests/estimate.test.js`, `tests/estimate-api.test.js`, `tests/estimate-ui.test.js` |
| B-09 | Có lệnh `npm test`, chạy được từ môi trường cài đặt sạch | Sử dụng script kiểm thử của Node.js | `package.json`, `package-lock.json` |
| B-10 | CI chạy `npm ci` và `npm test` khi có Pull Request | Cấu hình GitHub Actions với Node.js 18, 20 và 22 | `.github/workflows/ci.yml` |
| B-11 | Không sử dụng PII hoặc secret | Sử dụng dữ liệu tổng hợp, không đưa thông tin cá nhân hoặc bí mật vào dự án | `data/seed.json`, tài liệu dự án |
| B-12 | Giao diện sử dụng được bằng bàn phím, thông báo lỗi rõ ràng | Hỗ trợ nhập liệu, điều hướng và hiển thị thông báo lỗi cho học sinh | `public/exercise.html`, `public/assets/js/pages/exercise.js`, kiểm thử giao diện |

## 5. Kế hoạch kiểm thử

| Nhóm kiểm thử | Nội dung | Kết quả mong đợi |
|---|---|---|
| Normal | Nhập khoảng ước lượng hợp lý và kết quả chính xác đúng | Nhận đủ 5 điểm |
| Normal | Ước lượng hợp lý nhưng kết quả chính xác sai | Nhận 3 điểm |
| Normal | Ước lượng không hợp lý nhưng kết quả chính xác đúng | Nhận 2 điểm |
| Normal | Cả ước lượng và kết quả chính xác đều sai | Nhận 0 điểm |
| Boundary | Cận dưới bằng giá trị cho phép nhỏ nhất | Được chấp nhận nếu thỏa các điều kiện |
| Boundary | Cận trên bằng giá trị cho phép lớn nhất | Được chấp nhận nếu thỏa các điều kiện |
| Invalid | Nhập chữ, số âm hoặc bỏ trống trường bắt buộc | Hiển thị thông báo lỗi |
| Invalid | Cận dưới lớn hơn hoặc bằng cận trên | Không chấp nhận dữ liệu |
| Invalid | Nhập số thập phân hoặc dữ liệu không phải số nguyên | Không chấp nhận dữ liệu |
| API | Lấy danh sách câu hỏi trước khi nộp bài | Không để lộ đáp án |
| API | Nộp bài với dữ liệu hợp lệ | Máy chủ chấm điểm và lưu kết quả |
| UI | Nhập dữ liệu và thao tác bằng bàn phím | Giao diện hoạt động đúng |
| Regression | Làm các dạng câu hỏi cũ | Cách chấm điểm cũ không bị thay đổi |
| Database | Tải lại trang sau khi đã nộp bài | Kết quả đã lưu vẫn được giữ |

## 6. Yêu cầu kiểm thử và chất lượng

- Các quy tắc nghiệp vụ phải có kiểm thử tự động.
- Kiểm thử phải bao gồm trường hợp thông thường, trường hợp biên và dữ liệu không hợp lệ.
- Các dạng câu hỏi cũ phải tiếp tục hoạt động.
- Lệnh `npm test` phải chạy thành công.
- CI phải thực hiện cài đặt phụ thuộc và chạy kiểm thử tự động.
- Không đưa dữ liệu cá nhân hoặc thông tin bí mật vào mã nguồn.

## 7. Tiêu chí hoàn thành

Tính năng được xem là hoàn thành khi:
1. Tích hợp được vào luồng học tập hiện có.
2. Có tối thiểu 12 câu hỏi synthetic.
3. Quy tắc ước lượng và chấm điểm được triển khai ở phía máy chủ.
4. API không để lộ đáp án trước khi nộp bài.
5. Kết quả làm bài được lưu vào database.
6. Phản hồi phân biệt rõ hai thành phần ước lượng và tính chính xác.
7. Các bài kiểm thử tự động chạy thành công.
8. CI được cấu hình và hoạt động đúng.
9. Không làm ảnh hưởng các chức năng cũ và các thành phần nằm ngoài phạm vi.
