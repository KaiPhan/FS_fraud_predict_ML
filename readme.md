# BUILDING AN INTERPRETABLE ENSEMBLE MODEL FOR PREDICTING FRAUDULENT FINANCIAL STATMENTS - APPLYING FOR VIETNAMESE MARKET 
# XÂY DỰNG MÔ HÌNH KẾT HỢP CÁC THUẬT TOÁN HỌC MÁY ĐỂ DỰ ĐOÁN BÁO CÁO TÀI CHÍNH GIAN LẬN - ÁP DỤNG CHO THỊ TRƯỜNG CHỨNG KHOÁN VIỆT NAM
<details> 
<summary>Mục lục</summary>

  - [1. Tổng quan](#1-tổng-quan)
    - [Giới thiệu](#giới-thiệu)
    - [Cấu trúc project](#cấu-trúc-project)
  - [2. Cài đặt môi trường và thư viện cần thiết](#2-cài-đặt-môi-trường-và-thư-viện-cần-thiết)
  - [3. Đánh giá](#3-đánh-giá)
  - [4. Tác giả](#4-tác-giả)
  - [5. Tài liệu tham khảo](#5-tài-liệu-tham-khảo)

</details>

## 1. Tổng quan
### Giới thiệu
#### Bài toán đặt ra
Báo cáo tài chính là công cụ thể hiện tình hình tài chính và kết quả hoạt động kinh doanh của doanh nghiệp. Do đó, vấn đề liên quan đến sự minh bạch và trung thực của báo cáo tài chính của các công ty niêm yết trên thị trường chứng khoán luôn được quan tâm hàng đầu. Đáng chú ý, những vụ gian lận báo cáo tài chính sau nhiều năm mới bị phát hiện, gây ra tâm lý nghi ngờ cho nhà đầu tư, ảnh hưởng tới hoạt động của thị trường. Các gian lận chậm bị phát hiện đã có tác động tiêu cực đến việc ra quyết định của các nhà đầu tư. Điều này có thể dẫn đến việc dòng tiền lưu thông không hiệu quả, gây ra nhiều hệ lụy cho cả nền kinh tế nếu không có những biện pháp khắc phục tình trạng này.

Mục đích của đề tài là cung cấp một công cụ hiệu quả hơn để dự đoán khả năng gian lận báo cáo tài chính, định hướng kiểm tra các khoản mục có rủi ro gian lận trên báo cáo tài chính đã được xác định có khả năng gian lận cao nhằm tăng tính hữu hiệu và hiệu quả trong công việc của các kiểm toán viên độc lập. Ngoài ra, các nhà đầu tư, các cơ quan quản lý cũng có thể sử dụng công cụ này để đánh giá lại về báo cáo tài chính sau kiểm toán để đưa ra các quyết định phù hợp.


#### Tập dữ liệu 
Tập dữ liệu được sử dụng trong nghiên cứu này là các báo cáo tài chính chưa được kiểm toán từ năm 2010 đến năm 2019, được cung cấp bởi FiinGroup. Tập dữ liệu bao gồm 1506 công ty phi tài chính trên các sàn giao dịch HNX, HoSE và UpCOM với 189 chỉ tiêu tài chính. 

Sau khi loại bỏ các bản ghi có giá trị bị thiếu hoặc các bản ghi không tính đoán được chỉ số Beneish M-Score (do thiếu dữ liệu của năm liền trước), tập dữ liệu bao gồm 4883 dòng và 190 cột (bao gồm 189 chỉ tiêu tài chính và 1 cột nhãn gian lận hoặc không gian lận ). Một công ty có thể gian lận nếu có Z-Score ≤ 5,85 và M-Score > -2,22. Cuối cùng, tác giả có 858 báo cáo tài chính được dán nhãn gian lận và 4025 không gian lận.

#### Quy trình thực hiện nghiên cứu
Quy trình thực hiện nghiên cứu của tác giả, theo đó chi tiết các bước sẽ được trình bày ở phần tiếp theo.
![Sơ đồ mô hình nghiên cứu](/overall_process.PNG)


## 2. Cài đặt môi trường và thư viện cần thiết
Project này được cài đặt trên môi trưởng ảo được tạo bởi `miniconda`. Lựa chọn phiên bản phù hợp và cài đặt `miniconda` tại [link](https://docs.conda.io/en/latest/miniconda.html).

Khởi tạo môi trường ảo sử dụng `miniconda` với phiên bản python là 3.7:
> `conda create --name <ml-project> python==3.7`

Các thư viện sử dụng trong project này được liệt kê ở file [requirements.txt](#requirements.txt), bao gồm:
- `numpy==1.19.5`: xử lý dữ liệu dạng ma trận số
- `pandas==1.1.5`: xử lý dữ liệu dạng bảng
- `scikit_learn==1.0.1`: xây dựng mô hình K-Nearest Neighbors, Decision Tree, Random Forest, Linear Regression
- `xgboost ==0.90`: xây dựng mô hình XGBoost.
- `lightgbm ==2.2.3`: xây dựng mô hình LightGBM.
- `shap ==0.40.0`: thư viện phương pháp giải thích các mô hình học máy.

Để cài đặt các thư viện trên, thực hiện lệnh sau:
>`pip install -r requirements.txt`

