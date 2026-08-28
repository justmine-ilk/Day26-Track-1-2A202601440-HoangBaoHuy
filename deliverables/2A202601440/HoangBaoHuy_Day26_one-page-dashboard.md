# Operating Dashboard — TutorAI Vietnam

**Model:** B2C · **Cập nhật:** 2026-08-28 · **Owner phiên họp:** Hoàng Bảo Huy

**Chẩn đoán:** Sinh viên tự trả tiền và tự dùng TutorAI trong LMS/web study flow; TutorAI đo trực tiếp completed job, retention và thanh toán của sinh viên.

**North Star:** D30 cohort retention · hiện tại chưa đo · mục tiêu ≥40% · trạng thái 🔧

## Cây đèn 3 tầng

| Tầng · ID | Metric và định nghĩa ngắn | Hiện tại · 🟢 / 🟡 / 🔴 · Nguồn | Nhịp · Owner | Báo trước cho · Luật |
|---|---|---|---|---|
| L · L-01 | Activated ≤7 ngày ÷ qualified testers | Chưa đo · ≥60 / 40–59,9 / <40 · `[TB]` | Tuần · Product Operations | D30 retention + paid · R-01 |
| L · L-02 | Active tại D30 ÷ activated cohort | Chưa đo · ≥40 / 25–39,9 / <25 · `[TB]` | Tháng · Product Operations | LTV/CAC + acquisition · R-02 |
| O · O-01 | Completed không retry/handoff ÷ attempted credits | 80% giả định · ≥80 / 67,8–79,9 / <67,8 · `[MH-02]` | Tuần · Product Operations | Cost/Job + GM · R-03 |
| O · O-02 | Direct AI COGS ÷ completed jobs | 2.250 VND giả định · ≤2.250 / 2.251–3.316 / >3.316 · `[MH-01]` | Tuần · FinOps | GM + quota · R-04 |
| O · O-03 | Paid trong 28 ngày ÷ activated đủ 28 ngày | Chưa đo · ≥30 / 15–29,9 / <15 · `[TB]` | Tháng · Growth Operations | LTV/CAC + acquisition · R-05 |
| G · G-01 | (Revenue − direct COGS) ÷ revenue | 72,9% giả định · ≥60 / 50–59,9 / <50 · `[MH-01]` | Tháng · Finance | Runway + pricing · R-04 |
| G · G-02 | Observed retained gross profit ÷ fully-loaded CAC | Chưa đo · ≥3,0× / 1,5–2,9× / <1,5× · `[TB]` | Quý · Finance | Acquisition scale · R-05 |

## Luật quyết định

| ID | NẾU · TRONG · VÀ | THÌ | KHÔNG THÌ | Dừng? |
|---|---|---|---|---|
| R-01 | Activation <40% · 2 cohort tuần · ≥30 testers/cohort | Dừng tuyển cohort 14 ngày; sửa một bước onboarding | Không tăng paid ads để bù signup | CÓ |
| R-02 | D30 retention <25% · 2 cohort · ≥25 activated/cohort | Sprint vào 3 failure slice lớn nhất | Không thêm feature không gắn failure slice | KHÔNG |
| R-03 | Containment <67,8% · 2 tuần · ≥100 attempts/tuần | Giảm quota, sửa routing, chạy lại eval slice | Không mở rộng acquisition | CÓ |
| R-04 | Cost/job >3.316 VND · 2 tuần · ≥100 jobs/tuần | Giới hạn context, route model tier, giữ QA | Không cắt QA hoặc bỏ retry log | KHÔNG |
| R-05 | Trial-to-paid <15% · 2 tháng · ≥30 offered/cohort | Tắt paid channel, phỏng vấn 10 non-converters | Không hạ giá đại trà | KHÔNG |

## Cổng 90 ngày

| Ngày | Một metric · ngưỡng | Evidence | Đạt / Trượt |
|---:|---|---|---|
| 30 | Activation 7 ngày · ≥60% trên ≥30 testers | Event log + 10 interview notes redacted | GO / FIX |
| 60 | Observed containment · ≥67,8% trên ≥100 attempts | Eval output + routing log | GO / PIVOT |
| 90 | Plan gross margin · ≥60% trên ≥30 subscriptions/4 tuần | Billing export + COGS ledger | GO / KILL |

**Kill criteria:** KILL mở rộng paid self-serve ngày 90 nếu GM <60% sau hai chu kỳ tối ưu cost và cohort 30 subscriptions không giữ được ngưỡng trong bốn tuần.

**Chưa đo được:** D30 retention, observed containment và fully-loaded LTV/CAC; cần event cohort, eval output, billing/COGS ledger; owner Product Operations/Finance; có số lần lượt 2026-11-26, 2026-10-27 và 2027-02-28.

## Phụ lục trang 2

| ID | Input và phép tính | Kết quả |
|---|---|---|
| MH-01 | 199.000 VND × (1 − 60%) = 79.600 VND; 79.600 ÷ 24 jobs = 3.316,67 VND/job | Cost/Job đỏ >3.316 VND; GM tối thiểu 60% |
| MH-02 | 54.000 ÷ (6.633,33 × (1 − 60%) × 30) = 67,84% | Containment đỏ <67,8%; dừng mở rộng acquisition |
