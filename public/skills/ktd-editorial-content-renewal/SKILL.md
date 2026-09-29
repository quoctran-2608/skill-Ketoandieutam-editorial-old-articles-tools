# KTD Editorial Content Renewal v1.7 — Official Skill

**Skill Runtime:** 1.6.3  
**Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Status:** OFFICIAL — áp dụng từ 2026-09-07 sau lượt kiểm thử thực tế do owner phê duyệt.

**Maintenance 1.6.1:** làm rõ bảo tồn inline semantic markup đã được Chặng 1 phân loại (`ct-key-highlight`, `ct-key-emphasis`, `strong`, `em`) mà không nâng lỗi hình thức nhỏ thành blocker QA hoặc mở thêm vòng sửa.

**Maintenance 1.6.2:** khôi phục năng lực freshness/roll-forward có giới hạn cho bài hướng dẫn hiện hành bị gắn năm/ngày/regime cũ, đồng thời giữ nguyên 6 bước, bounded research, Sxx/Dxx, Preservation, semantic reconciliation và loop budget của v1.7. Không thay năm cơ học và không biến bài lịch sử/kỳ kê khai cũ thành bài hiện hành.

**Maintenance 1.6.3:** tăng cường Source Fidelity theo nguyên tắc `PRESERVE-THEN-PATCH`: cập nhật/correct đúng phần cần đổi nhưng không dùng một subclaim cần sửa làm giấy phép rewrite, rút gọn hoặc flatten cả high-value region đang còn đúng. Giữ teaching density, cấu trúc thực hành và semantic presentation của bài nguồn; chỉ làm mới cách diễn đạt khi không làm nghèo giá trị. Không đổi 6 bước, Prompt Set, research topology hay loop budget.

## 1. Sứ mệnh

Làm mới bài viết Kế Toán Diệu Tâm theo hướng **đúng hơn, mới hơn nhưng vẫn nhận ra bài gốc**, với bốn mục tiêu chính:

1. cập nhật nội dung lỗi thời hoặc sai theo căn cứ hiện hành khi thật sự cần;
2. làm mới ví dụ do tác giả tạo bằng tên/số/bối cảnh khác và tính lại kết quả phụ thuộc;
3. diễn đạt lại prose thường **vừa đủ**, không ép viết thành một bài hoàn toàn khác;
4. loại bỏ quảng bá/CTA/self-praise nhưng giữ phần kiến thức và tài nguyên hữu ích.

Nguyên tắc trung tâm:

> **Bảo tồn bài gốc là mặc định; thay đổi phải có mục đích. Correctness được quyền thay đổi nội dung, nhưng stylistic simplification không được quyền làm nghèo nội dung.**

Thứ tự giá trị phải giữ ổn định:
> **Đúng quy định hiện hành trước → bảo tồn chiều sâu/chi tiết/chức năng dạy học → làm mới cách diễn đạt khi an toàn. “Khác bản gốc” là mục tiêu phụ, không phải KPI được phép đánh đổi chất lượng.**

## 2. Hai trục độc lập + một guard freshness của Accuracy

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
- inline semantic emphasis đã được Chặng 1 phân loại như `mark.ct-key-highlight`, `span.ct-key-emphasis` và `strong`/`em` có chủ đích khi chúng giúp quét ý, nhấn điều kiện hoặc giữ sắc thái;
- image/caption/resource hữu ích;
- đoạn giải thích/case thực hành có độ sâu đáng giữ.

**Preservation không tự tạo research target.** Một phần rất đáng giữ vẫn chỉ mở Rxx/Dxx cho material claim thật sự bên trong nó.

### 2.3 Freshness / Roll-forward Contract — guard của Accuracy, không phải hệ research mới

Mục đích của Freshness là phân biệt đúng giữa **bài hướng dẫn hiện hành đang bị cũ** và **nội dung lịch sử/kỳ áp dụng có chủ đích**.

Mốc thời gian:
- dùng ngày/năm hiện tại do system/runtime của lượt xử lý cung cấp;
- nếu orchestration có `CURRENT_DATE` / `CURRENT_YEAR`, coi đó là mốc freshness ưu tiên;
- không hard-code một năm cố định vào Skill;
- một năm cũ xuất hiện trong bài KHÔNG tự động có nghĩa phải thay bằng năm hiện tại.

Mỗi bài có yếu tố thời gian đáng kể phải được phân loại đúng MỘT trong ba trạng thái sau, hoặc `MIXED` nếu có hai lớp đồng thời:

- `CURRENT_GUIDANCE` — lời hứa chính của bài là hướng dẫn người đọc áp dụng **hiện nay/đang dùng**. Nếu title/intro/heading/rule/amount/threshold/regime đang gắn một năm cũ nhưng chức năng bài rõ ràng là current guidance, năm cũ là **freshness candidate**, không được mặc định đóng băng thành historical Sxx.
- `PERIOD_SPECIFIC` — bài cố ý giải quyết một kỳ/thời điểm lịch sử cụ thể, ví dụ quyết toán cho một năm đã chốt, hồ sơ của kỳ cũ, quy định “tại thời điểm X”, hoặc phân tích retrospective. Phải giữ đúng kỳ đó; KHÔNG roll-forward chỉ vì hiện tại đã sang năm mới.
- `MIXED` — bài vừa hướng dẫn hiện hành vừa cần giữ phần lịch sử/chuyển tiếp/so sánh nhiều thời kỳ. Chỉ lớp current guidance được roll-forward; phần lịch sử phải giữ đúng năm/ngày và được viết đủ rõ để không bị hiểu là quy tắc hiện hành.

#### Khi nào freshness là material risk

Bước 1 phải mở **một Rxx freshness có giới hạn** khi đồng thời có dấu hiệu cụ thể rằng:
- title/intro/scope/heading đang trình bày một năm/ngày/mức/regime cũ như lời hứa hướng dẫn đang áp dụng;
- bài thuộc dạng nội dung có khả năng thay đổi theo thời gian như pháp luật, thuế, BHXH, tiền lương, mức/ngưỡng/tỷ lệ, biểu mẫu, thủ tục, deadline, cơ quan có thẩm quyền hoặc annual guidance;
- nếu giữ nguyên mốc cũ khi đăng lại hiện nay có khả năng làm người đọc áp dụng sai hoặc khiến bài thất bại mục tiêu “làm mới”.

Không mở Rxx chỉ vì:
- số năm nằm trong tên/số hiệu văn bản;
- ngày ban hành/ngày hiệu lực lịch sử cần provenance;
- ví dụ đang cố ý minh họa một kỳ cũ;
- bảng so sánh nhiều năm;
- bài period-specific có title nêu đúng kỳ cần xử lý;
- một năm xuất hiện như background/historical reference không còn được dùng làm current treatment.

#### Roll-forward KHÔNG phải tìm-thay năm

Nếu `CURRENT_GUIDANCE` cần roll-forward:
- research đúng **current governing rule/fact** và những material dependency bị thay đổi;
- không thay `2025 → 2026` một cách cơ học;
- không đổi năm trong số hiệu văn bản, effective date, historical comparison hoặc provenance nếu bản thân chúng vẫn đúng;
- nếu luật/regime thay đổi giữa hai năm, phải cập nhật authority/treatment trước rồi mới cập nhật title/example/amount phụ thuộc;
- mọi material surface cùng decision phải đồng bộ: title, intro/scope, heading, explanation, formula/rate/threshold/deadline, example, warning/note, table và summary khi chúng thực sự mang claim time-sensitive;
- historical context hữu ích vẫn được giữ theo Preservation, nhưng phải phân biệt rõ với current treatment.

Freshness dùng **chính Sxx/Rxx/Dxx hiện có**. Không tạo namespace Fxx, không tạo prompt thứ 7, không tăng clarification/repair budget.

## 3. Materiality — giữ ưu điểm của v1.6

Chỉ coi là blocker accuracy nếu sai sót có khả năng đáng kể như:
- làm người đọc áp dụng sai;
- sai phạm vi/đối tượng/thời kỳ/chế độ;
- title/intro/scope hứa rộng hơn căn cứ;
- current-guidance article giữ material claim thời gian cũ trái Freshness Target/Dxx đã khóa;
- sai kết luận chính, công thức, mức/tỷ lệ/ngưỡng/thời hạn hoặc treatment chính;
- bỏ điều kiện/ngoại lệ trọng yếu;
- sai nội dung official cần fidelity;
- mâu thuẫn material giữa explanation/example/table/warning/summary.

Không mặc định block vì:
- tài khoản đối ứng phụ không phải teaching target;
- payment state/method phụ;
- route phụ không đổi treatment chính;
- wording/polish;
- năm/ngày lịch sử hoặc period-specific hợp lệ;
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

Freshness roll-forward chỉ thay đổi phần time-sensitive khi có căn cứ. Nó không cấp blanket permission để xóa historical explanation, example depth, table, warning hoặc sequence có giá trị.

### 4.1 Preserve-Then-Patch / Source Fidelity Contract

Mục tiêu của contract này là bảo đảm bài mới có thể **đúng hơn và diễn đạt mới hơn nhưng không dở hơn bài nguồn**.

Một **preservation anchor** là high-value source region có một hoặc nhiều vai trò đáng giữ như:
- official/statutory wording hoặc quotation còn đúng và còn giá trị provenance;
- danh sách chi tiết các trường hợp/điều kiện/ngoại lệ;
- công thức, bảng, checklist, warning/note/key-line;
- worked example hoặc case có nhiều bước;
- practical/procedural/accounting sequence hoặc grouping mang giá trị thao tác;
- blockquote/list/table/accounting group/figure/resource hoặc semantic emphasis giúp người đọc quét và hiểu bài;
- đoạn giải thích có nuance, chiều sâu hoặc mật độ kiến thức rõ ràng vượt prose tổng quát.

Không tạo namespace/id mới cho preservation anchor, không inventory mọi paragraph và không yêu cầu text/HTML parity 1:1. Bước 1–3 chỉ cần nhận diện nhẹ ở cấp region khi thực sự có giá trị.

#### Ba chế độ xử lý source region

1. **Vùng còn đúng và có giá trị** → `GIỮ` hoặc `LIGHT REPHRASE` có giới hạn. Có thể đổi cách diễn đạt prose tác giả, nhưng phải giữ ý, nuance, chi tiết hữu ích, teaching density, quan hệ logic và semantic presentation tương đương.
2. **Vùng hỗn hợp: chỉ một subclaim/điều kiện cần cập nhật** → `PRESERVE-THEN-PATCH`. Sửa đúng subclaim/condition bị ảnh hưởng; các phần còn đúng mặc định giữ. Không dùng một correction cục bộ làm giấy phép rewrite/rút gọn toàn vùng.
3. **Vùng material stale/sai ở treatment chính** → `SỬA CHO ĐÚNG RỒI GIỮ`. Correctness được ưu tiên, nhưng phải tái tạo teaching function, practical depth và meaning-bearing presentation ở mức tương đương hoặc tốt hơn khi evidence/Plan cho phép.

Quy tắc cốt lõi:
> **Update what must change. Preserve what still works. Rephrase where useful. Never simplify away teaching value.**

Với official/statutory passage còn đúng:
- không paraphrase chỉ để tạo novelty;
- nếu vấn đề nằm ở cách hiểu hiện hành, condition/exception hoặc current clarification xung quanh passage, ưu tiên giữ quotation/faithful wording rồi thêm clarification bên ngoài;
- chỉ thay official passage khi evidence cho thấy authority/version/treatment đó thực sự phải cập nhật.

`Dxx` hoặc freshness correction chỉ authorize **claim/decision đã khóa**, không tự authorize rewrite những chi tiết không bị ảnh hưởng trong cùng region.

“Viết khác đi” được khuyến khích ở prose thường khi an toàn, nhưng không được dùng để:
- bỏ enumeration hữu ích;
- biến multi-step sequence thành summary;
- biến table/list/accounting grouping thành generic prose nếu functional role giảm;
- làm mất condition/exception/nuance;
- strip có hệ thống semantic emphasis;
- làm mờ provenance của official/source-attributed content.

### 4.2 Canonical inline semantic preservation — guard nhẹ, không phải blocker mới

Đầu vào của Chặng 2 là Canonical HTML đã qua Chặng 1. Vì vậy các inline primitive hợp lệ đã có sẵn như:
- `mark.ct-key-highlight`;
- `span.ct-key-emphasis`;
- `strong` và `em` có chủ đích;

được mặc định coi là **semantic presentation đã được phân loại**, không phải paint cũ cần dọn lại.

Quy tắc:
- nếu wording và semantic role của đoạn vẫn giữ, ưu tiên giữ nguyên primitive và vùng nhấn tương ứng;
- nếu `LIGHT REPHRASE` làm thay đổi câu chữ hoặc ranh giới cụm từ, tái tạo một vùng nhấn tương đương bằng primitive canonical phù hợp thay vì strip toàn bộ;
- chỉ remove/reclassify khi Plan thật sự đổi semantic role, nội dung được sửa khiến vùng nhấn cũ không còn đúng, hoặc vùng đó trở nên dư thừa sau một biến đổi có lý do;
- không xóa inline semantic chỉ vì “HTML sạch hơn”, vì chữ vẫn còn, hoặc vì toàn bộ blockquote/paragraph đã được giữ;
- không cần inventory từng `mark`/`span`, không tạo Pxx/Rxx/Dxx riêng cho từng inline range và không dựng ma trận parity;
- Bước 1/3 có thể dùng **một ghi chú bảo tồn nhẹ ở cấp bài hoặc region** thay vì liệt kê từng range.

Rất quan trọng:
> `minor primitive drift không phải blocker` chỉ mô tả **mức độ QA**, KHÔNG phải giấy phép cho Writer chủ động strip inline semantic markup hợp lệ.

Mất một inline emphasis đơn lẻ trong khi nội dung, scope và teaching role vẫn còn được coi là **minor presentation drift**: không tự mở research, không tự làm Bước 5 fail và không dùng Bước 6 chỉ để phục hồi lỗi hình thức đó.

Nhưng nếu một preservation anchor bị **strip/flatten có hệ thống** nhiều emphasis/primitive làm giảm khả năng quét ý, nhận điều kiện/kết luận hoặc làm nghèo meaning-bearing presentation, đó không còn là isolated minor drift; Bước 5 được phép dùng blocker Preservation hiện có phù hợp.

## 5. Các hành động biên tập chuẩn

### `UPDATE / CORRECT WITH EVIDENCE`
Dùng khi source lỗi thời/sai và material enough để cần sửa.

Nếu update xuất phát từ freshness roll-forward, phải update theo current Dxx/evidence và các material surface liên quan; không chỉ đổi số năm ở title.

Nếu chỉ một subclaim trong preservation anchor cần update, mặc định dùng `PRESERVE-THEN-PATCH`: sửa đúng phần được Dxx/evidence authorize, giữ phần còn đúng.

### `REFRESH EXAMPLE`
Dùng với author-created substantive example:
- đổi tên/người/doanh nghiệp;
- đổi số liệu;
- có thể đổi bối cảnh;
- tính lại toàn bộ dependent values;
- giữ teaching purpose + practical depth + learning sequence.

Nếu Freshness Target = `CURRENT_GUIDANCE` và example đang đóng vai current practical example, Plan có thể chuyển example sang target period/current amounts khi Dxx/evidence đã khóa. Nếu example cố ý là historical/transition example thì giữ kỳ lịch sử.

### `LIGHT REPHRASE`
Dùng với prose thường:
- diễn đạt khác vừa đủ;
- giữ đúng ý, logic, nuance và chi tiết hữu ích;
- không synonym-spin;
- không bắt buộc redesign toàn article;
- không đặt mục tiêu “substantially different”.

`LIGHT REPHRASE` không mặc định cho phép xóa các inline semantic primitive đã được Chặng 1 phân loại. Nếu cụm từ được viết lại nhưng chức năng nhấn vẫn còn, tái tạo emphasis tương đương.

`LIGHT REPHRASE` cũng không được giảm teaching density: nếu source có một danh sách/sequence/condition bundle hữu ích, có thể đổi wording hoặc cách tổ chức nhẹ nhưng không rút thành generic summary chỉ để “khác”.

### `REMOVE PROMOTION`
- pure promotion/self-praise/sales/social CTA → bỏ;
- promotional wrapper + useful knowledge → bỏ wrapper, giữ useful core;
- legitimate attribution/provenance → giữ khi cần;
- useful resource không bị xóa chỉ vì nằm gần brand language.

## 6. Official content fidelity

Official form/table/template/statutory wording/quotation có thể giữ gần nguyên văn khi fidelity cần thiết.

Không paraphrase official content chỉ để tạo novelty. Không trộn prose do tác giả tạo vào official content làm sai provenance.

Nếu official/statutory passage **vẫn đúng và còn giá trị**, current clarification phải ưu tiên đặt bên ngoài passage thay vì rewrite toàn bộ passage. Một condition/exception cần bổ sung không tự động làm mất quyền tồn tại của wording/provenance còn đúng.

Freshness không được đổi năm/số hiệu/ngày trong official quotation hoặc provenance nếu evidence không cho phép. Nếu version official đã bị thay thế và material cho current guidance, phải dùng Dxx/evidence để update đúng version thay vì sửa chữ cơ học.

## 7. Canonical workflow — đúng 6 bước

### Bước 1 — Kiểm tra bài hiện tại

Phải:
- đọc title + Canonical HTML nguồn;
- xác định mốc ngày/năm hiện tại từ runtime/system nếu có;
- phân loại freshness ở cấp bài: `CURRENT_GUIDANCE | PERIOD_SPECIFIC | MIXED`, kèm lý do ngắn;
- lập public scope sơ bộ Sxx, nhưng KHÔNG mặc định biến một năm cũ trong current-guidance title thành scope lịch sử cố định;
- nếu current-guidance có năm/ngày/regime cũ material, tạo một Rxx freshness bounded để kiểm current treatment + các dependency chính;
- xác định CORE hẹp;
- chỉ tạo Rxx cho risk material cụ thể;
- inventory substantive examples E##;
- lập **Danh sách phần giá trị cần giữ** nhẹ;
- nhận diện nhẹ preservation anchor ở cấp region khi có official wording/provenance, detailed enumeration, condition/exception bundle, multi-step example/procedure/accounting grouping, table/list/warning/media hoặc semantic presentation có teaching value;
- nếu một preservation anchor chỉ có một phần nghi ngờ stale/sai, đánh dấu đây là **partial-update risk** thay vì giả định toàn vùng cần rewrite;
- theo dõi presentation/resource có teaching value;
- nếu Canonical HTML có `ct-key-highlight`/`ct-key-emphasis` hoặc `strong`/`em` có chủ đích, ghi một lưu ý bảo tồn nhẹ ở cấp bài/region khi cần; không inventory từng inline range và không tạo research target chỉ vì emphasis;
- phân loại promotion theo communicative intent.

Freshness output tối thiểu phải nói rõ:
- `PHÂN LOẠI FRESHNESS: CURRENT_GUIDANCE | PERIOD_SPECIFIC | MIXED`;
- mốc hiện tại đang dùng;
- year/date/regime nào là current-guidance candidate cần verify;
- year/date nào phải giữ vì historical/period-specific;
- Rxx freshness hoặc `KHÔNG CẦN Rxx FRESHNESS — lý do`.

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
- nếu có Rxx freshness, khóa trước: `FRESHNESS TARGET: CURRENT_GUIDANCE | PERIOD_SPECIFIC | MIXED` và mốc target áp dụng;
- với `CURRENT_GUIDANCE`, xác minh current governing rule/fact/effective date và chỉ các material dependency cần để đưa bài về hiện hành;
- với `PERIOD_SPECIFIC`, nghiên cứu đúng kỳ bài hứa phục vụ; không kéo sang current year chỉ để “mới”;
- với `MIXED`, tách current treatment khỏi historical/transition context;
- reconcile Sxx thật sự thuộc public scope;
- khóa Dxx material;
- ghi coverage theo Sxx và relation type;
- không research toàn bộ high-value region chỉ vì region đó được bảo tồn;
- không research mọi year/date occurrence; chỉ research material freshness targets;
- không promote citation tham khảo thành scope chi phối nếu không có căn cứ.

Dxx chỉ READY khi các Sxx liên quan đã reconcile đủ.

Dxx phải khóa đúng **material decision/subclaim cần sửa**, không mặc định biến toàn bộ source region thành rewrite target. Evidence cho một correction cục bộ không phải blanket authorization để làm mất các chi tiết còn đúng của preservation anchor.

Nếu current regime đã thay đổi, Dxx phải khóa authority/treatment hiện hành và chỉ rõ historical authority nào còn được phép xuất hiện dưới vai trò bối cảnh. Không dùng title năm cũ để giới hạn research vào regime cũ khi Bước 1 đã phân loại `CURRENT_GUIDANCE`.

Relation type chuẩn:
- `DÙNG CHUNG`;
- `PHẢI TÁCH`;
- `PHẢI KÈM ĐIỀU KIỆN/NGOẠI LỆ`;
- `CÓ THỂ VIẾT TRUNG TÍNH`.

### Bước 3 — Renewal Plan

Không mở research mới.

Phải tạo:
- **Freshness Target + Roll-forward Surface Map**;
- Public Scope Contract;
- Sxx + Dxx → article mapping;
- material claim traceability;
- Preservation Contract;
- Example Refresh Plan;
- Presentation/Resource Plan khi cần;
- title action.

`Freshness Target + Roll-forward Surface Map` phải ghi:
- `FRESHNESS TARGET: CURRENT_GUIDANCE | PERIOD_SPECIFIC | MIXED`;
- current/target period đã được Bước 2 khóa;
- `TITLE ACTION: GIỮ | VIẾT LẠI | CẬP NHẬT`;
- các material surface cần update đồng bộ: title | intro/scope | heading | explanation | formula/rate/threshold/deadline | example | warning/note | table | summary, nhưng CHỈ liệt kê surface thực sự mang time-sensitive claim;
- các historical/period-specific surface phải GIỮ và lý do;
- không lập danh sách mọi year/date chỉ để đạt parity.

Nếu `CURRENT_GUIDANCE`, Plan không được READY khi còn một current-guidance material claim cũ chưa có disposition `UPDATE/CORRECT`, `GENERALIZE` hợp lệ hoặc historical reclassification có căn cứ.
Nếu `PERIOD_SPECIFIC`, Plan không được ép đổi sang năm hiện tại.
Nếu `MIXED`, Plan phải chỉ rõ ranh giới current layer và historical layer.

Disposition cho high-value region:
- `GIỮ`;
- `LÀM MỚI NHƯNG GIỮ CHỨC NĂNG`;
- `SỬA CHO ĐÚNG RỒI GIỮ`;
- `GỘP VỚI NỘI DUNG TƯƠNG ĐƯƠNG`;
- `BỎ — LÝ DO HỢP LỆ`.

Nếu một preservation anchor chỉ cần sửa một phần, Plan phải nêu **mutation boundary** nhẹ ở cấp region, theo dạng:
`MUTATION BOUNDARY: SỬA <claim/condition/treatment được Dxx authorize>; GIỮ <chi tiết/logic/structure/provenance/semantic role còn đúng>.`

Mutation boundary không phải exact-text matrix và không yêu cầu liệt kê từng inline range. Mục đích là ngăn correction cục bộ biến thành wholesale rewrite.

Với official/statutory passage còn đúng nhưng cần current clarification, ưu tiên disposition `GIỮ + BỔ SUNG CLARIFICATION` hoặc `SỬA PHẦN CẦN THIẾT RỒI GIỮ`, thay vì paraphrase toàn passage chỉ để novelty.

Nếu gộp/move/replace phải chỉ destination/equivalent. “Cùng chủ đề” chưa đủ để gọi là equivalent.

Không có blanket permission kiểu “SUPPORTING được gộp/rút gọn”.

Với inline semantic markup, Plan không cần liệt kê từng `mark`/`span`. Chỉ cần một guard nhẹ ở cấp bài hoặc region, ví dụ:
`INLINE SEMANTIC DEFAULT: GIỮ primitive/range hợp lý từ Canonical HTML; chỉ reclassify/remove khi biến đổi semantic có lý do.`

Guard này không tạo material target mới, không ảnh hưởng Dxx coverage và không làm tăng loop budget.

### Bước 4 — Viết lại bài

Chỉ chạy khi Plan sẵn sàng.

Thứ tự ưu tiên:
1. Correctness;
2. Preservation;
3. Refresh Example;
4. Light Rephrase;
5. Remove Promotion.

Writer không phải researcher/QA mới. Không tạo Rxx/Sxx/Dxx mới, không mở web research, không dựng legacy exact-detail matrix.

**Preserve-Then-Patch execution guard:**
- không rewrite toàn bộ một preservation anchor chỉ vì một subclaim/condition bên trong cần update;
- áp dụng đúng `MUTATION BOUNDARY` của Plan: sửa phần được authorize, giữ phần còn đúng;
- prose tác giả có thể rephrase vừa đủ để bài mới không máy móc giống source, nhưng teaching density, detail, nuance, logical relationship và meaning-bearing presentation phải tương đương hoặc tốt hơn;
- official/statutory passage còn đúng ưu tiên giữ quotation/faithful wording; nếu cần current clarification, đặt clarification ngoài passage trừ khi Dxx yêu cầu sửa chính passage;
- không dùng “gọn hơn”, “an toàn hơn” hoặc “khác hơn” làm lý do thay enumeration/sequence/table/list/accounting grouping bằng generic prose;
- nếu specificity ceiling không cho phép lặp một chi tiết cụ thể của source nhưng functional primitive vẫn đáng giữ, dùng **canonical neutral equivalent trong mức specificity được phép** thay vì prose-only flattening khi làm vậy giữ được learning function.

**Freshness execution guard:**
- `CURRENT_GUIDANCE` → thực thi Roll-forward Surface Map theo đúng Dxx/Plan trên mọi material surface liên quan; không để title đã current nhưng body/example/table vẫn mang current treatment cũ;
- `PERIOD_SPECIFIC` → giữ đúng kỳ đã khóa, không “nâng năm” cho mới;
- `MIXED` → current layer theo Dxx hiện hành, historical layer giữ đúng provenance và được diễn đạt đủ rõ là historical/transition context;
- tuyệt đối không find-replace năm cơ học;
- không đổi year trong số hiệu văn bản, ngày hiệu lực, historical comparison hoặc official quote chỉ vì year < current year;
- nếu current example được roll-forward, tính lại dependent values theo evidence/Plan; không chỉ đổi năm trong câu mở đầu.

Multi-step example không được collapse thành one-line summary nếu làm mất learning outcome.

Nếu source region có treatment cũ sai nhưng teaching function tốt:
> sửa treatment theo Dxx rồi tái tạo teaching function.

Meaning-bearing presentation không bị flatten vô lý. Có thể dùng canonical EDS equivalent nếu functional role còn tương đương hoặc tốt hơn.

**Inline semantic guard của Writer:**
- khi source Canonical HTML đã có `mark.ct-key-highlight`, `span.ct-key-emphasis` hoặc `strong`/`em` có chủ đích và nội dung/role tương ứng vẫn được giữ, Writer phải giữ primitive + vùng nhấn đó hoặc tái tạo equivalent nếu wording thay đổi;
- không strip inline semantic chỉ vì blockquote/paragraph vẫn còn, vì text content chưa mất, hoặc để HTML gọn/sạch hơn;
- nếu correctness buộc sửa nội dung bên trong vùng nhấn, sửa nội dung theo Dxx rồi đặt lại emphasis ở range mới phù hợp; không bảo tồn wording sai chỉ để giữ format;
- không được strip có hệ thống nhiều emphasis/primitive trong một preservation anchor chỉ vì từng primitive riêng lẻ có thể bị xem là minor drift ở QA;
- đây là self-check trong lượt viết, không phải lý do mở research hoặc tạo blocker mới.

### Bước 5 — Final QA

Bước 5 là cổng an toàn trước khi đăng, không phải researcher và không sửa HTML.

Chỉ có **hai pass trong cùng Prompt 5**:

#### Pass 1 — Coverage + Preservation
Kiểm:
- public scope coverage;
- material claim traceability;
- Dxx coverage theo Sxx;
- CORE material coverage;
- Freshness Target đã được thực thi ở các material surface Plan đã map;
- high-value regions trong Preservation Contract;
- mutation boundary của preservation anchor có partial update;
- Example Refresh Plan;
- presentation/resource có giá trị.

**Freshness QA là kiểm tra material, không phải quét mọi năm:**
- nếu Plan = `CURRENT_GUIDANCE`, một claim/material amount/regime cũ còn được Final trình bày như current treatment trái Dxx/Surface Map → blocker `FRESHNESS DRIFT`;
- nếu Plan = `PERIOD_SPECIFIC`, việc giữ năm/kỳ cũ đúng scope KHÔNG phải lỗi freshness;
- nếu Plan = `MIXED`, historical year/date được phép giữ khi vai trò lịch sử/chuyển tiếp rõ và không lẫn với current treatment;
- không tạo `FRESHNESS DRIFT` chỉ vì thấy year < current year;
- `FRESHNESS DRIFT` phải chỉ ra Dxx/claim/surface cụ thể và vì sao nó trái Freshness Target đã khóa.

Preservation chỉ reconcile high-value region đã được Bước 1–3 đánh dấu, không quét mọi SUPPORTING paragraph.

Khi reconcile preservation anchor, không đòi exact wording/count parity; kiểm **functional equivalence và teaching density**. Các dấu hiệu material failure gồm:
- detailed enumeration/condition/exception bundle có giá trị bị rút thành generic summary;
- official/source-attributed passage còn đúng bị paraphrase mạnh làm mất provenance hoặc chi tiết hữu ích mà Plan không authorize;
- multi-step practical/procedural/accounting sequence bị flatten thành prose làm giảm thao tác học;
- table/list/accounting group/warning/blockquote/meaning-bearing structure bị thay bằng dạng yếu hơn mà không có equivalent;
- nhiều inline semantic primitive trong cùng anchor bị strip có hệ thống làm giảm khả năng quét điều kiện/kết luận/điểm cần nhớ;
- Final vượt mutation boundary: correction cục bộ nhưng làm mất chi tiết còn đúng ngoài phần được authorize.

Chỉ dùng đúng ba preservation blocker:
- `MẤT_NỘI_DUNG_GIÁ_TRỊ`;
- `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`;
- `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`.

`FRESHNESS DRIFT` là blocker Accuracy, KHÔNG phải blocker Preservation thứ tư.

Mất một inline `ct-key-highlight`/`ct-key-emphasis`/`strong`/`em` đơn lẻ, khi câu chữ và teaching role vẫn còn, không tự nâng thành blocker; tối đa xem là minor presentation drift/gợi ý nhỏ nếu đáng nhắc. Nhưng **systematic semantic stripping trong một preservation anchor** có thể là blocker bằng ba loại Preservation hiện có nếu làm giảm functional value.

#### Pass 2 — Material Accuracy
Với từng Dxx Final thực sự dùng, kiểm:
- phạm vi/hiệu lực, bao gồm current target period nếu Dxx là current-guidance;
- khác biệt giữa các Sxx;
- kết luận/treatment chính;
- condition/exception trọng yếu;
- cross-surface consistency;
- freshness consistency trên đúng material target/surface đã map.

Không dùng word count, paragraph count, heading count, pixel parity hoặc “còn năm cũ” đơn thuần làm điều kiện PASS.

### Bước 6 — Minimal Repair theo cụm

`MINIMAL` = **phạm vi sửa tối thiểu**, KHÔNG phải cắt nội dung cho dễ PASS.

Đơn vị repair:
> `Scope + Decision + Preservation Cluster`

Thứ tự:
1. Correctness;
2. Preservation Target;
3. Cross-surface Consistency;
4. Minimum Necessary Change.

Nếu Bước 5 đóng gói `FRESHNESS DRIFT` và Dxx/Plan hiện có đã đủ:
- sửa đúng các material surface thuộc cluster theo Freshness Target;
- dùng current treatment/period đã khóa, không mở research mới;
- giữ historical/period-specific dates đúng vai trò;
- không blanket-replace mọi year trong Final;
- nếu sửa một amount/threshold/formula làm thay đổi dependent values trong example/table, cập nhật đồng bộ các dependent values đã được Plan/Dxx authorize.

Nếu freshness repair cần evidence material mới mà hồ sơ chưa có, không đoán; dùng clarification theo routing hiện hành nếu còn quyền, hoặc chuyển biên tập chuyên môn thủ công theo hard stop.

Nếu blocker là Preservation và Dxx/Plan đã đủ:
- dùng **Canonical source region làm restoration baseline**, không dùng bản Final đã bị làm nghèo làm chuẩn;
- phục hồi content/function/presentation còn đúng trước, rồi áp dụng đúng correction nằm trong mutation boundary;
- không copy lại stale/sai treatment;
- nếu source dùng list/table/accounting group/step sequence/blockquote hoặc primitive có teaching function, ưu tiên phục hồi canonical primitive hoặc functional equivalent, không đổi thành prose-only chỉ vì dễ sửa;
- nếu specificity ceiling cấm một mã/route/detail cụ thể, dùng neutral functional equivalent trong mức specificity được phép khi điều đó bảo tồn learning function;
- tái tạo semantic emphasis tương đương cho những điều kiện/kết luận/điểm cần nhớ thuộc restored region khi source đã có meaning-bearing emphasis.

Không giải quyết accuracy bằng cách xóa high-value region nếu có thể sửa đúng rồi giữ.

Không giải quyết preservation bằng cách copy lại stale treatment.

Ngoài repair cluster phải giữ Final gần nhất tối đa; không global rewrite/polish, không refresh thêm example, không mở section mới vô cớ.

Bước 6 không research mới, không tạo Rxx/Sxx/Dxx mới, không quay lại Bước 1–4.

Không chạy Bước 6 chỉ để phục hồi một inline emphasis bị mất nếu đó chỉ là minor presentation drift và không làm mất teaching function đáng kể.

## 8. Example contract

Với author-created substantive example:
- đổi tên/số/bối cảnh theo Plan;
- tính lại toàn bộ dependent values;
- kiểm arithmetic;
- giữ `inputs → intermediate steps → outputs` khi các bước có learning value;
- giữ practical depth tương đương;
- giữ procedural/accounting sequence nếu chính sequence là learning target;
- material treatment phải tuân Dxx;
- nếu example là current-guidance target, kỳ/mức/rule phải tuân Freshness Target; nếu example là historical/period-specific thì giữ đúng kỳ đó.

QA/Repair không được quay về tên/số cũ chỉ vì dễ hơn.

Official/source-attributed example giữ fidelity/provenance và không bị ép refresh novelty.

## 9. Meaning-bearing presentation

Các primitive/role sau được bảo tồn theo chức năng khi có teaching/editorial value:
- warning/content box;
- key-line/highlight;
- inline `ct-key-highlight`/`ct-key-emphasis` và `strong`/`em` có chủ đích;
- list/checklist/steps;
- table/comparison;
- accounting group;
- example/note;
- figure/image/caption;
- useful resource/link.

Với inline semantic markup, ưu tiên giữ đúng primitive và semantic range khi wording không đổi; nếu wording đổi thì giữ functional emphasis tương đương. Không cần exact-range matrix, pixel parity hoặc exact structural count.

Một primitive đơn lẻ có thể drift ở mức minor; nhưng **mất có hệ thống presentation role của cả high-value region** không được che giấu bằng cách đánh giá từng thẻ riêng lẻ. Functional role của region mới là đơn vị Preservation chính.

## 10. Research Boundedness

Research chỉ phục vụ material accuracy, bao gồm material freshness khi current-guidance có dấu hiệu lỗi thời cụ thể.

Không mở research chỉ vì:
- example có nhiều số;
- table có nhiều cell;
- accounting group có nhiều tài khoản phụ;
- region được đánh dấu high-value;
- inline emphasis/presentation cần bảo tồn;
- một year/date lịch sử tồn tại;
- period-specific article không trùng current year;
- có thể tưởng tượng thêm regime/exception ngoài public scope.

Khi có Rxx freshness, research theo **decision cluster**, không theo từng lần xuất hiện của năm/ngày. Một current rule/effective period/amount được xác minh một lần rồi carry-forward qua các material surface tương ứng.

Preservation-only blocker không mở research.

## 11. Clarification branch — nhánh phụ, tối đa 1 lần

`Làm rõ căn cứ khi cần` không phải Bước 7.

Chỉ dùng khi Bước 2, 3 hoặc 5 yêu cầu material evidence/coverage thật sự còn thiếu, bao gồm một freshness decision material mà current treatment chưa đủ căn cứ.

Không dùng clarification chỉ để xác nhận “có nên đổi năm cho mới” khi bài đã rõ là period-specific/historical hoặc khi evidence hiện có đã đủ cho Freshness Target.

Routing:
- trước Rewrite → làm rõ rồi quay lại Bước 2 → 3 → 4;
- sau Bước 5 → nếu đủ căn cứ đi **thẳng Bước 6**, không quay lại Bước 2–4.

Preservation-only blocker không được dùng nhánh này.

## 12. Hard loop budget

Mỗi article-run:
- clarification: tối đa 1 lần;
- Bước 6: tối đa 1 lần;
- sau Bước 6: Bước 5 đúng 1 lần cuối.

Freshness và Preserve-Then-Patch không tạo thêm loop hoặc prompt.

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
- không đưa Sxx/Rxx/Cxx/Pxx/E##/Dxx, `CURRENT_DATE`, `CURRENT_YEAR`, Freshness Target, mutation boundary, blocker state, research state hoặc lời nhắc biên tập vào HTML công khai.

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
- không hard-code golden article/regulation/year vào runtime.

Khuyến nghị orchestration:
- nếu Assistant có thể inject thời gian, thêm `CURRENT_DATE` và `CURRENT_YEAR` vào prompt context để Freshness Contract có mốc rõ;
- nếu chưa inject, model dùng current date của system/runtime; không được suy rằng năm trong source luôn là current target.

## 17. Official freeze rule

v1.7 là runtime chính thức. Không mở thêm phase chỉ để hoàn thiện wording hoặc lý thuyết.

Chỉ mở lại kiến trúc khi có evidence thực tế cho thấy đồng thời:
- Final còn lỗi material; và
- QA không bắt được lỗi đó hoặc workflow sai ở mức material; và
- fix có thể giữ generic, bounded, không overfit một bài/văn bản.

Maintenance patch được phép làm rõ một guard đã thuộc triết lý hiện hành nếu không đổi 6 bước, không đổi loop budget, không nâng lỗi nhỏ thành blocker và không overfit một bài cụ thể. Trường hợp này dùng patch version của Skill Runtime, không cần mở phase/prompt-set mới.

Freshness/Roll-forward Contract 1.6.2 là maintenance guard theo nguyên tắc trên: dùng Sxx/Rxx/Dxx sẵn có, không tạo namespace/prompt/loop mới, không hard-code một năm hay một lĩnh vực cụ thể và không phục hồi legacy full-audit behavior.

Preserve-Then-Patch / Source Fidelity Contract 1.6.3 cũng là maintenance guard theo nguyên tắc trên: không đổi Prompt Set 1.7.0, không tạo namespace/prompt/loop mới, không đòi parity máy móc và không làm giảm quyền của Correctness; nó chỉ khóa mutation boundary để correction cục bộ không làm nghèo high-value source region.

Nếu lỗi material được Bước 5 bắt, Bước 6 sửa đúng một lần và QA cuối PASS thì đó là hành vi mong đợi, không phải lý do tự động mở phase mới.
