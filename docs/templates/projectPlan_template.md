# Kế hoạch và tiến độ — {{TEN_DU_AN}}

**Phiên bản:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_THUC_HIEN_DA_TONG_KET}}  
**Người điều phối:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Lập kế hoạch từ các yêu cầu đã chọn. Ghi tiến độ bằng đầu ra kiểm chứng được và phân biệt mốc dự kiến với thực tế. Xem [cách dùng bộ mẫu](README.md).

## 1. Mục tiêu và đầu vào

- **Khoảng thời gian:** {{NGAY_BAT_DAU}} đến {{NGAY_KET_THUC}}
- **Phạm vi cam kết:** {{THAM_CHIEU_REQUIREMENTS_VA_PHIEN_BAN}}
- **Ngân sách tối đa:** {{SO_TIEN_VA_DON_VI}}
- **Nhân lực / thời gian khả dụng:** {{SO_THANH_VIEN_VA_GIO_MOI_TUAN}}
- **Mốc cố định:** {{NGAY_BAO_CAO_DEMO_NGHIEM_THU}}

## 2. Thành viên và trách nhiệm

| Thành viên | Phần phụ trách chính | ID yêu cầu | Sản phẩm bàn giao | Người phối hợp / rà soát |
|---|---|---|---|---|
| {{HO_TEN}} | {{PHAN_CONG}} | {{F_NF_ID}} | {{MACH_CODE_TAI_LIEU_BANG_CHUNG}} | {{HO_TEN}} |

## 3. Công việc và phụ thuộc

| Mã việc | Công việc / ID yêu cầu | Đầu ra và điều kiện hoàn tất | Người chính | Phụ thuộc | Công sức dự kiến | Bắt đầu / hạn | Trạng thái / bằng chứng |
|---|---|---|---|---|---|---|---|
| W01 | {{CONG_VIEC_F_ID}} | {{DAU_RA_KIEM_CHUNG_DUOC}} | {{HO_TEN}} | {{MA_VIEC_HOAC_KHONG_CO}} | {{GIO_NGUOI}} | {{CAC_NGAY}} | {{CHUA_LAM_DANG_LAM_BI_CHAN_XONG_VA_LINK}} |

**Tiêu chí hoàn tất chung:** {{BUILD_CHAY_DUOC_KIEM_THU_LIEN_QUAN_DAT_TAI_LIEU_CAP_NHAT_VA_NGUOI_RA_SOAT}}.

## 4. Các mốc bàn giao

| Mốc | Ngày dự kiến | Đầu ra / điều kiện chấp nhận | Người xác nhận | Ngày thực tế | Sai lệch và cách xử lý |
|---|---|---|---|---|---|
| Chốt phạm vi | {{NGAY}} | {{REQUIREMENTS_DUOC_CHOT}} | {{HO_TEN}} | {{CHUA_HOAN_TAT_HOAC_NGAY}} | {{NOI_DUNG}} |
| Chạy được luồng đầu tiên | {{NGAY}} | {{F_ID_VA_TC_ID}} | {{HO_TEN}} | {{NGAY}} | {{NOI_DUNG}} |
| Tích hợp chức năng bắt buộc | {{NGAY}} | {{CAC_DIEU_KIEN}} | {{HO_TEN}} | {{NGAY}} | {{NOI_DUNG}} |
| Kiểm thử và bàn giao | {{NGAY}} | {{BAO_CAO_KET_QUA_TAI_LIEU_DEMO}} | {{HO_TEN}} | {{NGAY}} | {{NOI_DUNG}} |

Thêm khoảng dự phòng cho mua linh kiện, tích hợp và sửa lỗi: {{SO_NGAY_VA_CACH_BO_TRI}}.

## 5. Ngân sách và mua sắm

Chi tiết linh kiện được quản lý trong tài liệu phần cứng: {{DUONG_DAN_BOM}}. Bảng này tổng hợp chi phí toàn dự án.

| Nhóm chi phí | Dự toán | Thực chi | Người theo dõi | Ghi chú / bằng chứng |
|---|---:|---:|---|---|
| Linh kiện và vật tư theo BOM | {{SO_TIEN}} | {{SO_TIEN_HOAC_CHUA_CHI}} | {{HO_TEN}} | {{THAM_CHIEU}} |
| Dịch vụ / hosting / kết nối | {{SO_TIEN}} | {{SO_TIEN}} | {{HO_TEN}} | {{CHU_KY_TINH_PHI}} |
| Vận chuyển và chi phí khác | {{SO_TIEN}} | {{SO_TIEN}} | {{HO_TEN}} | {{CHI_TIET}} |
| Dự phòng | {{SO_TIEN}} | {{SO_TIEN}} | {{HO_TEN}} | {{DIEU_KIEN_SU_DUNG}} |
| **Tổng** | **{{TONG}}** | **{{TONG}}** | | {{CHENH_LECH_SO_VOI_NGAN_SACH}} |

**Linh kiện có thời gian chờ dài:** {{MODEL_NGAY_CAN_DAT_NGAY_CAN_CO_VA_PHUONG_AN_THAY_THE}}.

## 6. Rủi ro và phương án xử lý

| ID | Rủi ro | Khả năng / tác động | Dấu hiệu kích hoạt | Phòng ngừa | Phương án khi xảy ra | Người theo dõi |
|---|---|---|---|---|---|---|
| R01 | {{RUI_RO}} | {{THAP_VUA_CAO_VA_CO_SO}} | {{DAU_HIEU}} | {{HANH_DONG_SOM}} | {{PHUONG_AN_DU_PHONG}} | {{HO_TEN}} |

## 7. Cập nhật định kỳ và thay đổi kế hoạch

| Ngày | Đầu ra hoàn thành / bằng chứng | Việc tiếp theo | Vướng mắc / người gỡ | Thay đổi mốc hoặc phạm vi |
|---|---|---|---|---|
| {{NGAY}} | {{KET_QUA_VA_LINK}} | {{CONG_VIEC}} | {{VAN_DE_VA_HO_TEN}} | {{THAY_DOI_HOAC_KHONG_CO}} |

**Nhịp cập nhật và nơi theo dõi công việc:** {{TAN_SUAT_HOP_ISSUE_BOARD_HOAC_TAI_LIEU}}.  
**Cách chốt thay đổi phạm vi:** {{AI_XAC_NHAN_CACH_GHI_QUYET_DINH_VA_CAP_NHAT_REQUIREMENTS}}.
