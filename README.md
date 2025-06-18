
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

| Mô hình         | All Features     | Best Features    |
|----------------|------------------|------------------|
| Random Forest  | RMSE tương đương | RMSE tương đương |
| XGBoost        | **Tốt hơn**      | Kém hơn          |
| LightGBM       | Kém hơn          | **Tốt hơn**      |

- **XGBoost** và **LightGBM** được chọn để huấn luyện lại trên toàn bộ dữ liệu.
- Sử dụng hai mô hình này để dự đoán giá xe trên bộ dữ liệu thực tế (giá bị ẩn).
- **Kaggle đánh giá LGBM cao hơn XGBoost** trên tập test.

---

