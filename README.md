# Hướng dẫn chạy code 
Dự án sử dụng **Python + Selenium** để crawl dữ liệu kinh tế/market. Làm theo các bước dưới đây để chạy mã thành công.

---

## ✅ 1. Cài đặt Python & Thư viện

### 1.1. Cài Python 3.x  
Tải tại: https://www.python.org/downloads/

#### 1.2. Cài các thư viện cần thiết
 ```pip install -r requirements.txt ```
 
- Nếu chưa có requirements.txt

 ```pip freeze > requirements.txt ```
 ## Cài đặt WebDriver (ChromeDriver)
 Selenium cần WebDriver để điều khiển trình duyệt.
 
 1  Kiểm tra phiên bản Chrome → Settings → About Chrome (Ví dụ: Version 121.x)

 2 Tải ChromeDriver tương ứng https://googlechromelabs.github.io/chrome-for-testing/#stable

 3 Đặt WebDriver vào thư mục dự án
project/
  ├── crawl.py
  ├── chromedriver.exe
  ├── requirements.txt
# Tóm tắt 
Chủ đề: Định lượng sự "Bất ngờ" Vĩ mô và Hệ quả Liên thị trường

- Cơ chế Phản ứng Ngược (Good News is Bad News): Phân tích 24 tháng qua cho thấy thị trường Mỹ đang vận hành trong trạng thái "nhạy cảm lãi suất" cực độ. Các dữ liệu kinh tế tích cực (Positive Surprise) thường dẫn đến phản ứng tiêu cực của S&P 500 (trung bình -0.07%) do lo ngại về lạm phát dai dẳng và kịch bản "Lãi suất cao hơn trong thời gian dài hơn" (Higher for longer).
- Áp lực Tiêu cực Chiếm ưu thế: Với tỷ lệ 56.25% Negative Surprise, nền kinh tế Mỹ đang bộc lộ những dấu hiệu hụt hơi so với kỳ vọng lạc quan của giới phân tích, đặc biệt là ở mảng Tiêu dùng (Retail Sales) và Sản xuất (PMI).

- Ma trận Rủi ro Vĩ mô: CPI tiếp tục là biến số gây sốc lớn nhất và dẫn dắt tâm lý rủi ro (Risk Appetite) toàn cầu. Trong khi đó, GDP duy trì sự ổn định, cho thấy sự "bất ngờ" chủ yếu nằm ở các yếu tố chi phí và tiêu dùng hơn là tăng trưởng tổng thể.

- Điểm bất thường USD/VND - DXY: Hệ số tương quan -0.52 cho thấy sự phân hóa rõ rệt giữa bối cảnh quốc tế và nội địa. Trong khi DXY có xu hướng hạ nhiệt, tỷ giá USD/VND lại chịu áp lực tăng từ các yếu tố nội tại (chênh lệch lãi suất âm, áp lực khối ngoại), đòi hỏi một chiến lược quản trị rủi ro tỷ giá chủ động hơn từ phía NHNN.

- Khuyến nghị Chiến lược: Nhà đầu tư cần đặc biệt cẩn trọng trong các tuần công bố CPI và báo cáo Việc làm, đồng thời ưu tiên các nhóm cổ phiếu có bảng cân đối kế toán mạnh để chống chọi với biến động liên thị trường phức tạp trong nửa đầu năm 2026.
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
---
# 📄 Power BI Report (PDF Preview)

📄 [Xem báo cáo PR ASEAN (PDF)](reports/PR_ASEAN.pdf)


# III. Tổng hợp các Insight
## 3.1 Cơ chế phản ứng ngược của thị trường trong kỷ nguyên lãi suất cao
Quan sát Định lượng: Phản ứng trung bình của S&P 500, DXY là $-0.1\%$ (khi tin xấu) và $-0.07\%$ (khi tin tốt).
### 3.1.1 Một số lý do thường được các phân tích & nhà đầu tư nhìn nhận:

-Dữ liệu quá tốt → lo lãi suất cao / Fed thắt chặt hơn: Nếu tăng trưởng/lao động nóng lên, nhà đầu tư lo ngại lạm phát và kỳ vọng Fed sẽ giữ lãi suất cao hoặc tăng — bất lợi cho cổ phiếu.

-Định giá cổ phiếu đã cao — tin tốt không đủ bù rủi ro: Khi thị trường đã “đánh giá cao” nhiều kỳ vọng sẵn, một dữ liệu tốt cũng dễ bị xem là “không quá bất ngờ” → không bật giá mạnh.

-Tâm lý “risk-off”, lo ngại về kinh tế vĩ mô chung — lạm phát, nợ, bong bóng công nghệ / quá nhiệt: Những nỗi lo này đôi khi lấn át dữ liệu tích cực, khiến thị trường phản ứng tiêu cực hơn.

-Tin tốt bị “priced-in” trước — market đã phản ứng trước đó: Khi tin tốt đã được phản ánh vào giá từ trước (kỳ vọng), khi công bố thật — thị trường có thể “ngưng bật”, hoặc thậm chí bán để chốt lời.
### 3.1.2 Ví dụ & xu hướng tại thị trường Mỹ 2024–2025
- Trong năm 2025, mặc dù nhiều kỳ vọng từ việc hạ lãi suất hoặc chính sách hỗ trợ kinh tế, thị trường Mỹ vẫn bị đánh giá có biến động mạnh, với rủi ro từ định giá cao, khả năng suy yếu của nền kinh tế và áp lực từ lạm phát — khiến cổ phiếu dễ bị “nhạy cảm” hơn với tin tức vĩ mô, dù tin tốt. https://vn.investing.com/news/world-news/chuyen-gia-canh-bao-chung-khoan-my-co-the-giam-35-trong-nua-dau-nam-2025-2277679

- Một bài viết gần đây phân tích rằng sau báo cáo việc làm mạnh (non-farm payrolls tốt hơn dự báo), thay vì thị trường tăng, nhiều chỉ số chính như S&P 500, Dow Jones Industrial Average và Nasdaq Composite lại “lực đỡ không đủ” và giảm điểm — lý do chính được nêu là dữ liệu tốt khiến nhà đầu tư lo sợ lãi suất sẽ được giữ cao hơn hoặc Fed sẽ thắt chặt.     https://economictimes.indiatimes.com/news/international/us/why-are-markets-tanking-in-spite-of-a-strong-jobs-report-heres-the-main-reason-and-it-is-worrying/articleshow/117128480.cms.com

- Có những phiên dù tin vĩ mô — hay dữ liệu doanh nghiệp cá biệt — cho thấy tín hiệu khả quan, nhưng do áp lực thị trường rộng hơn (lo ngại lãi suất, định giá cao, tâm lý “risk-off”), giá cổ phiếu vẫn giảm hoặc dao động mạnh, thay vì bật lên mạnh như trước. (Đây là hệ quả của việc thị trường Mỹ — giống nhiều thị trường phát triển khác — đôi khi phản ứng mạnh hơn với kỳ vọng về chính sách lãi suất & rủi ro vĩ mô hơn là dữ liệu doanh nghiệp riêng lẻ.)
### 3.1.2 Điểm yếu của số liệu
- Thiếu yếu tố kỳ vọng chính sách (lãi suất), định giá thị trường, sentiment/risk appetite vào mô hình hoặc bảng phân tích. Vì vậy việc phân tích cho một thị trường như Mỹ — việc dùng “positive surprise → kỳ vọng thị trường tăng” không phải lúc nào cũng đúng.

- Chưa đánh giá được bối cảnh vĩ mô & định giá hiện tại, nên việc dự đoán chỉ hoàn toàn là đựa vào số liệu.

*Vì vậy xảy ra hiện tượng hiếm gặp là S&P 500 và DXY cùng giảm                  
Thông thường:

-S&P 500 tăng → DXY giảm (nhà đầu tư rời bỏ USD để tìm rủi ro cao)

-S&P 500 giảm → DXY tăng (nhà đầu tư chạy về USD – nơi trú ẩn an toàn)  

Khi nào mô hình “S&P 500 ↓ & DXY ↓” xuất hiện trong lịch sử? 
| Giai đoạn |Điều gì xảy ra |
| :--- | :--- |
| **2020 – COVID crash (tháng 3/2020)** |Chứng khoán giảm mạnh, USD giảm do Fed nới lỏng khẩn cấp|
| **Cuối 2007 – đầu 2008 (khủng hoảng tài chính)** | Kinh tế suy yếu, Fed cắt lãi suất → USD yếu & chứng khoán giảm|
| **2023 – kỳ vọng Fed pivot** |Chứng khoán điều chỉnh, USD giảm theo lãi suất danh nghĩa giảm|

## 3.2 Tần suất bất ngờ Positive vs Negative Surprise
Trong giai đoạn 24 tháng, tỷ lệ các bất ngờ tiêu cực (56.25%) xuất hiện nhiều hơn đáng kể so với bất ngờ tích cực (43.75%). Mức chênh lệch này cho thấy thị trường liên tục chứng kiến các báo cáo kinh tế kém hơn dự đoán, phản ánh hai yếu tố quan trọng:       
- Động lực tăng trưởng thực tế yếu hơn kỳ vọng       
- Các mô hình dự báo của giới phân tích có xu hướng lạc quan hơn thực tế diễn biến vĩ mô.

Tần suất Negative Surprise cao cũng hàm ý rằng nền kinh tế có thể đang chịu áp lực từ nhiều phía — bao gồm tiến trình giảm phát chậm hơn, nhu cầu hạ nhiệt, và mức độ bất định gia tăng về lộ trình chính sách tiền tệ. Trong bối cảnh này, thị trường dễ rơi vào trạng thái thận trọng, khi nhà đầu tư chú trọng hơn đến rủi ro suy giảm tăng trưởng và khả năng Fed phải duy trì lập trường chính sách dài hạn hơn so với kỳ vọng ban đầu.
## 3.3 Mức độ bất ngờ của các chỉ số kinh tế
1.CPI – Chỉ số gây “shock” thị trường mạnh nhất
CPI thường có độ lệch lớn nhất giữa Actual vs Forecast, đặc biệt trong các tháng có biến động giá năng lượng và chi phí nhà ở.Những cú “miss” hoặc “beat” CPI thường kéo theo phản ứng mạnh trên thị trường trái phiếu, làm lợi suất biến động ngay trong ngày công bố.Chính vì tác động trực tiếp lên kỳ vọng lạm phát, CPI trở thành chỉ số có biên độ bất ngờ lớn và tác động lan tỏa mạnh nhất lên thị trường.

2.Retail Sales – Chỉ số bất ngờ “khó dự đoán” thứ hai
Retail Sales dễ có bất ngờ lớn do hành vi chi tiêu của người tiêu dùng thay đổi theo mùa vụ, ưu đãi, hoặc cú sốc tâm lý.Các nhà phân tích thường dự báo thận trọng, nên chỉ số này đôi khi vượt kỳ vọng rất mạnh hoặc hụt sâu.Retail Sales tạo bất ngờ mạnh trong giai đoạn suy yếu kinh tế vì nó phản ánh “sức khỏe tiêu dùng” – động lực chính của kinh tế Mỹ.

3.PMI – Chỉ số gây bất ngờ vừa phải, nhưng phản ánh xu hướng kinh tế nhanh nhất
PMI hiếm khi có biến động mạnh như CPI hay Retail Sales.PMI dựa trên khảo sát doanh nghiệp nên dữ liệu ổn định hơn và ít bị tác động bởi mùa vụTuy nhiên, khi PMI bất ngờ vượt 50 hoặc rơi dưới 50, thị trường phản ứng ngay vì đây là tín hiệu thay đổi chu kỳ. Mức độ bất ngờ PMI trung bình nhưng ý nghĩa thị trường lại rất cao.

4.GDP – Chỉ số gây bất ngờ thấp nhất
GDP được tổng hợp từ nhiều thành phần có dữ liệu sớm như PMI, sản lượng công nghiệp, bán lẻ…=> Các dự báo GDP thường khá chính xác.Bất ngờ GDP chủ yếu đến từ số liệu điều chỉnh (revision) trong các lần công bố sau, không phải bản công bố đầu tiên.Do đó, GDP có độ lệch thấp nhất và tác động của các cú “miss/beat” lên thị trường thường nhẹ hơn.
### 3.3.1 Tổng kết
- CPI: gây bất ngờ lớn nhất, tác động thị trường mạnh nhất.
- Retail Sales: xếp thứ hai, khó dự đoán, biến động mạnh theo tâm lý tiêu dùng.
- PMI: Chỉ số gây bất ngờ vừa phải.
- GDP: ổn định nhất, ít bất ngờ.
## 3.4 Mối quan hệ nghịch đảo giữa S&P 500 và DXY Index
Phân tích xu hướng 24 tháng cho thấy S&P 500 và DXY duy trì mối quan hệ nghịch đảo rõ rệt, dù cường độ thay đổi theo từng giai đoạn kinh tế – tiền tệ.

1.Khi đồng USD mạnh lên, chứng khoán Mỹ thường chịu áp lực

DXY tăng thường gắn với:
- Kỳ vọng Fed duy trì lãi suất cao
- Dòng tiền phòng thủ chuyển sang tài sản an toàn
- Điều kiện tài chính thắt chặt
                       
Trong các giai đoạn DXY bật tăng mạnh, S&P 500 ghi nhận xu hướng điều chỉnh hoặc mất đà tăng. Điều này củng cố mô hình kinh điển: USD mạnh → chứng khoán yếu.

2.Khi đồng USD suy yếu, S&P 500 có xu hướng phục hồi

DXY giảm cho thấy điều kiện tài chính “nới lỏng” hơn:
- Fed có khả năng cắt giảm lãi suất
- Dòng tiền quay lại tài sản rủi ro
- Nhà đầu tư tăng khẩu vị rủi ro

Trong giai đoạn USD suy yếu, S&P 500 thường có nhịp tăng ổn định hơn, với biên độ dao động thấp: USD yếu → cổ phiếu hưởng lợi.

3.Biểu đồ 24 tháng cho thấy tính nghịch đảo được duy trì ổn định

- DXY và S&P 500 hiếm khi cùng tăng hoặc cùng giảm kéo dài.

- Các điểm đảo chiều của DXY thường đi trước S&P 500 1–3 tuần, cho thấy USD có thể là indicator sớm của tâm lý rủi ro.

- Ở các thời điểm CPI “gây bất ngờ” hoặc Fed phát tín hiệu mạnh, hai đường giá thường tách xa nhau hơn — thể hiện phản ứng trái chiều.

4.Một số trường hợp phá vỡ mô hình nghịch đảo

Mặc dù quan hệ inverse là chủ đạo, nhưng vẫn xuất hiện vài phiên “bất quy tắc”:

Cả S&P 500 và DXY cùng giảm (risk-off toàn thị trường)
- Cả hai cùng tăng (thường khi dữ liệu kinh tế rất mạnh, hỗ trợ tăng trưởng doanh nghiệp)
- Tuy nhiên, tần suất thấp, không làm thay đổi xu hướng nghịch đảo tổng thể.
### 3.4.1 Tổng kết
Biểu đồ cho thấy mối quan hệ nghịch đảo giữa S&P 500 và DXY là xu hướng chủ đạo trong 24 tháng qua. DXY phản ánh kỳ vọng chính sách tiền tệ và tâm lý rủi ro, trong khi S&P 500 phản ứng theo dòng tiền và triển vọng tăng trưởng vì vậy:
- DXY tăng → S&P 500 giảm
- DXY giảm → S&P 500 phục hồi

Đây là một trong những tín hiệu quan trọng giúp nhà phân tích dự báo hướng đi của thị trường chứng khoán Mỹ trong bối cảnh kinh tế biến động mạnh.
## 3.5 Kết luận về mức tương quan giữa USD/VND và DXY (-0.52)

Thông thường USD/VND và DXY có tương quan dương thuận chiều. Tuy nhiên, con số -0.52 trong 24 tháng qua phản ánh một giai đoạn đặc biệt: Trong khi DXY hạ nhiệt từ đỉnh, tỷ giá USD/VND lại chịu áp lực tăng do các yếu tố nội tại (Chênh lệch lãi suất VND-USD âm sâu, nhu cầu thanh toán ngoại tệ cuối năm, và áp lực rút vốn của khối ngoại)
## 3.6 Khuyến nghị nhà đầu tư
Chiến thuật giao dịch: Khi DXY tiệm cận vùng kháng cự (ví dụ 106-107), nhà đầu tư nên bắt đầu tích lũy các nhóm cổ phiếu nhạy cảm với tỷ giá và lãi suất như Bất động sản, Chứng khoán vì kỳ vọng áp lực vĩ mô sắp đạt đỉnh.

Theo dõi biến số sớm: Retail Sales và PMI là các chỉ báo dẫn dắt (Leading indicators) giúp dự báo sớm kết quả kinh doanh của nhóm ngành Bán lẻ và Sản xuất trên sàn HOSE.
