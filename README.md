# I. Lên ý tưởng và Mục tiêu

## 1.1 Vấn đề cốt lõi (The Problem)

Thị trường tài chính (**cổ phiếu, ngoại hối**) không chỉ phản ứng với các dữ liệu kinh tế (**GDP, CPI, Retail Sales, PMI / ISM**) mà còn phản ứng với **sự bất ngờ** của dữ liệu đó so với **kỳ vọng** (Forecast).

## 1.2 Mục tiêu Báo cáo (The Goal)

Chứng minh mối quan hệ nhân quả: Phân tích **sự bất ngờ** của 4 chỉ số vĩ mô Mỹ (**GDP, CPI, PMI, Retail Sales**) và **tác động** của nó lên 3 tài sản thị trường quan trọng (**S&P 500, DXY, USD/VND**) trong 24 tháng qua.

## 1.3 Khán giả mục tiêu

Nhà đầu tư cá nhân, Chuyên viên phân tích, hoặc Quản lý quỹ muốn hiểu rõ **cách tin tức vĩ mô biến thành hành động giá**.

---

# II. Chiến lược Dữ liệu (Data Strategy)

Khung thời gian được chuẩn hóa là **24 tháng (2 năm)** để đảm bảo tính **đồng bộ** và **tin cậy** cho phần **phân tích tương quan**.
## 2.1 Dữ liệu vĩ mô
Được cào trực tiếp trên trang Investing dùng thư viện selenium của Python.
Mục đích: Đo lường mức độ "Bất ngờ" của dữ liệu kinh tế Mỹ.
### 📁 Cấu trúc file dữ liệu vĩ mô(macro_events_summary_history.csv)
| Chỉ số (Indicators) | Giá trị Phân tích | Công thức Tính toán|
| :--- | :--- | :--- |
| **GDP, CPI, PMI, Retail Sales** | Actual, Forecast, Deviation, và Impact (Trend) | **Deviation** = Actual - Forecast <br> **Impact (Trend)**: Positive (Actual > Forecast) \| Negative (Actual < Forecast) |
## 2.2 Dữ liệu Thị trường
Sử dụng thư viện yfinance trong Python thay vì lấy dữ liệu trực tiếp từ trang Investing.com là do tính tự động hóa và hiệu suất do Yahoo Finance lấy dữ liệu trực tiếp từ các sàn giao dịch lớn, trong khi Investing.com có thể tổng hợp từ nhiều nguồn khác nhau cộng với việc lấy dữ liệu trên trang Investing rất chậm. Phải sử dụng Selenium để điều hướng, click, và chờ tải dữ liệu.
Mục đích: Theo dõi xu hướng giá và tính toán tương quan.
### 📁 Cấu trúc file dữ liệu thị trường(market_trends_history_24m.csv)
| Chỉ số (Indicators) |Phân tích được |
| :--- | :--- |
| **S&P 500 (^GSPC)** | Đo lường Tâm lý rủi ro toàn cầu|
| **DXY Index (DX-Y.NYB)** | Đo lường Sức mạnh của Đồng Đô la Mỹ (USD)|
| **USD/VND Rate (VND=X)** |Đo lường Tỷ giá hối đoái|

