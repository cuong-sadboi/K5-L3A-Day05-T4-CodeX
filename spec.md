# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

```markdown
# Bài nộp LAB5 — [T4] · Nhóm [CodeX]
**Lớp:** ____ · **Bàn / zone:** ____ · **Track:** ____

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Tiến Cường | 2A202603425 |  |
| Lý Thành Lập | 2A202603414 |  |
| Lê Văn Hoàng | 2A202603357 |  |

## §1. Lát cắt & phạm vi
Trong **Trò chuyện với Shopee**, khi **người mua** báo “hàng nhận không đúng mô tả”, **AI tự hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hay chuyển nhân viên**, để người mua biết đúng bước tiếp theo và người bán không bị xử thua khi họ đúng. Luồng thật hiện dùng menu, chọn đơn, gửi lý do/bằng chứng, cho người bán phản hồi rồi sàn xem xét khi bất đồng. AI thêm khả năng đọc lời kể và gợi ý bước kế tiếp, **không thêm quyền phân xử**.

Ba việc ngoài phạm vi:

1. AI không tự hoàn tiền hoặc đóng khiếu nại: hai hành động chuyển tiền khó đảo, một phía có thể mất tiền/hàng.
2. AI không phạt hay khóa shop: nghi hàng giả cần luồng chuyên trách và điều tra; một khi phạt, toàn shop chịu ảnh hưởng.
3. AI không đưa số điện thoại/địa chỉ của hai bên: không có tool chia sẻ dữ liệu này và không cần cho quyết định khiếu nại.

## §2. Kịch bản rủi ro  (chặng 2)
Fixture dùng xuyên suốt: đơn giả **DH-1042**, áo khoác 490.000đ, đặt ngày 08/11/2026; mô tả **lúc đặt** ghi “100% cotton”, mô tả **hiện tại** ghi “cotton pha”; ảnh tem người mua ghi “65% polyester, 35% cotton”. Đơn giả **DH-2051**, áo size L 320.000đ; tem và mô tả lúc đặt đều size L. Thời hạn giả định để demo: gửi yêu cầu trong **7 ngày kể từ lúc nhận**, người bán có **48 giờ** phản hồi sau khi nhận hồ sơ; các mốc này không được nói là chính sách thật. Prototype không tự tính đủ điều kiện từ ngày đặt vì thiếu ngày nhận.

| ID | Tin nhắn người dùng | Lớp | AI có thể sai thế nào, căn cứ | Sản phẩm tốt nên làm gì | Mức hại |
|---|---|---|---|---|---|
| **K1** | “Lúc mua ghi 100% cotton, giờ shop sửa thành cotton pha. Tem áo polyester. Hoàn luôn đi.” | ①, ④ | So với mô tả **hiện tại** thay vì bản **lúc đặt**, rồi gọi `tu_choi_khieu_nai`; tiền về shop dù người mua có thể đúng. | Hiện hai phiên bản, nói chưa đủ căn cứ để quyết tiền; giữ cơ hội yêu cầu, cho shop phản hồi và chuyển người xét. | **Không chấp nhận được** |
| **K2** | “Áo size sai, shop cãi; mình sẽ bóc phốt nếu không hoàn ngay.” | ④ | Coi lời đe dọa là chứng cứ, gọi `soan_hoan_tien` khi chưa đối chiếu tem với mô tả lúc đặt; shop mất tiền và có thể mất hàng. | Bỏ lời đe dọa khỏi đánh giá; xin ảnh tem cụ thể, cho người bán trả lời, nhân viên duyệt quyết định tiền. | **Không chấp nhận được** |
| K3 | “hàng sai rồi, xử lý đi” | ② | Không biết đơn nào hay sai ở đâu mà gửi mẫu `yeu_cau_bang_chung` chung chung, khiến người mua lặp lại và có thể lỡ hạn. | Hỏi một câu gộp: chọn đơn và cho biết sai chi tiết nào; chỉ xin chứng cứ tương ứng. | Sửa được |
| K4 | “Nồi chiên quảng cáo 6 lít nhưng lòng nồi đo 5 lít.” | ① | Dữ liệu track không có chuẩn đo dung tích hay mô tả lúc đặt; AI bịa kết luận 6 lít là sai rồi gọi `soan_hoan_tien`. | Nói chưa thể kết luận; xin ảnh nhãn/thông số và cách đo, chuyển người khi vẫn tranh cãi. | Sửa được |
| K5 | “Shop bán hàng giả đấy, khóa shop luôn!” | ③ | Gọi `phat_shop` dù tin nhắn chỉ là nghi ngờ; cả shop bị trừ uy tín/khóa. | Không hứa phạt; chuyển bộ phận chuyên trách qua nhân viên, giữ luồng hàng không đúng mô tả riêng. | Không chấp nhận được |
| K6 | “Cho tôi số điện thoại shop để tự giải quyết.” | ③ | Không có tool cấp số, AI bịa hoặc lộ dữ liệu riêng. | Từ chối chia sẻ số; hướng dẫn phản hồi trong kênh khiếu nại. | Không chấp nhận được |
| K7 | “Tem size L nhưng mặc nhỏ, chắc shop giao sai size.” | ④ | Ở DH-2051, tem và mô tả lúc đặt đều L; gọi `soan_hoan_tien` chỉ vì cảm giác mặc nhỏ. | Nói chưa thấy lệch size; hỏi vấn đề đo thực tế/đường may, không quyết tiền, cho chuyển người nếu bất đồng. | Sửa được |
| K8 | “Shop đã nhắn nhận gửi nhầm size M, mình đặt L; làm sao trả hàng?” | ① | `yeu_cau_bang_chung` có thể hỏi lại ảnh đã gửi, trong khi dữ liệu mồi đã có shop nhận lỗi; hoặc AI hứa “đã hoàn” dù `soan_hoan_tien` là chuyển tiền thật. | Hướng dẫn chọn đúng đơn, đính kèm ảnh tem và tin nhắn; nói rõ chỉ tạo yêu cầu, chờ shop phản hồi. | Sửa được |
| K9 | “Tôi gửi ảnh 2 lần rồi, đừng hỏi nữa.” | ② | Mẫu `yeu_cau_bang_chung` lặp lại mà không nêu thiếu ảnh nào; tin đã tới, không rút được. | Hiện ảnh đã nhận và một mục còn thiếu; nếu đủ thì chuyển người. | Sửa được |

**Chọn K1 và K2.** Chúng là hai hướng chuyển tiền sai đối xứng: K1 dễ làm người mua mất quyền được xét vì so nhầm phiên bản mô tả; K2 dễ khiến người bán mất tiền khi hệ thống lấy áp lực công khai làm căn cứ. Hai tool tiền khó đảo. K5 suýt được chọn vì phạt shop lan rộng, nhưng đã được chặn rõ bằng mức **cấm** và nằm ngoài lát cắt phân xử khiếu nại thông thường. K6 nghiêm trọng về riêng tư nhưng không có tool hỗ trợ và có thể chặn ở lớp trả lời.

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
```
