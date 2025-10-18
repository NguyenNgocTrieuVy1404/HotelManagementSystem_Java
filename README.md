# Hệ Thống Quản Lý Hóa Đơn Khách Sạn

## Mô tả
Ứng dụng Java Swing quản lý hóa đơn khách sạn theo giờ và theo ngày. Dự án học tập áp dụng Clean Architecture, Use Case pattern và SOLID principles.

## Chức năng chính
- ✅ Thêm, sửa, xóa, tìm kiếm hóa đơn khách sạn
- ✅ Quản lý hóa đơn theo giờ và theo ngày
- ✅ Tính toán thành tiền tự động
- ✅ Báo cáo thống kê (tổng số lượng, trung bình thành tiền)
- ✅ Giao diện Swing hiện đại với Nimbus Look & Feel

## Kiến trúc dự án

### Clean Architecture + Use Case Pattern
```
src/main/java/
├── AppQuanLyHoaDon.java           # Main class - Dependency Injection
├── addInvoiceKS/                  # Use Case: Thêm hóa đơn
│   ├── Entity/Invoice.java        # Domain Entity
│   ├── UseCase/                   # Business Logic
│   └── Database/                  # Data Access
├── addInvoiceDisplayKS/           # Use Case: Hiển thị form thêm
│   ├── UI/                        # Presentation Layer
│   └── UseCase/                   # Use Case Logic
├── editInvoiceKS/                 # Use Case: Sửa hóa đơn
├── deleteInvoiceKS/               # Use Case: Xóa hóa đơn
├── findInvoiceKS/                 # Use Case: Tìm kiếm hóa đơn
├── avgAmountItemKS/               # Use Case: Tính trung bình thành tiền
├── totalQuantityItemKS/           # Use Case: Tổng số lượng theo loại
└── quanLyHoaDon/                  # Use Case: Quản lý tổng thể
```

### SOLID Principles áp dụng
- **S** - Single Responsibility: Mỗi Use Case chỉ làm 1 việc
- **O** - Open/Closed: Dễ mở rộng Use Case mới
- **L** - Liskov Substitution: Interface có thể thay thế
- **I** - Interface Segregation: Interface nhỏ, chuyên biệt
- **D** - Dependency Inversion: Phụ thuộc vào abstraction

## Công nghệ
- **Java 8** - Ngôn ngữ lập trình
- **Maven** - Quản lý dependency
- **MySQL** - Cơ sở dữ liệu
- **JDBC** - Kết nối database
- **JCalendar** - Date picker
- **Swing** - Giao diện người dùng

## Cài đặt

### 1. Yêu cầu
- Java 8+
- Maven 3.6+
- MySQL Server
- IDE Java (Eclipse/IntelliJ)

### 2. Setup database
```sql
CREATE DATABASE quanlyhoadonks;

CREATE TABLE hoadon (
    maHD VARCHAR(50) PRIMARY KEY,
    ngayHD DATE,
    tenKH VARCHAR(100),
    maPhong VARCHAR(50),
    loaiHoaDon VARCHAR(50),
    donGia DOUBLE,
    soGioThue INT,
    soNgayThue INT,
    thanhTien DOUBLE
);

CREATE TABLE loaihoadon (
    loaiHoaDon VARCHAR(50) PRIMARY KEY
);

INSERT INTO loaihoadon VALUES ('Theo Giờ'), ('Theo Ngày');
```

### 3. Cấu hình kết nối
Sửa các file ConnectionDB trong từng package:
```java
private static final String URL = "jdbc:mysql://localhost:3306/quanlyhoadonks";
private static final String USER = "root";
private static final String PASSWORD = "your_password";
```

### 4. Chạy ứng dụng
```bash
# Clone project
git clone <repository-url>
cd CuoiKy_QLHoaDonKS

# Compile và chạy
mvn clean compile
mvn exec:java -Dexec.mainClass="AppQuanLyHoaDon"
```

## Cách sử dụng

1. **Thêm hóa đơn**: Chọn "Thêm hóa đơn" → Điền thông tin → Chọn loại (Theo giờ/Ngày)
2. **Sửa hóa đơn**: Chọn "Sửa hóa đơn" → Chọn hóa đơn → Sửa thông tin
3. **Xóa hóa đơn**: Chọn "Xóa hóa đơn" → Chọn hóa đơn → Xác nhận
4. **Tìm kiếm**: Chọn "Tìm kiếm" → Nhập tên khách hàng
5. **Báo cáo**: Menu "Báo cáo" → Chọn loại thống kê

## Công thức tính tiền

**Hóa đơn theo giờ:**
- `số giờ thuê × đơn giá`
- Giới hạn: 1-30 giờ

**Hóa đơn theo ngày:**
- `số ngày thuê × đơn giá`
- Không giới hạn số ngày

## Use Case Pattern

### Cấu trúc Use Case
```
UseCase/
├── InputBoundary.java     # Interface input
├── OutputBoundary.java    # Interface output  
├── UseCase.java          # Business logic
├── InputDTO.java         # Data transfer object
└── OutputDTO.java        # Response object
```

### Ví dụ: AddInvoiceUseCase
- **Input**: AddInvoiceInputDTO (maHD, ngayHD, tenKH...)
- **Output**: ResponseDataAdd (message, errorMessage)
- **Validation**: Kiểm tra dữ liệu đầu vào
- **Business Rules**: Ngày HD từ hôm nay, không quá 7 ngày

## Clean Architecture Layers

1. **Entity Layer**: Domain objects (Invoice, InvoiceDay, InvoiceHour)
2. **Use Case Layer**: Business logic và rules
3. **Interface Adapters**: Controllers, Presenters, Gateways
4. **Frameworks & Drivers**: UI, Database, Web

## Lưu ý
- Đây là dự án học tập áp dụng Clean Architecture
- Mỗi Use Case được đóng gói độc lập
- Dễ dàng test và maintain
- Có thể mở rộng thêm Use Case mới
