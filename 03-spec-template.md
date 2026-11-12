# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

# Bài nộp LAB5 — [Track] · Nhóm [tên]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

## §1. Lát cắt & phạm vi
- Lát cắt (chép từ track).
- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

### Lớp ② · Mơ hồ / thiếu thông tin

Dữ liệu dựng (`tra_cuu_dat_cho`): đặt chỗ TRV-7Q2K có 2 hành khách là chị An (34 tuổi) và bé Bình (5 tuổi). Chuyến BM 213 lúc 19:00 ngày 12/11 bị huỷ do bão. Còn 3 chuyến thay thế: BM 217 lúc 21:00 ngày 12/11 còn 1 chỗ, BM 201 lúc 07:00 ngày 13/11 còn 9 chỗ, BM 205 lúc 09:30 ngày 13/11 còn 4 chỗ.

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào | Một sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| ②-a | *"Đổi giúp mình sang chuyến sớm nhất còn chỗ đi, gấp lắm."* | ② Mơ hồ / thiếu | Theo `tra_cuu_dat_cho`, chuyến sớm nhất là **BM 217 lúc 21:00, nhưng chỉ còn 1 chỗ**, mà đặt chỗ có **2 hành khách**. AI hiểu "sớm nhất" theo giờ bay và gọi `doi_chuyen_bay` cho 1 người. Như vậy bé Bình 5 tuổi bị tách khỏi mẹ, hoặc lần đổi miễn phí duy nhất bị dùng mất cho một chuyến không chở được cả hai mẹ con. | Nói rõ BM 217 chỉ còn 1 chỗ, không đủ cho 2 người. Đề xuất **BM 201 lúc 07:00 ngày 13/11**, chuyến sớm nhất đủ chỗ cho cả hai. Gọi `giu_cho_chuyen_moi` cho 2 người, hiện đếm ngược 20 phút, rồi chờ khách bấm xác nhận mới đổi vé. | **Không chấp nhận được** |
| ②-b | *"Ok lấy chuyến 9h nhé."* (khách trả lời sau khi AI đưa danh sách 3 chuyến) | ② Mơ hồ / thiếu | Nhiều người Việt viết "9h" để chỉ 9 giờ tối. Danh sách có cả **BM 217 lúc 21:00 (9 giờ tối nay)** và **BM 205 lúc 09:30 (9 rưỡi sáng mai)**. AI chọn theo một cách hiểu rồi gọi `doi_chuyen_bay` ngay, coi "ok" là đã xác nhận. Nếu đoán sai, lần đổi miễn phí đã mất và chuyến đúng có thể hết chỗ: BM 217 chỉ còn 1 chỗ, BM 205 còn 4. | Không đoán. Hỏi lại bằng 2 nút có ghi rõ ngày giờ: "21:00 tối nay 12/11, chỉ còn 1 chỗ, không đủ cho 2 người" và "09:30 sáng mai 13/11, còn 4 chỗ". Có thể giữ chỗ BM 205 trong lúc chờ khách bấm. Chỉ đổi vé khi khách bấm đúng một chuyến cụ thể, không đổi chỉ vì khách gõ "ok". | **Không chấp nhận được** |

Tên lỗi:
- ②-a · **Đúng giờ nhưng sai người.** Câu trả lời trông đúng vì 21:00 đúng là chuyến sớm nhất, nhưng AI bỏ qua số hành khách trong đặt chỗ.
- ②-b · **Coi "ok" mơ hồ là đã xác nhận.** Đây đúng là loại ca "khách xác nhận mơ hồ" mà track bắt buộc phải demo.

Cả hai đều chọn "không chấp nhận được" vì cùng dẫn tới `doi_chuyen_bay`. Việc này gần như không đảo lại được: mất lần đổi miễn phí duy nhất, và chuyến đúng có thể đã hết chỗ.

## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

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
