rer

# Yêu cầu và phạm vi —}

**Phiên bản:** {{PHIEN_BAN}}**Trạng thái:** {{NHAP_DANG_RA_SOAT_DA_CHOT}}**Người phụ trách:** {{HO_TEN}}**Cập nhật:** {{YYYY-MM-DD}}

> Thay các biến `{{...}}`. Tài liệu này quản lý yêu cầu chính thức; kế hoạch, thiết kế và kiểm thử tham chiếu các ID tại đây. Xem [cách dùng bộ mẫu](README.md).

## 1. Bài toán và mục tiêu

- **Vấn đề hiện tại:** {{VAN_DE_VA_BOI_CANH_SU_DUNG}}
- **Người gặp vấn đề:** {{DOI_TUONG}}
- **Mục tiêu:** {{KET_QUA_MONG_MUON_VA_CACH_DO}}
- **Điều kiện triển khai:** {{SAN_PHAM_THAT_HAY_GIA_LAP_DIA_DIEM_SO_THIET_BI}}
- **Tài liệu đầu vào:** {{DE_XUAT_YEU_CAU_MON_HOC_HOAC_YEU_CAU_KHACH_HANG}}

## 2. Người dùng và tình huống sử dụng

| Vai trò    | Nhu cầu    | Quyền được cấp         | Tình huống sử dụng |
| ----------- | ----------- | --------------------------- | ---------------------- |
| {{VAI_TRO}} | {{NHU_CAU}} | {{XEM_DIEU_KHIEN_CAU_HINH}} | {{BOI_CANH_TAN_SUAT}}  |

## 3. Phạm vi và giả định

| Nhóm           | Nội dung                                  | Cách xác nhận / người chịu trách nhiệm |
| --------------- | ------------------------------------------ | ---------------------------------------------- |
| Trong phạm vi  | {{CHUC_NANG_THIET_BI_KHU_VUC_DUOC_HO_TRO}} | {{NGUOI_XAC_NHAN}}                             |
| Ngoài phạm vi | {{VIEC_KHONG_CAM_KET_TRONG_PHIEN_BAN_NAY}} | {{LY_DO}}                                      |
| Giả định     | {{DIEU_KIEN_DANG_GIA_DINH}}                | {{CACH_KIEM_CHUNG_VA_HAN}}                     |
| Ràng buộc     | {{NGAN_SACH_THOI_GIAN_HA_TANG_QUY_DINH}}   | {{NGUON_RANG_BUOC}}                            |

## 4. Yêu cầu chức năng

Mỗi hàng mô tả một hành vi kiểm chứng được. Dùng mức ưu tiên `Bắt buộc / Nên có / Có thể bổ sung`.

| ID  | Chức năng và tác nhân | Đầu vào / điều kiện trước | Kết quả cần có       | Ưu tiên       | Người phụ trách |
| --- | -------------------------- | --------------------------------- | ------------------------ | --------------- | ------------------- |
| F01 | {{CHUC_NANG}}              | {{DAU_VAO_DIEU_KIEN}}             | {{DAU_RA_QUAN_SAT_DUOC}} | {{MUC_UU_TIEN}} | {{HO_TEN}}          |
| F02 | {{CHUC_NANG}}              | {{DAU_VAO_DIEU_KIEN}}             | {{DAU_RA_QUAN_SAT_DUOC}} | {{MUC_UU_TIEN}} | {{HO_TEN}}          |

### Luồng chi tiết cho}

- **Tác nhân và điều kiện trước:** {{AI_KHOI_TAO_TRANG_THAI_CAN_CO}}
- **Luồng chính:** {{CAC_BUOC_TU_KICH_HOAT_DEN_KET_QUA}}
- **Luồng thay thế:** {{VI_DU_CHUYEN_CHE_DO_THU_CONG}}
- **Luồng lỗi:** {{MAT_MANG_DU_LIEU_SAI_KHONG_DU_QUYEN}}
- **Điều kiện sau:** {{TRANG_THAI_THIET_BI_DU_LIEU_VA_GIAO_DIEN}}

Lặp phần này cho chức năng cần làm rõ.

## 5. Yêu cầu chất lượng và xử lý sự cố

Ghi giá trị, đơn vị, điều kiện đo và khoảng thời gian quan sát. Tránh các mô tả chỉ có “nhanh”, “ổn định” hoặc “chính xác”.

| ID   | Thuộc tính                             | Mục tiêu / hành vi                            | Điều kiện và cách đo                          |
| ---- | ---------------------------------------- | ------------------------------------------------ | --------------------------------------------------- |
| NF01 | Độ trễ                                | {{GIOI_HAN_VA_DON_VI}}                           | {{DIEM_BAT_DAU_KET_THUC_SO_LAN_DO_TAI_HE_THONG}}    |
| NF02 | Sai số cảm biến                       | {{SAI_SO_CHO_PHEP}}                              | {{THIET_BI_THAM_CHIEU_DAI_DO_DIEU_KIEN_MOI_TRUONG}} |
| NF03 | Dữ liệu quá cũ hoặc cảm biến lỗi | {{NGUONG_XAC_DINH_VA_PHAN_HOI}}                  | {{CACH_NGAT_CAM_BIEN_HOAC_NGUNG_GUI_DU_LIEU}}       |
| NF04 | Mất mạng / broker                      | {{HANH_VI_CUC_BO_VA_KET_NOI_LAI}}                | {{THOI_GIAN_NGAT_VA_CACH_KHOI_PHUC}}                |
| NF05 | Khởi động lại / mất điện          | {{TRANG_THAI_DAU_RA_VA_CAU_HINH_CAN_KHOI_PHUC}}  | {{CAC_TRANG_THAI_TRUOC_KHI_TAT_NGUON}}              |
| NF06 | Truy cập và dữ liệu                  | {{QUYEN_TRUY_CAP_DU_LIEU_DUOC_LUU_THOI_HAN_LUU}} | {{KIEM_TRA_QUYEN_VA_XOA_DU_LIEU}}                   |

**Ví dụ minh họa:** “Trong mạng thử nghiệm đã mô tả, ít nhất 19/20 lệnh bật được thiết bị xác nhận đã áp dụng trong 3 giây; đo từ lúc người dùng gửi lệnh.” Đây là ví dụ cách viết, chưa phải cam kết của dự án.

## 6. Tiêu chí nghiệm thu và truy vết

| Yêu cầu | Điều kiện thử | Kết quả được chấp nhận | Test case | Người xác nhận |
| --------- | ----------------- | ----------------------------- | --------- | ------------------ |
| F01       | {{GIVEN}}         | {{WHEN_THEN_KEM_NGUONG_DO}}   | TC01      | {{HO_TEN}}         |
| NF01      | {{DIEU_KIEN_DO}}  | {{NGUONG_VA_TY_LE_DAT}}       | {{TC_ID}} | {{HO_TEN}}         |

**Điều kiện nghiệm thu chung:** {{YEU_CAU_BAT_BUOC_PHAI_DAT_LOI_NAO_KHONG_DUOC_CON_VA_TAI_LIEU_CAN_BAN_GIAO}}.

## 7. Câu hỏi còn mở và thay đổi phạm vi

| Mã | Vấn đề / yêu cầu thay đổi | Ảnh hưởng        | Người xử lý | Hạn     | Quyết định / trạng thái  |
| --- | -------------------------------- | ------------------- | --------------- | -------- | ----------------------------- |
| Q01 | {{NOI_DUNG}}                     | {{ID_CHI_PHI_LICH}} | {{HO_TEN}}      | {{NGAY}} | {{CHUA_CHOT_HOAC_QUYET_DINH}} |

## 8. Lịch sử cập nhật

| Ngày    | Phiên bản   | Thay đổi và lý do         | Người xác nhận |
| -------- | ------------- | ----------------------------- | ------------------ |
| {{NGAY}} | {{PHIEN_BAN}} | {{THAY_DOI_CAC_ID_LIEN_QUAN}} | {{HO_TEN}}         |
