# Xây dựng Data LakeHouse cho hế thống gợi ý phim

- [Rental Sakila Project](#rental-sakila-project)
  - [1. Giới thiệu đề tài](#1-giới-thiệu-đề-tài)
  - [2. Thông tin về dataset](#2-thông-tin-về-dataset)
  - [3.1 Nội dung chính dự án](#31-nội-dung-chính-dự-án)
    - [3.1 Xây dựng kho dữ liệu bằng công cụ SSIS](#31-xây-dựng-kho-dữ-liệu-bằng-công-cụ-ssis)
    - [3.2. Xây dựng cube và truy vấn bằng công cụ SSAS](#32-xây-dựng-cube-và-truy-vấn-bằng-công-cụ-ssas)
    - [3.3. Xây dựng Dashboard](#33-xây-dựng-dashboard)
## 1. Objective
Mục tiêu của project, là triển khai xây dựng hệ thống Data Lakehouse và các ứng dụng từ kiến trúc này để ứng dụng lên website gợi ý phim.
 
## 2. Design
### 2.1 System Architecture
[![Picture2.png](https://i.postimg.cc/FF0CcLcM/Picture2.png)](https://postimg.cc/s1DJC1Tm)
- Data sources: Dữ liệu thô ban đầu gồm 2 nguồn từ file csv sẽ được lưu trữ trong Azure Data Lake Storage, nguồn còn lại được thu thập cào và lưu trữ trong MySQL Database trên Azure Database.
- Ingestion: Quá trình tải dữ liệu từ nguồn vào lớp Bronze trong Data Lakehouse sử dụng PySpark. 
- Transformation: Dữ liệu thô từ lớp Bronze được chuyển đổi và tinh chế trong các lớp dữ liệu Silver và Gold. Quá trình này được thực hiện bằng cách sử dụng PySpark (giao diện Python cho Apache Spark), cho phép sử dụng Python để tương tác với Spark và thực hiện các hoạt động xử lý dữ liệu lớn. Chuyển đổi dữ liệu thô thành các bộ dữ liệu được tinh chỉnh và chuẩn mực hơn. 
- Data Lakehouse:  Delta Lake được sử dụng làm định dạng bảng lưu trữ dữ liệu. Hive-metastore trong databricks được sử dụng để lưu trữ metadata cho các bảng dữ liệu, Apache Spark được sử dụng làm công cụ tính toán để truy vấn và xử lý dữ liệu.
 - Visualization: PowerBI được sử dụng để trực quan hóa và khám phá dữ liệu.
- Web recommendation: Xây dựng một trang web gợi ý phim sử dụng API từ mô hình Machine Learning đã triển khai.
- Orchestration: tính năng Workflow trong Databrick sử dụng Jobs Scheduler để lập lịch và chạy các công việc này theo định kỳ.
  
Tổng thể, kiến trúc này sử dụng các công nghệ được tích hợp sẵn trong Databricks và các công cụ để lưu trữ, xử lý và truy vấn dữ liệu từ các nguồn trong hệ sinh thái của Azure. Sự kết hợp này tạo ra một môi trường linh hoạt và hiệu quả để xây dựng các báo cáo quản trị và xây dựng các thuật toán gợi ý phim.

## 2.2 Database schema
[![Picture3.png](https://i.postimg.cc/VkzXTSJb/Picture3.png)](https://postimg.cc/bsFGSwHz)

## 2.3 Data lineage

### 3. Dashboard
- Dashboard báo cáo doanh thu 
[![dashboard-sales-reporting.png](https://i.postimg.cc/DZL56Pv2/dashboard-sales-reporting.png)](https://postimg.cc/mzZQ2M1q)
- Dashboard thông kê những yếu tố nổi bật theo thời gian 
![dashboard_sales_reporting](https://i.postimg.cc/W1sRkt7F/dashboard-list-top.png)
