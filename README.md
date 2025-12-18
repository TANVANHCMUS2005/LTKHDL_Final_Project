## Amazon Best Sellers 2025 – Global Software Market Intelligence

### 1. Project overview & team info

**Mục tiêu dự án**  
Phân tích bộ dữ liệu *Amazon Best Sellers 2025* cho danh mục Phần mềm & Sản phẩm Kỹ thuật số nhằm:
- Hiểu cấu trúc thị trường phần mềm toàn cầu (10 quốc gia).
- Khai thác mối quan hệ giữa giá, đánh giá sao, số lượng đánh giá và thứ hạng bán chạy.
- Trả lời **6 câu hỏi nghiên cứu** xoay quanh chiến lược giá, hiệu ứng đám đông, tập trung thương hiệu, phân khúc chiến lược, mô hình cấp phép và mô hình dự đoán mức độ hài lòng.

**Thông tin nhóm**  
- Nhóm: 5 
- Thành viên: 

    23127371: Lê Võ Xuân Hưng

    23127436: Phan Hoàng Văn Nghị

    23127515: Nguyễn Tấn Văn

---

### 2. Dataset source & description

**Nguồn dữ liệu**
- Nền tảng: Kaggle  
- Tên dataset: **Amazon Best Sellers 2025**  
- URL: `https://www.kaggle.com/datasets/sanskar21072005/amazon-best-sellers-2025/data`  
- Tác giả: *sanskar21072005* (Kaggle)  
- Giấy phép: **CC0 – Public Domain** (được phép sử dụng cho mục đích giáo dục, nghiên cứu; nên trích dẫn nguồn).

**Mô tả nội dung**
- Đối tượng: Top 100 sản phẩm phần mềm & kỹ thuật số bán chạy nhất trên Amazon tại 10 thị trường:
  - Ấn Độ (IN), Hoa Kỳ (US), Canada (CA), Úc (AU), Đức (DE), Pháp (FR), Ý (IT), Tây Ban Nha (ES), Nhật (JP), Mexico (MX).
- Quy mô:
  - Số dòng ban đầu: 999
  - Số cột ban đầu: 12
- Một số trường dữ liệu quan trọng:
  - `rank`: Thứ hạng bestseller (1–100).
  - `asin`: Mã định danh sản phẩm trên Amazon.
  - `product_title`: Tên/slogan đầy đủ của sản phẩm.
  - `product_price`: Giá sản phẩm theo nội tệ (được chuẩn hoá sang USD trong notebook).
  - `product_star_rating`: Điểm đánh giá trung bình (1–5 sao).
  - `product_num_ratings`: Số lượng đánh giá của khách hàng.
  - `product_url`: Link sản phẩm trên Amazon.
  - `country`: Quốc gia / thị trường.
  - `page`: Trang phân trang khi cào dữ liệu.

**Tiền xử lý chính đã thực hiện**
- Loại bỏ các cột không hữu ích: `Unnamed: 0`, `rank_change_label`.
- Làm sạch và chuẩn hoá `product_price`:
  - Xử lý định dạng số theo từng khu vực (dấu phẩy/dấu chấm).
  - Quy đổi về **USD** theo tỷ giá cố định cho từng quốc gia.
- Chuyển kiểu dữ liệu:
  - `product_price` → `float64`.
  - `product_num_ratings` → kiểu số nguyên (`Int64`).
- Xử lý missing values:
  - Loại bỏ các dòng có thiếu ở các cột quan trọng: `product_price`, `product_star_rating`, `product_num_ratings`.
- Tạo thêm các biến/feature phục vụ phân tích nâng cao:
  - `Market_Type` (Developed vs Emerging).
  - `Rating Group`, `Rank_Group`.
  - `brand_name` (trích xuất từ `product_title`).
  - `license_model` (Lifetime vs Subscription) từ text mining.
  - Các biến log-transform (`log_price`, `log_reviews`) và biến phục vụ mô hình học máy (`title_length`, `is_high_satisfaction`).

---

### 3. Research questions

Các câu hỏi nghiên cứu chính được triển khai trong notebook:

1. **Regional Pricing Strategy**  
   - Liệu có sự khác biệt đáng kể về **mức giá niêm yết** và **hành vi đánh giá sản phẩm** giữa các quốc gia thuộc nhóm thị trường Phát triển (*Developed*) và thị trường Mới nổi (*Emerging*) hay không?

2. **The "Social Proof" Paradox**  
   - Yếu tố nào quan trọng hơn để giúp sản phẩm lọt vào Top Bestseller:
     - **Chất lượng nội tại** (điểm rating cao)  
     - hay **hiệu ứng đám đông** (số lượng đánh giá rất lớn)?

3. **Market Concentration & Local Champions**  
   - Mức độ tập trung thị trường của các thương hiệu phần mềm thay đổi như thế nào giữa các quốc gia?  
   - Quốc gia nào bị thống trị bởi các “ông lớn” toàn cầu, và quốc gia nào chứng kiến sự trỗi dậy của thương hiệu nội địa?

4. **Unsupervised Strategic Segmentation**  
   - Có thể tự động nhóm các sản phẩm thành các phân khúc chiến lược (ví dụ: *Premium Niche*, *Mass Market (Cheap)*, *Low Quality / Risk*, *Market Leaders*) dựa trên:
     - Giá (`product_price`),  
     - Chất lượng (`product_star_rating`),  
     - Độ phổ biến (`product_num_ratings`),  
     mà **không cần nhãn sẵn** hay không?

5. **Subscription vs Lifetime License**  
   - Liệu có sự khác biệt có ý nghĩa thống kê về **mức độ hài lòng của khách hàng** (`product_star_rating`) và **độ phổ biến** (`rank`) giữa các sản phẩm phần mềm **Thuê bao (Subscription)** và **Mua đứt/Vĩnh viễn (Lifetime/Perpetual)** hay không?

6. **Predicting High Satisfaction**  
   - Liệu chúng ta có thể dự đoán một sản phẩm có **“Hài lòng cao”** (rating > 4.5) dựa trên các đặc điểm quan sát được như **giá**, **độ dài tiêu đề** và **quốc gia**, sử dụng mô hình học máy (Logistic Regression, Random Forest)?

---

### 4. Key findings summary

Tóm tắt các phát hiện quan trọng tương ứng với từng câu hỏi:

- **(Q1) Giá & Rating: Developed vs Emerging Markets**
  - Phân nhóm `Market_Type` và kiểm định **Mann-Whitney U** cho thấy:
    - Có **khác biệt có ý nghĩa thống kê** về phân phối **giá** giữa thị trường phát triển và mới nổi (p-value rất nhỏ).
    - Rating giữa hai nhóm cũng khác biệt có ý nghĩa.
  - Thị trường phát triển có mặt bằng giá cao hơn và dải giá rộng hơn, ủng hộ chiến lược **regional pricing** (phân biệt giá theo khu vực).

- **(Q2) Social Proof thắng Chất lượng**
  - Tương quan Spearman:
    - `Rating vs Rank`: ρ ≈ -0.087 (rất yếu).  
    - `Num Ratings vs Rank`: ρ ≈ -0.202 (yếu–trung bình).
  - Kết luận: **“Hiệu ứng đám đông” (số lượng đánh giá)** quan trọng hơn đáng kể so với **điểm số rating** trong việc giúp sản phẩm đạt thứ hạng bestseller tốt.

- **(Q3) Tập trung thương hiệu & HHI**
  - Từ biến `brand_name`, tính **thị phần theo quốc gia** và chỉ số **HHI**:
    - Mexico (MX) có HHI ~ 1831: thị trường tập trung vừa, bị chi phối bởi một số thương hiệu lớn.
    - US, DE có HHI thấp (< 900): thị trường cạnh tranh cao, không thương hiệu nào “một mình một chợ”.
  - Các thương hiệu nội địa như **Quick Heal, K7 Security (IN)**, **SourceNext (JP)**, **TurboTax (US)** cho thấy khả năng cạnh tranh mạnh tại “sân nhà”.

- **(Q4) 4 phân khúc chiến lược (K-Means, k=4)**
  - Dựa trên `log_price`, `log_reviews`, `product_star_rating`, mô hình K-Means phát hiện 4 phân khúc:
    - **Mass Market (Cheap)**: Giá thấp, review rất nhiều, rating khá (~4.1).
    - **Low Quality / Risk**: Giá cao nhất nhưng rating thấp nhất (~3.6) → nhóm rủi ro.
    - **Premium Niche**: Giá cao, review nhiều, rating tốt (~4.3).
    - **Market Leaders**: Rating cao nhất (~4.6) nhưng review còn ít → các “ngôi sao mới nổi”.
  - Đây là bản đồ hữu ích để định vị sản phẩm và lựa chọn chiến lược (gia nhập mass-market hay nhắm niche premium).

- **(Q5) Subscription vs Lifetime: Ai được yêu thích hơn?**
  - Sau khi gán nhãn `license_model` từ `product_title` và lọc dữ liệu “rác”:
    - Nhóm **Subscription** có rating trung bình ≈ **4.20**,  
    - Nhóm **Lifetime** ≈ **3.99**.
  - Kiểm định **T-test độc lập** cho rating:
    - P-value ≈ 6.59 × 10⁻⁶  < 0.05 → **chênh lệch có ý nghĩa thống kê**.
  - Kết luận: Người dùng **hài lòng hơn với mô hình thuê bao** (cập nhật liên tục, dịch vụ đi kèm) so với mua đứt, trái với giả thuyết “subscription fatigue”.

- **(Q6) Mô hình dự đoán High Satisfaction (ML)**
  - Biến mục tiêu: `is_high_satisfaction` = 1 nếu rating > 4.5.
  - Mô hình:
    - **Logistic Regression (class_weight='balanced')**: Accuracy ~ 66.7%, AUC ~ 0.75.
    - **Random Forest (class_weight='balanced')**: Accuracy ~ 82.5%, AUC ~ 0.79.
  - Feature importance cho thấy:
    - `product_price` là driver quan trọng nhất,
    - tiếp theo là `title_length` và một số dummy của `country`.
  - Kết luận: Chỉ với thông tin bề mặt (giá, tiêu đề, quốc gia), ta đã có thể dự đoán mức hài lòng cao với độ chính xác khoảng **80%**, phần sai số còn lại đến từ các yếu tố nội tại chưa được quan sát.

Ngoài ra, EDA cho thấy:
- Giá phân phối lệch phải mạnh, tồn tại nhiều outliers giá cao.  
- Rating nhìn chung cao (~4.1/5) nhưng số lượng review phân bố rất lệch (một số sản phẩm “bùng nổ” review, phần lớn còn lại ở mức vừa phải).

---

### 5. File structure explanation

Cấu trúc thư mục chính của project:

```text
LTKHDL_Final_Project/
├── Final_project.ipynb        # Notebook chính: EDA, tiền xử lý, phân tích Q1–Q6, mô hình ML
├── README.md                  # File mô tả project
├── .gitignore                 
└── data/
    └── raw/
        └── Amazon_bestsellers_items_2025.csv  # File dữ liệu gốc tải từ Kaggle
```

### 6. How to run

#### 6.1. Yêu cầu môi trường

- Python **3.8+** .
- Cài `pip` (trình quản lý gói Python).
- Cài `git` nếu muốn clone/pull từ GitHub.

#### 6.2. Thiết lập ban đầu

1. **Clone repo từ GitHub** (hoặc tải zip về và giải nén):

```bash
git clone https://github.com/TANVANHCMUS2005/LTKHDL_Final_Project.git
cd LTKHDL_Final_Project
```

2. (Tuỳ chọn) Tạo môi trường ảo:

```bash
python -m venv venv
venv\Scripts\activate   # Windows
# hoặc: source venv/bin/activate  # macOS / Linux
```

3. Cài các thư viện cần thiết:

```bash
pip install -r requirements.txt
```

> Nếu chưa có `requirements.txt`, bạn có thể cài thủ công các gói được liệt kê trong phần Dependencies bên dưới.

#### 6.3. Chạy notebook

1. Khởi động Jupyter:

```bash
jupyter notebook
```

2. Trong giao diện Jupyter:
   - Mở file `Final_project.ipynb`.
   - Chạy lần lượt các cell từ trên xuống dưới:
     - Đảm bảo path tới file CSV `data/raw/Amazon_bestsellers_items_2025.csv` đúng như trong project.

3. Kiểm tra lại:
   - Nếu gặp lỗi `FileNotFoundError`, hãy kiểm tra:
     - Bạn đang ở đúng thư mục gốc của project khi mở Jupyter.
     - Thư mục `data/raw/` có chứa file CSV đúng tên.

---

### 7. Dependencies

Các thư viện Python chính được sử dụng trong notebook:

- **Xử lý & phân tích dữ liệu**
  - `pandas`
  - `numpy`

- **Trực quan hoá**
  - `matplotlib`
  - `seaborn`

- **Thống kê & kiểm định**
  - `scipy` (đặc biệt là `scipy.stats` với Mann-Whitney U test, T-test, v.v.)

- **Học máy & tiền xử lý**
  - `scikit-learn`
    - `train_test_split`
    - `StandardScaler`, `OneHotEncoder`
    - `SimpleImputer`, `ColumnTransformer`, `Pipeline`
    - `LogisticRegression`, `RandomForestClassifier`
    - `KMeans`
    - Các metric: `accuracy_score`, `classification_report`, `roc_curve`, `auc`

- **Môi trường & notebook**
  - `jupyter` hoặc `jupyterlab`
