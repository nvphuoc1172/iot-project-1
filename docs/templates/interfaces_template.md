# Đặc tả dữ liệu và giao tiếp — {{TEN_DU_AN}}

**Phiên bản:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_RA_SOAT_DA_CHOT}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Đây là hợp đồng chung giữa firmware, backend và giao diện. Bỏ phần giao thức không sử dụng. Payload bên dưới chỉ là ví dụ minh họa. Xem [cách dùng bộ mẫu](README.md).

## 1. Quy ước chung

| Thuộc tính | Quy ước của dự án |
|---|---|
| Định danh thiết bị | {{DINH_DANG_TINH_DUY_NHAT_VA_CACH_CAP_ID}} |
| Phiên bản schema | {{TRUONG_VERSION_VA_QUY_TAC_TUONG_THICH}} |
| Mã hóa và định dạng | {{VI_DU_UTF8_JSON}} |
| Thời gian | {{DINH_DANG_MUI_GIO_NGUON_DONG_HO_CACH_XU_LY_CHUA_DONG_BO}} |
| Đơn vị và độ chính xác | {{TEN_TRUONG_DON_VI_SO_CHU_SO}} |
| Dữ liệu thiếu hoặc không hợp lệ | {{NULL_BO_TRUONG_CHAT_LUONG_DU_LIEU_HOAC_MA_LOI}} |
| Giới hạn | {{KICH_THUOC_PAYLOAD_TAN_SUAT_VA_TIMEOUT}} |

## 2. MQTT

**Môi trường và cấu hình kết nối:** {{THAM_CHIEU_SETUP_OPERATIONS_KHONG_GHI_MAT_KHAU}}.  
**Xác thực và quyền topic:** {{DANH_TINH_CLIENT_VA_PHAM_VI_PUBLISH_SUBSCRIBE}}.

| Topic | Bên gửi → bên nhận | Mục đích / ID yêu cầu | QoS | Retain | Chu kỳ / sự kiện | Schema |
|---|---|---|---|---|---|---|
| {{TOPIC_TELEMETRY}} | {{GUI_NHAN}} | {{F_ID}} | {{QOS}} | {{TRUE_FALSE_VA_LY_DO}} | {{CHU_KY}} | {{SCHEMA}} |
| {{TOPIC_COMMAND}} | {{GUI_NHAN}} | {{F_ID}} | {{QOS}} | {{TRUE_FALSE_VA_LY_DO}} | {{SU_KIEN}} | {{SCHEMA}} |
| {{TOPIC_RESULT}} | {{GUI_NHAN}} | {{F_ID}} | {{QOS}} | {{TRUE_FALSE_VA_LY_DO}} | {{SU_KIEN}} | {{SCHEMA}} |
| {{TOPIC_STATUS}} | {{GUI_NHAN}} | {{NF_ID}} | {{QOS}} | {{TRUE_FALSE_VA_LY_DO}} | {{HEARTBEAT_LWT_HOAC_KHAC}} | {{SCHEMA}} |

### Payload và quy tắc kiểm tra

**Ví dụ minh họa:** bản tin đo cảm biến; ngày giờ và giá trị là dữ liệu mẫu.

```json
{
  "schema_version": 1,
  "device_id": "device-01",
  "message_id": "boot-01:42",
  "measured_at": "2026-01-01T00:00:00Z",
  "temperature_c": 28.5,
  "quality": "valid"
}
```

| Trường | Kiểu | Bắt buộc | Đơn vị / giá trị hợp lệ | Quy tắc khi sai / thiếu |
|---|---|---|---|---|
| {{TEN_TRUONG}} | {{KIEU}} | {{CO_KHONG}} | {{DON_VI_ENUM_MIN_MAX}} | {{TU_CHOI_DANH_DAU_HOAC_MAC_DINH}} |

### Vòng đời lệnh điều khiển

- **Định danh và nội dung:** {{COMMAND_ID_TARGET_HANH_DONG_THAM_SO}}
- **Thời hạn lệnh:** {{EXPIRES_AT_HOAC_TTL_VA_CACH_KIEM_TRA_DONG_HO}}
- **Tiếp nhận và hoàn tất:** {{CAC_TRANG_THAI_ACCEPTED_APPLIED_REJECTED_FAILED_HOAC_TUONG_DUONG}}
- **Phản hồi:** {{COMMAND_ID_TRANG_THAI_THUC_TE_MA_LOI_THOI_DIEM_XU_LY}}
- **Timeout / thử lại:** {{BEN_CHIU_TRACH_NHIEM_SO_LAN_KHOANG_CHO}}
- **Lệnh trùng / sai thứ tự:** {{CACH_PHAT_HIEN_TINH_IDEMPOTENT_VA_THOI_GIAN_LUU_ID}}
- **Kết nối lại:** {{XU_LY_LENH_CU_RETAINED_HOAC_HANG_DOI_DE_KHONG_AP_DUNG_NGOAI_Y_MUON}}
- **Giới hạn xác nhận:** {{PHAN_HOI_CHI_XAC_NHAN_GPIO_HAY_CO_PHAN_HOI_VAT_LY}}

Ghi rõ chính sách giữ bản tin và hết hạn cho từng loại dữ liệu; không suy ra rằng MQTT gửi thành công đồng nghĩa tải vật lý đã hoạt động.

## 3. HTTP API hoặc giao tiếp với web

**Base URL / phiên bản:** {{DIA_CHI_THEO_MOI_TRUONG_VA_VERSION}}.  
**Cơ chế xác thực và phân quyền:** {{CO_CHE_VA_VAI_TRO}}.

| Phương thức / đường dẫn | Mục đích / ID | Quyền | Request | Response thành công | Lỗi |
|---|---|---|---|---|---|
| {{METHOD_PATH}} | {{F_ID_MO_TA}} | {{VAI_TRO}} | {{PATH_QUERY_BODY_SCHEMA}} | {{STATUS_BODY_SCHEMA}} | {{STATUS_MA_LOI}} |

### Chi tiết endpoint {{METHOD_PATH}}

- **Điều kiện trước:** {{DIEU_KIEN}}
- **Request mẫu:** {{NOI_DUNG_HOAC_DUONG_DAN_OPENAPI}}
- **Response mẫu:** {{NOI_DUNG_KEM_STATUS}}
- **Kiểm tra dữ liệu:** {{TRUONG_BAT_BUOC_GIOI_HAN}}
- **Phân trang / lọc / giới hạn tần suất:** {{QUY_UOC_NEU_CO}}
- **Cách theo dõi lệnh bất đồng bộ:** {{COMMAND_ID_ENDPOINT_HOAC_SU_KIEN_CAP_NHAT}}

Nếu dùng WebSocket/SSE, ghi URL, sự kiện, schema, xác thực và cách đồng bộ lại sau khi mất kết nối: {{DAC_TA}}.

## 4. Lưu trữ dữ liệu

**Loại kho dữ liệu:** {{DATABASE_FILE_HOAC_KHONG_LUU}}.  
**Sơ đồ quan hệ / cấu trúc:** {{DUONG_DAN_HOAC_SO_DO}}.

| Bảng / collection | Trường và kiểu | Khóa / quan hệ / index | Mục đích | Thời hạn lưu |
|---|---|---|---|---|
| {{TEN}} | {{SCHEMA}} | {{RANG_BUOC}} | {{NOI_DUNG}} | {{THOI_HAN_VA_CACH_XOA}} |

**Phân biệt thời gian đo và thời gian nhận:** {{CAC_TRUONG_VA_CACH_DUNG}}.  
**Đổi schema / migration:** {{CACH_NANG_CAP_TUONG_THICH_VA_KHOI_PHUC}}.

## 5. Mã lỗi và tương thích

| Mã | Tình huống | Bên phát hiện | Bên nhận cần làm gì | Có thử lại không |
|---|---|---|---|---|
| {{ERROR_CODE}} | {{DIEU_KIEN}} | {{THANH_PHAN}} | {{HANH_VI_HIEN_THI_HOAC_XU_LY}} | {{DIEU_KIEN_THU_LAI}} |

| Thay đổi hợp đồng | Phiên bản bị ảnh hưởng | Cách triển khai tương thích | Test case |
|---|---|---|---|
| {{THAY_DOI}} | {{FIRMWARE_BACKEND_UI}} | {{THU_TU_CAP_NHAT_HOAC_MIGRATION}} | {{TC_ID}} |
