# Memo Teardown — Cursor AI

**Họ tên:** Đinh Xuân Quyền

**Vì sao chọn sản phẩm này:** Em chọn Cursor vì đây là một ví dụ rất thực tế cho bài học về Vertical AI. Thay vì làm một cái tool bọc ngoài API (wrapper mỏng) cho có lệ, đội ngũ Cursor đã chủ động can thiệp sâu vào workflow của dev để tạo ra giá trị khác biệt hẳn.

**§1. Timeline các cập nhật lớn**

| Thời điểm | Cập nhật                                                                  | Context lúc đó                                                                                                                                  | Nguyên lý                                                                                                                                                                                                                                                                                                               |
| ------------ | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 01/2023      | Ra mắt Cursor (Fork thẳng từ VS Code)                                    | Github Copilot đang chiếm ưu thế dưới dạng extension. Hầu hết các tool AI lúc đó đều làm extension để dễ kéo user từ VS Code. | **Tránh bẫy Wrapper mỏng**: Làm extension thì bị kìm hãm bởi API của IDE cũ. Fork VS Code cực kỳ tốn sức nhưng lại giúp Cursor toàn quyền sửa UI/UX, tạo lợi thế độc quyền mà các extension khác không làm được. (Nguồn: [Cursor Github](https://github.com/getcursor/cursor))   |
| 03/2023      | Tích hợp GPT-4 ngay khi model vừa ra mắt                                | OpenAI vừa ra mắt GPT-4 với khả năng logic tốt hơn hẳn GPT-3.5.                                                                            | **Quy tắc x10**: Đưa model mạnh nhất vào lập trình để nâng chất lượng code lên gấp 10 lần, thay vì tối ưu chi phí bằng các model yếu hơn. (Nguồn: [Cursor Changelog](https://cursor.com/changelog))                                                                                        |
| 10/2023      | Nhận đầu tư 8 triệu USD từ quỹ OpenAI Startup Fund                   | OpenAI đang gom tiền đầu tư cho các dự án AI-native.                                                                                       | **Vertical AI (AI Expert + Domain Expert)**: Thay vì làm chatbot đa năng, Cursor chọn ngách siêu hẹp là lập trình. Họ dùng hiểu biết (domain expertise) về thói quen viết code của dev để thiết kế tính năng. (Nguồn: [Wikipedia Cursor](https://en.wikipedia.org/wiki/Cursor_(software))) |
| 04/2024      | Ra mắt Copilot++ (hiện tại là Cursor Tab)                               | Các tool khác chỉ biết gợi ý dòng code tiếp theo. Thực tế dev tốn rất nhiều thời gian để xóa và sửa code cũ.                   | **Khai thác Tri thức ẩn (Tacit Knowledge)**: Cursor học được thói quen "sửa dòng trên, xóa dòng dưới" của dev để gợi ý sửa nhiều dòng cùng lúc chỉ bằng một nút Tab. (Nguồn: [Cursor Changelog](https://cursor.com/changelog))                                                         |
| 08/2024      | Ra mắt Composer (Edit nhiều file cùng lúc)                              | Dev hiếm khi code một tính năng chỉ trong 1 file (thường dính đến HTML, CSS, JS...). Việc chat với AI để sửa từng file rất mệt.  | **First Principles Thinking & JTBD**: User không cần "gõ một đoạn code", việc họ thực sự cần hoàn thành là "lên sóng một tính năng mới". Composer giải quyết đúng nhu cầu gốc rễ này. (Nguồn: [Cursor Forum](https://forum.cursor.com/))                                                |
| 08/2024      | Bỏ tính năng tự nhập API Key (Bring Your Own Key) cho các tác vụ AI | Cursor muốn quản lý tốt hơn chi phí và tối ưu model phía server.                                                                         | **Kiểm soát chất lượng End-to-end**: Tránh tình trạng user cắm API key xài model dỏm rồi chê app tệ, bắt user chuyển sang gói Pro $20/tháng để có trải nghiệm đồng nhất. (Nguồn: [Cursor Changelog](https://cursor.com/changelog))                                                        |

**Vì sao chọn những mốc này:** Em chọn lọc những lần ra mắt tính năng lớn (như Fork VS Code, Copilot++, Composer) vì đây là các quyết định bản lề thay đổi cách dev viết code, thể hiện rõ bài học về việc tìm kiếm lợi thế cạnh tranh. Em bỏ qua các bản cập nhật sửa lỗi nhỏ lẻ vì chúng không làm thay đổi chiến lược sản phẩm.

**§2. Tệp user & JTBD**

|                                        | Early adopters                                                                                                   | Tệp hiện tại                                                                                                             |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Đặc điểm                           | Frontend dev ở các startup nhỏ, mê công nghệ mới, thích thử nghiệm tool AI ngoài VS Code quen thuộc. | Dev ở mọi cấp độ, Tech lead, CTO. Mở rộng dần sang khối doanh nghiệp  cần đẩy nhanh tiến độ dự án.       |
| JTBD chính                            | "Viết hàm nhanh hơn", "Khám phá xem tool AI này code xịn đến đâu".                                    | "Hoàn thành toàn bộ một tính năng/dự án trong thời gian ngắn nhất", "Đọc hiểu và refactor source code cũ". |
| Trước đó họ làm bằng cách nào | Dùng VS Code + Github Copilot, đoạn nào khó quá thì copy paste sang ChatGPT hỏi.                         | Vẫn dùng Cursor nhưng thay vì tự gõ, họ chuyển sang giao việc cho Composer tự sửa nhiều file.                  |

**Dịch chuyển tệp:** Sự xuất hiện của **Composer (08/2024)** là bước ngoặt. Tính năng này biến Cursor từ cái máy gõ thành một công cụ giải quyết bài toán lớn, kéo theo sự quan tâm của các Senior/Tech Lead - những người quan tâm tới việc giao sản phẩm nhanh hơn là việc ngồi gõ phím.

**Switching cost (map 4 forces):**

* **Push (Vấn đề với sản phẩm cũ):** Dùng VS Code + Copilot bị chậm, context loanh quanh 1 file, mất công copy-paste qua lại.
* **Pull (Sức hút cái mới):** Cursor Tab sửa được nhiều dòng cực mượt, Composer xử lý được cả chục file cùng lúc (tăng tốc x10).
* **Anxiety (Nỗi lo chuyển đổi):** Lúc mới qua sợ mất phím tắt quen thuộc, sợ hư môi trường. Cursor giải quyết bằng cách cho 1 click import nguyên xi setting từ VS Code sang.
* **Habit (Thói quen cũ):** User ngại đổi giao diện, lười học luồng làm việc mới.
  => **Lực giữ mạnh nhất hiện tại:** Chính là thói quen dùng *Cursor Tab*. Một khi dev đã quen nhịp độ cứ gõ rồi ấn Tab để app tự sửa nhiều dòng liên tiếp, nếu quay lại VS Code bình thường sẽ thấy vô cùng hụt hẫng và chậm chạp.

**§3. Ba dự đoán hướng đi (6–12 tháng tới)**

**Dự đoán 1** *(loại: mở rộng tính năng / sản phẩm)*

- **Dự đoán:** Cursor sẽ cho ra mắt dạng Cloud Agent (chạy ngầm trên server), dev chỉ cần gõ yêu cầu rồi đi ngủ, sáng hôm sau có sẵn một Pull Request hoàn chỉnh để review.
- **Lập luận:** Dựa vào cột mốc ra mắt Composer ở §1 và sự chuyển dịch tệp user sang Tech Lead ở §2. Những người này phải xử lý luồng công việc phức tạp, tốn thời gian. Việc có agent chạy ngầm sẽ giúp tối ưu hóa triệt để sức lao động của họ.

**Dự đoán 2** *(loại: đe dọa từ Big Tech)*

- **Dự đoán:** Microsoft sẽ sớm mang các tính năng y chang Composer hay Cursor Tab tích hợp thẳng vào VS Code. Cursor sẽ phải đáp trả bằng cách tự train các model AI chuyên biệt gõ code ngon hơn OpenAI.
- **Lập luận:** Bài học về "Wrapper mỏng" cho thấy VS Code có mạng lưới phân phối quá khủng. Dù Cursor đã fork mã nguồn để tạo thế phòng thủ, Big Tech vẫn dư sức đập đi làm lại. Cursor buộc phải đào sâu hơn nữa vào Domain Expertise (hiểu thói quen dev) để sống sót.

**Dự đoán 3** *(loại: mở rộng segment & mô hình kiếm tiền)*

- **Dự đoán:** Cursor sẽ đẩy mạnh gói doanh nghiệp (Enterprise), cho phép tool tự động đọc ticket từ Jira, tự pull code, viết code và chạy test CI/CD.
- **Lập luận:** Tệp user hiện tại (§2) đang dịch chuyển sang team/doanh nghiệp. JTBD của họ không chỉ dừng ở mức viết code mà là giải quyết gọn gàng các task (ticket) trong Jira và đưa lên môi trường test thành công.

**§4. AI Log**

| Việc                                                     | AI làm hay bạn làm?                     | Bạn kiểm chứng/phán đoán lại thế nào?                                                                                                                |
| --------------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Đào timeline ra mắt tính năng của Cursor            | AI (Dùng Web Search để lọc thông tin) | Em tự lên mạng dò lại chéo các trang blog và changelog của Cursor để đối chiếu ngày tháng, loại bỏ các mốc update nhỏ lẻ kiểu fix bug. |
| Gắn nhãn nguyên lý (x10, wrapper, tacit knowledge...) | Em tự làm                                | Dựa trên những gì học ở Day 1, em tự phân tích sự kiện thực tế của app và ráp nối vào đúng thuật ngữ của bài giảng.                  |
| Phân tích tệp User và JTBD                            | Em tự làm                                | Đúc kết từ quan sát của cá nhân và xem các review từ cộng đồng dev khi họ chuyển qua dùng Cursor.                                            |
| Suy nghĩ ra 3 dự đoán                                 | Em tự làm                                | Logic hoàn toàn dựa trên những dữ liệu em vừa móc ra ở timeline và hành vi user ở trên, không để AI tự đẻ ra dự đoán viển vông.      |
