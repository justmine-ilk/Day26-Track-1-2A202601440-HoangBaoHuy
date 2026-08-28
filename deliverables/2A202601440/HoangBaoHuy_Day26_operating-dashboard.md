# Operating Dashboard — TutorAI Vietnam

> Worksheet nguồn công khai cho Day 26. Mọi con số chưa có từ cohort TutorAI
> được ghi là giả định hoặc kế hoạch đo; dashboard không tuyên bố đó là kết quả pilot.

- Học viên: Hoàng Bảo Huy
- Mã học viên: 2A202601440
- Mô hình: B2C
- Cập nhật: 2026-08-28
- North Star: D30 cohort retention đạt ít nhất 40% trước khi tăng chi acquisition

## Chẩn đoán mô hình

TutorAI Vietnam là B2C vì sinh viên tự trả 199.000 VND mỗi tháng, tự dùng workspace học tập cho bài của họ và TutorAI đo trực tiếp các hành vi mở tài liệu, hoàn thành job, quay lại học và trả phí; vì vậy retention là đèn bật trước trước khi đổ thêm ngân sách acquisition.

| Dữ liệu đầu vào | Trạng thái | Nằm ở đâu hoặc cần gì để đo | Ngày có số |
|---|---|---|---|
| Unit economics Day 24 | Đo được | Workbook Day 24: ARPU 199.000 VND, CAC giả định 500.000 VND, GM kế hoạch 72,9% | 2026-08-28 |
| Value Metric và Cost/Job Day 25 | Đo được | Workbook Day 25: 30 attempts, 80% containment, 24 completed jobs, COGS 54.000 VND và Cost/Job 2.250 VND | 2026-08-28 |

## Kiểm kê đèn ứng viên

| Đèn ứng viên từ handbook | Tầng | Trạng thái | Bằng chứng hiện có hoặc kế hoạch đo |
|---|---|---|---|
| Đường cong retention có phẳng không | L | 🔧 | Instrument cohort signup, weekly active study và D30 return; khóa baseline sau bốn cohort vào 2026-10-31 |
| Activation rate | L | 🔧 | Event first source-grounded completed job trong 7 ngày được thêm vào LMS/web funnel trước 2026-09-07 |
| p95 cost/user/tháng ÷ ARPU | O | ✅ | Day 25 cost model đã có Cost/Job; bổ sung phân vị p95 khi có event cost theo student vào 2026-09-30 |
| Trial → paid | O | 🔧 | Theo dõi offer, checkout và subscription active ở pilot Month 3; có cohort report vào 2026-11-26 |
| Retention M12 | G | ❌ | Chưa đủ thời gian; chỉ đánh giá sau cohort đủ 12 tháng vào 2027-08-28 |
| Chi phí free tier ÷ tổng COGS | O | 🔧 | Gắn cost tag vào credit request trước public beta, có baseline sau bốn tuần vào 2026-10-31 |
| Tỷ lệ refund | O | ❌ | Chưa có thanh toán thực; ghi payment event và refund reason trước offer pilot vào 2026-11-12 |
| LTV/CAC · CAC payback · GM | G | 🔧 | Day 24 là giả định; thay bằng cohort revenue, fully-loaded CAC và COGS quan sát được vào 2026-11-26 |

## Đèn báo sớm

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| L-01 | Activation 7 ngày | Sinh viên có ít nhất một source-grounded completed job trong 7 ngày ÷ qualified student testers | Tuần · Product Operations | Chưa đo | ≥60% | 40–59,9% | <40% | [TB] Instrument signup, document-open và first completed-job trong 4 cohort tuần; 60% là mục tiêu Month 1 (18/30) và khóa baseline ngày 2026-10-31. | 2026-08-28 | D30 retention và trial-to-paid | R-01 |
| L-02 | D30 cohort retention | Sinh viên active có ít nhất một completed job ở ngày 30 ÷ sinh viên đã activate trong cohort | Tháng · Product Operations | Chưa đo | ≥40% | 25–39,9% | <25% | [TB] Dùng cùng định nghĩa active trong 4 cohort, đọc retention ở D7/D14/D30 và chốt baseline ngày 2026-11-26; metric báo trước LTV. | 2026-08-28 | LTV/CAC và quyết định acquisition | R-02 |

## Đèn vận hành

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| O-01 | Observed containment | Completed jobs không retry hoặc unsupported handoff ÷ attempted credit requests trong cohort | Tuần · Product Operations | 80% giả định kế hoạch | ≥80% | 67,8–79,9% | <67,8% | [MH] MH-02 tính floor 67,8% để giữ 60% GM; 80% là giả định Day 25, cần thay bằng cohort quan sát được. | 2026-08-28 | Cost/Job và gross margin | R-03 |
| O-02 | Chi phí AI trên mỗi completed job | Tổng API, infrastructure, sampled QA, retry reserve và overhead trực tiếp ÷ completed jobs | Tuần · FinOps | 2.250 VND giả định kế hoạch | ≤2.250 VND | 2.251–3.316 VND | >3.316 VND | [MH] MH-01 suy trần 3.316 VND/job cho GM 60%; 2.250 VND là Cost/Job Day 25 chưa được pilot xác nhận. | 2026-08-28 | Gross margin và quota | R-04 |
| O-03 | Trial-to-paid 4 tuần | Sinh viên được offer trả phí và active subscription trong 28 ngày ÷ sinh viên đã activate đủ 28 ngày | Tháng · Growth Operations | Chưa đo | ≥30% | 15–29,9% | <15% | [TB] Log offer-shown, checkout và active subscription trong 4 cohort; 30% là mục tiêu Month 3 (30 paying/100 testers), khóa baseline ngày 2026-11-26. | 2026-08-28 | LTV/CAC và paid acquisition | R-05 |

## Đèn kết quả

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| G-01 | Plan gross margin | (Base-plan revenue − direct COGS) ÷ base-plan revenue | Tháng · Finance | 72,9% giả định kế hoạch | ≥60% | 50–59,9% | <50% | [MH] MH-01 dùng GM tối thiểu 60% để đặt trần Cost/Job; 72,9% là output Day 25, không phải kết quả billing thực tế. | 2026-08-28 | Runway và pricing | R-04 |
| G-02 | Observed LTV/CAC | Gross profit cohort dự kiến theo churn quan sát được ÷ fully-loaded CAC của cùng cohort | Quý · Finance | Chưa đo | ≥3,0× | 1,5–2,9× | <1,5× | [TB] Ghép cohort revenue, retained gross profit và paid-acquisition spend trong 2 quý; Day 24 7,25× chỉ là giả định để đối chiếu, baseline có ngày 2027-02-28. | 2026-08-28 | Quy mô acquisition và runway | R-05 |

## Luật quyết định

| ID | NẾU | TRONG | VÀ | THÌ | KHÔNG THÌ | Luật dừng? |
|---|---|---|---|---|---|---|
| R-01 | Activation 7 ngày <40% | 2 cohort tuần liên tiếp | Mỗi cohort có ít nhất 30 qualified testers | Dừng tuyển cohort mới 14 ngày, xem replay 20 session và sửa một bước onboarding trước cohort kế tiếp | Không tăng ngân sách paid ads để bù số signup thấp | CÓ |
| R-02 | D30 retention <25% | 2 cohort D30 liên tiếp | Mỗi cohort có ít nhất 25 activated students | Chuyển sprint kế tiếp sang ba failure slice khiến sinh viên không quay lại và thử lại trên cohort 30 người | Không thêm feature mới không gắn với failure slice | KHÔNG |
| R-03 | Observed containment <67,8% | 2 tuần liên tiếp | Có ít nhất 100 attempted credit requests mỗi tuần | Giảm quota trial xuống 20 credits, sửa routing unsupported và chạy lại eval slice trước khi mở thêm offer | Không mở rộng paid acquisition khi cost floor đã bị phá | CÓ |
| R-04 | Chi phí AI/completed job >3.316 VND | 2 tuần liên tiếp | Có ít nhất 100 completed jobs mỗi tuần | Giới hạn context, chuyển model tier cho câu hỏi đơn giản và giữ sampled QA trước kỳ billing tiếp theo | Không cắt QA hoặc bỏ retry log để làm chi phí trông thấp hơn | KHÔNG |
| R-05 | Trial-to-paid 4 tuần <15% | 2 cohort tháng liên tiếp | Có ít nhất 30 activated students đã nhận offer mỗi cohort | Tắt thử nghiệm paid channel, phỏng vấn 10 non-converters và thay một giả thuyết packaging trước cohort sau | Không hạ giá đại trà khi chưa biết objection chính | KHÔNG |

## Cổng gác 90 ngày

| Ngày | Metric gác cổng | Ngưỡng | Bằng chứng vật lý | Nếu đạt | Nếu trượt |
|---:|---|---|---|---|---|
| 30 | Activation 7 ngày | ≥60% trên ít nhất 30 qualified testers | Export event log signup-to-completed-job và 10 interview notes đã redacted | GO | FIX |
| 60 | Observed containment | ≥67,8% trên ít nhất 100 attempted credit requests | Versioned eval output, routing log và containment cohort report | GO | PIVOT |
| 90 | Plan gross margin | ≥60% trên ít nhất 30 active subscriptions trong 4 tuần | Billing export, COGS ledger và monthly finance review | GO | KILL |

## Kill criteria

KILL hướng mở rộng paid self-serve vào ngày 90 nếu plan gross margin dưới 60% sau hai chu kỳ tối ưu cost liên tiếp và cohort 30 subscription vẫn không giữ được ngưỡng này trong bốn tuần.

## Chưa đo được

| Đèn hoặc giả định | Cần gì để đo | Ai chịu trách nhiệm | Ngày có số |
|---|---|---|---|
| D30 cohort retention của TutorAI | Event retention cohort với activation và completed-job theo cùng student ID đã pseudonymize | Product Operations | 2026-11-26 |
| Observed containment thay cho giả định 80% | 100 session eval có outcome, retry và unsupported-handoff reason | Product Operations | 2026-10-27 |
| Fully-loaded CAC và observed LTV/CAC | Cohort revenue, retained gross profit, paid media spend và growth labor ledger | Finance | 2027-02-28 |

## Phụ lục ngưỡng suy từ mô hình

| ID | Metric | Input Day 24–25 | Phép tính | Kết quả và ngưỡng áp dụng |
|---|---|---|---|---|
| MH-01 | Trần Cost/Completed Job tại GM 60% | ARPU 199.000 VND/tháng; GM tối thiểu 60%; 24 completed jobs/tháng | 199.000 VND × (1 − 60%) = 79.600 VND COGS tối đa/tháng; 79.600 VND ÷ 24 jobs = 3.316,67 VND/job | O-02 xanh ≤2.250 VND theo plan; vàng 2.251–3.316 VND; đỏ >3.316 VND. G-01 phải giữ ≥60% GM. |
| MH-02 | Containment tối thiểu tại GM 60% | Direct COGS 54.000 VND/tháng; giá phân bổ 199.000 ÷ 30 = 6.633,33 VND/credit; 30 attempted credits; GM mục tiêu 60% | 54.000 VND ÷ (6.633,33 VND × (1 − 60%) × 30) = 67,84% | O-01 xanh ≥80% theo plan; vàng 67,8–79,9%; đỏ <67,8% và phải dừng mở rộng acquisition. |

## Ghi nhận AI critique

| Phản biện | Chấp nhận hay bác bỏ | Thay đổi đã thực hiện | Lý do |
|---|---|---|---|
| Không được xem giả định Day 25 là pilot evidence | Chấp nhận | Gắn nhãn “giả định kế hoạch” cho 80% containment, 2.250 VND/job và 72,9% GM | Tránh biến mô hình thành bằng chứng quan sát được |
| Retention cần là đèn bật trước của B2C | Chấp nhận | Chọn D30 retention làm North Star và liên kết activation tới retention | Phù hợp model B2C và ngăn phản xạ tăng acquisition quá sớm |
| Rule phải cấm một phản xạ sai | Chấp nhận | Thêm vế “Không thì” cụ thể cho cả 5 rule | Đủ điều kiện rubric và tránh hành động gây hại |
