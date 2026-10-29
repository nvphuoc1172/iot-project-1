# Thiết kế phần cứng — {{TEN_DU_AN}}

**Phiên bản:** {{PHIEN_BAN}}  
**Trạng thái:** {{NHAP_DANG_RA_SOAT_DA_CHOT}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Điền đúng model và biến thể linh kiện đang dùng. Nếu giả lập, ghi rõ phần nào được giả lập và phần nào chưa kiểm chứng trên phần cứng thật. Xem [cách dùng bộ mẫu](README.md).

## 1. Tổng quan mô hình

- **Board và phiên bản mạch:** {{MODEL_BOARD_REVISION}}
- **Kích thước, vị trí lắp, môi trường sử dụng:** {{MO_TA}}
- **Chức năng liên quan:** {{CAC_F_ID}}
- **Bản vẽ, ảnh lắp đặt, tệp mô phỏng:** {{DUONG_DAN_TEP_VA_PHIEN_BAN}}

## 2. Danh sách linh kiện và vật tư (BOM)

**Đơn vị tiền:** {{DON_VI}}. **Ngày tham khảo giá:** {{NGAY}}. Đơn giá cần gắn đúng model, biến thể và nguồn tham khảo.

| ID | Linh kiện / model cụ thể | Thông số cần dùng | SL | Đơn giá | Thành tiền | Nguồn / datasheet | Chức năng |
|---|---|---|---:|---:|---:|---|---|
| HW01 | {{TEN_MODEL}} | {{DIEN_AP_DONG_DAI_DO_GIAO_TIEP}} | {{SL}} | {{GIA}} | {{SL_NHAN_GIA}} | {{NGUON}} | {{F_ID}} |
| HW02 | {{TEN_MODEL}} | {{THONG_SO}} | {{SL}} | {{GIA}} | {{THANH_TIEN}} | {{NGUON}} | {{F_ID}} |
| | **Tổng linh kiện** | | | | **{{TONG}}** | | |

**Chi phí khác:** {{DAY_HOP_DAU_NOI_VAN_CHUYEN_DU_PHONG}}. **Tổng dự toán phần cứng:** {{TONG_VA_CACH_TINH}}.

## 3. Sơ đồ nguyên lý và bảng đấu nối

**Sơ đồ nguyên lý:** {{DUONG_DAN_BAN_VE_CO_NHAN_CHAN_VA_NGUON}}.  
**Ảnh đấu nối thực tế:** {{DUONG_DAN_ANH_DANH_DAU_HW_ID}}.

| Linh kiện | Chân linh kiện | Chân board / GPIO | Chiều tín hiệu | Mức logic / nguồn | Điện trở / driver / ghi chú |
|---|---|---|---|---|---|
| {{HW_ID}} | {{TEN_CHAN}} | {{SO_CHAN_VA_TEN_GPIO}} | {{IN_OUT_HAI_CHIEU_NGUON}} | {{GIA_TRI}} | {{GHI_CHU}} |

- **Ràng buộc chân:** {{CHAN_BOOT_CHAN_DANH_RIENG_ADC_HOAC_CHUC_NANG_XUNG_DOT_THEO_BOARD}}
- **Mức tác động:** {{ACTIVE_HIGH_ACTIVE_LOW_VA_TRANG_THAI_KHI_RESET}}
- **Điểm nối mass và cách nối nguồn:** {{MO_TA_THEO_SO_DO}}
- **Phần chuyển mức / bảo vệ / cách ly:** {{THIET_KE_VA_CO_SO_CHON}}

## 4. Thiết kế nguồn và tải

| Nhánh nguồn / tải | Điện áp định mức | Dòng thường / đỉnh | Nguồn hoặc driver sử dụng | Cách xác minh |
|---|---|---|---|---|
| {{BOARD_CAM_BIEN_CO_CAU_CHAP_HANH}} | {{V}} | {{DONG_MA_HOAC_A}} | {{MODEL_VA_DINH_MUC}} | {{DATASHEET_HOAC_KET_QUA_DO}} |

- **Ngân sách dòng và phần dự phòng:** {{PHEP_TINH_TAI_DONG_THOI_KE_CA_LUC_KHOI_DONG}}
- **Dòng / áp giới hạn tại GPIO:** {{GIOI_HAN_THEO_TAI_LIEU_BOARD_VA_CACH_DAM_BAO}}
- **Trạng thái cơ cấu chấp hành khi cấp nguồn, reset, mất điều khiển:** {{TRANG_THAI_VA_CACH_DAM_BAO}}
- **Biện pháp cho tải đặc thù:** {{CHONG_XUNG_NGUOC_CAU_CHI_CACH_DIEN_CHONG_NUOC_NEU_LIEN_QUAN}}

## 5. Lắp đặt và kiểm tra ban đầu

| Bước | Thao tác | Kết quả cần có | Điểm đo / bằng chứng |
|---|---|---|---|
| 1 | {{KIEM_TRA_SO_DO_CUC_TINH_VA_DAU_NOI_KHI_CHUA_CAP_NGUON}} | {{DIEU_KIEN_DAT}} | {{DIEM_KIEM_TRA}} |
| 2 | {{KIEM_TRA_NGUON_TRUOC_KHI_GAN_TAI}} | {{DAI_DIEN_AP_CHO_PHEP}} | {{DIEM_DO}} |
| 3 | {{CHAY_THU_TUNG_CAM_BIEN_VA_TAI}} | {{TIN_HIEU_MONG_DOI}} | {{LOG_ANH_VIDEO}} |
| 4 | {{CHAY_DONG_THOI_VA_KHOI_DONG_LAI}} | {{DIEU_KIEN_DAT}} | {{TC_ID}} |

## 6. Hiệu chuẩn cảm biến

| Cảm biến | Thiết bị / mẫu tham chiếu | Quy trình và điều kiện | Công thức / hệ số | Sai số chấp nhận | Lưu hệ số ở đâu |
|---|---|---|---|---|---|
| {{HW_ID}} | {{THAM_CHIEU}} | {{CAC_DIEM_DO_SO_LAN_DO}} | {{CONG_THUC_DON_VI}} | {{NGUONG_THEO_NF_ID}} | {{TEP_HOAC_BO_NHO}} |

**Kết quả hiệu chuẩn:** {{THAM_CHIEU_BANG_SO_LIEU_TRONG_TESTING}}.  
**Khi nào cần hiệu chuẩn lại:** {{CHU_KY_HOAC_SU_KIEN}}.

## 7. Giới hạn và lịch sử thay đổi

| Phiên bản mạch / ngày | Thay đổi | Lý do | Ảnh hưởng firmware / kiểm thử |
|---|---|---|---|
| {{REV_NGAY}} | {{THAY_DOI}} | {{LY_DO}} | {{TEP_VA_TC_CAN_CAP_NHAT}} |

**Giới hạn mô hình và phần chưa kiểm chứng:** {{NOI_DUNG}}.
