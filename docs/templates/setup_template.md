# Hướng dẫn cài đặt và chạy — {{TEN_DU_AN}}

**Phiên bản:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_RA_SOAT_DA_CHOT}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Viết để thành viên mới dựng được hệ thống từ mã nguồn và linh kiện. Chỉ đưa lệnh thực sự đã kiểm tra; các ô bên dưới chưa phải lệnh có thể chạy. Xem [cách dùng bộ mẫu](README.md).

## 1. Môi trường đã xác minh

- **Commit / tag:** {{MA_PHIEN_BAN}}
- **Hệ điều hành:** {{TEN_VA_PHIEN_BAN}}
- **Board / revision:** {{MODEL_VA_REV}}
- **Ngày và người dựng thử:** {{NGAY_HO_TEN}}
- **Phạm vi hướng dẫn:** {{LOCAL_GIA_LAP_HOAC_MOI_TRUONG_KHAC}}

| Công cụ / dịch vụ | Phiên bản đã thử | Mục đích | Cách cài / nguồn chính thức |
|---|---|---|---|
| {{IDE_SDK_RUNTIME_PACKAGE_MANAGER}} | {{PHIEN_BAN}} | {{MUC_DICH}} | {{HUONG_DAN}} |
| {{MQTT_DATABASE_NODE_RED_NEU_DUNG}} | {{PHIEN_BAN}} | {{MUC_DICH}} | {{HUONG_DAN}} |

## 2. Chuẩn bị phần cứng và mạng

1. {{DOI_CHIEU_SO_DO_DAU_NOI_VA_PHIEN_BAN_MACH_TRONG_HARDWARE}}
2. {{CHUAN_BI_NGUON_CAP_CAP_USB_DRIVER_VA_QUYEN_TRUY_CAP_CONG}}
3. {{CAU_HINH_MANG_DIA_CHI_BROKER_MAY_CHU_VA_CAC_CONG_CAN_THIET}}
4. {{XAC_NHAN_KET_NOI_TRUOC_KHI_CHAY_UNG_DUNG}}

**Kết quả kiểm tra điều kiện đầu vào:** {{DAU_HIEU_HOAC_LENH_KIEM_TRA_VA_KET_QUA_MONG_DOI}}.

## 3. Lấy mã nguồn và cài phụ thuộc

| Thứ tự | Thư mục thực hiện | Lệnh cụ thể | Kết quả mong đợi |
|---|---|---|---|
| 1 | {{THU_MUC}} | {{LENH_LAY_MA_VA_CHON_TAG}} | {{MA_NGUON_DUNG_PHIEN_BAN}} |
| 2 | {{THU_MUC}} | {{LENH_CAI_PHU_THUOC_THEO_LOCKFILE_NEU_CO}} | {{DAU_HIEU_THANH_CONG}} |
| 3 | {{THU_MUC}} | {{LENH_BUILD_HOAC_CHUAN_BI}} | {{TEP_DAU_RA}} |

**Dữ liệu / tệp cần lấy riêng:** {{TEP_CAU_HINH_MAU_FLOW_NODE_RED_MIGRATION_DU_LIEU_MAU}}.

## 4. Cấu hình môi trường

Chỉ ghi tên biến và giá trị mẫu không nhạy cảm. Tài khoản, mật khẩu và khóa thật được cấp qua {{KENH_CAP_BI_MAT}}.

| Biến / mục cấu hình | Ý nghĩa | Bắt buộc | Giá trị mẫu không nhạy cảm | Nơi cấu hình |
|---|---|---|---|---|
| {{TEN_BIEN}} | {{Y_NGHIA}} | {{CO_KHONG}} | {{GIA_TRI_MAU}} | {{TEP_HOAC_GIAO_DIEN}} |

- **Tệp cấu hình mẫu trong repo:** {{DUONG_DAN}}
- **Tệp chứa bí mật cần loại khỏi Git:** {{DUONG_DAN_VA_QUY_TAC_IGNORE}}
- **Cấp tài khoản thử nghiệm và quyền:** {{CAC_BUOC_KHONG_GHI_MAT_KHAU_THAT}}
- **Cách kiểm tra cấu hình hợp lệ:** {{LENH_HOAC_THAO_TAC_VA_DAU_HIEU}}

## 5. Build và nạp firmware

| Thứ tự | Thao tác / lệnh và thư mục | Tham số cần chọn | Kết quả mong đợi |
|---|---|---|---|
| 1 | {{MO_PROJECT_HOAC_LENH_BUILD}} | {{BOARD_SDK_PROFILE}} | {{BUILD_THANH_CONG}} |
| 2 | {{LENH_HOAC_THAO_TAC_NAP}} | {{CONG_TOC_DO_PHIEN_BAN_BINARY}} | {{NAP_THANH_CONG}} |
| 3 | {{MO_SERIAL_MONITOR}} | {{BAUD_RATE}} | {{LOG_KHOI_DONG_DEVICE_ID_KET_NOI}} |

**Cấu hình lần đầu / hiệu chuẩn:** {{THAM_CHIEU_HARDWARE_VA_CAC_BUOC}}.  
**Nếu giả lập:** {{CACH_MO_MO_PHONG_PHU_THUOC_VA_GIOI_HAN}}.

## 6. Khởi tạo dữ liệu và chạy dịch vụ

| Thứ tự | Thành phần | Thư mục và lệnh / thao tác | Dấu hiệu sẵn sàng | Địa chỉ truy cập |
|---|---|---|---|---|
| 1 | {{DICH_VU_NEN}} | {{LENH_CAU_HINH_KHOI_CHAY}} | {{HEALTH_LOG}} | {{HOST_PORT}} |
| 2 | {{DATABASE_HOAC_KHO_DU_LIEU}} | {{MIGRATION_SEED_NEU_CO}} | {{DAU_HIEU}} | {{DIA_CHI}} |
| 3 | {{BACKEND_HOAC_NODE_RED}} | {{LENH_HOAC_IMPORT_FLOW_VA_DEPLOY}} | {{DAU_HIEU}} | {{DIA_CHI}} |
| 4 | {{GIAO_DIEN}} | {{LENH_KHOI_CHAY}} | {{DAU_HIEU}} | {{URL}} |

Sửa thứ tự theo phụ thuộc thực tế. Nếu dùng Node-RED, ghi thêm vị trí flow, các node bổ sung, cách cấu hình credentials và cách khôi phục flow: {{HUONG_DAN}}.

## 7. Kiểm tra nhanh sau cài đặt

| Bước | Thao tác | Kết quả cần thấy | Nếu lỗi, xem ở đâu |
|---|---|---|---|
| 1 | {{KIEM_TRA_THIET_BI_ONLINE}} | {{TRANG_THAI_LOG}} | {{LOG_VA_MUC_KHAC_PHUC}} |
| 2 | {{TAO_MOT_DU_LIEU_CAM_BIEN}} | {{GIA_TRI_VA_THOI_GIAN_TREN_UI}} | {{LOG_TOPIC}} |
| 3 | {{GUI_MOT_LENH_DIEU_KHIEN}} | {{TAI_PHAN_HOI_VA_UI_XAC_NHAN}} | {{COMMAND_ID_VA_LOG}} |

**Bằng chứng đã dựng thành công:** {{NGAY_COMMIT_NGUOI_THUC_HIEN_VA_DUONG_DAN_LOG_ANH}}. Nếu chưa dựng thử, ghi `Chưa xác minh`.

## 8. Dừng hệ thống và xử lý lỗi thường gặp

- **Đưa tải về trạng thái phù hợp trước khi dừng:** {{THAO_TAC}}
- **Thứ tự dừng:** {{THU_TU_VA_LENH}}
- **Chạy lại và dữ liệu được giữ:** {{HUONG_DAN}}
- **Đặt lại dữ liệu thử nghiệm:** {{THAO_TAC_PHAM_VI_DU_LIEU_BI_XOA_VA_DIEU_KIEN_THUC_HIEN}}

| Triệu chứng | Cách chẩn đoán | Nguyên nhân có thể | Cách khắc phục |
|---|---|---|---|
| {{TRIEU_CHUNG}} | {{LENH_HOAC_DIEM_KIEM_TRA}} | {{NGUYEN_NHAN}} | {{CAC_BUOC}} |
