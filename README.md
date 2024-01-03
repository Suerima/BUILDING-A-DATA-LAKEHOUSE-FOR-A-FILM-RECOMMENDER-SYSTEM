# Xây dựng Data LakeHouse cho hế thống gợi ý phim

- [Rental Sakila Project](#rental-sakila-project)
  - [1. Giới thiệu đề tài](#1-giới-thiệu-đề-tài)
  - [2. Thông tin về dataset](#2-thông-tin-về-dataset)
  - [3.1 Nội dung chính dự án](#31-nội-dung-chính-dự-án)
    - [3.1 Xây dựng kho dữ liệu bằng công cụ SSIS](#31-xây-dựng-kho-dữ-liệu-bằng-công-cụ-ssis)
    - [3.2. Xây dựng cube và truy vấn bằng công cụ SSAS](#32-xây-dựng-cube-và-truy-vấn-bằng-công-cụ-ssas)
    - [3.3. Xây dựng Dashboard](#33-xây-dựng-dashboard)
## 1. Mục tiêu
Mục tiêu của project, là triển khai xây dựng hệ thống Data Lakehouse và các ứng dụng từ kiến trúc này để ứng dụng lên website gợi ý phim.
 
## 2. Kiến trúc hệ thống 
Dataset được lấy từ https://www.kaggle.com/datasets/atanaskanev/sqlite-sakila-sample-database

[![Picture2.png](https://i.postimg.cc/FF0CcLcM/Picture2.png)](https://postimg.cc/s1DJC1Tm)

Sau khi nghiên cứu, thì em đã lấy ra các thuộc tính và các bảng cần thiết cho dự án của mình, bao gồm các bảng:
- Address: lưu thông tin địa chỉ
- Actor: thông tin các diễn viên trong một bộ phim
- Customer: thông tin về khách hàng
- Category: các thể loại phim
- Date: lưu thông tin ngày tháng thuê
- Film: thông tin chi tiết về bộ phim
- Store: thông tin cửa hàng
- Staff: thông tin nhân viên
- Rental: thông tin giao dịch ngày thuê, ngày trả và giá cả cho thuê

## 3. Nội dung chính dự án

### 3.1 Xây dựng kho dữ liệu bằng công cụ SSIS
- Tạo StageSakila lưu trữ các table stage và DWHSakila lưu trữ các tabel Dim - Fact
- Đổ dữ liệu từ excel vào các bảng stage
- Đổ dữ liệu từ stage vào các bảng Dim và Fact
- Tạo các khoá ngoại giữa các bảng Fact và các bảng Dim

### 3.2. Xây dựng cube và truy vấn bằng công cụ SSAS
- Tạo Data Source từ kho dữ liệu database DWHSakila
- Tạo Data Source View
- Tạo cube, thêm measure và các dim cần thiết
- Truy vấn các câu hỏi mà nhóm đưa ra bằng công cụ SSAS, Pivot Table, PowerBI

### 3.3. Xây dựng Dashboard với PowerBI
- Dashboard báo cáo doanh thu 
[![dashboard-sales-reporting.png](https://i.postimg.cc/DZL56Pv2/dashboard-sales-reporting.png)](https://postimg.cc/mzZQ2M1q)
- Dashboard thông kê những yếu tố nổi bật theo thời gian 
![dashboard_sales_reporting](https://i.postimg.cc/W1sRkt7F/dashboard-list-top.png)
