# KTD Editorial Content Renewal v1.7 — Phase 5 Candidate Runtime Skill

**Target Skill Runtime:** 1.6.0  
**Target Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Phase 5 scope:** kế thừa Phase 2 cho Bước 1–3, Phase 3 cho Bước 4, Phase 4 cho Bước 5 và triển khai candidate Bước 6 — Minimal Repair.  
**Status:** CANDIDATE — không phải file live mà Assistant production đang nạp.

## 1. Nền tảng kế thừa

Phase 5 giữ nguyên toàn bộ contract đã khóa:

- Accuracy và Preservation là hai trục độc lập;
- Sxx/Rxx/Dxx chỉ phục vụ material accuracy;
- CORE hẹp;
- SUPPORTING không phải giấy phép xóa/rút tùy ý;
- Source Preservation Default;
- Research Boundedness;
- `UPDATE/CORRECT`, `REFRESH EXAMPLE`, `LIGHT REPHRASE`, `REMOVE PROMOTION`;
- Danh sách phần giá trị cần giữ + Preservation Contract;
- Writer thực thi theo Correctness → Preservation → Refresh Example → Light Rephrase → Remove Promotion;
- Final QA có đúng hai pass: Coverage + Preservation → Material Accuracy;
- chỉ ba preservation blocker: `MẤT_NỘI_DUNG_GIÁ_TRỊ`, `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`, `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`;
- hard loop budget của v1.6;
- đúng 6 canonical prompts;
- báo cáo user-facing bằng tiếng Việt rõ ràng.

Phase 5 không thay thế các candidate trước; nó hoàn thiện contract logic cho Bước 6.

## 2. Vai trò của Bước 6

Bước 6 là **Minimal Repair theo cụm**, không phải Writer lần hai, không phải researcher và không phải cơ hội thiết kế lại toàn bài.

Chỉ chạy khi có một trong hai đầu vào hợp lệ:

1. Bước 5 trả `KẾT QUẢ CUỐI: CHƯA ĐẠT — SỬA MỘT LẦN Ở BƯỚC 6` cùng `CÁC LỖI CÓ THỂ SỬA MỘT LẦN Ở BƯỚC 6`; hoặc
2. Bước 5 trả `KẾT QUẢ CUỐI: CẦN LÀM RÕ CĂN CỨ`, nhánh `Làm rõ căn cứ khi cần` vừa được dùng hợp lệ và trả gói bổ sung đủ để sửa một lần.

Mỗi bài chỉ được chạy Bước 6 **một lần**.

Nếu trạng thái workflow cho thấy Bước 6 đã dùng, Bước 6 phải trả:

`CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`

và dừng.

## 3. Định nghĩa đúng của “Minimal Repair”

`Minimal` nghĩa là **phạm vi sửa tối thiểu cần thiết để giải quyết blocker đã được Bước 5 đóng gói**, không phải cắt bài cho ngắn hoặc xóa nội dung để dễ PASS.

Bước 6 không được:

- giải quyết lỗi accuracy bằng cách xóa high-value region khi có thể sửa treatment và giữ chức năng;
- giải quyết lỗi preservation bằng cách chép lại wording/treatment cũ đã lỗi thời;
- thu hẹp public scope chỉ để né một Dxx trừ khi Bước 5 đã authorize rõ;
- đổi toàn bộ cấu trúc, giọng văn hoặc ví dụ không liên quan;
- đặt mục tiêu giảm word count;
- mở thêm research để “chắc hơn”.

Correctness và Preservation cùng ràng buộc repair.

## 4. Nguồn được phép dùng

Bước 6 chỉ dùng:

- title + Canonical HTML nguồn;
- Final title + Final Canonical HTML gần nhất từ Bước 4;
- Bước 1 + Danh sách phần giá trị cần giữ;
- Bước 2 + Sxx/Dxx;
- Bước 3 + Renewal Plan + Preservation Contract + Example Refresh Plan + Presentation/Resource Plan;
- Bước 5 + từng cụm lỗi sửa một lần;
- gói bổ sung căn cứ sau `Làm rõ căn cứ khi cần` nếu nhánh đó vừa được dùng hợp lệ;
- Skill hiện hành.

Không mở web research mới.
Không tạo Rxx/Sxx/Dxx mới trong Bước 6.
Không tự suy diễn evidence mới từ trí nhớ.

## 5. Đơn vị sửa là Scope + Decision + Preservation Cluster

Mỗi repair cluster có thể chứa:

- Sxx/public scope;
- Dxx/material treatment;
- high-value item/disposition;
- destination/equivalent cần phục hồi;
- các bề mặt liên quan: title, intro, scope statement, explanation, formula, example, warning/note, accounting group, table, resource, summary/conclusion.

Bước 6 phải sửa **đồng bộ trong cùng một lượt** tất cả bề mặt thực sự bị ảnh hưởng.

Không chia cùng một Dxx hoặc cùng một high-value region thành nhiều vòng sửa.

## 6. Thứ tự ưu tiên khi sửa một cluster

1. **Correctness** — treatment/scope đúng theo Sxx/Dxx/evidence đã khóa;
2. **Preservation target** — teaching function, practical depth và presentation role theo Preservation Contract;
3. **Cross-surface consistency** — mọi nơi cùng nói về cluster phải đồng bộ;
4. **Minimum necessary change** — giữ nguyên phần không liên quan.

Không dùng stylistic polish để mở rộng phạm vi sửa.

## 7. Repair accuracy blocker

### `LỖI SO VỚI Dxx`

Sửa treatment đúng theo Dxx trên mọi bề mặt có cùng decision.

### `CROSS-SURFACE CONFLICT`

Đồng bộ intro/explanation/formula/example/warning/table/summary liên quan; không để treatment cũ còn sót.

### `SCOPE OVERCLAIM`

Chỉ thu hẹp title/intro/scope/heading/summary khi gói Bước 5 xác nhận đây là repair hợp lệ và không phá promise/CORE ngoài authorization.

Nếu phạm vi phải giữ nhưng evidence hiện có chưa đủ treatment, không tự thu hẹp để né lỗi; chuyển thủ công nếu không có gói clarification đủ căn cứ.

### `UNMAPPED MATERIAL CLAIM`

- nếu Bước 5 cho phép bỏ/generalize vì claim không CORE và không high-value → bỏ/generalize tối thiểu;
- nếu claim thuộc high-value region → ưu tiên sửa/viết trung tính sao cho teaching function còn;
- nếu cần treatment material mới → chỉ sửa khi gói clarification đã cung cấp căn cứ + coverage đủ.

### `SCOPE COVERAGE GAP`

Chỉ sửa khi gói clarification đã reconcile đủ Sxx liên quan. Không tự đoán.

## 8. Repair preservation blocker

### `MẤT_NỘI_DUNG_GIÁ_TRỊ`

Phục hồi high-value item theo disposition đã khóa hoặc dựng equivalent ở đúng destination đã Plan chỉ định.

Nếu source item chứa material treatment cũ sai:

- không copy nguyên lỗi cũ;
- dùng Dxx để sửa phần sai;
- giữ lại teaching purpose và practical value tương đương.

### `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`

Phục hồi các bước/quan hệ có learning value bị mất, ví dụ:

- intermediate steps trong worked example;
- practical sequence;
- comparison/breakdown;
- condition/warning cần để hiểu đúng;
- procedural/accounting sequence khi chính sequence là mục tiêu dạy học.

Không cần khôi phục cùng số chữ; phải khôi phục **functional value**.

### `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`

Phục hồi semantic role bằng canonical EDS primitive/equivalent phù hợp:

- warning/content box;
- key-line;
- checklist/steps;
- table/comparison;
- accounting grouping;
- example/note;
- image/caption/useful resource.

Chỉ phục hồi URL/src/anchor/resource đã có trong source/Plan/evidence. Không invent URL, file, image src hoặc download path.

## 9. Example repair

Khi cluster ảnh hưởng author-created example đã được refresh:

- ưu tiên giữ tên/số/bối cảnh đã refresh ở Bước 4;
- nếu phải thêm lại intermediate step bị mất, tích hợp step đó với bộ số hiện hành;
- tính lại toàn bộ dependent values bị ảnh hưởng;
- kiểm arithmetic trước output;
- giữ `inputs → intermediate steps → outputs` khi các bước có learning value;
- giữ practical depth tương đương;
- material treatment phải tuân Dxx;
- không tự quay về tên/số cũ của source chỉ vì dễ hơn;
- không thêm giả định material mới để làm phép tính chạy được.

Nếu không thể tính đúng mà phải bịa thêm assumption material, chuyển `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

Official/source-attributed example giữ fidelity/provenance; không refresh novelty trái contract.

## 10. Promotional cleanup trong repair

Nếu high-value item nằm trong vùng source có quảng bá:

- chỉ phục hồi useful editorial core;
- không phục hồi self-praise/sales/social CTA;
- không biến hard-ad thành soft-ad;
- legitimate attribution/provenance chỉ giữ khi cần;
- useful resource hợp lệ có thể giữ nếu Plan đã xác định giá trị.

Repair preservation không phải lý do đưa quảng cáo trở lại.

## 11. Meaning-bearing presentation và resource

Bước 6 không cần pixel parity hoặc exact structural count.

Nó chỉ cần đảm bảo item bị blocker lấy lại đúng semantic/teaching function.

Có thể dùng canonical EDS equivalent khác nếu chức năng tương đương hoặc tốt hơn và không đổi meaning.

Không được:

- flatten warning thành prose nếu warning là functional target;
- đổi table thành prose nếu mất khả năng đối chiếu;
- bỏ checklist/steps nếu mất chức năng thực hành;
- xóa useful image/caption/resource chỉ để HTML gọn;
- invent replacement asset.

## 12. Giữ nguyên phần không liên quan

Bước 6 phải xem Final gần nhất là base patch.

Ngoài cluster đã được Bước 5 authorize:

- không viết lại toàn bài;
- không đổi heading/order vô cớ;
- không refresh thêm example mới;
- không polish hàng loạt;
- không thêm section mới;
- không thay resource không liên quan;
- không đổi official content để tạo novelty.

## 13. Không biến Bước 6 thành research/audit mới

Bước 6 không được:

- mở web research;
- tạo Rxx/Sxx/Dxx mới;
- phát minh thêm blocker ngoài gói QA;
- kiểm toán mọi supporting detail;
- dựng full accounting route khi không phải teaching target;
- tạo hypothetical regime/exception ngoài Sxx;
- quay lại Bước 1–4.

Nếu gặp minor detail ngoài cluster, giữ nguyên hoặc viết trung tính nếu Plan đã cho phép; không mở scope repair.

## 14. Khi nào phải dừng và chuyển thủ công

Trả `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG` nếu:

- Bước 6 đã dùng;
- cluster accuracy cần material evidence mới nhưng không có gói clarification đủ;
- repair yêu cầu invent rule/route/assumption material;
- gói QA tự mâu thuẫn trực tiếp về cùng Dxx/Sxx/functional target;
- không thể vừa giữ correctness vừa giữ functional target bằng evidence hiện có;
- resource bắt buộc phải thay nhưng không có replacement hợp lệ và không thể giữ safely.

Không dùng wording/polish/minor layout uncertainty để chuyển thủ công.

## 15. Self-check đúng một lượt trước output

Không research lại. Kiểm deterministic:

1. từng repair cluster đã được xử lý;
2. title/intro/scope/heading/summary không vượt Sxx;
3. material treatment đúng Dxx;
4. treatment cũ của cùng cluster không còn ở bề mặt khác;
5. high-value item đã đạt functional target;
6. multi-step example/sequences đã phục hồi đủ learning step cần thiết;
7. dependent values đã tính lại đúng;
8. presentation/resource blocker đã phục hồi chức năng mà không invent asset;
9. promotion không bị đưa trở lại;
10. phần ngoài cluster không bị thay đổi đáng kể;
11. public HTML không có workflow/research metadata.

Nếu lỗi có thể sửa bằng chính cluster/evidence đã có, sửa trong lượt này. Không tạo loop mới.

## 16. Output contract

Khi sửa được, output chỉ gồm:

`TIÊU ĐỀ CUỐI: <một dòng tiêu đề>`

Sau đó một fenced code block chứa duy nhất Canonical HTML hoàn chỉnh đã sửa.

Sau closing fence ghi đúng:

`BƯỚC 6 ĐÃ DÙNG: CÓ — BẮT BUỘC CHẠY BƯỚC 5 LẦN CUỐI.`

Không thêm báo cáo dài sau HTML.

Public HTML:

- H1 body = 0;
- dùng canonical EDS vocabulary;
- không inline style/arbitrary class/data-* nếu contract không cho phép;
- không script/form/input/event handler;
- không invent URL/src;
- không đưa Sxx/Rxx/Cxx/Pxx/E##/Dxx, blocker state, research state hoặc lời nhắc biên tập vào HTML công khai.

## 17. QA sau Bước 6 là lần cuối

Sau khi Bước 6 output thành công:

- bắt buộc chạy Bước 5 đúng một lần cuối;
- không chạy Bước 6 lần hai;
- không mở `Làm rõ căn cứ khi cần` lần mới;
- nếu còn blocker accuracy hoặc preservation đáng kể → `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`;
- không hạ blocker thành gợi ý nhỏ chỉ để kết thúc workflow.

## 18. Hard loop budget và UX no-regression

Không thay đổi:

- `Làm rõ căn cứ khi cần`: tối đa 1/article-run;
- Bước 6: tối đa 1/article-run;
- QA sau Bước 6: đúng 1 lần cuối;
- workflow chỉ hiện sau `Phân tích bài` thành công khi promote live;
- re-analyze reset workflow state/budget;
- clarification là nhánh phụ;
- sessionStorage only;
- đúng 6 canonical prompts;
- báo cáo user-facing tiếng Việt;
- không hard-code golden TSCĐ/regulation vào runtime.
