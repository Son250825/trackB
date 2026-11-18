
# DECISIONS – Nhóm 24

**Dự án:** Vườn Toán Lớp 3  
**Track:** B – Phát triển tính năng bài tập ước lượng

Tài liệu ghi lại các quyết định thiết kế và triển khai chức năng bài tập ước lượng (Estimate).

---

## ADR-00: Bổ sung loại câu hỏi Estimate

**Bối cảnh:**

Hệ thống hiện tại có 4 loại câu hỏi với cách xử lý và chấm điểm riêng. Nhóm cần bổ sung dạng bài tập ước lượng nhưng vẫn phải đảm bảo các chức năng cũ hoạt động bình thường.

**Quyết định:**

Bổ sung một type mới có tên `estimate`, không sửa đổi 4 type câu hỏi hiện có.

**Lý do:**

- Hạn chế ảnh hưởng đến chức năng cũ.
- Phân biệt rõ cách xử lý câu hỏi ước lượng với các dạng câu hỏi khác.
- Dễ kiểm thử và mở rộng về sau.

---

## ADR-01: Tổ chức vị trí bài tập ước lượng

**Bối cảnh:**

Cần xác định vị trí hiển thị dạng bài tập mới trong hệ thống học tập hiện có.

**Quyết định:**

Tổ chức bài tập ước lượng thành một mục riêng trong bài học số 10, bên cạnh các mục như "Bài tập cơ bản", "Bài tập nâng cao".

**Lý do:**

- Giúp học sinh dễ nhận biết dạng bài tập mới.
- Không làm xáo trộn cấu trúc các mục học tập hiện có.
- Tận dụng hệ thống bài học hiện tại.

---

## ADR-02: Lựa chọn hình thức nhập đáp án

**Bối cảnh:**

Có hai cách để học sinh trả lời câu hỏi ước lượng:
- Nhập một số duy nhất.
- Nhập một khoảng giá trị.

**Quyết định:**

Chọn hình thức nhập khoảng giá trị, gồm cận dưới (L) và cận trên (U).

Một khoảng ước lượng hợp lý cần đáp ứng:
- Cận dưới và cận trên là số nguyên dương.
- Cận dưới nhỏ hơn cận trên (L < U).
- Khoảng ước lượng nằm trong phạm vi từ 0,8X đến 1,2X, với X là đáp án chính xác.
- Khoảng ước lượng phải chứa đáp án chính xác.

**Lý do:**

- Khuyến khích học sinh tư duy theo khoảng thay vì chỉ đưa ra một kết quả duy nhất.
- Có tiêu chí đánh giá cụ thể, thống nhất.
- Có thể kiểm thử tự động.

---

## ADR-03: Thiết kế cách mã hóa đáp án ước lượng

**Bối cảnh:**

Cách chấm điểm hiện tại chủ yếu so sánh chuỗi đáp án chính xác, chưa hỗ trợ đánh giá câu trả lời theo khoảng giá trị.

**Quyết định:**

Bổ sung cách mã hóa đáp án dành riêng cho type `estimate`, lưu thông tin đáp án chính xác và khoảng giá trị được chấp nhận trong `correct_answer`.

Dữ liệu đáp án được biểu diễn theo định dạng:

`exact|min-max`

Trong đó:
- `exact`: đáp án chính xác.
- `min`: cận dưới của khoảng cho phép.
- `max`: cận trên của khoảng cho phép.

Logic chấm điểm sẽ đọc dữ liệu này để đánh giá khoảng ước lượng và đáp án chính xác của học sinh.

**Lý do:**

- Không cần thay đổi cấu trúc chấm điểm của 4 loại câu hỏi cũ.
- Dễ lưu trữ và xử lý dữ liệu.
- Có thể xác định kết quả chấm điểm một cách rõ ràng và tất định.

---

## ADR-04: Quyết định cách tính điểm

**Bối cảnh:**

Dạng bài tập ước lượng cần có cách tính điểm riêng để ghi nhận cả khả năng ước lượng và khả năng tính toán chính xác.

**Quyết định:**

Giữ nguyên cách tính điểm của các dạng câu hỏi cũ.

Đối với mỗi câu hỏi Estimate, tổng điểm là 5 sao:
- Nhập khoảng ước lượng hợp lý: 3 sao.
- Nhập đáp án chính xác: 2 sao.

Học sinh có thể nhận điểm ước lượng ngay cả khi chưa đưa ra đáp án chính xác, miễn là khoảng nhập vào hợp lệ theo quy tắc.

**Lý do:**

- Khuyến khích học sinh rèn luyện khả năng ước lượng.
- Ghi nhận riêng hai kỹ năng: ước lượng và tính toán.
- Không ảnh hưởng đến cơ chế tính điểm cũ.

---

## ADR-05: Tách riêng logic chấm điểm Estimate

### 1. Bối cảnh (Context)

Hệ thống cần bổ sung loại câu hỏi `estimate` vào chức năng luyện tập hiện có.

Logic chấm điểm cần:
- Kiểm tra khoảng ước lượng của học sinh.
- Kiểm tra kết quả tính toán chính xác.
- Tính điểm theo tỷ lệ 3 điểm cho ước lượng và 2 điểm cho kết quả chính xác.
- Không làm thay đổi cách chấm điểm của 4 loại câu hỏi cũ.

### 2. Các phương án (Options)

**Phương án A:**

Giữ logic chấm điểm trong `server/api.js`, bổ sung một hàm xử lý riêng để có thể kiểm thử độc lập.

**Phương án B:**

Tách toàn bộ logic chấm điểm Estimate sang file riêng `server/estimate.js`, sau đó import vào `server/api.js`.

### 3. Quyết định (Decision)

Chọn phương án B.

Tách logic chấm điểm câu hỏi Estimate thành module riêng tại `server/estimate.js`. API nộp bài trong `server/api.js` sẽ gọi module này để xử lý kết quả.

### 4. Lý do (Rationale)

- Tách biệt trách nhiệm giữa API và logic chấm điểm.
- Dễ kiểm thử độc lập.
- Dễ bảo trì và mở rộng.
- Hạn chế ảnh hưởng đến logic của 4 loại câu hỏi cũ.

---

## ADR-06: Kiểm tra dữ liệu đầu vào

**Bối cảnh:**

Học sinh có thể nhập dữ liệu không hợp lệ như nhập chữ, nhập số không hợp lệ hoặc nhập cận dưới lớn hơn hoặc bằng cận trên.

**Quyết định:**

Kiểm tra dữ liệu ngay trong quá trình nhập.

Nếu dữ liệu không hợp lệ:
- Hiển thị thông báo lỗi.
- Yêu cầu học sinh sửa dữ liệu.
- Không chuyển sang bước nhập đáp án chính xác cho đến khi hai cận hợp lệ.

**Lý do:**

- Ngăn dữ liệu không hợp lệ được gửi lên hệ thống.
- Giúp học sinh phát hiện và sửa lỗi ngay tại bước nhập.
- Đảm bảo dữ liệu đầu vào đáp ứng quy tắc chấm điểm.

---

## ADR-07: Quyết định thao tác bàn phím và trạng thái focus

**Bối cảnh:**

Học sinh cần thao tác thuận tiện khi nhập đáp án, đặc biệt khi sử dụng bàn phím thay vì chuột.

**Quyết định:**

Quy định thao tác bàn phím như sau:

**Phím Enter:**
1. Nhập cận dưới, nhấn Enter → chuyển con trỏ sang ô cận trên.
2. Nhập cận trên hợp lệ, nhấn Enter → chuyển con trỏ sang ô kết quả chính xác.
3. Nhập kết quả chính xác, nhấn Enter → vẫn ở ô đó, không tự động nộp bài.

**Phím Tab:**

Chuyển đến phần tử tiếp theo có thể tương tác.

**Phím Shift + Tab:**

Quay lại phần tử có thể tương tác trước đó.

**Trạng thái Focus:**

Khi một ô nhập hoặc phần tử được focus, cần có đường viền hoặc dấu hiệu trực quan rõ ràng để học sinh nhận biết vị trí đang thao tác.

**Lý do:**

- Giúp thao tác nhập liệu nhanh và thuận tiện.
- Hỗ trợ học sinh sử dụng bàn phím.
- Tránh việc nhấn Enter vô tình nộp bài.
- Cải thiện khả năng sử dụng giao diện.

---

## ADR-08: Cấu hình khoảng ước lượng riêng cho từng câu hỏi

**Bối cảnh:**

Mỗi câu hỏi có đáp án chính xác và phạm vi ước lượng phù hợp riêng. Không nên để hệ thống tự tạo khoảng chấp nhận một cách tùy ý khi học sinh nộp bài.

**Quyết định:**

Cấu hình sẵn đáp án chính xác và khoảng giá trị được chấp nhận cho từng câu hỏi trong dữ liệu câu hỏi.

Phiên bản hiện tại sử dụng 12 câu hỏi được chuẩn bị trước. Logic chấm điểm chỉ đọc dữ liệu đã cấu hình để kiểm tra câu trả lời.

**Lý do:**

- Đảm bảo kết quả chấm điểm nhất quán.
- Dễ kiểm soát độ khó và phạm vi chấp nhận của từng câu.
- Tránh việc mỗi câu hỏi có một cách tính khoảng ước lượng khác nhau trong code.

---

## ADR-09: Chỉ chấp nhận dữ liệu số nguyên không âm

**Bối cảnh:**

Trong quá trình nhập đáp án, học sinh có thể nhập chữ, số âm hoặc số thập phân. Những dữ liệu này không phù hợp với phạm vi bài tập hiện tại.

**Quyết định:**

Các ô nhập cận dưới, cận trên và kết quả chính xác chỉ chấp nhận số nguyên không âm.

Hệ thống kiểm tra:
- Dữ liệu phải là số hợp lệ.
- Không chấp nhận chữ hoặc ký tự không hợp lệ.
- Không chấp nhận số âm.
- Không chấp nhận số thập phân.
- Cận dưới phải nhỏ hơn cận trên.

Nếu dữ liệu không hợp lệ, hiển thị thông báo để học sinh sửa trước khi tiếp tục.

**Lý do:**

- Phù hợp với dạng bài tập toán lớp 3 hiện tại.
- Hạn chế lỗi nhập liệu.
- Giúp dữ liệu gửi lên hệ thống có định dạng thống nhất.

---

## ADR-10: Lưu bản nháp câu trả lời trong quá trình làm bài

**Bối cảnh:**

Học sinh có thể vô tình tải lại trang hoặc rời khỏi trang khi đang làm bài, dẫn đến mất những câu trả lời đã nhập.

**Quyết định:**

Sử dụng `localStorage` để lưu tạm dữ liệu câu trả lời trong quá trình làm bài.

Khi học sinh quay lại bài tập, hệ thống khôi phục dữ liệu đã lưu trước đó.

Sau khi nộp bài thành công, hệ thống xóa bản nháp tương ứng.

**Lý do:**

- Hạn chế mất dữ liệu khi học sinh đang làm bài.
- Tạo trải nghiệm sử dụng liên tục.
- Tránh giữ lại bản nháp sau khi bài làm đã được nộp thành công.

---

## ADR-11: Chấm điểm ở phía máy chủ và lưu kết quả bài làm

**Bối cảnh:**

Nếu chỉ chấm điểm ở phía giao diện, kết quả có thể không đáng tin cậy. Hệ thống cần đảm bảo dữ liệu bài làm và điểm số được xử lý tập trung.

**Quyết định:**

Giao diện gửi câu trả lời đến API nộp bài thông qua `POST /api/submissions`.

Máy chủ thực hiện:
- Nhận dữ liệu câu trả lời.
- Xác định loại câu hỏi.
- Gọi logic chấm điểm tương ứng.
- Tính tổng điểm.
- Lưu câu trả lời và kết quả vào database.
- Trả kết quả về giao diện.

Đối với câu hỏi Estimate, sử dụng module `server/estimate.js`. Các loại câu hỏi cũ tiếp tục sử dụng logic chấm điểm hiện có.

**Lý do:**

- Đảm bảo kết quả chấm điểm được xử lý ở phía máy chủ.
- Dữ liệu bài làm được lưu trữ tập trung.
- Giữ được sự tương thích với các dạng bài tập cũ.

---

## ADR-12: Tổ chức kiểm thử tự động theo từng thành phần

**Bối cảnh:**

Chức năng Estimate có nhiều phần cần kiểm tra: logic chấm điểm, API, lưu dữ liệu và giao diện nhập đáp án.

**Quyết định:**

Sử dụng bộ kiểm thử tự động của Node.js với lệnh `npm test`.

Chia kiểm thử thành các nhóm:
- Kiểm thử logic chấm điểm Estimate.
- Kiểm thử API và quá trình xử lý bài nộp.
- Kiểm thử giao diện và thao tác nhập liệu.

Các trường hợp kiểm thử bao gồm dữ liệu hợp lệ, dữ liệu không hợp lệ và các tình huống biên.

**Lý do:**

- Dễ phát hiện lỗi khi thay đổi code.
- Kiểm tra được từng thành phần độc lập.
- Hạn chế việc sửa chức năng mới làm ảnh hưởng chức năng cũ.

---

## ADR-13: Tự động chạy kiểm thử thông qua CI

**Bối cảnh:**

Việc chỉ chạy kiểm thử trên máy cá nhân chưa đủ để đảm bảo code hoạt động trong môi trường sạch hoặc trên các phiên bản Node.js khác nhau.

**Quyết định:**

Sử dụng GitHub Actions để tự động chạy kiểm thử khi có Pull Request và khi push lên nhánh `main`.

Quy trình CI thực hiện:
1. Checkout mã nguồn.
2. Thiết lập phiên bản Node.js.
3. Cài đặt dependencies bằng `npm ci`.
4. Chạy bộ kiểm thử bằng `npm test`.

**Lý do:**

- Phát hiện lỗi trước khi hợp nhất code.
- Kiểm tra khả năng cài đặt và chạy dự án từ môi trường sạch.
- Tăng độ tin cậy của sản phẩm.
