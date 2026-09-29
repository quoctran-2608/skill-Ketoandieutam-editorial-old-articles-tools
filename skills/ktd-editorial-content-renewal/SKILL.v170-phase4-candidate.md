# KTD Editorial Content Renewal v1.7 — Phase 4 Candidate Runtime Skill

**Target Skill Runtime:** 1.6.0  
**Target Prompt Set:** 1.7.0  
**Workflow policy:** `MATERIAL_ACCURACY_AND_PRESERVATION_V4`  
**Canonical workflow:** 6 bước  
**Phase 4 scope:** kế thừa Phase 2 cho Bước 1–3, Phase 3 cho Bước 4 và triển khai candidate Bước 5 — Final QA. Bước 6 chưa promote.  
**Status:** CANDIDATE — không phải file live mà Assistant production đang nạp.

## 1. Nền tảng kế thừa

Phase 4 giữ nguyên các contract đã khóa:

- Accuracy và Preservation là hai trục độc lập;
- Sxx/Rxx/Dxx chỉ phục vụ material accuracy;
- CORE hẹp;
- SUPPORTING không phải giấy phép xóa/rút tùy ý;
- Source Preservation Default;
- Research Boundedness;
- `UPDATE/CORRECT`, `REFRESH EXAMPLE`, `LIGHT REPHRASE`, `REMOVE PROMOTION`;
- Danh sách phần giá trị cần giữ + Preservation Contract;
- Writer thực thi theo Correctness → Preservation → Refresh Example → Light Rephrase → Remove Promotion;
- hard loop budget của v1.6;
- đúng 6 canonical prompts;
- báo cáo user-facing bằng tiếng Việt rõ ràng.

Phase 4 không thay thế Phase 2–3 candidate; nó bổ sung contract cho Bước 5.

## 2. Vai trò của Bước 5

Bước 5 là **cổng an toàn trước khi đăng**, không phải researcher, không phải Writer lần hai và không phải kỳ thi chứng minh mọi dòng tuyệt đối.

Bước 5 phải trả lời hai câu hỏi riêng:

1. **Độ chính xác:** Final có sai/vượt phạm vi một quyết định chuyên môn trọng yếu đủ mức khiến người đọc dễ áp dụng sai hoặc ảnh hưởng uy tín không?
2. **Giá trị bài gốc:** Final có làm mất hoặc làm nghèo đáng kể một phần đã được xác định là có giá trị giảng dạy/thực hành/trình bày không?

Bước 5 không mở research mới.

## 3. Hai pass — giữ đúng một Prompt 5

Bước 5 chỉ có hai pass khái niệm trong cùng một prompt:

### Pass 1 — Coverage + Preservation

Kiểm:

- public scope coverage theo Sxx;
- material claim traceability về Dxx;
- Dxx scope coverage;
- CORE material coverage;
- các item trong Danh sách phần giá trị cần giữ / Preservation Contract;
- Example Refresh Plan;
- meaning-bearing presentation/resource có giá trị.

Không inventory lại toàn bài và không lập Vxx matrix.

### Pass 2 — Material Accuracy

Với từng Dxx thực sự được Final sử dụng, kiểm:

- phạm vi/hiệu lực;
- khác biệt giữa các Sxx khi relation yêu cầu tách;
- kết luận chính/formula/math/rate/threshold/deadline/classification/treatment chính;
- condition/exception trọng yếu;
- nhất quán xuyên bài.

Không tạo Dxx mới chỉ vì QA nghĩ ra một giả thuyết ngoài public scope.

## 4. Preservation QA chỉ nhắm high-value region

Preservation QA **không quét mọi SUPPORTING paragraph**.

Nó chỉ bắt buộc reconcile:

- item đã có trong Danh sách phần giá trị cần giữ;
- item có disposition trong Preservation Contract;
- substantive example trong Example Refresh Plan;
- table/checklist/warning/key-line/accounting group/image/resource đã được Plan đánh dấu có teaching/editorial value.

Nếu một supporting detail không thuộc các nhóm trên, không material và không làm thay đổi teaching function, wording/merge/rút gọn nhẹ không phải blocker.

## 5. Ba preservation blocker duy nhất

### `MẤT_NỘI_DUNG_GIÁ_TRỊ`

Dùng khi một high-value region biến mất hoặc bị bỏ phần cốt lõi mà không có disposition hợp lệ, destination tương đương hoặc lý do bỏ đã được Plan authorize.

### `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`

Dùng khi region vẫn còn nhưng functional value giảm đáng kể, ví dụ:

- multi-step example bị collapse thành one-line summary;
- practical sequence mất step có learning value;
- comparison/breakdown mất quan hệ cần để hiểu;
- warning/risk signal bị làm yếu tới mức mất chức năng;
- example giữ broad topic nhưng không còn minh họa learning objective nguồn.

### `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`

Dùng khi table/checklist/warning/key-line/accounting grouping/image/caption/useful resource có giá trị bị xóa hoặc flatten đến mức mất chức năng, trong khi Plan không authorize một equivalent hợp lệ.

Không tạo thêm loại preservation blocker riêng lẻ.

## 6. Functional equivalence trong QA

MOVE/MERGE/REPLACE chỉ PASS preservation khi destination/equivalent thực sự giữ được chức năng cần thiết.

“Cùng chủ đề”, “vẫn còn nhắc đến” hoặc “bài vẫn đúng về CORE” chưa đủ nếu phần thực hành/teaching role quan trọng đã collapse.

Ngược lại, không yêu cầu:

- exact word count;
- exact paragraph count;
- exact heading count;
- pixel parity;
- giữ nguyên primitive khi canonical equivalent khác giữ chức năng tốt hơn;
- giữ duplicate example khi Plan đã merge thành một equivalent tốt hơn.

## 7. QA cho ví dụ

Với author-created substantive example đã được refresh:

- tên/số/bối cảnh phải khác theo Plan;
- dependent values phải được tính lại nhất quán;
- material treatment phải tuân Dxx;
- `inputs → intermediate steps → outputs` phải còn khi các bước có learning value;
- practical depth phải tương đương;
- không dùng số lượng example toàn bài để bù cho một E## cụ thể bị làm nghèo.

Official/source-attributed example được kiểm fidelity/provenance, không bắt đổi tên/số để tạo novelty.

## 8. QA cho presentation/resource

Không block vì cosmetic drift nhỏ.

Chỉ block khi mất chức năng đáng kể của một item đã được xác định có giá trị, ví dụ:

- warning trở thành prose không còn risk signal;
- bảng so sánh thành đoạn văn làm mất khả năng đối chiếu;
- checklist/steps mất khả năng thực hành;
- image/caption hữu ích biến mất không có lý do;
- useful resource bị xóa chỉ vì wrapper quảng bá bị dọn.

Operational migration issue không block publish safety nếu editorial value vẫn được bảo toàn hoặc Plan đã ghi việc vận hành riêng.

## 9. Accuracy QA giữ materiality của v1.6

Không block chỉ vì:

- tài khoản đối ứng phụ không phải teaching target;
- payment state/method phụ;
- route phụ không đổi treatment chính;
- wording/polish;
- supporting detail không high-value được generalize hợp lý;
- hypothetical regime/exception ngoài Sxx;
- official wording được giữ gần nguyên để bảo toàn fidelity.

Blocker accuracy phải chỉ ra Sxx/Dxx/claim cụ thể + ảnh hưởng trọng yếu.

## 10. Không mở vòng audit mới

Bước 5 không được:

- mở web research mới;
- tạo Sxx/Rxx/Dxx mới từ giả thuyết;
- dựng lại exact-detail/full-route matrix legacy;
- yêu cầu chứng minh mọi supporting detail;
- đếm structural parity như một điều kiện PASS;
- sửa HTML trực tiếp.

Nếu lỗi sửa được hoàn toàn từ evidence + Plan hiện có, đóng gói cho Bước 6.

Nếu thật sự thiếu material evidence:

- trước Bước 6 và nhánh `Làm rõ căn cứ khi cần` chưa dùng → cho phép nhánh đó đúng 1 lần;
- nếu đã dùng hoặc đang là QA sau Bước 6 → `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

Preservation-only blocker không được mở research; phải sửa từ source + Plan + Dxx hiện có hoặc chuyển thủ công khi hết budget.

## 11. Gói sửa cho Bước 6

Mỗi blocker sửa được phải đóng thành **một cụm**, không chia thành nhiều vòng.

Gói ghi:

- loại blocker;
- Sxx/Dxx liên quan nếu là accuracy;
- high-value item / disposition liên quan nếu là preservation;
- treatment hoặc functional target đúng;
- các bề mặt phải reconcile cùng lượt: title/intro/scope/explanation/formula/example/warning-note/table/resource/summary khi liên quan;
- destination/equivalent cần phục hồi nếu là MOVE/MERGE/REPLACE.

Cùng một decision hoặc cùng một high-value region không được tạo nhiều vòng sửa.

## 12. Điều kiện PASS

Chỉ `ĐẠT` hoặc `ĐẠT — CÓ GỢI Ý NHỎ` khi đồng thời:

- không `SCOPE OVERCLAIM`;
- không `UNMAPPED MATERIAL CLAIM`;
- không `SCOPE COVERAGE GAP`;
- CORE material decisions traceable;
- mọi Dxx dùng trong Final pass Material Accuracy;
- không cross-surface material conflict;
- không `MẤT_NỘI_DUNG_GIÁ_TRỊ`;
- không `LÀM_NGHÈO_CHỨC_NĂNG_GIẢNG_DẠY`;
- không `MẤT_TÀI_NGUYÊN_TRÌNH_BÀY_GIÁ_TRỊ`.

Gợi ý nhỏ không được dùng để giấu blocker.

## 13. QA sau Bước 6

QA sau Bước 6 là lần tự động cuối:

- không yêu cầu Bước 6 lần hai;
- không mở nhánh làm rõ mới;
- nếu còn blocker accuracy hoặc preservation đáng kể → `CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`;
- không hạ blocker thành gợi ý nhỏ chỉ để kết thúc workflow.

## 14. Output user-facing

Báo cáo phải tiếng Việt, ngắn, không bắt editor giải mã thuật ngữ tiếng Anh.

Các section chính:

- `KIỂM TRA PHẠM VI VÀ TRUY VẾT`;
- `KIỂM TRA GIÁ TRỊ BÀI GỐC`;
- `ĐỐI CHIẾU QUYẾT ĐỊNH TRỌNG YẾU`;
- `LỖI CHẶN ĐĂNG`;
- `GỢI Ý KHÔNG CHẶN ĐĂNG`;
- `VIỆC CẦN LÀM SAU`;
- khi cần: `CÁC LỖI CÓ THỂ SỬA MỘT LẦN Ở BƯỚC 6`.

Không in lại toàn bộ Sxx/Dxx/Preservation Contract đã pass.

## 15. Kết quả cuối và hard loop budget

Giữ đúng các trạng thái:

- `KẾT QUẢ CUỐI: ĐẠT`;
- `KẾT QUẢ CUỐI: ĐẠT — CÓ GỢI Ý NHỎ`;
- `KẾT QUẢ CUỐI: CHƯA ĐẠT — SỬA MỘT LẦN Ở BƯỚC 6`;
- `KẾT QUẢ CUỐI: CẦN LÀM RÕ CĂN CỨ`;
- `KẾT QUẢ CUỐI: CẦN BIÊN TẬP CHUYÊN MÔN THỦ CÔNG`.

Hard budget không đổi:

- `Làm rõ căn cứ khi cần`: tối đa 1/article-run;
- Bước 6: tối đa 1/article-run;
- QA sau Bước 6: đúng 1 lần cuối.

Preservation không được mở thêm loop.

## 16. UX no-regression

Khi promote live ở phase sau phải giữ:

- workflow ẩn tới khi `Phân tích bài` thành công;
- re-analyze reset state/budget;
- clarification là nhánh phụ;
- sessionStorage only;
- Bước 6 mở lại Bước 5 đúng một lần cuối;
- đúng 6 canonical prompts;
- không hard-code golden TSCĐ/regulation vào runtime.