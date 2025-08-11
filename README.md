
# 🚗 ACT61 MFE - Car Price Prediction Competition

**🔗 Link cuộc thi**: [Kaggle Competition Page](https://www.kaggle.com/competitions/act61-mfe-prediction-competition/overview)

## 🎯 Mục tiêu
Xây dựng mô hình học máy để **dự báo giá xe ô tô** dựa trên các đặc trưng đầu vào.  
**Metric đánh giá:** Root Mean Squared Error (RMSE)

## 🧠 Mô hình sử dụng
- Random Forest (RF)  
- XGBoost (XGB)  
- LightGBM (LGBM)

---

## 🔁 Quy trình thực hiện

### 1. Data Preprocessing
- `name`: Trích xuất tên hãng xe từ chuỗi.
- `mileage`: Chuẩn hóa đơn vị (kmpl hoặc km/kg).
- `torque`: Trích giá trị từ chuỗi văn bản và quy đổi đơn vị về Nm.

### 2. Exploratory Data Analysis (EDA)
- Phân tích đơn biến và hai biến.
- Vẽ biểu đồ: histogram, boxplot, scatter plot.
- Heatmap tương quan.
- Trực quan hóa dữ liệu bằng t-SNE.

### 3. Modeling
- Chia dữ liệu thành **train/test** theo tỷ lệ **80:20**.
- Impute giá trị thiếu (đặc biệt đối với Random Forest).
- Encoding:
  - `OneHotEncoder` cho các biến categorical thông thường.
  - `TargetEncoderSmooth` cho `name` và `owner` (do chứa các giá trị hiếm).
- Feature Selection:
  - Dùng Backward Feature Elimination để chọn tập feature tối ưu.
- Hyperparameter Tuning:
  - Dùng Optuna để tìm tham số tối ưu.
- Mỗi mô hình được huấn luyện theo 2 cách:
  - Với **toàn bộ feature**
  - Với **tập feature tối ưu (best features)**

### 4. Model Evaluation
- Dự báo trên tập test và tính RMSE.
- Vẽ biểu đồ:
  - Feature importance
  - SHAP values

---

## ✅ Kết quả chính
- Kết quả RMSE trên tập test

| Mô hình         | All Features     | Best Features    |
|----------------|------------------|------------------|
| Random Forest  | 126597           |     125442       |
| XGBoost        | 112356           | 137937           |
| LightGBM       | 109571           | 104126          |

- **LightGBM** hiệu quả hơn khi train với best features, **XGBoost** hiệu quả hơn khi train với all features.
- **LightGBM** cho RMSE nhỏ nhất ở cả 2 trường hợp.
- **XGBoost** và **LightGBM** được chọn để huấn luyện lại trên toàn bộ dữ liệu.
- Sử dụng hai mô hình này để dự đoán giá xe trên bộ dữ liệu thực tế (giá xe bị ẩn đi).
- **Kaggle đánh giá LGBM (RMSE = 116121) cao hơn XGBoost (RMSE = 132651)**.
<img width="1056" height="450" alt="image" src="https://github.com/user-attachments/assets/40df026d-0548-4564-851e-4846a416b9f7" />


---

