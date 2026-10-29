# Kiểm thử và kết quả — {{TEN_DU_AN}}

**Phiên bản tài liệu:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_KIEM_THU_DA_TONG_KET}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Lập tiêu chí trước khi chạy thử. Chỉ ghi đạt khi có kết quả thực tế và bằng chứng. Các hàng gợi ý không phải kết quả đã chạy. Xem [cách dùng bộ mẫu](README.md).

## 1. Phạm vi và điều kiện kiểm thử

- **Yêu cầu đầu vào:** {{DUONG_DAN_REQUIREMENTS_VA_PHIEN_BAN}}
- **Trong phạm vi / chưa kiểm thử:** {{CAC_ID_VA_LY_DO}}
- **Firmware / backend / UI:** {{COMMIT_TAG_HOAC_BINARY_HASH}}
- **Phần cứng và cấu hình:** {{BOARD_REV_CAM_BIEN_NGUON_NGUONG_CAU_HINH}}
- **Mạng và dịch vụ:** {{SO_THIET_BI_TOPOLOGY_PHIEN_BAN_DICH_VU}}
- **Công cụ đo và dữ liệu thử:** {{THIET_BI_THAM_CHIEU_SCRIPT_MAU_DU_LIEU}}
- **Điều kiện bắt đầu / dừng thử:** {{CAC_DIEU_KIEN}}

## 2. Ma trận yêu cầu và test case

| Yêu cầu | Mục đích kiểm tra | Test case | Loại kiểm thử | Người thực hiện |
|---|---|---|---|---|
| F01 | {{HANH_VI_CAN_CHUNG_MINH}} | TC01 | {{DON_LE_TICH_HOP_TOAN_LUONG}} | {{HO_TEN}} |
| {{NF_ID}} | {{THUOC_TINH_CAN_DO}} | {{TC_ID}} | {{DO_HIEU_NANG_HOAC_THU_LOI}} | {{HO_TEN}} |

**Quy tắc đánh giá:** `Đạt / Không đạt / Bị chặn / Chưa chạy`. Không tính các trường hợp chưa chạy hoặc bị chặn là đạt.

## 3. Test case chi tiết

Sao chép khối này cho mỗi test case; lưu từng lần chạy ở bảng kết quả để giữ lịch sử.

### TC01 — {{TEN_TEST_CASE}}

- **Yêu cầu liên quan:** {{F_NF_ID}}
- **Mục tiêu:** {{DIEU_CAN_CHUNG_MINH}}
- **Điều kiện trước:** {{TRANG_THAI_THIET_BI_DU_LIEU_QUYEN_MANG}}
- **Đầu vào:** {{GIA_TRI_PAYLOAD_THAO_TAC}}
- **Các bước:**
  1. {{BUOC_1}}
  2. {{BUOC_2}}
  3. {{BUOC_3}}
- **Kết quả mong đợi:** {{DAU_RA_VA_TRANG_THAI_QUAN_SAT_DUOC}}
- **Ngưỡng đạt:** {{GIA_TRI_DON_VI_SO_LAN_TY_LE_DAT_THEO_REQUIREMENTS}}
- **Cách đo:** {{DIEM_BAT_DAU_KET_THUC_CONG_CU_NGUON_DONG_HO}}
- **Cách đưa hệ thống về trạng thái ban đầu:** {{THAO_TAC_RESET_DU_LIEU_VA_TAI}}

## 4. Các tình huống IoT cần cân nhắc

Chọn tình huống áp dụng và tạo test case chi tiết; ghi lý do khi không áp dụng.

| Tình huống | Cách tạo điều kiện | Điều cần quan sát | Test case / lý do không áp dụng |
|---|---|---|---|
| Mất Wi-Fi rồi kết nối lại | {{CACH_NGAT_VA_THOI_GIAN}} | Trạng thái tải, UI, dữ liệu và quá trình kết nối lại | {{TC_ID}} |
| Broker / backend dừng | {{CACH_DUNG_VA_KHOI_PHUC}} | Phát hiện lỗi, hành vi cục bộ và khôi phục | {{TC_ID}} |
| Mất điện / khởi động lại | {{TRANG_THAI_TRUOC_KHI_NGAT_NGUON}} | Trạng thái đầu ra lúc boot, cấu hình và lệnh cũ | {{TC_ID}} |
| Cảm biến lỗi / dữ liệu quá cũ | {{CACH_MO_PHONG_HOAC_NGAT}} | Cờ chất lượng, cảnh báo và logic tự động | {{TC_ID}} |
| Lệnh trùng / hết hạn / sai thứ tự | {{CAC_PAYLOAD_VA_THU_TU_GUI}} | Không gây thao tác ngoài chính sách đã chốt | {{TC_ID}} |
| Tham số không hợp lệ | {{NULL_NGOAI_DAI_SAI_KIEU}} | Bị từ chối đúng hợp đồng, có thông báo phù hợp | {{TC_ID}} |
| Không đủ quyền | {{TAI_KHOAN_HOAC_THONG_TIN_XAC_THUC_SAI}} | Không đọc/điều khiển ngoài quyền | {{TC_ID}} |
| Tải đồng thời / chạy kéo dài | {{SO_THIET_BI_TAN_SUAT_THOI_LUONG}} | Độ trễ, dữ liệu mất, lỗi hoặc reboot | {{TC_ID}} |
| Chuyển thủ công / tự động | {{CHUOI_SU_KIEN}} | Quy tắc ưu tiên và trạng thái nhất quán | {{TC_ID}} |

## 5. Nhật ký các lần chạy

| Lần chạy / ngày | Test case | Người chạy | Bản build / cấu hình | Kết quả thực tế | Trạng thái | Bằng chứng | Lỗi liên quan |
|---|---|---|---|---|---|---|---|
| {{RUN_ID_NGAY}} | TC01 | {{HO_TEN}} | {{COMMIT_PROFILE}} | {{CHUA_CO_KET_QUA}} | Chưa chạy | {{DUONG_DAN}} | {{ISSUE_ID_HOAC_KHONG_CO}} |

**Nơi lưu bằng chứng:** {{VI_DU_THU_MUC_DOCS_EVIDENCE_RUN_ID}}. Ghi test case, thời gian và phiên bản trong tên tệp hoặc chú thích; che thông tin bí mật và dữ liệu cá nhân trước khi chia sẻ.

## 6. Số liệu đo và cách tính

| Chỉ số | Dữ liệu thô / tệp | Số mẫu | Cách tính | Kết quả thực đo | Mục tiêu | Kết luận |
|---|---|---|---|---|---|---|
| {{DO_TRE_SAI_SO_TY_LE_THANH_CONG}} | {{DUONG_DAN}} | {{N}} | {{CONG_THUC_DON_VI_CACH_XU_LY_MAU_LOI}} | {{CHUA_DO_HOAC_GIA_TRI}} | {{NF_ID_NGUONG}} | {{CHUA_DU_CO_SO_HOAC_KET_LUAN}} |

Nếu dùng timestamp từ nhiều máy/thiết bị, mô tả cách đồng bộ hoặc sai số phép đo: {{PHUONG_PHAP}}.

## 7. Lỗi và kiểm thử lại

| Mã lỗi | Test case / lần chạy | Triệu chứng và mức ảnh hưởng | Người xử lý | Bản sửa | Lần chạy lại / trạng thái |
|---|---|---|---|---|---|
| BUG01 | {{TC_RUN_ID}} | {{MO_TA}} | {{HO_TEN}} | {{COMMIT_HOAC_CHUA_SUA}} | {{RUN_ID_HOAC_CHUA_CHAY_LAI}} |

## 8. Tổng kết và nghiệm thu

- **Số test case:** {{TONG}} = {{DAT}} đạt + {{KHONG_DAT}} không đạt + {{BI_CHAN}} bị chặn + {{CHUA_CHAY}} chưa chạy. Với test đã chạy nhiều lần, dùng lần chạy mới nhất trên bản được nghiệm thu.
- **Yêu cầu chưa được kiểm chứng:** {{CAC_ID_VA_LY_DO}}
- **Lỗi còn mở / giới hạn phép thử:** {{NOI_DUNG_VA_ANH_HUONG}}
- **Kết luận:** {{DU_DIEU_KIEN_CHUA_DU_DIEU_KIEN_HOAC_NGHIEM_THU_CO_DIEU_KIEN}}
- **Người xác nhận và ngày:** {{HO_TEN_NGAY}}
