# KTD Editorial Content Renewal v1.7 — Phase 3 Candidate Runtime Skill

**Target Skill Runtime:** 1.6.0  
**Target Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Phase 3 scope:** kế thừa toàn bộ Phase 2 cho Bước 1–3 và triển khai candidate Bước 4 — Writer. Bước 5–6 vẫn chưa promote.  
**Status:** CANDIDATE — không phải file live mà Assistant production đang nạp.

## 1. Nền tảng kế thừa

Phase 3 kế thừa không thay đổi các contract đã khóa ở Phase 1–2:

- Accuracy và Preservation là hai trục độc lập;
- Sxx/Rxx/Dxx chỉ phục vụ material accuracy;
- CORE hẹp;
- SUPPORTING không phải giấy phép xóa;
- Preservation Default;
- Research Boundedness;
- bốn transformation hợp lệ: `UPDATE/CORRECT`, `REFRESH EXAMPLE`, `LIGHT REPHRASE`, `REMOVE PROMOTION`;
- Danh sách phần giá trị cần giữ;
- Preservation Contract ở Bước 3;
- hard loop budget của v1.6;
- user-facing reports bằng tiếng Việt rõ ràng;
- đúng 6 canonical prompts, không thêm Bước 7.

Candidate Phase 2 vẫn là canonical implementation cho Bước 1–3 cho đến khi full v1.7 được promote.

## 2. Vai trò của Bước 4

Bước 4 là **người viết**, không phải researcher, không phải một vòng Audit mới và không phải QA cuối.

Chỉ chạy khi Plan gần nhất ghi:

`SẴN SÀNG LÀM MỚI: CÓ`

Bước 4 phải tin các kết luận đã khóa trong:

- source title + Canonical HTML;
- Bước 1;
- Bước 2 và Sxx/Dxx;
- Bước 3 Renewal Plan;
- Danh sách phần giá trị cần giữ;
- Preservation Contract;
- Example Refresh Plan;
- Resource/Presentation Plan.

Bước 4 không được tự mở research mới chỉ vì một chi tiết phụ làm nó không chắc chắn.

## 3. Thứ tự ưu tiên khi viết

Bước 4 thực thi theo thứ tự:

1. **Correctness** — tuân Sxx/Dxx và phần cần UPDATE/CORRECT;
2. **Preservation** — giữ teaching function, practical depth và meaning-bearing presentation;
3. **Refresh Example** — đổi tên/số/bối cảnh phù hợp và tính lại dependent values;
4. **Light Rephrase** — diễn đạt khác vừa đủ nhưng giữ ý, logic và độ giàu;
5. **Remove Promotion** — bỏ quảng bá nhưng giữ useful editorial core.

Stylistic simplification không được lấn át correctness hoặc preservation.

## 4. Source Preservation Default trong Writer

Source là baseline editorial mặc định.

Nếu một substantive region:

- không có Dxx yêu cầu sửa;
- không có Plan yêu cầu move/merge/remove;
- không phải promotion;
- không có lý do hợp lệ để đổi chức năng;

thì Bước 4 phải giữ **giá trị và chức năng** của region đó.

Không được coi mục tiêu “bài ngắn hơn”, “gọn hơn”, “sạch hơn”, “an toàn hơn” là authorization đủ để xóa/rút một high-value region.

Không đặt target word-count reduction.

## 5. Correctness execution

Bước 4 phải:

- giữ title/intro/scope/heading/summary trong đúng public scope Sxx;
- tuân Dxx và relation type đã khóa;
- không universalize treatment riêng của một Sxx;
- giữ condition/exception material đủ gần nơi áp dụng;
- không tự thêm formula/rate/threshold/deadline/classification/treatment/procedure/exception material mới nếu Plan không map về Dxx;
- cập nhật đồng bộ mọi bề mặt cùng nói về một Dxx: explanation, formula, example, warning, table, summary;
- không invent legal/accounting bridge.

Nếu một detail phụ chưa được khóa nhưng không phải teaching target và Plan cho phép neutral wording, viết trung tính thay vì dừng.

## 6. Preservation Contract execution

Với từng high-value item trong Plan:

### `GIỮ`
Giữ teaching function, practical depth, quan hệ kiến thức và presentation role. Có thể light rephrase prose nhưng không được làm nghèo.

### `LÀM MỚI NHƯNG GIỮ CHỨC NĂNG`
Có thể đổi wording, ví dụ, bố cục cục bộ hoặc presentation primitive nếu semantic role và learning outcome tương đương hoặc tốt hơn.

### `SỬA CHO ĐÚNG RỒI GIỮ`
Sửa material treatment theo Dxx rồi tái tạo phần giải thích/example/table/sequence sao cho teaching function còn nguyên ở mức tương đương.

### `GỘP VỚI NỘI DUNG TƯƠNG ĐƯƠNG`
Chỉ được gộp vào destination Plan đã chỉ định. Final destination phải còn đủ learning outcome, không chỉ cùng broad topic.

### `BỎ — LÝ DO HỢP LỆ`
Chỉ bỏ đúng authorization của Plan. Không mở rộng removal sang useful neighboring content.

## 7. Functional Equivalence Gate — nhẹ nhưng bắt buộc

Khi MOVE/MERGE/REPLACE, Bước 4 tự hỏi cục bộ:

- người đọc còn học được cùng điều cốt lõi không;
- các bước thực hành có learning value còn không;
- quan hệ so sánh/điều kiện còn nhìn thấy không;
- warning/risk signal còn đủ mạnh không;
- example có còn minh họa đúng learning objective không;
- table/checklist có còn dùng được như công cụ thực hành không.

“Cùng chủ đề” không đủ để coi là tương đương.

Gate này không yêu cầu lập ma trận mới và không mở research mới.

## 8. Example Refresh Contract

Với author-created substantive example đã được Plan chọn `REFRESH EXAMPLE` hoặc tương đương:

- thay tên người/doanh nghiệp khi có;
- thay số liệu đủ để example không còn là bản chép của source;
- có thể đổi bối cảnh minh họa nếu không đổi doctrine;
- tính lại **toàn bộ dependent values**;
- kiểm arithmetic trước output;
- giữ teaching purpose;
- giữ `inputs → intermediate steps → outputs` khi các bước có learning value;
- giữ practical depth tương đương;
- giữ procedural/accounting sequence nếu chính sequence là teaching value;
- material treatment phải tuân Dxx;
- không thêm material rule mới chỉ để làm example “phong phú hơn”.

Một multi-step example không được collapse thành một phép tính một dòng nếu làm mất learning outcome.

Official/source-attributed example không được tự ý đổi tên/số như author-created example nếu fidelity/provenance cần giữ.

## 9. Light Rephrase Contract

Với prose do tác giả viết và không phải official/statutory wording:

- diễn đạt khác vừa đủ;
- giữ đúng ý;
- giữ logic và quan hệ giữa các ý;
- giữ mức chi tiết hữu ích;
- có thể cải thiện clarity/transition/readability;
- không synonym-spin cơ học;
- không bắt buộc đổi heading/order/paragraph boundaries nếu source đang tốt;
- không tự rút một đoạn giàu nội dung chỉ vì có thể viết ngắn hơn.

Mục tiêu không phải tạo một bài “substantially different”. Mục tiêu là một bài được làm mới nhưng vẫn nhận ra tinh thần và chất lượng bài gốc.

## 10. Official content fidelity

Official form/table/template/statutory wording/quotation có yêu cầu fidelity:

- được phép giữ gần nguyên văn;
- không paraphrase để tạo novelty giả;
- không trộn author-created wording vào official content khiến nguồn bị hiểu sai;
- nếu Plan yêu cầu update version, dùng đúng version/evidence đã khóa.

## 11. Meaning-bearing presentation

Nếu source đã là Canonical HTML hợp lệ và semantic role không đổi, ưu tiên giữ primitive/classes hiện hành.

Không được flatten vô lý:

- warning/content box → paragraph thường;
- key-line/highlight → câu chìm trong prose;
- semantic list/checklist/steps → đoạn văn rời;
- table/comparison → prose chung chung làm mất khả năng đối chiếu;
- accounting group → prose nếu grouping có teaching value;
- example/note → plain text nếu role vẫn còn;
- image/caption hữu ích → mất âm thầm.

Có thể dùng canonical EDS equivalent khác khi Plan đã đổi role hợp lệ hoặc equivalent mới giữ chức năng tốt hơn. Không yêu cầu pixel parity hay exact heading count.

## 12. Media / links / resources

Tuân Plan:

- `GIỮ` → giữ URL/src/anchor hợp lệ;
- `THAY` → chỉ dùng replacement đã có căn cứ/được cung cấp;
- `BỎ CÓ LÝ DO` → chỉ bỏ đúng authorization;
- không invent URL, file, image src, download path hoặc resource title;
- không xóa useful resource chỉ vì vùng xung quanh có brand language;
- operational migration note không được đi vào public HTML.

## 13. Promotional cleanup

Áp dụng theo communicative intent:

- pure promotion/self-praise/sales/social CTA → bỏ;
- promotional wrapper + useful knowledge → bỏ wrapper, giữ useful core;
- legitimate attribution/provenance → giữ khi cần;
- không biến hard-ad thành soft-ad;
- không làm mất useful link/resource nếu giá trị editorial còn.

## 14. Không biến Writer thành một vòng kiểm toán mới

Bước 4 không được:

- tạo Rxx/Sxx/Dxx mới;
- mở web research mới;
- yêu cầu `Làm rõ căn cứ khi cần` chỉ vì tự nghi ngờ lại evidence đã khóa;
- dựng lại full exact-detail applicability matrix;
- bắt full accounting route khi route không phải teaching target;
- tạo blocker từ hypothetical regime/exception ngoài public scope;
- quay lại Audit chỉ vì wording/detail phụ chưa tuyệt đối.

Nếu Plan cho neutral wording với detail phụ, hãy viết neutral và tiếp tục.

## 15. Điều kiện duy nhất để Writer dừng trước khi xuất bài

Writer chỉ dừng khi **Plan tự mâu thuẫn trực tiếp** đến mức không thể thực hiện đồng thời, ví dụ cùng Dxx + cùng Sxx lại yêu cầu hai treatment trái nhau.

Khi đó trả đúng bằng tiếng Việt:

`CHƯA THỂ VIẾT — KẾ HOẠCH MÂU THUẪN VỚI QUYẾT ĐỊNH TRỌNG YẾU — CHẠY LẠI BƯỚC 3.`

Không dùng Checkpoint 4B, không mở research mới.

Các uncertainty nhỏ, supporting detail, primitive minor hoặc stylistic preference không được dùng làm lý do block.

## 16. Writer self-check — cục bộ, không research

Trước output, tự kiểm đúng một lượt:

1. title/scope không rộng hơn Sxx;
2. material claims tuân Dxx/Plan;
3. không có material claim mới ngoài Plan;
4. high-value items đã thực hiện đúng disposition;
5. multi-step examples/sequences không bị collapse;
6. dependent values đã tính lại đúng;
7. meaning-bearing presentation không bị flatten đáng kể;
8. promotion đã dọn nhưng useful core/resource còn;
9. không có workflow/research/editorial-state metadata trong public HTML.

Nếu phát hiện lỗi có thể sửa bằng chính Plan, sửa ngay trong lượt viết. Không mở loop mới.

## 17. Output contract

Nếu viết được, output chỉ gồm:

`HÀNH ĐỘNG TIÊU ĐỀ: GIỮ | VIẾT LẠI | CẬP NHẬT`

`TIÊU ĐỀ CUỐI: <một dòng tiêu đề>`

Sau đó một fenced code block chứa duy nhất Canonical HTML hoàn chỉnh.

Không thêm báo cáo sau HTML.

Public HTML:

- H1 body = 0;
- dùng EDS/canonical HTML hợp lệ;
- không để Sxx/Rxx/Cxx/Pxx/E##/Dxx hay trạng thái workflow trong bài;
- không có soft-ad residue;
- không invent URL/src.

## 18. Hard loop budget và UX no-regression

Không thay đổi:

- `Làm rõ căn cứ khi cần`: tối đa 1 lần/article-run;
- Bước 6: tối đa 1 lần;
- QA sau Bước 6: đúng 1 lần cuối;
- workflow chỉ hiện sau `Phân tích bài` thành công khi promote live;
- báo cáo user-facing tiếng Việt;
- sessionStorage only;
- đúng 6 canonical prompts.
