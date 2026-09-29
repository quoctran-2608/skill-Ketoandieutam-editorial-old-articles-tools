# KTD Editorial Content Renewal v1.7 — Phase 2 Candidate Runtime Skill

**Target Skill Runtime:** 1.6.0  
**Target Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Phase 2 scope:** triển khai thật Bước 1–3 ở candidate runtime; Bước 4–6 vẫn kế thừa contract v1.6 cho tới các phase sau.  
**Status:** CANDIDATE — không phải file live mà Assistant production đang nạp.

## 1. Mục tiêu

Làm mới bài đã qua Chặng 1 thành phiên bản hiện hành, đủ chính xác chuyên môn để bảo vệ uy tín Kế Toán Diệu Tâm, nhưng không làm mất tinh thần, độ giàu nội dung, ví dụ thực hành và các khối trình bày có giá trị của bài gốc.

Nguyên tắc trung tâm:

> **Bảo tồn bài gốc là mặc định; thay đổi phải có mục đích. Correctness được quyền thay đổi nội dung, nhưng stylistic simplification không được quyền làm nghèo nội dung.**

Workflow phải làm tốt bốn việc:

1. cập nhật phần lỗi thời theo văn bản/chính sách hiện hành khi ảnh hưởng material accuracy;
2. làm mới ví dụ bằng tên/số liệu/bối cảnh khác, tính lại dependent values nhưng giữ teaching function và practical depth;
3. diễn đạt lại nhẹ prose do tác giả viết, giữ đúng ý và độ giàu nội dung;
4. loại bỏ quảng bá thương hiệu theo communicative intent, giữ useful editorial core.

## 2. Hai trục độc lập

### Accuracy

Accuracy dùng Sxx/Rxx/Dxx để trả lời: nội dung nào phải được kiểm chứng và khóa đúng để bài đủ an toàn đăng?

- `Sxx`: phạm vi công khai thật sự của bài;
- `Rxx`: hàng đợi kiểm chứng chỉ cho rủi ro material;
- `Dxx`: quyết định chuyên môn trọng yếu;
- CORE → Dxx coverage;
- material claim traceability;
- condition/exception và cross-surface consistency.

### Preservation

Preservation trả lời: phần nào của bài gốc có giá trị giảng dạy/thực hành/trình bày mà Final không được âm thầm làm nghèo?

Preservation **không tự tạo research target**. Một example/table/warning có thể rất đáng giữ nhưng chỉ một vài claim bên trong cần Dxx.

Nếu correctness xung đột với source cũ: sửa phần sai theo evidence rồi cố giữ teaching function bằng phiên bản đúng.

## 3. Materiality — giữ kỷ luật của v1.6

Chỉ coi là có thể chặn đăng khi vấn đề có khả năng đáng kể:

- làm người đọc áp dụng sai;
- sai văn bản/chế độ/đối tượng/fact pattern/thời kỳ;
- title/intro/scope statement hứa rộng hơn evidence;
- sai kết luận chính;
- sai formula/rate/threshold/deadline/classification/account/treatment/procedure chính;
- thiếu condition/exception trọng yếu;
- sai official form/table/template;
- mâu thuẫn material giữa explanation/formula/example/warning/table/summary;
- làm mất một phần teaching/practical value lớn đến mức Final không còn tương đương chức năng.

Không tự động chặn vì:

- tài khoản đối ứng phụ không phải teaching target;
- phương thức/trạng thái thanh toán phụ;
- bước trung gian không đổi treatment chính;
- wording/polish nhỏ;
- decorative style drift nhỏ;
- resource migration thuần vận hành;
- giả thuyết “có thể còn chế độ/ngoại lệ khác” nhưng không có scope/claim/evidence cụ thể.

## 4. CORE vẫn hẹp; SUPPORTING không phải giấy phép xóa

`CORE` chỉ dùng khi mất/sai nội dung đó sẽ làm hỏng lời hứa chính, làm người đọc áp dụng sai đáng kể hoặc làm mất learning objective chính.

Không biến mọi câu, mọi example, mọi bút toán, mọi số tài khoản thành CORE.

`SUPPORTING` chỉ có nghĩa là không phải material accuracy blocker mặc định. Nó **không** có nghĩa được tự động rút/xóa.

SUPPORTING chỉ được MOVE/MERGE/REPLACE/RÚT khi functional value tương đương hoặc tốt hơn. Không được:

- rút example nhiều bước thành một phép tính một dòng làm mất bài học;
- flatten table/checklist/warning hữu ích thành prose chung chung;
- bỏ image/caption/resource hữu ích mà không đánh giá;
- textbook hóa một đoạn thực hành giàu nội dung chỉ để ngắn hơn.

## 5. Preservation Default

Bước 1 lập một **Danh sách phần giá trị cần giữ**, nhẹ và có chọn lọc. Chỉ ghi những region có nguy cơ bị AI làm nghèo:

- worked example nhiều bước;
- practical sequence/procedure/accounting flow;
- bảng/checklist mang quan hệ kiến thức;
- warning/note/key-line có teaching role;
- accounting group có teaching function;
- image/figure/caption/resource hữu ích;
- comparison/breakdown nhiều thành phần;
- đoạn giải thích/case thực hành đặc biệt giàu giá trị.

Không tạo Vxx matrix mới. Có thể tham chiếu Cxx/E##/Pxx đã có.

Substantive source region mặc định `GIỮ GIÁ TRỊ VÀ CHỨC NĂNG` nếu không có lý do hợp lệ để đổi/bỏ.

Lý do hợp lệ để bỏ/merge một high-value region:

- sai/lỗi thời và sau khi cập nhật không còn learning value;
- trùng lặp thật sự và đã merge vào nơi tương đương;
- out-of-scope sau narrowing hợp lệ;
- pure promotion;
- media/resource không còn hữu ích và bỏ không làm mất teaching value.

“Cho ngắn hơn”, “gọn hơn”, “an toàn hơn” không phải authorization đủ.

## 6. Bốn transformation hợp lệ

### UPDATE / CORRECT WITH EVIDENCE

Dùng khi source lỗi thời hoặc sai material. Chỉ thay treatment material khi evidence đủ theo Sxx/Dxx.

### REFRESH EXAMPLE

Với author-created example:

- đổi tên người/doanh nghiệp;
- đổi số liệu;
- có thể đổi bối cảnh phù hợp;
- tính lại toàn bộ dependent values;
- giữ teaching purpose;
- giữ inputs → intermediate steps → outputs nếu các bước có learning value;
- giữ practical depth tương đương;
- sửa treatment cũ nếu evidence yêu cầu.

Không cần research tên/số minh họa giả định.

### LIGHT REPHRASE

Với prose không phải official/statutory wording:

- diễn đạt khác vừa đủ;
- giữ ý, logic, quan hệ giữa các ý và mức chi tiết hữu ích;
- không synonym-spin cơ học;
- không bắt buộc redesign section;
- không tự rút chỉ vì có thể viết ngắn hơn.

### REMOVE PROMOTION

- pure promotion/self-praise/sales/social CTA → bỏ;
- promotional wrapper + useful knowledge → bỏ wrapper, giữ useful core;
- attribution/provenance hợp lệ → giữ khi cần;
- không đổi hard-ad thành soft-ad;
- không xóa useful link/resource chỉ vì vùng chứa nó có brand language.

## 7. Sxx và Dxx

Giữ engine v1.6.

Sxx chỉ mô tả phạm vi bài thực sự công bố hoặc dựa vào để hướng dẫn. Không biến mọi citation thành scope chi phối.

Dxx không có quota; chỉ tạo khi sai decision đó có thể ảnh hưởng đáng kể đến thực hành, kết luận chính hoặc uy tín.

Mỗi Dxx phải có:

- quyết định cần chốt;
- CORE liên quan;
- căn cứ chính;
- coverage theo Sxx có khả năng chi phối;
- kết luận theo từng Sxx thực sự chi phối;
- relation type;
- chỉ dẫn cách viết;
- `COVERAGE: ĐỦ | THIẾU`;
- trạng thái căn cứ.

Relation type:

- `DÙNG CHUNG`;
- `PHẢI TÁCH`;
- `PHẢI KÈM ĐIỀU KIỆN/NGOẠI LỆ`;
- `CÓ THỂ VIẾT TRUNG TÍNH`.

Không tạo khác biệt/blocker từ suy đoán.

## 8. Research boundedness

Bước 2 chỉ research:

- Rxx material;
- Sxx public scope có khả năng chi phối Dxx;
- Dxx cần khóa;
- official content/version/effectivity khi material.

Không research mọi detail chỉ vì preservation muốn giữ region đó.

Ví dụ có 8 con số nhưng chỉ rule capitalization là material: research rule; tên/số giả định chỉ cần logic và phép tính nội bộ nhất quán.

Không ép full accounting route nếu route không phải teaching target hoặc không đổi treatment chính.

## 9. Bước 1 — Audit + Preservation Baseline

Bước 1 phải:

1. đọc title + Canonical HTML + inventory resource + Skill;
2. tạo Sxx sơ bộ;
3. xác định CORE hẹp;
4. tạo Rxx chỉ cho rủi ro material cụ thể;
5. map CORE → Rxx;
6. inventory example E##;
7. tạo **Danh sách phần giá trị cần giữ**;
8. audit promotion/resource;
9. tách rõ:
   - `CÓ THỂ CHẶN ĐĂNG`;
   - `CẦN BẢO TỒN GIÁ TRỊ`;
   - `CHI TIẾT PHỤ CÓ THỂ VIẾT TRUNG TÍNH`.

Bước 1 không được hỏi “phần nào của high-value example có thể bỏ cho gọn”. Chỉ được chỉ ra detail thật sự incidental mà việc generalize không làm mất teaching function.

## 10. Bước 2 — Research + Sxx/Dxx Register

Bước 2 là owner chính của evidence completeness, không phải preservation auditor.

Phải:

- xác nhận Sxx;
- research Rxx material;
- tạo Dxx;
- reconcile Dxx với Sxx có khả năng chi phối;
- map CORE → Dxx;
- chốt treatment cần UPDATE/CORRECT;
- ghi rõ high-value region nào chứa material decision cần sửa, nhưng không biến toàn region thành research target;
- đề xuất narrowing chỉ khi không phá CORE/user intent.

Nếu một high-value example có treatment cũ sai, output phải hướng tới `SỬA CHO ĐÚNG RỒI GIỮ CHỨC NĂNG`, không mặc định xóa example.

## 11. Bước 3 — Renewal Plan + Preservation Contract

Bước 3 không mở research mới.

Plan phải có bốn lớp:

### A. Accuracy plan

- title/public scope;
- Sxx + Dxx → section/surface;
- material claim traceability;
- cross-surface consistency.

### B. Transformation plan

Với section/region liên quan, chọn khi cần:

- `UPDATE/CORRECT`;
- `REFRESH EXAMPLE`;
- `LIGHT REPHRASE`;
- `REMOVE PROMOTION`;
- `PRESERVE`.

Không cần gắn action cho mọi paragraph; chỉ những region có thay đổi đáng kể hoặc high-value region cần protection.

### C. Preservation contract

Với mỗi item trong Danh sách phần giá trị cần giữ, chọn một disposition:

- `GIỮ`;
- `LÀM MỚI NHƯNG GIỮ CHỨC NĂNG`;
- `SỬA CHO ĐÚNG RỒI GIỮ`;
- `GỘP VỚI NỘI DUNG TƯƠNG ĐƯƠNG`;
- `BỎ — LÝ DO HỢP LỆ`.

Nếu `GỘP`, phải nêu nơi nhận và functional equivalent. Nếu `BỎ`, phải nêu lý do hợp lệ.

### D. Example refresh plan

Mỗi author-created substantive example phải ghi:

- teaching purpose;
- phần material cần tuân Dxx;
- inputs/intermediate steps/outputs cần giữ về chức năng;
- tên/số/bối cảnh nào sẽ đổi;
- dependent values nào phải tính lại;
- presentation role cần giữ nếu có.

Không được dùng mục chung kiểu `SUPPORTING ĐƯỢC GỘP/RÚT GỌN` làm blanket authorization.

## 12. Official content và presentation

Official form/table/statutory wording/template ưu tiên fidelity; không ép paraphrase để tạo novelty.

Meaning-bearing presentation mặc định được bảo tồn về vai trò:

- warning vẫn phải có risk signal tương đương;
- example vẫn phải được nhận ra là example;
- table/checklist phải giữ khả năng so sánh/thực hành;
- accounting group phải giữ grouping khi grouping là teaching value;
- image/caption/resource hữu ích phải được `GIỮ | THAY | BỎ CÓ LÝ DO`.

Không yêu cầu pixel parity hoặc exact heading count.

## 13. Hard loop budget — không thay đổi

- `Làm rõ căn cứ khi cần`: tối đa 1 lần/article-run;
- Bước 6: tối đa 1 lần;
- QA sau Bước 6: đúng 1 lần cuối;
- hết budget mà còn material blocker → `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

Preservation không được mở thêm research/repair loop.

## 14. Ngôn ngữ user-facing

Báo cáo cho editor phải ưu tiên tiếng Việt rõ ràng. Mã Sxx/Rxx/Cxx/Pxx/E##/Dxx chỉ dùng khi cần nối bước.

Không bắt editor giải mã thuật ngữ tiếng Anh nếu có thể diễn đạt tiếng Việt tự nhiên.

## 15. No-regression UX của v1.6

Khi candidate được promote vào live runtime sau các phase sau, phải giữ:

- đúng 6 canonical prompts;
- workflow ẩn cho tới khi `Phân tích bài` thành công;
- re-analyze reset copy state/loop budget/last step;
- clarification là nhánh phụ;
- sessionStorage only;
- Step 6 mở lại Step 5 cho QA cuối;
- không hard-code bài TSCĐ, thông tư hay regression case vào production logic.
