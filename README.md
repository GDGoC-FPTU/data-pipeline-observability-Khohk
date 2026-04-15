[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574078&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** khoithien1955@gmail.com
**Name:** Nguyễn Trọng Thiên Khôi

---

## Mo ta

Bài lab xây dựng một ETL Pipeline hoàn chỉnh để trích xuất dữ liệu từ `raw_data.json`, kiểm tra và làm sạch dữ liệu (loại bỏ các bản ghi có giá <= 0 hoặc thiếu category), tính giá sau giảm 10%, rồi lưu kết quả vào `processed_data.csv`. Sau đó chạy thí nghiệm so sánh phản hồi của AI Agent khi nhận dữ liệu sạch (`processed_data.csv`) và dữ liệu rác (`garbage_data.csv`) để minh hoạ tầm quan trọng của chất lượng dữ liệu.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao garbage data
python generate_garbage.py

# Buoc 2: Chay thi nghiem so sanh Clean vs Garbage data
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- **Tổng số bản ghi đầu vào:** 5 (từ `raw_data.json`)
- **Bản ghi hợp lệ (kept):** 3 — Laptop ($1200), Chair ($45), Monitor ($300)
- **Bản ghi bị loại (dropped):** 2
  - ID 3 (Mystery Box): Price <= 0
  - ID 4 (Phone): Missing Category
- **Output:** `processed_data.csv` với 3 bản ghi, đã tính giá giảm 10%

**Kết quả thí nghiệm Agent Simulation:**
- Clean Data → Agent trả lời đúng: `"the best choice is Laptop at $1200"`
- Garbage Data → Agent bị đánh lừa: `"the best choice is Nuclear Reactor at $999999"`
