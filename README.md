# Xây dựng Data LakeHouse cho hệ thống gợi ý phim

## 1. Objective
Mục tiêu của project, là triển khai xây dựng hệ thống Data Lakehouse và ứng dụng từ kiến trúc này lên website gợi ý phim.
 
## 2. Design
### 2.1 System Architecture
[![Picture2.png](https://i.postimg.cc/FF0CcLcM/Picture2.png)](https://postimg.cc/s1DJC1Tm)
- Data sources: Dữ liệu thô ban đầu gồm 2 nguồn từ file csv sẽ được lưu trữ trong Azure Data Lake Storage, nguồn còn lại được thu thập cào và lưu trữ trong MySQL Database trên Azure Database.
- Ingestion: Quá trình tải dữ liệu từ nguồn vào lớp Bronze trong Data Lakehouse sử dụng PySpark. 
- Transformation: Dữ liệu thô từ lớp Bronze được chuyển đổi và tinh chế trong các lớp dữ liệu Silver và Gold được thực hiện bằng PySpark.
- Data Lakehouse:
  - Delta Lake được sử dụng làm định dạng bảng lưu trữ dữ liệu.
  - Hive-metastore trong databricks được sử dụng để lưu trữ metadata cho các bảng dữ liệu.
  - Apache Spark được sử dụng làm công cụ tính toán để truy vấn và xử lý dữ liệu.
- Visualization: PowerBI được sử dụng để trực quan hóa và khám phá dữ liệu.
- Web recommendation: Xây dựng một trang web gợi ý phim sử dụng API từ mô hình Machine Learning đã triển khai.
- Orchestration: tính năng Workflow trong Databrick sử dụng Jobs Scheduler để lập lịch và chạy các công việc này theo định kỳ.
  
Tổng thể, kiến trúc này sử dụng các công nghệ được tích hợp sẵn trong Databricks và các công cụ để lưu trữ, xử lý và truy vấn dữ liệu từ các nguồn trong hệ sinh thái của Azure. Sự kết hợp này tạo ra một môi trường linh hoạt và hiệu quả để xây dựng các báo cáo quản trị và xây dựng các thuật toán gợi ý phim.

## 2.2 Database schema
[![Picture3.png](https://i.postimg.cc/VkzXTSJb/Picture3.png)](https://postimg.cc/bsFGSwHz)

Thông tin các bảng:
- Bảng movie chứa dữ liệu liên quan đến thông tin về từng bộ phim
- Bảng genre lưu trữ thông tin về các thể loại của các bộ phim
- Bảng actor lưu trữ thông tin liên quan đến actor
- Bảng budget lưu trữ thông tin liên quan đến ngân sách
- Bảng keyword lưu trữ thông tin về các từ khóa
- Bảng trailer lưu trữ thông tin về trailer của phim
- Bảng liên kết quan hệ n-n giữa bộ phim và diễn viên
- Bảng liên kết quan hệ n-n giữa đạo diễn và bộ phim
- Bảng liên kết quan hệ n-n giữa bộ phim và từ khóa
- Bảng liên kết quan hệ n-n giữa bộ phim và thể loại

## 2.3 Data lineage
Với data lineage dày đặc, nên việc tách 2 workflow phục vụ cho từng mục đích riêng sẽ dễ trực quan hơn

**Workflow phục vụ cho Machine Learning**

[![ml-workflow.png](https://i.postimg.cc/x1GtNDzL/ml-workflow.png)](https://postimg.cc/2164gtT5)
- Dữ liệu từ Data Source là MySQL và file csv load vào bronze layer
- Từ bronze layer, dữ liệu được dedupe, clean và fill missing theo các tiêu chuẩn đã đặt ra ở silver layer
- Sau đó dữ liệu sẽ được phục vụ cho Machine Learning

**Workflow phục vụ cho Lớp Warehouse**

[![fact-workflow-jpg.png](https://i.postimg.cc/44M8r1GH/fact-workflow-jpg.png)](https://postimg.cc/5jBqzL6f)
- Dữ liệu từ Data Source là MySQL và file csv load vào bronze layer
- Từ bronze layer, dữ liệu được dedupe, clean và fill missing ở silver layer
- Sau đó transformm, tính toán nâng cao và phân tách ở gold layer
  
**Lược đồ hình sao cho lớp DWH**

[![Picture5.png](https://i.postimg.cc/vZB5b4sg/Picture5.png)](https://postimg.cc/0bTzC2rP)

Thông tin các bảng:
- Bảng dim_info thể hiện cho thông tin bộ phim
- Bảng dim_company thể hiện đối tượng các công ty sản xuất phim
- Bảng dim_language thể hiện về ngôn ngữ sử dụng trong bộ phim
- Bảng dim_genre thể hiện thông tin thể loại
- Bảng dim_date thể hiện đối tượng thời gian
- Bảng fact_movie mỗi dòng trong bảng tương ứng thông tin tình trạng cụ thể về một bộ phim.

### 3. Dashboard
- Dashboard báo cáo tình trạng các bộ phim trên toàn thế giới 
[![Picture4.png](https://i.postimg.cc/NfLPPfzD/Picture4.png)](https://postimg.cc/CzTNRYYn)
