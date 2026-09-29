# KTD Editorial Content Renewal v1.7 — Phase 6 Integrated Candidate Skill

**Target Skill Runtime:** 1.6.0  
**Target Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Status:** CANDIDATE — chưa thay runtime live v1.6.

## 1. Sứ mệnh

Làm mới bài viết Kế Toán Diệu Tâm theo hướng **đúng hơn, mới hơn nhưng vẫn nhận ra bài gốc**, với bốn mục tiêu chính:

1. cập nhật nội dung lỗi thời hoặc sai theo căn cứ hiện hành khi thật sự cần;
2. làm mới ví dụ do tác giả tạo bằng tên/số/bối cảnh khác và tính lại kết quả phụ thuộc;
3. diễn đạt lại prose thường **vừa đủ**, không ép viết thành một bài hoàn toàn khác;
4. loại bỏ quảng bá/CTA/self-praise nhưng giữ phần kiến thức và tài nguyên hữu ích.

Nguyên tắc trung tâm:

> **Bảo tồn bài gốc là mặc định; thay đổi phải có mục đích. Correctness được quyền thay đổi nội dung, nhưng stylistic simplification không được quyền làm nghèo nội dung.**

## 2. Hai trục độc lập

### 2.1 Accuracy

Accuracy dùng Sxx/Rxx/Dxx để trả lời:
- bài đang công bố phạm vi nào;
- quyết định chuyên môn trọng yếu nào phải đúng;
- evidence nào đủ để bảo vệ quyết định đó;
- treatment/condition/exception nào phải nhất quán xuyên bài.

### 2.2 Preservation

Preservation bảo vệ:
- worked example nhiều bước;
- practical/procedural/accounting sequence có giá trị học;
- bảng/checklist/comparison có quan hệ kiến thức;
- warning/note/key-line có vai trò dạy học;
- image/caption/resource hữu ích;
- đoạn giải thích/case thực hành có độ sâu đáng giữ.

**Preservation không tự tạo research target.** Một phần rất đáng giữ vẫn chỉ mở Rxx/Dxx cho material claim thật sự bên trong nó.

## 3. Materiality — giữ ưu điểm của v1.6

Chỉ coi là blocker accuracy nếu sai sót có khả năng đáng kể như:
- làm người đọc áp dụng sai;
- sai phạm vi/đối tượng/thời kỳ/chế độ;
- title/intro/scope hứa rộng hơn căn cứ;
- sai kết luận chính, công thức, mức/tỷ lệ/ngưỡng/thời hạn hoặc treatment chính;
- bỏ điều kiện/ngoại lệ trọng yếu;
- sai nội dung official cần fidelity;
- mâu thuẫn material giữa explanation/example/table/warning/summary.

Không mặc định block vì:
- tài khoản đối ứng phụ không phải teaching target;
- payment state/method phụ;
- route phụ không đổi treatment chính;
- wording/polish;
- hypothetical regime/exception ngoài public scope;
- supporting detail không high-value được viết trung tính hợp lý.

Không có quota Rxx/Dxx. Không dựng lại exact-detail/full-route matrix legacy.

## 4. Source Preservation Default

`SUPPORTING` chỉ có nghĩa là **không phải material accuracy blocker mặc định**. Nó KHÔNG có nghĩa được tự động rút, xóa hoặc flatten.

Một substantive source region mặc định được giữ giá trị nếu:
- không có Dxx yêu cầu sửa;
- Plan không authorize move/merge/remove;
- không phải quảng bá thuần;
- không có lý do hợp lệ làm thay đổi teaching/editorial function.

Không dùng các lý do chung như “ngắn hơn”, “gọn hơn”, “sạch hơn”, “an toàn hơn” để làm mất high-value content.

## 5. Các hành động biên tập chuẩn

### `UPDATE / CORRECT WITH EVIDENCE`
Dùng khi source lỗi thời/sai và material enough để cần sửa.

### `REFRESH EXAMPLE`
Dùng với author-created substantive example:
- đổi tên/người/doanh nghiệp;
- đổi số liệu;
- có thể đổi bối cảnh;
- tính lại toàn bộ dependent values;
- giữ teaching purpose + practical depth + learning sequence.

### `LIGHT REPHRASE`
Dùng với prose thường:
- diễn đạt khác vừa đủ;
- giữ đúng ý, logic, nuance và chi tiết hữu ích;
- không synonym-spin;
- không bắt buộc redesign toàn article;
- không đặt mục tiêu “substantially different”.

### `REMOVE PROMOTION`
- pure promotion/self-praise/sales/social CTA → bỏ;
- promotional wrapper + useful knowledge → bỏ wrapper, giữ useful core;
- legitimate attribution/provenance → giữ khi cần;
- useful resource không bị xóa chỉ vì nằm gần brand language.

## 6. Official content fidelity

Official form/table/template/statutory wording/quotation có thể giữ gần nguyên văn khi fidelity cần thiết.

Không paraphrase official content chỉ để tạo novelty. Không trộn prose do tác giả tạo vào official content làm sai provenance.

## 7. Canonical workflow — đúng 6 bước

### Bước 1 — Kiểm tra bài hiện tại

Phải:
- đọc title + Canonical HTML nguồn;
- lập public scope sơ bộ Sxx;
- xác định CORE hẹp;
- chỉ tạo Rxx cho risk material cụ thể;
- inventory substantive examples E##;
- lập **Danh sách phần giá trị cần giữ** nhẹ;
- theo dõi presentation/resource có teaching value;
- phân loại promotion theo communicative intent.

Output phải tách rõ:
1. `CÓ THỂ CHẶN ĐĂNG`;
2. `CẦN BẢO TỒN GIÁ TRỊ`;
3. `CHI TIẾT PHỤ CÓ THỂ VIẾT TRUNG TÍNH`.

Kết thúc bằng đúng:
- `CẦN KIỂM CHỨNG: CÓ`; hoặc
- `CẦN KIỂM CHỨNG: KHÔNG`.

Không tạo Vxx matrix.

### Bước 2 — Kiểm chứng nội dung trọng yếu

Chỉ chạy khi cần kiểm chứng hoặc editor yêu cầu.

Phải:
- ưu tiên nguồn có thẩm quyền và đúng subject/fact pattern/phạm vi/thời kỳ;
- reconcile Sxx thật sự thuộc public scope;
- khóa Dxx material;
- ghi coverage theo Sxx và relation type;
- không research toàn bộ high-value region chỉ vì region đó được bảo tồn;
- không promote citation tham khảo thành scope chi phối nếu không có căn cứ.

Dxx chỉ READY khi các Sxx liên quan đã reconcile đủ.

Relation type chuẩn:
- `DÙNG CHUNG`;
- `PHẢI TÁCH`;
- `PHẢI KÈM ĐIỀU KIỆN/NGOẠI LỆ`;
- `CÓ THỂ VIẾT TRUNG TÍNH`.

### Bước 3 — Renewal Plan

Không mở research mới.

Phải tạo:
- Public Scope Contract;
- Sxx + Dxx → article mapping;
- material claim traceability;
- Preservation Contract;
- Example Refresh Plan;
- Presentation/Resource Plan khi cần;
- title action.

Disposition cho high-value region:
- `GIỮ`;
- `LÀM MỚI NHƯNG GIỮ CHỨC NĂNG`;
- `SỬA CHO ĐÚNG RỒI GIỮ`;
- `GỘP VỚI NỘI DUNG TƯƠNG ĐƯƠNG`;
- `BỎ — LÝ DO HỢP LỆ`.

Nếu gộp/move/replace phải chỉ destination/equivalent. “Cùng chủ đề” chưa đủ để gọi là equivalent.

Không có blanket permission kiểu “SUPPORTING được gộp/rút gọn”.

### Bước 4 — Viết lại bài

Chỉ chạy khi Plan sẵn sàng.

Thứ tự ưu tiên:
1. Correctness;
2. Preservation;
3. Refresh Example;
4. Light Rephrase;
5. Remove Promotion.

Writer không phải researcher/QA mới. Không tạo Rxx/Sxx/Dxx mới, không mở web research, không dựng legacy exact-detail matrix.

Multi-step example không được collapse thành one-line summary nếu làm mất learning outcome.

Nếu source region có treatment cũ sai nhưng teaching function tốt:
> sửa treatment theo Dxx rồi tái tạo teaching function.

Meaning-bearing presentation không bị flatten vô lý. Có thể dùng canonical EDS equivalent nếu functional role còn tương đương hoặc tốt hơn.

### Bước 5 — Final QA

Bước 5 là cổng an toàn trước khi đăng, không phải researcher và không sửa HTML.

Chỉ có **hai pass trong cùng Prompt 5**:

#### Pass 1 — Coverage + Preservation
Kiểm:
- public scope coverage;
- material claim traceability;
- Dxx coverage theo Sxx;
- CORE material coverage;
- high-value regions trong Preservation Contract;
- Example Refresh Plan;
- presentation/resource có giá trị.

Preservation chỉ reconcile high-value region đã được Bước 1–3 đánh dấu, không quét mọi SUPPORTING paragraph.

Chỉ dùng đúng ba preservation blocker:
- `MẤT_NỘI_DUNG_GIÁ_TRỊ`;
- `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`;
- `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`.

#### Pass 2 — Material Accuracy
Với từng Dxx Final thực sự dùng, kiểm:
- phạm vi/hiệu lực;
- khác biệt giữa các Sxx;
- kết luận/treatment chính;
- condition/exception trọng yếu;
- cross-surface consistency.

Không dùng word count, paragraph count, heading count hoặc pixel parity làm điều kiện PASS.

### Bước 6 — Minimal Repair theo cụm

`MINIMAL` = **phạm vi sửa tối thiểu**, KHÔNG phải cắt nội dung cho dễ PASS.

Đơn vị repair:
> `Scope + Decision + Preservation Cluster`

Thứ tự:
1. Correctness;
2. Preservation Target;
3. Cross-surface Consistency;
4. Minimum Necessary Change.

Không giải quyết accuracy bằng cách xóa high-value region nếu có thể sửa đúng rồi giữ.

Không giải quyết preservation bằng cách copy lại stale treatment.

Ngoài repair cluster phải giữ Final gần nhất tối đa; không global rewrite/polish, không refresh thêm example, không mở section mới vô cớ.

Bước 6 không research mới, không tạo Rxx/Sxx/Dxx mới, không quay lại Bước 1–4.

## 8. Example contract

Với author-created substantive example:
- đổi tên/số/bối cảnh theo Plan;
- tính lại toàn bộ dependent values;
- kiểm arithmetic;
- giữ `inputs → intermediate steps → outputs` khi các bước có learning value;
- giữ practical depth tương đương;
- giữ procedural/accounting sequence nếu chính sequence là learning target;
- material treatment phải tuân Dxx.

QA/Repair không được quay về tên/số cũ chỉ vì dễ hơn.

Official/source-attributed example giữ fidelity/provenance và không bị ép refresh novelty.

## 9. Meaning-bearing presentation

Các primitive/role sau được bảo tồn theo chức năng khi có teaching/editorial value:
- warning/content box;
- key-line/highlight;
- list/checklist/steps;
- table/comparison;
- accounting group;
- example/note;
- figure/image/caption;
- useful resource/link.

Không cần pixel parity hoặc exact structural count.

## 10. Research Boundedness

Research chỉ phục vụ material accuracy.

Không mở research chỉ vì:
- example có nhiều số;
- table có nhiều cell;
- accounting group có nhiều tài khoản phụ;
- region được đánh dấu high-value;
- có thể tưởng tượng thêm regime/exception ngoài public scope.

Preservation-only blocker không mở research.

## 11. Clarification branch — nhánh phụ, tối đa 1 lần

`Làm rõ căn cứ khi cần` không phải Bước 7.

Chỉ dùng khi Bước 2, 3 hoặc 5 yêu cầu material evidence/coverage thật sự còn thiếu.

Routing:
- trước Rewrite → làm rõ rồi quay lại Bước 2 → 3 → 4;
- sau Bước 5 → nếu đủ căn cứ đi **thẳng Bước 6**, không quay lại Bước 2–4.

Preservation-only blocker không được dùng nhánh này.

## 12. Hard loop budget

Mỗi article-run:
- clarification: tối đa 1 lần;
- Bước 6: tối đa 1 lần;
- sau Bước 6: Bước 5 đúng 1 lần cuối.

Nếu QA cuối vẫn còn blocker accuracy hoặc preservation đáng kể:
> `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

Không hạ blocker thành gợi ý nhỏ chỉ để kết thúc workflow.

## 13. Kết quả Bước 5

Các trạng thái chuẩn:
- `KẾT QUẢ CUỐI: ĐẠT`;
- `KẾT QUẢ CUỐI: ĐẠT — CÓ GỢI Ý NHỎ`;
- `KẾT QUẢ CUỐI: CHƯA ĐẠT — SỬA MỘT LẦN Ở BƯỚC 6`;
- `KẾT QUẢ CUỐI: CẦN LÀM RÕ CĂN CỨ`;
- `KẾT QUẢ CUỐI: CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

## 14. Public HTML firewall

Final public HTML:
- H1 body = 0;
- dùng canonical EDS vocabulary;
- không inline style/arbitrary class/data-* ngoài contract;
- không script/form/input/event handler;
- không invent URL/src/download path;
- không đưa Sxx/Rxx/Cxx/Pxx/E##/Dxx, blocker state, research state hoặc lời nhắc biên tập vào HTML công khai.

## 15. User-facing language

Báo cáo AI phải ưu tiên **tiếng Việt thuần, rõ, dễ hiểu**.

Mã Sxx/Dxx/E## chỉ xuất hiện khi thực sự cần chỉ đúng claim/scope/example hoặc nối sang bước tiếp theo.

Không bắt editor giải mã jargon kỹ thuật tiếng Anh.

## 16. UX contract khi tích hợp Assistant

Phải giữ:
- workflow ẩn cho tới khi `Phân tích bài` thành công;
- phân tích lại reset copy state + clarification budget + Step 6 budget + lastStep;
- clarification hiển thị như nhánh phụ, visually secondary;
- cảnh báo rõ `Không phải bước tiếp theo — chỉ sao chép khi AI yêu cầu.`;
- article content chỉ lưu trong `sessionStorage`, không `localStorage`;
- không gửi article data tới remote endpoint;
- Bước 6 dùng xong mở lại Bước 5 cho QA lần cuối;
- đúng 6 canonical prompts;
- không hard-code golden TSCĐ/regulation vào runtime.

## 17. Freeze candidate rule

Phase 6 chỉ là integration candidate.

Không promote live v1.7 cho tới khi:
- integration guard PASS;
- candidate UX no-regression PASS;
- diverse real-world benchmark PASS;
- golden TSCĐ regression PASS theo cả Accuracy + Preservation + Efficiency;
- không xuất hiện repeated systematic failure mới.
