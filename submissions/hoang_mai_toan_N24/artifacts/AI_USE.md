# AI_USE — NHÓM 24 — TRACK B

## 1. Công cụ/model

| Công cụ | Model/phiên bản |
|---|---|
| ChatGPT | GPT-6 (theo thông tin model hiển thị trong phiên sử dụng) |

## 2. Mục đích sử dụng

Nhóm sử dụng AI để hỗ trợ các công việc:

- Giải thích cấu trúc dự án và mã nguồn starter.
- Phân tích yêu cầu chức năng ước lượng.
- Đề xuất cách tổ chức logic kiểm tra và chấm điểm.
- Hỗ trợ đọc hiểu, rà soát và sửa lỗi mã nguồn.
- Gợi ý các trường hợp kiểm thử.
- Hỗ trợ soạn thảo và rà soát tài liệu bàn giao.

## 3. Phạm vi sử dụng

Các file/module có liên quan đến quá trình AI hỗ trợ:

| File/module | Phạm vi hỗ trợ |
|---|---|
| `server/estimate.js` | Phân tích và rà soát logic kiểm tra, chấm điểm |
| `server/api.js` | Giải thích cách tích hợp logic ước lượng vào API |
| `server/db.js` | Hỗ trợ đọc hiểu phần lưu trữ dữ liệu |
| `data/seed.json` | Hỗ trợ kiểm tra dữ liệu câu hỏi mẫu |
| `public/exercise.html` | Rà soát cấu trúc giao diện bài tập |
| `public/assets/js/pages/exercise.js` | Hỗ trợ xử lý tương tác và kiểm tra dữ liệu nhập |
| `tests/` | Gợi ý và rà soát các trường hợp kiểm thử |
| `artifacts/` | Hỗ trợ soạn thảo tài liệu bàn giao |

AI cũng được sử dụng để hỗ trợ giải thích quy định Git, GitHub và quy trình nộp bài.

## 4. Kiểm chứng đầu ra AI

Nhóm kiểm chứng các nội dung được đề xuất bằng cách:

- Đối chiếu với yêu cầu và quy định của đề bài.
- Kiểm tra lại mã nguồn sau khi chỉnh sửa.
- Chạy lệnh `npm.cmd test`.
- Ghi nhận kết quả kiểm thử: 52 tests passed, 0 failed trên máy phát triển.
- Rà soát các thay đổi để bảo đảm không sửa các phần bị giới hạn theo B-07.

Kết quả CI trên GitHub cần được kiểm tra riêng trước khi bàn giao.

## 5. Quyết định của nhóm

| Nội dung AI hỗ trợ | Quyết định | Lý do |
|---|---|---|
| Giải thích cấu trúc và mã nguồn | Giữ và đối chiếu | Giúp thành viên hiểu dự án trước khi chỉnh sửa |
| Đề xuất logic chức năng ước lượng | Sửa và điều chỉnh | Phải phù hợp với yêu cầu thực tế của đề bài |
| Gợi ý kiểm thử | Giữ, bổ sung và rà soát | Cần kiểm tra hành vi thực tế của chương trình |
| Hỗ trợ sửa lỗi | Chỉ giữ sau khi kiểm tra | Tránh phát sinh lỗi hoặc ảnh hưởng chức năng cũ |
| Soạn thảo tài liệu | Chỉnh sửa trước khi sử dụng | Bảo đảm nội dung phản ánh đúng sản phẩm của nhóm |

Nhóm không mặc định chấp nhận toàn bộ đầu ra AI. Các đề xuất không phù hợp với yêu cầu, phạm vi hoặc kết quả kiểm thử sẽ được chỉnh sửa hoặc loại bỏ.

## 6. Người chịu trách nhiệm

| Mã thành viên | Vai trò | Trách nhiệm |
|---|---|---|
| Lead-BE | Leader | Review và chấp thuận các thay đổi liên quan đến backend |
| Dev-FE | Member | Review giao diện và tương tác phía frontend |
| Dev-TEST | Member | Review các trường hợp kiểm thử và kết quả kiểm thử |

Nhóm chịu trách nhiệm cuối cùng đối với các nội dung được tích hợp vào sản phẩm.

## 7. Quyền riêng tư và bảo mật

- Không đưa mật khẩu, API key, token hoặc thông tin xác thực vào prompt hay tài liệu AI-use.
- Không đưa thông tin cá nhân thật của học sinh, giáo viên hoặc thành viên nhóm vào nội dung gửi AI.
- Không công khai lịch sử prompt riêng tư.
- Chỉ ghi nhận những thông tin cần thiết để truy vết quá trình hỗ trợ và quyết định kỹ thuật.