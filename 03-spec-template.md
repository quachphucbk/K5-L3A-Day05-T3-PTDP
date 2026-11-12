# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

```markdown
# Bài nộp LAB5 — [Track] · Nhóm [tên]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

## §1. Lát cắt & phạm vi
- Lát cắt (chép từ track).
- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

### Kịch bản 1 — Sửa được
- Tên lỗi: Báo chuyến vẫn bay dù đã bị huỷ.
- Tin người dùng: "Chuyến của mình mấy giờ bay vậy?"
- Lớp: ① AI bịa.
- AI có thể sai: AI trả lời chuyến BM 213 vẫn bay lúc 19:00, bỏ qua trạng thái đã huỷ.
- Bằng chứng: tra_cuu_dat_cho ghi BM 213 lúc 19:00, trạng thái ĐÃ HUỶ do bão.
- Sản phẩm tốt nên làm gì: Kiểm tra trạng thái, đính chính chuyến đã huỷ và đề xuất chuyến thay thế trước khi khách hành động theo thông tin sai.
- Nhãn: Sửa được.

### Kịch bản 2 — Không chấp nhận được
- Tên lỗi: Đoán giờ hạ cánh khi không có thông tin.
- Tin người dùng: "Chuyến bị huỷ rồi à? Vậy đổi giúp mình sang sáng mai nhé."
- Lớp: ① AI bịa.
- AI có thể sai: AI tự khẳng định chuyến BM 201 lúc 07:00 sẽ đến trước 09:00, khiến khách tin và quyết định đổi.
- Bằng chứng: tra_cuu_dat_cho chỉ cung cấp giờ khởi hành 07:00, không có giờ đến. Tool doi_chuyen_bay làm mất lượt đổi miễn phí, khó hoàn tác.
- Sản phẩm tốt nên làm gì: Không đoán giờ đến; thông báo thiếu dữ liệu và xác nhận rõ chuyến bay, hành khách trước khi đổi vé.
- Nhãn: Không chấp nhận được.

## §3. Khi AI sai  (chặng 3)


## 3.1 Kịch bản — AI tự ý hoàn vé khi khách chưa xác nhận

- Tin người dùng: "Nếu tôi không bay nữa thì có được hoàn tiền không?"
- Lớp: ④ Đặc thù domain.
- Tên lỗi: Biến câu hỏi thành hành động không thể hoàn tác.
- AI có thể sai: Tự gọi `gui_yeu_cau_hoan_ve` dù khách chỉ hỏi thông tin.
- Bằng chứng: Tool `gui_yeu_cau_hoan_ve` gửi yêu cầu hoàn vé, sau khi gửi không thể huỷ.
- Nhãn: Không chấp nhận được.

### 1. Khi AI không chắc, nên làm gì?

- Chọn: Trả lời kèm giới hạn.
- AI giải thích chính sách hoàn vé dựa trên dữ liệu nhưng không tự gửi yêu cầu.
- Không chọn hỏi lại ngay vì khách chỉ hỏi về quyền hoàn tiền.
- Không chuyển nhân viên ngay vì AI có dữ liệu chính sách. Nếu không xác minh được thì mới chuyển nhân viên.

### 2. AI nói gì, nguyên văn?

- "Chuyến bay của bạn đã bị huỷ do bão. Theo chính sách, bạn được hoàn toàn bộ tiền vé hoặc đổi chuyến miễn phí một lần trong 48 giờ. Nếu gửi yêu cầu hoàn, bạn không thể huỷ yêu cầu sau đó. Tôi chưa thực hiện thao tác hoàn vé nào. Bạn có muốn xem hướng dẫn hoàn tiền không?"
- Không hứa tiền về ngay hoặc cam kết thời gian hoàn khi chưa có dữ liệu.

### 3. Người dùng thấy gì trên màn hình?

- Trạng thái: Chưa gửi yêu cầu hoàn vé.
- Độ chắc chắn: Thông tin chính sách đã được xác minh từ dữ liệu đặt chỗ, không hiển thị tỷ lệ tự đoán.
- Bằng chứng: Mã đặt chỗ TRV-7Q2K, chuyến BM 213 đã huỷ do bão và chính sách hoàn toàn bộ vé.
- Cảnh báo: Gửi yêu cầu hoàn rồi không thể huỷ.
- Nút: "Xem chính sách", "Tiếp tục hoàn vé", "Gặp nhân viên".

### 4. Người dùng có thể làm gì tiếp?

- Xem chính sách và điều kiện hoàn tiền.
- Tiếp tục quy trình hoàn vé, xác nhận rõ trước khi gửi.
- Chọn đổi chuyến hoặc gặp nhân viên.
- Nếu không làm gì: AI không tự gửi yêu cầu hoàn hoặc thay đổi vé.
- Nếu AI đã gửi nhầm: Không thể tự hoàn tác qua tool, phải chuyển nhân viên hỗ trợ ngay.

### 5. Ai được báo và sau bao lâu?

- Khách hàng: Được cảnh báo trước khi xác nhận gửi yêu cầu hoàn vé.
- Nếu AI gửi nhầm: Báo khách ngay khi phát hiện lỗi.
- Nhân viên: Nhận cảnh báo ngay khi hệ thống phát hiện yêu cầu hoàn gửi sai.
- Nhân viên thấy: Mã đặt chỗ, thời gian thực hiện, lịch sử chat, thao tác AI đã làm và trạng thái yêu cầu hoàn.
- Đây là cơ chế thông báo do nhóm đề xuất thiết kế.

### 6. Đây là loại lỗi gì?

- Phân loại: Lỗi hệ thống.
- Nguyên nhân: AI hiểu câu hỏi về chính sách thành lệnh thực hiện hoàn vé.
- Không phải lỗi người dùng vì khách chưa yêu cầu gửi hoàn vé.
- Cách xử lý: AI xin lỗi, thông báo trung thực trạng thái yêu cầu hoàn và chuyển nhân viên nếu đã gửi nhầm.
- Cách khắc phục: Sửa quy trình xác nhận, không chỉ sửa nội dung câu trả lời.

### 7. Chỉ sửa câu chữ có đủ không?

- Không đủ, phải thay đổi thiết kế hệ thống.
- Bắt buộc xác nhận rõ hành khách và yêu cầu hoàn trước khi gọi `gui_yeu_cau_hoan_ve`.
- Hiển thị cảnh báo không thể hoàn tác trước khi xác nhận.
- Chặn AI tự gọi tool hoàn vé khi khách chỉ hỏi thông tin.
- Lưu lịch sử thao tác để phát hiện và xử lý lỗi.

## 3.2. Bốn đường đi của trải nghiệm

### Kịch bản: AI tự ý hoàn vé khi khách chưa xác nhận

- Tin người dùng: "Nếu tôi không bay nữa thì có được hoàn tiền không?"
- Lớp: ④ Đặc thù domain.
- Nhãn: Không chấp nhận được.

### 1. Happy path — AI xử lý đúng

- AI nhận biết khách chỉ đang hỏi về chính sách hoàn tiền.
- Gọi `tra_cuu_dat_cho` để kiểm tra thông tin.
- Thông báo khách được hoàn toàn bộ vé vì chuyến bị huỷ do bão.
- Hiển thị nút "Xem chính sách" và "Tiếp tục hoàn vé".
- Không tự gọi `gui_yeu_cau_hoan_ve` khi khách chưa xác nhận.

### 2. Low-confidence — AI không chắc chắn

- AI không truy xuất được dữ liệu đặt chỗ hoặc chính sách.
- Thông báo: "Hiện tôi chưa xác minh được điều kiện hoàn tiền của vé này."
- Hiển thị nút "Thử lại" và "Gặp nhân viên".
- Không tự gửi yêu cầu hoàn tiền khi chưa xác minh.

### 3. Failure — AI xử lý sai

- AI hiểu câu hỏi "Có được hoàn tiền không?" thành yêu cầu hoàn vé.
- Tự gọi `gui_yeu_cau_hoan_ve` khi khách chưa xác nhận.
- Yêu cầu hoàn vé được gửi và không thể huỷ.
- Khách có nguy cơ mất cơ hội đổi chuyến và phải chờ xử lý hoàn tiền.

### 4. Correction — Người dùng sửa AI

- Khách phản hồi: "Tôi chỉ hỏi thôi, ai bảo bạn hoàn vé?"
- AI kiểm tra xem yêu cầu hoàn đã được gửi hay chưa.
- Nếu chưa gửi: Dừng thao tác và xác nhận vé chưa bị thay đổi.
- Nếu đã gửi: Xin lỗi, thông báo không thể tự huỷ yêu cầu và gọi `chuyen_nhan_vien` ngay.
- Nhân viên nhận thông tin đặt chỗ, lịch sử trò chuyện và thao tác sai.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
```
