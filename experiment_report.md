# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** Nguyễn Trọng Thiên Khôi
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Kết quả đúng, Laptop là sản phẩm có giá cao nhất sau khi lọc dữ liệu hợp lệ |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Kết quả sai hoàn toàn — Agent bị đánh lừa bởi dữ liệu rác chứa giá trị bất thường |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng `garbage_data.csv`, Agent đã đưa ra kết quả sai nghiêm trọng vì dữ liệu đầu vào chứa nhiều lỗi chất lượng:

- **Duplicate IDs:** ID `1` xuất hiện hai lần (Laptop và Banana), gây nhầm lẫn khi truy vấn theo khóa.
- **Wrong data types:** Cột `price` có giá trị `"ten dollars"` (chuỗi ký tự thay vì số), khiến so sánh giá trị bị lỗi hoặc bỏ qua.
- **Outliers (giá trị bất thường):** Sản phẩm "Nuclear Reactor" có giá `999999` — một outlier cực đoan. Vì không có bước lọc, Agent coi đây là sản phẩm có giá trị nhất và trả về kết quả này.
- **Null values:** ID và category bị thiếu ở dòng "Ghost Item", dữ liệu này lẽ ra phải bị loại bỏ.

Những vấn đề trên cho thấy nếu không có pipeline kiểm soát chất lượng dữ liệu, AI Agent sẽ xử lý toàn bộ dữ liệu rác như dữ liệu hợp lệ, dẫn đến quyết định sai lệch.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý.

Dù prompt được viết tốt đến đâu, nếu dữ liệu đầu vào chứa lỗi (outliers, null, sai kiểu dữ liệu, trùng lặp), AI Agent vẫn sẽ đưa ra kết quả sai. Thí nghiệm này chứng minh rằng ETL pipeline và bước kiểm soát chất lượng dữ liệu là nền tảng không thể thiếu trước khi đưa dữ liệu vào bất kỳ hệ thống AI nào. **Garbage in, garbage out** — chất lượng đầu ra phụ thuộc hoàn toàn vào chất lượng đầu vào.
