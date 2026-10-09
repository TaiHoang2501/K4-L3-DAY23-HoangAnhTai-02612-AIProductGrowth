# Worksheet — BookingBot AI Agent

Họ tên: Hoàng Anh Tài · MSSV: 2A202602612 · Ngày làm: 09/10/2026

---

## Trạm 1 — Loại mô hình

### 1. Trả lời 3 câu hỏi xác định loại mô hình (theo thực tế hôm nay)

1. **Ai trả tiền cho bạn?**
   - **Doanh nghiệp (B2B):** Tiền đến từ hợp đồng thuê bao phần mềm/bản quyền dịch vụ B2B do các Chủ đầu tư BĐS (Vinhomes) và các Sàn phân phối F1 thanh toán hàng năm (ACV), không thu tiền từ khách mua nhà cá nhân.
2. **Ai dùng sản phẩm?**
   - **Chính tổ chức trả tiền (B2B):** Người trực tiếp thao tác và hưởng lợi là đội ngũ quản lý điều phối giỏ hàng và chuyên viên môi giới nội bộ thuộc hệ thống phân phối/sàn F1 để quản lý lịch, giỏ căn và phân bổ lịch xem nhà.
3. **Nếu có bên trung gian: bạn có chạm được người dùng cuối không?**
   - **Không chạm end-user:** Khách mua nhà cuối cùng chỉ làm việc với môi giới người thật ngoài đời. BookingBot hoạt động như một hệ thống hỗ trợ nghiệp vụ chuyên sâu phía sau (Back-office Agent), kết nối trực tiếp vào CSDL giỏ hàng nội bộ qua VPC/API của doanh nghiệp. Do đó, sản phẩm là **B2B** thuần túy, không phải B2B2C.

### 2. Câu chốt loại

> **Chúng tôi là B2B** vì tiền đến từ hợp đồng bản quyền dịch vụ/phần mềm của **Chủ đầu tư Vinhomes và các Sàn phân phối BĐS F1**, người dùng thật là **đội ngũ điều phối giỏ hàng và môi giới nội bộ** thuộc hệ thống phân phối, và chúng tôi tích hợp giải pháp qua **API/VPC bảo mật kết nối trực tiếp với Cơ sở dữ liệu (CSDL) giỏ hàng** của doanh nghiệp (không trực tiếp tương tác với người mua nhà cuối cùng).

### 3. Rà soát bảng đèn §3 B2B (từ HANDBOOK §3.2)

| Đèn | Tầng | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|---|
| **Time-to-first-value (TTFV)** ⭐ | Leading | 🔧 | Cần log ngày bàn giao kết nối CSDL và log bản ghi ca xem nhà thành công đầu tiên (`VH-YYYY-XXXXX`) trên hệ thống |
| **Pipeline coverage** | Leading | ✅ | Nằm trên hệ thống CRM bán hàng B2B (tổng deal giai đoạn Qualified ÷ chỉ tiêu quý) |
| **% deal chết ở khâu security/procurement** | Leading | 🔧 | Cần biên bản ghi nhận nguyên nhân dừng deal từ bộ phận Pháp chế/IT Security của Chủ đầu tư |
| **POC → paid** | Operating | 🔧 | Cần theo dõi tỷ lệ ký hợp đồng chính thức sau 30 ngày thử nghiệm tại phân khu pilot |
| **Sales cycle (tuần)** | Operating | ✅ | Đo từ ngày tạo cơ hội Qualified trên CRM đến ngày ký hợp đồng thành công |
| **Usage depth trong tài khoản** | Operating | 🔧 | Cần thiết lập sự kiện Product Analytics đo thao tác duyệt lịch/cập nhật căn hàng tuần của môi giới nội bộ |
| **Chi phí triển khai ÷ ACV** | Operating | 🔧 | Cần bảng chấm công giờ làm kỹ thuật (Timesheet Dev) tích hợp CSDL giỏ hàng đối chiếu với giá trị hợp đồng năm |
| **Tập trung doanh thu** | Operating | ✅ | Bảng theo dõi doanh thu kế toán (doanh thu từ phân khu/sàn lớn nhất ÷ tổng doanh thu) |
| **Chi phí Inference AI / lượt khớp lịch (Cost/Job)** | Leading | ✅ | Dashboard giám sát API logging (Langfuse / Azure OpenAI Token usage) chia cho tổng lượt tạo Booking Request |
| **NRR (Net Revenue Retention)** | Lagging | ❌ | Chưa đo được vì sản phẩm mới ở giai đoạn đầu, cần tối thiểu 12 tháng vận hành hợp đồng để có số gia hạn/mở rộng |
| **Gross Margin** | Lagging | 🔧 | Cần bảng đối soát chi phí hạ tầng cloud + API LLM đối chiếu với doanh thu định kỳ hàng quý |
| **CAC payback** | Lagging | ❌ | Chưa đo được chu kỳ hoàn vốn thực tế; hiện đang dùng giả định mô hình tài chính (< 12 tháng), cần ít nhất 2 quý dữ liệu chi phí bán hàng và dòng tiền thu hồi thực tế |

---

## Trạm 2 — Thẻ đèn

**North Star:** **Time-to-first-value (TTFV)** — hiện tại: Chưa có dữ liệu thực tế (đang triển khai pilot) — mục tiêu: **< 14 ngày** (từ lúc bàn giao kết nối CSDL đến khi chốt ca xem nhà thật đầu tiên).

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | **L** ⭐ | **Time-to-first-value (TTFV)** | Đếm số ngày từ khi hoàn tất nghiệm thu kết nối CSDL giỏ hàng đến khi phát sinh ca xem nhà thực tế đầu tiên (`viewing_completed` có mã Deal). **Không** đếm các ca test nội bộ của ban quản lý. | `Ngày phát sinh viewing_completed đầu tiên − Ngày hoàn tất tích hợp CSDL` | Mỗi khách hàng/phân khu · Kỹ sư triển khai | POC → paid (tầng O) & NRR (tầng G) |
| 2 | **L** | **% Deal vượt qua thẩm định Security CSDL** | Đếm % deal vượt qua vòng kiểm tra an toàn dữ liệu/CSDL của CĐT trong vòng 21 ngày. **Không** đếm deal mới ở vòng gặp gỡ ban đầu chưa nộp hồ sơ kỹ thuật. | `(Số deal vượt qua Security trong 21 ngày) ÷ (Tổng deal bước vào vòng Security)` | Hàng tháng · Sales Lead & Security Lead | Sales cycle (tầng O) & Win rate |
| 3 | **L** (AI Cost) | **Chi phí Inference AI trên mỗi yêu cầu khớp lịch (Cost/Job)** | Đếm toàn bộ chi phí token suy luận (LLM API + Embedding vector search trên CSDL giỏ hàng) để hoàn tất 1 Booking Request. **Không** đếm chi phí server web hay lưu trữ database tĩnh. | `Tổng chi phí token LLM & Embedding trong kỳ ÷ Tổng số Booking Request tạo thành công` | Hàng tuần · Lead AI Engineer | Gross Margin (tầng G) |
| 4 | **O** | **POC → paid** | Đếm % dự án phân khu pilot chuyển đổi thành hợp đồng dịch vụ chính thức có trả phí sau thời gian thử nghiệm. **Không** đếm các biên bản ghi nhớ (MOU) phi thương mại. | `(Số phân khu pilot ký hợp đồng trả tiền) ÷ (Tổng số phân khu hoàn thành nghiệm thu pilot)` | Hàng quý · Giám đốc kinh doanh | Doanh thu định kỳ & NRR (tầng G) |
| 5 | **O** | **Chi phí triển khai & tích hợp CSDL ÷ ACV** | Đếm chi phí nhân sự kỹ thuật Onboarding (giờ công dev mapping CSDL giỏ hàng) trên Giá trị hợp đồng năm (ACV). **Không** đếm chi phí hoa hồng bán hàng (Sales Commission). | `(Tổng giờ công kỹ thuật Onboarding × 250.000đ + chi phí hạ tầng sandbox) ÷ ACV` | Mỗi hợp đồng hoàn tất nghiệm thu · Tech Lead | Gross Margin & CAC payback (tầng G) |
| 6 | **O** | **Mức độ sử dụng sâu (Usage Depth)** | Đếm % nhân sự môi giới/điều phối viên được cấp tài khoản có thao tác duyệt hoặc cập nhật slot xem nhà $\ge 1$ lần/tuần. **Không** đếm hành vi đăng nhập chỉ để xem lướt rồi thoát. | `(Số user nội bộ thao tác nghiệp vụ hàng tuần) ÷ (Tổng số user được cấp license)` | Hàng tuần · Product Manager | NRR & Churn năm đầu (tầng G) |
| 7 | **G** | **Gross Margin** | Lãi gộp sau khi trừ toàn bộ chi phí server, bản quyền phần mềm và chi phí token inference AI. **Không** trừ chi phí bán hàng và marketing (CAC). | `(Doanh thu dịch vụ − COGS kỹ thuật trực tiếp) ÷ Doanh thu dịch vụ` | Hàng quý · Kế toán trưởng | Runway & Định giá doanh nghiệp |
| 8 | **G** | **Net Revenue Retention (NRR)** | Đếm % doanh thu định kỳ (ARR) giữ lại và mở rộng từ các sàn/phân khu cũ sau 12 tháng. **Không** đếm doanh thu phát sinh từ khách hàng mới ký lần đầu trong kỳ (New Logos). | `(ARR từ tập khách hàng cũ tại thời điểm T+12) ÷ (ARR từ chính tập khách hàng đó tại thời điểm T) × 100%` | Hàng quý / Hàng năm · Finance Lead & Kế toán trưởng | Tốc độ tích lũy vốn & Định giá doanh nghiệp |

**Đèn chi phí AI là đèn số:** **3** (`Chi phí Inference AI trên mỗi yêu cầu khớp lịch - Cost/Job AI Matching`).

---

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | **Time-to-first-value (TTFV)** | < 14 ngày | 14–30 ngày | > 30 ngày | **[TB]** | Chưa có chuẩn ngành BĐS; đang đo trên 2 sàn pilot để lấy baseline chính thức trước ngày 15/11/2026; mốc > 30 ngày là ngưỡng đỏ vì chu kỳ mở bán không cho phép đối tác chờ lâu hơn. |
| 2 | **% Deal vượt qua thẩm định Security CSDL** | $\ge 80\%$ | 60–80% | < 60% | **[BM]** | Benchmark ngành B2B AI tỷ lệ deal chết ở khâu procurement/security phải < 20% (ICONIQ State of AI 2026, kiểm tra ngày 27/08/2026). |
| 3 | **Chi phí Inference AI / Booking Request (Cost/Job)** | $\le 8.500$đ | 8.500–15.000đ | > 15.000đ | **[MH] 1** | Suy từ Gross Margin mục tiêu $\ge 60\%$ và doanh thu phân bổ trên mỗi booking quota theo gói ACV chuẩn (xem chi tiết phép tính ở Phụ lục [MH] 1). |
| 4 | **POC → paid** | $\ge 50\%$ | 35–50% | < 35% | **[BM]** | Trung vị chuyển đổi POC $\rightarrow$ Paid của phần mềm AI B2B đạt ~50% năm 2026 (ICONIQ State of GTM 2026, kiểm tra ngày 27/08/2026). |
| 5 | **Chi phí triển khai & tích hợp CSDL ÷ ACV** | < 15% | 15–25% | > 25% | **[MH] 2** | Suy từ mô hình chi phí năm đầu: chi phí Onboarding vượt 25% ACV sẽ biến công ty sản phẩm thành đơn vị gia công dịch vụ và ăn mòn toàn bộ biên lãi (xem Phụ lục [MH] 2). |
| 6 | **Usage Depth** | $\ge 60\%$ | 30–60% | < 30% | **[TB]** | Chưa có chuẩn riêng cho ngành BĐS; đo 2 chu kỳ vận hành trên sàn F1 để lấy baseline chính thức trước 30/11/2026; ngưỡng < 30% sau 60 ngày là dấu hiệu churn sớm theo HANDBOOK §3.2. |
| 7 | **Gross Margin** | $\ge 60\%$ | 50–60% | < 50% | **[BM]** | Trung vị Gross Margin của công ty B2B AI-native đạt ~53% năm 2026 (ICONIQ State of AI 07/2026, kiểm tra ngày 27/08/2026); đặt mục tiêu $\ge 60\%$ để có biên an toàn. |
| 8 | **Net Revenue Retention (NRR)** | $\ge 110\%$ | 100–110% | < 100% | **[BM]** | Trung vị SaaS đạt 101% (Benchmarkit 2025, kiểm tra ngày 27/08/2026); mục tiêu $\ge 110\%$ để mở rộng doanh thu tự nhiên trong tệp khách cũ. |

---

### Phụ lục [MH] — phép tính (≥2)

#### **[MH] 1 — Chi phí Inference AI trên mỗi yêu cầu khớp lịch (Cost/Job AI Matching)**

```text
Đầu vào (từ mô hình tài chính và Cost/Job của tôi):
- Giá trị hợp đồng chuẩn (ACV) cho 1 sàn phân phối/phân khu: 240.000.000đ/năm (tương đương 20.000.000đ/tháng).
- Hạn mức thiết kế hệ thống cam kết xử lý trong gói cơ sở: 800 lượt Booking Request đạt chuẩn/tháng.
- Doanh thu phân bổ danh nghĩa cho mỗi lượt Booking Request = 20.000.000đ ÷ 800 = 25.000đ/job.
- Gross Margin mục tiêu cho phân hệ AI: GM ≥ 60%
  → Tổng giá vốn hàng bán trực tiếp (COGS) tối đa trên mỗi job = 25.000đ × (1 − 60%) = 10.000đ/job.
- Chi phí hạ tầng server, vector DB và lưu trữ phụ trợ phân bổ chiếm ~15% COGS = 1.500đ/job.
- Trần chi phí Inference AI tối đa (LLM prompt + completion + embedding) = 10.000đ − 1.500đ = 8.500đ/job.
- Nếu chi phí Inference vượt quá 15.000đ/job, Gross Margin phân hệ rớt xuống dưới 34% (ngưỡng báo động đỏ gây thâm hụt tài chính).

Kết quả ngưỡng:
→ 🟢 ≤ 8.500đ/job
→ 🟡 8.500đ – 15.000đ/job
→ 🔴 > 15.000đ/job
```

#### **[MH] 2 — Chi phí triển khai & tích hợp CSDL ÷ ACV**

```text
Đầu vào (từ mô hình tài chính năm đầu):
- ACV hợp đồng chuẩn: 240.000.000đ/năm.
- Trần COGS năm đầu để đảm bảo Gross Margin tổng thể ≥ 60%: COGS tối đa = 40% × ACV = 96.000.000đ/khách hàng.
- Chi phí API token và hạ tầng cloud ước tính cả năm chiếm: 15% ACV = 36.000.000đ.
- Ngân sách tối đa còn lại cho công tác kỹ thuật Onboarding, kết nối API/CSDL giỏ hàng và thiết lập phân quyền:
  = 96.000.000đ − 36.000.000đ = 60.000.000đ (tương đương đúng 25% ACV).
- Với đơn giá chi phí nhân sự kỹ sư triển khai nội bộ là 250.000đ/giờ công:
  - Dưới 15% ACV (≤ 36.000.000đ tương đương ≤ 144 giờ công dev): Triển khai tiêu chuẩn hóa, tự động hóa cao.
  - Từ 15% – 25% ACV (36.000.000đ – 60.000.000đ tương đương 144 – 240 giờ công dev): Chấp nhận được trong năm đầu nhưng cần theo dõi.
  - Vượt quá 25% ACV (> 60.000.000đ tương đương > 240 giờ công dev): Chi phí nhân sự ăn mòn toàn bộ biên lãi, mô hình biến thành đơn vị làm outsourcing/gia công kỹ thuật.

Kết quả ngưỡng:
→ 🟢 < 15% ACV
→ 🟡 15% – 25% ACV
→ 🔴 > 25% ACV
```

---

## Trạm 4 — 5 luật quyết định

*(Đánh dấu ⏹ cho luật dừng — có 2 luật dừng)*

1. ⏹ **NẾU** Time-to-First-Value (TTFV) > 30 ngày **TRÊN** 3 đối tác phân khu liên tiếp **VÀ** mỗi phân khu đã nạp $\ge 50$ căn hộ vào CSDL **THÌ** đóng băng toàn bộ hoạt động ký thêm hợp đồng pilot mới, tập trung toàn bộ đội ngũ kỹ thuật trong 3 tuần để chuẩn hóa luồng kết nối CSDL và bộ lọc tự động matching **KHÔNG THÌ** không được tuyển thêm nhân sự sales hoặc tiếp tục mở rộng phễu khách hàng mới khi quy trình triển khai đang bị tắc nghẽn.

2. ⏹ **NẾU** tỷ lệ deal bị kẹt hoặc từ chối ở khâu thẩm định bảo mật CSDL (Security & Procurement) > 20% **TRONG** 1 quý **THÌ** tạm dừng hoạt động demo bán hàng trong 2 tuần, hoàn thiện bộ tài liệu Evidence Pack và báo cáo kiểm toán bảo mật dữ liệu lưu trữ VPC theo tiêu chuẩn nội bộ của Chủ đầu tư **KHÔNG THÌ** không được giảm giá hợp đồng để thuyết phục đối tác bỏ qua các tiêu chí an toàn thông tin.

3. **NẾU** Chi phí Inference AI trên mỗi lượt Booking Request > 15.000đ **TRONG** 2 tuần liên tiếp **THÌ** kích hoạt ngay cơ chế Semantic Cache cho các câu hỏi thường gặp về dự án, chuyển tác vụ trích xuất tiêu chí căn hộ cơ bản sang mô hình nhỏ (Small Language Model) và giới hạn trần 10 lượt chat cho mỗi phiên đặt lịch **KHÔNG THÌ** không được tự ý tăng giá gói hợp đồng giữa chừng làm vi phạm cam kết với đối tác.

4. **NẾU** Chi phí triển khai và tích hợp CSDL > 25% ACV **TRÊN** 2 hợp đồng liên tiếp **THÌ** đóng gói và chuẩn hóa schema dữ liệu thành cổng tự phục vụ (Self-serve Connector), đồng thời ban hành điều khoản phụ phí triển khai (Setup Fee) nếu đối tác yêu cầu cấu trúc CSDL tùy biến phức tạp **KHÔNG THÌ** không được tiếp tục chào bán gói phần mềm với cam kết hỗ trợ tích hợp miễn phí mọi loại cấu trúc dữ liệu.

5. **NẾU** Mức độ sử dụng sâu (Usage Depth) của đội ngũ môi giới/điều phối viên < 30% **TRONG** 2 tuần liên tiếp (sau mốc 45 ngày kể từ ngày go-live) **THÌ** cử trực tiếp 1 Chuyên viên Hỗ trợ khách hàng (Customer Success) xuống sàn đào tạo lại nghiệp vụ và tích hợp thông báo nhắc lịch tự động qua tin nhắn Zalo ZNS cho môi giới **KHÔNG THÌ** không được chào bán thêm các phân hệ tính năng nâng cao cho sàn khi tính năng lõi chưa được đưa vào quy trình làm việc hàng ngày.
