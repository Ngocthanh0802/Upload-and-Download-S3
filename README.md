# 📦 Upload Image and Download Image to S3 bằng API Gateway và Lambda

## 📘 Thông tin sinh viên
- 🙋‍♂️ **Họ và tên:** Nguyễn Ngọc Thanh
- 🧾 **MSSV:** 2180602939
- 📧 **Email:** nnthanh0802@gmail.com
- 🎓 **Trường:** Đại học Công nghệ TP.HCM (HUTECH)  
- 🗓️ **Ngày thực hiện:** 07/07/2025

---

## 1. 📄 Tóm tắt nội dung 

Dự án xây dựng hệ thống REST API cho phép upload và download hình ảnh lên Amazon S3 thông qua AWS API Gateway và Lambda, sử dụng ngôn ngữ Python và kiểm thử bằng Postman

### 📌 Nội dung:
- **Tuyên bố vấn đề rút gọn:** Các hệ thống lưu trữ file truyền thống gây tốn kém, khó mở rộng và khó bảo trì.
- **Giải pháp:** Dùng AWS API Gateway kết hợp Lambda và S3 để tạo hệ thống REST API cho phép upload/download hình ảnh đơn giản, bảo mật, không cần server.
- **Tính năng chính:**
  - Upload/download ảnh bằng HTTP API.
  - Lưu trữ không giới hạn trên S3.
  - Bảo mật bằng IAM.
- **Lợi ích kinh doanh & ROI:**
  - Cắt giảm >70% chi phí vận hành.
  - Rút ngắn thời gian triển khai lên đến 60%.
- **Đầu tư và thời gian:**
  - 1 tháng thực hiện.
  - Chi phí hạ tầng khoảng 5 USD/tháng (dự kiến 1,000 request/ngày).
- **Chỉ số thành công:**
  - <200ms phản hồi API
  - 99.9% uptime


---

## 2. 🎯 Đặt vấn đề 

### 📌 Thực trạng hiện tại
Hầu hết ứng dụng upload ảnh dùng server backend riêng, gây ra:
- Chi phí cao (server, bảo trì, nhân sự)
- Khó mở rộng khi lượng truy cập tăng
- Rủi ro bảo mật cao nếu không quản lý đúng

### 💢 Điểm đau và tác động
- Upload ảnh lớn gây nghẽn server
- Tệp hình ảnh không được mã hóa khi lưu trữ
- Tốn thời gian xử lý và nhân lực bảo trì server

### 👥 Các bên liên quan
- **DevOps**: Mong muốn giảm tải vận hành
- **Developer**: Cần API đơn giản, dễ tích hợp
- **Người dùng cuối**: Trải nghiệm upload nhanh, an toàn

### 🚨 Hậu quả nếu không thay đổi
- Lãng phí tài nguyên
- Tốc độ triển khai chậm
- Không đảm bảo bảo mật khi mở rộng quy mô

### 🌍 Cơ hội thị trường
- Số lượng ứng dụng xử lý hình ảnh tăng mạnh
- AWS Free Tier giúp dễ tiếp cận cho startup

---

## 3. 🏗️ Kiến trúc giải pháp 

### 🧱 Sơ đồ kiến trúc tổng quan
![Diagran](Screenshot%202025-07-09%20170331.png)

### 🧩 Lựa chọn dịch vụ AWS
- **Amazon S3**: Lưu trữ ảnh gốc.
- **AWS Lambda**: Xử lý logic upload/download.
- **API Gateway**: Giao tiếp RESTful.
- **IAM**: Phân quyền truy cập.
- **CloudWatch**: Logging và giám sát.

### 🔄 Tương tác và luồng dữ liệu
1. Client gửi HTTP request lên API Gateway
2. API Gateway chuyển request cho Lambda
3. Lambda xử lý logic, tương tác với S3
4. Kết quả trả về client

### 🔐 Kiến trúc bảo mật
- IAM Roles kiểm soát từng hành động
- Bucket S3 để private, truy cập thông qua presigned URL
- Mã hóa AES-256 cho dữ liệu lưu trữ
- Logging mọi request bằng CloudWatch

### 📈 Khả năng mở rộng & hiệu suất
- Lambda và API Gateway có thể tự động scale
- S3 không giới hạn dung lượng
- Đảm bảo <200ms phản hồi khi request nhỏ (<1MB)

### 🔗 Tích hợp hệ thống khác
- Có thể mở rộng kết nối với DynamoDB để lưu metadata
- Kết hợp Cognito để quản lý người dùng nâng cao


---

## 4. 🔧 Triển khai kỹ thuật 

### 📋 Giai đoạn thực hiện
1. Phân tích yêu cầu và xác định use case
2. Xây dựng function upload/download bằng Python
3. Tạo REST API trong API Gateway
4. Cấu hình IAM và bucket S3
5. Viết test case, monitor và deploy
6. Viết test case & kiểm thử bằng Postman

### 💻 Yêu cầu kỹ thuật
- Ngôn ngữ: Python 3.9
- Bộ nhớ Lambda: 128–512MB
- Storage: S3 bucket với chính sách private
- Mạng: Public API (Gateway), private storage (S3)

### 🛠️ Phương pháp phát triển
- Triển khai mô-đun tách biệt
- Dùng AWS SAM để quản lý template
- CI/CD qua GitHub Actions hoặc AWS CodePipeline

### 🧪 Chiến lược kiểm thử
- Unit test cho từng hàm Lambda
- Tích hợp test qua Postman hoặc curl
- Load test qua Artillery hoặc JMeter

### 🚀 Kế hoạch triển khai
- Deploy qua AWS SAM
- CloudWatch theo dõi logs & alerts
- Backup định kỳ từ S3

### 🔧 Quản lý cấu hình
- Biến môi trường Lambda dùng cho config động
- Versioning S3 bật để kiểm soát thay đổi file


---

## 5. 📅 Dòng thời gian & Các mốc 

### 🗓️ Phân tích giai đoạn
- **Tuần 1:** Thu thập yêu cầu & thiết kế kiến trúc
- **Tuần 2:** Xây dựng Lambda(Python) & tích hợp API Gateway
- **Tuần 3:** Cấu hình bảo mật IAM và S3
- **Tuần 4:** Kiểm thử, triển khai, viết tài liệu

### 📌 Mốc quan trọng
- ✅ Hoàn thành sơ đồ kiến trúc
- ✅ Viết thành công hàm Lambda upload/download
- ✅ Kết nối được API Gateway với Lambda
- ✅ Đảm bảo upload thành công file thực tế

### 🔗 Phụ thuộc
- Tài khoản AWS đủ quyền
- DevOps setup môi trường CI/CD
- Quy trình xét duyệt bảo mật (nếu có)

### 👥 Phân bổ nguồn lực
- 1 Developer backend
- 1 người kiểm thử & monitor
- 1 người hỗ trợ triển khai cuối

### ⏱️ Thời gian đệm rủi ro
- Mỗi tuần dành 0.5 ngày cho xử lý lỗi phát sinh

---

## 6. 💰 Dự toán ngân sách 

### 🧾 Chi phí hạ tầng
- **Amazon S3:** $0.023/GB
- **AWS Lambda:** 1 triệu request đầu miễn phí, sau đó $0.20/million
- **API Gateway:** ~$3.5/million request
- **CloudWatch logs:** ~$0.50/GB

### 👨‍💻 Chi phí phát triển
- 2 dev × $500 = $1,000 cho 1 tháng

### 🔄 Chi phí vận hành định kỳ
- Ước tính 1000 request/ngày → khoảng $5–7/tháng
- Gồm: Lambda, Gateway, lưu trữ S3, logs CloudWatch

### 📊 Tính toán ROI
- So với sử dụng EC2, giảm ít nhất 70% chi phí hạ tầng
- Triển khai nhanh hơn → tiết kiệm thời gian phát hành

### 🧠 Chiến lược tối ưu
- Sử dụng AWS Free Tier tối đa
- Cấu hình lifecycle cho S3 để xóa file không cần thiết
- Dùng CloudWatch metric để cảnh báo kịp thời

---

## 7. ⚠️ Đánh giá rủi ro 

### ⚡ Rủi ro tiềm ẩn

| Loại rủi ro              | Mức độ      | Mô tả |


| Cấu hình IAM sai         | Trung bình  | Gây lộ dữ liệu hoặc hạn chế truy cập |

| Quá tải Lambda           | Thấp        | Request cao bất ngờ vượt giới hạn concurrency |

| API Gateway lỗi xác thực | Thấp        | Không nhận diện đúng người dùng |

### 🛡️ Chiến lược giảm thiểu
- Xem xét kỹ IAM Policy, test kỹ quyền truy cập
- Đặt limit và alarm cho Lambda
- Dùng JWT hoặc Cognito để xác thực an toàn

### 🆘 Kế hoạch dự phòng
- Dùng CloudTrail để audit
- Snapshot định kỳ dữ liệu nếu cần
- Tạm thời chuyển sang EC2 hosting trong trường hợp khẩn cấp

### 🧭 Quy trình giám sát
- Thiết lập CloudWatch Dashboard
- Gửi cảnh báo qua email hoặc SNS
- Log toàn bộ request và response để truy vết

---

## 8. 🎯 Kết quả mong đợi 

### 📈 Chỉ số thành công
- Upload/download thành công ≥ 99%
- Phản hồi <200ms với ảnh <1MB
- 99.9% uptime trong 1 tháng

### 🔥 Lợi ích ngắn hạn (0–6 tháng)
- Cải thiện tốc độ và trải nghiệm người dùng
- Giảm gánh nặng vận hành server

### 🌱 Lợi ích trung hạn (6–18 tháng)
- Tái sử dụng cho các dự án upload khác
- Dễ dàng mở rộng cho audio, video hoặc tài liệu

### 🏆 Giá trị dài hạn (18+ tháng)
- Là nền tảng upload chuẩn cho toàn bộ hệ sinh thái ứng dụng
- Hệ thống giám sát và bảo mật tự động hóa

### 🧑‍💻 Cải thiện UX/UI
- Upload qua API đơn giản hơn cho mobile/web app
- Đảm bảo người dùng không cần đăng nhập AWS nhưng vẫn bảo mật

