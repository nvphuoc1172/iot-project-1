# Triển khai và vận hành — {{TEN_DU_AN}}

**Phiên bản tài liệu / sản phẩm:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_RA_SOAT_DA_BAN_GIAO}}  
**Người phụ trách vận hành:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Dùng khi bàn giao hoặc tiếp tục vận hành hệ thống. Ghi thao tác thực tế, đầu mối xử lý và cách xác minh kết quả. Không ghi mật khẩu, token hoặc khóa riêng vào tài liệu. Xem [cách dùng bộ mẫu](README.md).

## 1. Phạm vi và trách nhiệm

- **Môi trường áp dụng:** {{THU_NGHIEM_NOI_BO_HOAC_THUC_TE}}
- **Phiên bản / cấu hình đang vận hành:** {{TAG_COMMIT_BOARD_REV_CONFIG_PROFILE}}
- **Giờ cần hoạt động và mục tiêu khôi phục:** {{THEO_REQUIREMENTS_HOAC_THOA_THUAN_BAN_GIAO}}
- **Điều kiện được phép bảo trì:** {{KHUNG_GIO_VA_CACH_THONG_BAO}}

| Vai trò | Người / nhóm phụ trách | Quyền được cấp | Kênh liên hệ / người thay thế |
|---|---|---|---|
| {{VAN_HANH_HA_TANG_PHAN_MEM_PHAN_CUNG}} | {{DAU_MOI}} | {{PHAM_VI_QUYEN}} | {{KENH_VA_DAU_MOI_DU_PHONG}} |

## 2. Danh mục triển khai

| Thành phần / thiết bị | Vị trí / môi trường | Địa chỉ / định danh | Phiên bản | Cấu hình / nơi lưu | Người quản lý |
|---|---|---|---|---|---|
| {{TEN}} | {{VI_TRI}} | {{HOST_DEVICE_ID_PORT}} | {{PHIEN_BAN}} | {{THAM_CHIEU_KHONG_CHUA_BI_MAT}} | {{HO_TEN}} |

**Sơ đồ mạng và phụ thuộc:** {{THAM_CHIEU_ARCHITECTURE}}.  
**Cài đặt từ đầu:** {{THAM_CHIEU_SETUP}}.  
**Khác biệt với môi trường phát triển:** {{CAU_HINH_QUYEN_CHUNG_CHI_TAI_NGUYEN}}.

## 3. Quy trình triển khai phiên bản

| Bước | Thao tác / lệnh thực tế và nơi thực hiện | Người thực hiện | Điều kiện chuyển bước / bằng chứng |
|---|---|---|---|
| 1 | {{CHON_BAN_PHAT_HANH_VA_KIEM_TRA_TUONG_THICH}} | {{HO_TEN}} | {{TESTING_VA_CONFIG_DA_XAC_NHAN}} |
| 2 | {{SAO_LUU_DU_LIEU_CAU_HINH_VA_BAN_HIEN_TAI}} | {{HO_TEN}} | {{BAN_SAO_LUU_CO_THE_KHOI_PHUC}} |
| 3 | {{DUA_TAI_VE_TRANG_THAI_PHU_HOP}} | {{HO_TEN}} | {{CACH_XAC_NHAN}} |
| 4 | {{CAP_NHAT_DICH_VU_FIRMWARE_VA_SCHEMA_THEO_THU_TU}} | {{HO_TEN}} | {{LOG_VA_PHIEN_BAN_DUNG}} |
| 5 | {{KIEM_TRA_LUONG_DU_LIEU_DIEU_KHIEN_VA_THEO_DOI}} | {{HO_TEN}} | {{TC_VA_NGUONG_DAT}} |

- **Thứ tự cập nhật các thành phần:** {{PHU_THUOC_FIRMWARE_BACKEND_UI_DATABASE}}
- **Gián đoạn dự kiến:** {{THOI_LUONG_VA_ANH_HUONG}}
- **Điều kiện hủy triển khai / quay lại:** {{DAU_HIEU_NGUONG_VA_NGUOI_QUYET_DINH}}

## 4. Cấu hình, thông tin bí mật và quyền truy cập

| Hạng mục | Nơi quản lý | Ai được truy cập | Cách cấp / thay đổi / thu hồi | Chu kỳ hoặc sự kiện cần kiểm tra |
|---|---|---|---|---|
| {{TAI_KHOAN_KHOA_CHUNG_CHI_CAU_HINH}} | {{KHO_QUAN_LY_HOAC_DUONG_DAN_KHONG_GHI_GIA_TRI}} | {{VAI_TRO}} | {{QUY_TRINH}} | {{THOI_DIEM}} |

- **Quyền MQTT, API và giao diện quản trị:** {{THAM_CHIEU_INTERFACES_VA_QUYEN_THEO_VAI_TRO}}
- **Kết nối từ xa và bảo vệ đường truyền:** {{CO_CHE_THUC_TE_VA_GIOI_HAN}}
- **Cấp mới / thay thế / thu hồi thiết bị:** {{CAC_BUOC_VA_XU_LY_DANH_TINH_CU}}
- **Dữ liệu cá nhân, thời hạn lưu và xóa:** {{CHINH_SACH_VA_CACH_THUC_HIEN_HOAC_KHONG_AP_DUNG}}
- **Nội dung cần che trong log và bản sao lưu:** {{DANH_SACH_VA_CACH_KIEM_TRA}}

## 5. Giám sát và cảnh báo

| Chỉ số / sự kiện | Nguồn quan sát | Ngưỡng và thời gian duy trì | Người nhận / kênh | Hành động đầu tiên |
|---|---|---|---|---|
| Thiết bị offline / dữ liệu quá cũ | {{HEARTBEAT_LOG_HOAC_UI}} | {{NGUONG_THEO_NF_ID}} | {{DAU_MOI}} | {{HUONG_DAN}} |
| Lệnh timeout / thất bại | {{COMMAND_RESULT_HOAC_LOG}} | {{NGUONG}} | {{DAU_MOI}} | {{HUONG_DAN}} |
| Dịch vụ / lưu trữ gặp lỗi | {{HEALTH_LOG_TAI_NGUYEN}} | {{NGUONG}} | {{DAU_MOI}} | {{HUONG_DAN}} |

**Vị trí log, thời hạn lưu và cách tra theo thiết bị / lệnh:** {{DUONG_DAN_QUY_UOC_VA_CAU_LENH}}.  
**Kiểm tra cảnh báo có hoạt động:** {{CACH_THU_TAN_SUAT_VA_BANG_CHUNG}}.

## 6. Sao lưu và khôi phục

**Mục tiêu mất dữ liệu tối đa (RPO):** {{THOI_GIAN}}.  
**Mục tiêu thời gian phục hồi (RTO):** {{THOI_GIAN}}. Hai giá trị này là mục tiêu; ghi kết quả thực đo sau lần thử khôi phục.

| Đối tượng cần sao lưu | Tần suất | Nơi lưu / quyền truy cập | Thời hạn giữ | Cách kiểm tra bản sao |
|---|---|---|---|---|
| {{DATABASE_FLOW_CAU_HINH_HE_SO_HIEU_CHUAN_BINARY}} | {{TAN_SUAT}} | {{NOI_LUU}} | {{THOI_HAN}} | {{PHUONG_PHAP}} |

### Quy trình khôi phục

1. {{XAC_DINH_PHAM_VI_SU_CO_VA_CHON_BAN_SAO}}
2. {{CHUAN_BI_MOI_TRUONG_VA_PHIEN_BAN_TUONG_THICH}}
3. {{LENH_HOAC_THAO_TAC_KHOI_PHUC_THEO_THU_TU}}
4. {{KIEM_TRA_DU_LIEU_CAU_HINH_VA_LUONG_DIEU_KHIEN_TRUOC_KHI_SU_DUNG_LAI}}

| Ngày thử | Bản sao / phiên bản | Môi trường thử | Thời gian phục hồi / dữ liệu thiếu | Kết quả / bằng chứng |
|---|---|---|---|---|
| {{NGAY_HOAC_CHUA_THU}} | {{DINH_DANH}} | {{MOI_TRUONG}} | {{THUC_DO_HOAC_CHUA_CO}} | {{KET_QUA_VA_LINK}} |

## 7. Quay về phiên bản trước

- **Bản firmware / dịch vụ / cấu hình ổn định trước đó:** {{DINH_DANH_VA_NOI_LUU}}
- **Thao tác quay lại:** {{THU_TU_LENH_NAP_LAI_HOAC_CHUYEN_BAN_PHAT_HANH}}
- **Tương thích dữ liệu và migration:** {{CO_THE_DAO_NGUOC_HAY_CAN_KHOI_PHUC_BAN_SAO}}
- **Dữ liệu phát sinh sau cập nhật:** {{CACH_GIU_HOAC_CHAP_NHAN_MAT_DU_LIEU_THEO_MUC_TIEU}}
- **Điều kiện xác nhận phục hồi thành công:** {{TC_CHI_SO_VA_THOI_GIAN_THEO_DOI}}
- **Ngày đã thử quy trình và bằng chứng:** {{NGAY_KET_QUA_HOAC_CHUA_THU}}

## 8. Xử lý sự cố

| Triệu chứng | Kiểm tra ban đầu | Cách giảm ảnh hưởng | Cách khôi phục | Khi nào chuyển người phụ trách khác |
|---|---|---|---|---|
| {{SU_CO}} | {{CAC_DIEM_KIEM_TRA_VA_LOG}} | {{HANH_DONG_VOI_TAI_VA_DICH_VU}} | {{CAC_BUOC}} | {{DIEU_KIEN_VA_DAU_MOI}} |

**Mẫu ghi nhận sự cố:** {{THOI_GIAN_PHAM_VI_ANH_HUONG_PHIEN_BAN_BANG_CHUNG_HANH_DONG_NGUYEN_NHAN_VA_VIEC_PHONG_NGUA}}.

## 9. Bảo trì và bàn giao

| Công việc | Chu kỳ / điều kiện | Người thực hiện | Điều kiện hoàn tất / bằng chứng |
|---|---|---|---|
| {{KIEM_TRA_NGUON_DAY_CAM_BIEN_HIEU_CHUAN}} | {{TAN_SUAT}} | {{HO_TEN}} | {{TIEU_CHI}} |
| {{KIEM_TRA_SAO_LUU_QUYEN_CHUNG_CHI_CAP_NHAT}} | {{TAN_SUAT}} | {{HO_TEN}} | {{TIEU_CHI}} |

**Hồ sơ bàn giao:** {{DANH_MUC_THIET_BI_PHIEN_BAN_TAI_LIEU_QUYEN_TRUY_CAP_DA_CAP_VA_LOI_CON_MO}}.  
**Người nhận / ngày xác nhận:** {{HO_TEN_NGAY}}.  
**Phần chưa đáp ứng điều kiện vận hành và cách xử lý:** {{NOI_DUNG_HOAC_KHONG_CO}}.
