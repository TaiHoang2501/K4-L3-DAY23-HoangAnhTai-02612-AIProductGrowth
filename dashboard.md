# OPERATING DASHBOARD — BookingBot AI Agent

**Loại mô hình:** B2B (Doanh nghiệp · Chủ đầu tư & Sàn BĐS F1 Vinhomes) · **Cập nhật:** 09/10/2026 · Hoàng Anh Tài – 2A202602612  
**NORTH STAR:** **Time-to-first-value (TTFV)** — hiện tại: Chưa có baseline (đang chạy pilot) — mục tiêu: **< 14 ngày**

---

### Đèn báo sớm (Leading — nhìn hằng ngày/tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn & Lý do | Báo trước cho |
|---|---|---|---|---|
| **Time-to-first-value (TTFV)** ⭐ | Pilot | < 14 ngày / 14–30 ngày / > 30 ngày | **[TB]** Quá 30 ngày đối tác mất kiên nhẫn bỏ rơi pilot | POC → paid (tầng O) & NRR (tầng G) |
| **% Deal duyệt Security CSDL** | 75% | $\ge 80\%$ / 60–80% / < 60% | **[BM] 27/08/2026** Ngưỡng an toàn chống gãy deal ở khâu dữ liệu | Sales cycle (tầng O) & Win rate |
| **Chi phí Inference AI / Booking (Cost/Job)** | 7.200đ | $\le 8.500$đ / 8.500–15.000đ / > 15.000đ | **[MH] 1** Bảo vệ Gross Margin $\ge 60\%$ và hạn mức ACV chuẩn | Gross Margin (tầng G) |

---

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn & Lý do | Báo trước cho |
|---|---|---|---|---|
| **POC → paid** | 50% | $\ge 50\%$ / 35–50% / < 35% | **[BM] 27/08/2026** Mốc chuyển đổi hòa vốn ngành AI B2B (ICONIQ) | Doanh thu định kỳ & NRR (tầng G) |
| **Chi phí triển khai CSDL ÷ ACV** | 18% | < 15% / 15–25% / > 25% | **[MH] 2** Ngăn chi phí dev Onboarding biến cty thành bên gia công | Gross Margin & CAC payback (tầng G) |
| **Usage Depth (Môi giới thao tác/tuần)** | 42% | $\ge 60\%$ / 30–60% / < 30% | **[TB]** Dưới 30% sau 60 ngày là tín hiệu churn sớm không thể gia hạn | NRR & Churn năm đầu (tầng G) |

---

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn & Lý do |
|---|---|---|---|
| **Gross Margin** | 58% | $\ge 60\%$ / 50–60% / < 50% | **[BM] 27/08/2026** Trung vị biên gộp công ty AI-native 2026 (ICONIQ) |
| **Net Revenue Retention (NRR)** | — | $\ge 110\%$ / 100–110% / < 100% | **[BM] 27/08/2026** Đảm bảo mở rộng doanh thu không cần bán thêm khách (Benchmarkit) |

---

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ **NẾU** TTFV > 30 ngày **TRÊN** 3 đối tác phân khu liên tiếp **VÀ** mỗi phân khu đã nạp $\ge 50$ căn vào CSDL **THÌ** đóng băng toàn bộ việc ký hợp đồng pilot mới, tập trung kỹ thuật chuẩn hóa kết nối CSDL và auto-matching trong 3 tuần **KHÔNG THÌ** không được tuyển thêm sales khi quy trình triển khai đang bị nghẽn.
2. ⏹ **NẾU** tỷ lệ deal bị kẹt ở khâu kiểm tra bảo mật CSDL > 20% **TRONG** 1 quý **THÌ** tạm dừng demo bán hàng 2 tuần, hoàn thiện hồ sơ Evidence Pack và báo cáo kiểm toán bảo mật VPC theo chuẩn của Chủ đầu tư **KHÔNG THÌ** không được giảm giá hợp đồng để thuyết phục đối tác bỏ qua tiêu chí an toàn thông tin.
3. **NẾU** Chi phí Inference AI > 15.000đ/Booking **TRONG** 2 tuần liên tiếp **THÌ** kích hoạt ngay Semantic Cache, chuyển tác vụ trích xuất tiêu chí sang mô hình nhỏ (SLM) và áp trần 10 lượt chat/phiên **KHÔNG THÌ** không tự ý tăng giá ACV giữa chu kỳ làm mất uy tín với khách hàng.
4. **NẾU** Chi phí triển khai và tích hợp CSDL > 25% ACV **TRÊN** 2 hợp đồng liên tiếp **THÌ** đóng gói schema thành cổng tự phục vụ (Self-serve Connector) và ban hành phụ phí Setup Fee cho yêu cầu tùy biến **KHÔNG THÌ** không tiếp tục chào bán gói phần mềm cam kết miễn phí tùy biến dữ liệu.
5. **NẾU** Usage Depth của đội ngũ môi giới < 30% **SAU** 45 ngày go-live **THÌ** cử trực tiếp 1 nhân sự Customer Success xuống sàn đào tạo lại luồng thao tác và tích hợp nhắc lịch tự động qua Zalo ZNS **KHÔNG THÌ** không chào bán thêm phân hệ tính năng nâng cao khi người dùng chưa thành thạo tính năng lõi.

---

### Cổng gác 90 ngày

| Ngày | Metric (đúng 1 metric) | Ngưỡng qua cổng | Bằng chứng vật lý | Nếu trượt |
|---|---|---|---|---|
| **30** | Tích hợp CSDL & TTFV phân khu pilot đầu tiên | Hoàn tất tích hợp $\ge 100$ căn và TTFV $\le 14$ ngày | Biên bản nghiệm thu kỹ thuật kết nối CSDL + Log ca xem nhà thành công có mã Deal | FIX (sửa luồng kết nối CSDL trong 30 ngày) / PIVOT nếu CĐT từ chối kết nối API |
| **60** | Usage Depth của môi giới trên 3 phân khu thử nghiệm | $\ge 60\%$ user nội bộ thao tác hàng tuần | Báo cáo trích xuất Product Analytics có xác nhận của Giám đốc Sàn giao dịch | FIX 1 lần (đào tạo lại nghiệp vụ sàn) / PIVOT luồng tương tác sang bot chat mini |
| **90** | Tỷ lệ chuyển đổi POC → Paid | $\ge 50\%$ (ít nhất 2 trên 4 phân khu pilot ký hợp đồng năm) | Hợp đồng cung cấp dịch vụ có chữ ký số đại diện Chủ đầu tư/Sàn + Biên lai chuyển khoản | PIVOT (đổi sang gói tính phí theo ca chốt Deal thành công) / KILL |

**KILL CRITERIA:** Sau 90 ngày (trước ngày 08/01/2027), nếu không có ít nhất 1 sàn phân phối/chủ đầu tư ký hợp đồng trả phí chính thức với ACV $\ge 150.000.000$đ hoặc TTFV trung bình vẫn $> 45$ ngày sau khi đã dùng 1 lần quyền FIX, dừng toàn bộ dự án để chuyển tài nguyên sang bài toán khác.

**CHƯA ĐO ĐƯỢC:** Net Revenue Retention (NRR) và Tỷ lệ tái ký hợp đồng sau 12 tháng (cần gì để đo: cần tối thiểu 1 chu kỳ vận hành 12 tháng trọn vẹn từ các hợp đồng đã ký; khi nào có số: dự kiến có số liệu thực tế vào Quý 4/2027).
