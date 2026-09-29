# KTD Editorial Content Renewal — Runtime Skill

**Skill Runtime:** 1.5.0  
**Prompt Set:** 1.6.0  
**Workflow policy:** MATERIAL_DECISION_COVERAGE_V3

## 1. Mục tiêu

Làm mới bài thành phiên bản hiện hành, rõ ràng, hữu ích và **đủ an toàn để đăng**, đồng thời tránh biến quy trình thành cuộc kiểm toán mọi chi tiết.

Mục tiêu vận hành:

1. tăng độ chính xác chuyên môn ở đúng các quyết định có thể làm độc giả áp dụng sai hoặc ảnh hưởng uy tín;
2. bảo đảm title/intro/scope statement không hứa rộng hơn căn cứ đã khóa;
3. bảo đảm mọi material teaching claim trong Final truy vết được về quyết định chuyên môn đã đủ căn cứ;
4. áp dụng tổng quát cho kế toán, thuế, pháp lý, thủ tục, biểu mẫu, bài một hoặc nhiều chế độ/phạm vi;
5. không hard-code logic theo một bài, một thông tư hay một regression case;
6. giữ điểm dừng cứng, không chạy vòng vô hạn.

## 2. Chuẩn trọng yếu

Một lỗi chỉ được **CHẶN ĐĂNG** khi có khả năng đáng kể:

- làm người đọc áp dụng sai;
- làm sai văn bản/chế độ/đối tượng/fact pattern/thời kỳ áp dụng;
- làm phạm vi công khai rộng hơn evidence có thể bảo vệ;
- làm sai kết luận chính của bài;
- làm sai formula/rate/threshold/deadline/classification/account/treatment/procedure chính;
- bỏ condition/exception trọng yếu khiến rule dễ áp sai;
- làm sai official form/table/template;
- tạo mâu thuẫn trọng yếu giữa intro/body/formula/example/warning/table/summary.

Các vấn đề sau **không tự động chặn đăng**:

- TK112/TK331 hoặc trạng thái thanh toán trong ví dụ khi không phải teaching target;
- tài khoản đối ứng phụ hoặc bước trung gian không làm thay đổi treatment;
- supporting detail được gộp/rút gọn hợp lý;
- wording/polish/emphasis nhỏ;
- resource migration không ảnh hưởng correctness.

## 3. CORE được định nghĩa hẹp

`CORE` chỉ dành cho nội dung mà nếu mất/sai sẽ:

- làm bài không còn đáp ứng title/phạm vi chính; hoặc
- khiến độc giả hiểu/áp dụng sai đáng kể; hoặc
- làm hỏng một learning objective chính.

Không biến mọi câu, mọi ví dụ, mọi bút toán hay mọi số tài khoản thành CORE.

`SUPPORTING` có thể được gộp, rút gọn hoặc viết trung tính nếu không làm mất bài học chính và không tạo sai lệch trọng yếu.

## 4. Bảng phạm vi công khai — Sxx

Sxx mô tả những phạm vi mà bài thực sự công bố hoặc dựa vào để hướng dẫn người đọc, lấy từ title, intro, scope box, câu áp dụng, đối tượng, thời kỳ, chế độ hoặc lớp quy định.

Không biến mọi citation thành Sxx chi phối. Một nguồn có thể chỉ là bối cảnh hoặc chỉ chi phối một số decision.

Mỗi Sxx cần xác định:

- phạm vi/đối tượng/thời kỳ/chế độ hoặc lớp quy định;
- vai trò trong bài;
- `TRONG PHẠM VI` hay `CHỈ BỐI CẢNH/THAM KHẢO`;
- nếu trong phạm vi, nhóm decision nào nó có thể chi phối.

Các câu hứa rộng như “hiện hành”, “áp dụng chung”, “mọi doanh nghiệp”, “theo quy định năm ...” là public-scope signal và phải được kiểm khi chúng ảnh hưởng treatment.

## 5. Bảng quyết định chuyên môn trọng yếu — Dxx

Bước 2 tạo Bảng Dxx nhỏ, **không có quota**.

Một Dxx chỉ tồn tại khi sai decision đó có thể ảnh hưởng đáng kể đến thực hành, kết luận chính hoặc uy tín.

Mỗi Dxx phải khóa:

- decision cần chốt;
- CORE liên quan;
- căn cứ chính;
- coverage theo các Sxx trong phạm vi có khả năng chi phối;
- kết luận theo từng Sxx thực sự chi phối;
- relation type;
- chỉ dẫn cách viết;
- `COVERAGE: ĐỦ | THIẾU`;
- trạng thái căn cứ.

### Coverage theo Sxx

Mỗi Sxx có khả năng chi phối Dxx phải được phân loại một trong:

- `CHI PHỐI — CÙNG KẾT LUẬN`;
- `CHI PHỐI — KHÁC KẾT LUẬN`;
- `CHI PHỐI — CÓ ĐIỀU KIỆN/NGOẠI LỆ`;
- `KHÔNG CHI PHỐI Dxx — lý do cụ thể`.

Dxx chỉ được `COVERAGE: ĐỦ` khi tất cả Sxx trong public scope có khả năng chi phối decision đã được reconcile rõ. Không được ghi `ĐỦ CĂN CỨ` nếu coverage còn thiếu.

### Relation types

Chỉ dùng bốn loại:

- `DÙNG CHUNG` — mọi phạm vi thực sự chi phối cho cùng conclusion trọng yếu; một phạm vi duy nhất cũng có thể dùng loại này;
- `PHẢI TÁCH` — treatment trọng yếu khác nhau; Final phải tách rõ;
- `PHẢI KÈM ĐIỀU KIỆN/NGOẠI LỆ` — condition/exception làm thay đổi áp dụng đáng kể;
- `CÓ THỂ VIẾT TRUNG TÍNH` — exact detail không phải teaching target và có thể generalize an toàn.

Không tạo khác biệt/blocker từ suy đoán. Phải có claim cụ thể, scope cụ thể, evidence cụ thể và materiality cụ thể.

## 6. CORE → Dxx coverage

Mỗi CORE có nội dung chuẩn tắc/thực hành trọng yếu phải map tới ít nhất một Dxx đủ căn cứ, hoặc ghi rõ `KHÔNG CẦN Dxx` nếu đó không phải material teaching claim.

Mục đích là chống omission: formula/rule/rate/threshold/deadline/classification/procedure/exception chính không được lọt qua chỉ vì Bước 2 quên tạo Dxx.

## 7. Phân vai sáu bước

### Bước 1 — Audit

- xác định public scope sơ bộ Sxx;
- xác định CORE/Rxx/example/presentation risk;
- tạo CORE → Rxx coverage;
- không mở research queue bằng detail phụ.

### Bước 2 — Research + Scope/Dxx Register

Là owner chính của evidence completeness.

- xác nhận Sxx thật sự trong scope;
- nghiên cứu material decisions;
- reconcile mỗi Dxx với mọi Sxx trong scope có khả năng chi phối;
- tạo CORE → Dxx coverage;
- không transfer rule từ provision lân cận;
- không ép full route khi route không phải teaching target;
- không được mark ready khi `COVERAGE: THIẾU`.

### Thu hẹp phạm vi an toàn

Nếu một scope quá rộng/không đủ evidence, có thể đề xuất thu hẹp chỉ khi:

- không phá CORE hoặc user intent chính;
- title + intro + scope statement sẽ được cập nhật đồng bộ;
- không âm thầm bỏ một đối tượng/chế độ mà bài vẫn công bố phục vụ.

Nếu narrowing phá CORE thì phải làm rõ evidence hoặc chuyển manual review.

### Nhánh phụ — Làm rõ căn cứ khi cần

Mỗi bài tối đa **một lần**.

1. **Trước Rewrite**: giải quyết Dxx/Sxx coverage gap trọng yếu; sau khi đủ, quay lại Bước 2 → Bước 3 → Bước 4.
2. **Sau QA Bước 5**: chỉ giải quyết blocker/claim/scope gap cụ thể mà QA nêu; nếu đủ, tạo `BỔ SUNG CĂN CỨ CHO SỬA MỘT LẦN` gồm Sxx + Dxx + coverage + treatment + surfaces rồi đi **thẳng Bước 6**.

Nếu nhánh đã dùng mà vẫn thiếu material evidence/coverage, dừng ở `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

### Bước 3 — Plan

- chốt title/public scope không rộng hơn Sxx/Dxx;
- map Sxx + Dxx vào section và public wording;
- mọi material claim dự kiến phải trace về Dxx;
- `PHẢI TÁCH` phải map thành treatment riêng;
- `PHẢI KÈM...` phải map condition/exception tới nơi người đọc cần;
- cùng Dxx phải nhất quán qua intro/body/formula/example/table/summary;
- không mở research mới.

### Bước 4 — Rewrite

Là writer, không phải auditor.

Nếu Plan ready, phải viết. Không thêm material teaching claim mới ngoài Dxx/Plan. Không mở research mới. Chỉ dừng khi Plan tự mâu thuẫn trực tiếp cùng Sxx+Dxx; khi đó chạy lại Bước 3.

### Bước 5 — Publication Safety QA

QA có **hai pass**, nhưng không mở research mới.

#### Pass 1 — Coverage

1. `PUBLIC SCOPE COVERAGE`: title/intro/scope statement có rộng hơn Sxx không?
2. `MATERIAL CLAIM TRACEABILITY`: mọi material teaching claim có map về Dxx/official content không?
3. `Dxx SCOPE COVERAGE`: Dxx đang dùng có `COVERAGE: ĐỦ` và reconcile đủ Sxx liên quan không?
4. `CORE COVERAGE`: mọi CORE chuẩn tắc/thực hành chính còn trace được về Dxx không?

Các blocker chuẩn:

- `SCOPE OVERCLAIM`;
- `UNMAPPED MATERIAL CLAIM`;
- `SCOPE COVERAGE GAP`;
- `CORE COVERAGE GAP`.

#### Pass 2 — Correctness của Dxx

Với mỗi Dxx liên quan Final kiểm:

1. scope/effectivity;
2. scope differences nếu `PHẢI TÁCH`;
3. main conclusion;
4. condition/exception nếu `PHẢI KÈM...`;
5. cross-surface consistency.

Chỉ được PASS khi cả Coverage Pass và Decision Pass đều sạch blocker trọng yếu.

QA không được block bằng giả thuyết về regime/exception ngoài public scope. Blocker phải gắn với Sxx/Dxx/claim cụ thể đang tồn tại.

### Bước 6 — Scope + Decision Cluster Repair

Mỗi bài tối đa **một lần**.

Sửa theo cụm Sxx+Dxx trên tất cả surfaces:

- title;
- intro/scope statement;
- explanation;
- formula;
- example;
- warning/note;
- accounting entry liên quan;
- table;
- summary/conclusion.

`SCOPE OVERCLAIM` chỉ được repair bằng narrowing khi QA đã xác nhận narrowing deterministic, evidence hỗ trợ và không mất CORE. `UNMAPPED MATERIAL CLAIM` supporting có thể bỏ/generalize; material claim cần treatment mới chỉ sửa khi clarification package cung cấp Dxx+coverage đủ.

Sau Bước 6 chạy Bước 5 một lần cuối. Nếu còn blocker trọng yếu → manual review.

## 8. Ngân sách vòng lặp

Mỗi bài tối đa:

- `Làm rõ căn cứ khi cần`: 1 lần;
- Bước 6: 1 lần;
- QA sau Bước 6: 1 lần cuối.

Không tạo chuỗi vô hạn:

- clarification → rewrite → clarification;
- QA → repair → QA → repair;
- final QA → research mới.

Trạng thái cuối:

- `KẾT QUẢ CUỐI: ĐẠT`;
- `KẾT QUẢ CUỐI: ĐẠT — CÓ GỢI Ý NHỎ`;
- `KẾT QUẢ CUỐI: CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

## 9. Accounting / legal / tax precision

Khóa exact route, Điều/Khoản/Điểm, account classification, tax rate, threshold, deadline hoặc formula khi chúng là **material decision**.

Nếu detail chỉ phục vụ minh họa phụ và có thể viết trung tính mà không sai treatment, ưu tiên simplification.

Không chuyển condition/exception/addend từ sibling/adjacent provision nếu không có evidence bridge.

Primary evidence đúng fact pattern/scope/time ưu tiên hơn summary hoặc Plan cũ.

## 10. Official content

Official form/table/statutory wording/formal template được phép giữ gần nguyên văn khi fidelity cần thiết. Không ép paraphrase chỉ để novelty.

Official content vẫn phải đúng version/scope/effectivity nếu đó là material decision.

## 11. Coverage và trình bày

- Giữ đầy đủ CORE trọng yếu.
- Supporting có thể gộp/rút gọn hợp lý.
- Giữ hierarchy, warning/example/accounting/table relationships khi có vai trò dạy học.
- Minor primitive drift không chặn nếu meaning/hierarchy/teaching role còn nguyên.
- Không đưa Sxx/Rxx/Cxx/Pxx/E##/Dxx, checkpoint, research state hoặc instruction nội bộ vào public HTML.

## 12. Quảng bá và tài nguyên

- quảng bá thuần túy → bỏ;
- nội dung hữu ích trong vùng pha quảng bá → giữ phần hữu ích;
- không biến quảng cáo rõ thành soft-ad;
- không tự tạo URL/file/resource;
- migration tài nguyên là việc vận hành, không tự động chặn bài nếu content vẫn publish-safe.

## 13. Ngôn ngữ báo cáo

Mọi report user-facing dùng tiếng Việt rõ ràng. Technical token chỉ giữ khi cần nối workflow.

## 14. Chống overfitting và freeze candidate

Production prompt không được hard-code tên một bài, một thông tư hoặc một regression case để quyết định PASS/FAIL.

Regression phải kiểm logic bằng nhiều failure class khác nhau, gồm single-scope, multi-scope, condition locality, official fidelity, incidental detail, unmapped material claim, scope overclaim, cross-surface cluster và terminal loop budget.

Production behavior dựa trên các loại decision tổng quát: scope/applicability, measurement, classification, rate/threshold/deadline, accounting treatment, procedure, exception/interaction và official content.

Bản này được thiết kế như **freeze candidate**: sau khi đạt regression đa dạng, không tiếp tục thêm gate/rule chỉ để chữa một lỗi article-local đơn lẻ. Chỉ mở lại kiến trúc nếu có failure system-level lặp lại trên nhiều bài.

Mục tiêu là **kiểm sâu đúng những gì đáng kiểm, coverage đủ trước khi PASS, nhưng workflow vẫn kết thúc**.