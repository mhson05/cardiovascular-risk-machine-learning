# Bài Tập Lớn Học Máy (Machine Learning) - PTIT

## Đề tài: Dự đoán & Đánh giá Nguy cơ Bệnh Tim Mạch (Healthcare and Patient Risk Analysis)

## 1. Cấu trúc thư mục dự án

```text
cardiovascular-risk-ml-ptit/
│
├── .gitignore
├── healthcare_cvd_risk_pipeline.ipynb   # File Notebook chính, chạy end-to-end, nhúng sẵn kết quả
├── requirements.txt                     # Danh sách thư viện và phiên bản ghim ổn định
├── data/
    └── raw/
        ├── framingham.csv               # Tập A: 4.240 bệnh nhân, Mỹ (Tỷ lệ bệnh 15.19%)
        └── cardio_train.csv             # Tập B: 70.000 mẫu (68.619 sạch), Đông Âu (Tỷ lệ bệnh 49.47%)
```

---

## 2. Nguồn gốc & Thu thập Dữ liệu (Data Acquisition)

Dự án thu thập và đối chiếu hai tập dữ liệu độc lập nhằm đáp ứng yêu cầu nghiên cứu đa nguồn và đánh giá trôi dạt phân phối (Dataset Shift):

| Tập dữ liệu             | Nguồn / Xuất xứ                  | Thiết kế                             | Quy mô     | Nhãn dự đoán                                         |
| :---------------------- | :------------------------------- | :----------------------------------- | :--------- | :--------------------------------------------------- |
| **Tập A: Framingham**   | NHLBI & ĐH Boston (Kaggle)       | Thuần tập dài hạn (Cohort)           | 4.240 mẫu  | `TenYearCHD` (Biến cố tim mạch 10 năm, 15.19% dương) |
| **Tập B: Cardio Train** | Hồ sơ khám bệnh Đông Âu (Kaggle) | Cắt ngang lâm sàng (Cross-sectional) | 70.000 mẫu | `cardio` (Bệnh tim hiện mắc, 49.47% dương)           |

- **Đặc trưng chung:** Đồng bộ về 8 chỉ số lâm sàng (Tuổi, Giới tính, BMI, Huyết áp tâm thu/tâm trương, Cholesterol, Glucose, Hút thuốc).
- **Lưu trữ:** Đặt tại `data/raw/` dưới định dạng CSV gốc.

---

## 3. Hướng dẫn cài đặt & Thực thi nhanh với `uv`

### Bước 1: Cài đặt `uv` (nếu máy chưa có)

- **Windows (PowerShell):**
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
- **macOS / Linux:**
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

---

### Bước 2: Đồng bộ môi trường và cài đặt thư viện

Mở terminal tại thư mục gốc của dự án và chạy:

```bash
uv sync
```

---

### Bước 3: Chạy mã nguồn

Bạn có thể chạy dự án bằng một trong hai cách:

1. **Khởi động Jupyter trực tiếp qua `uv`:**

   ```bash
   uv run jupyter lab
   # hoặc
   uv run jupyter notebook
   ```

2. **Chạy qua VS Code:**
   - Mở file [`healthcare_cvd_risk_pipeline.ipynb`](healthcare_cvd_risk_pipeline.ipynb).
   - Nhìn góc trên cùng bên phải màn hình notebook, bấm **Select Kernel** -> chọn **Python Environments...** -> trỏ vào **`.venv`** (Python 3.11).
   - Bấm **Run All** để thực thi toàn bộ pipeline.
