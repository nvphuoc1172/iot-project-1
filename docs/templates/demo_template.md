# Kịch bản demo — {{TEN_DU_AN}}

**Phiên bản sản phẩm / commit:** {{PHIEN_BAN}}  
**Trạng thái kịch bản:** {{NHAP_DA_TAP_THU_DA_CHOT}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}  
**Buổi demo:** {{NGAY_GIO_MUI_GIO_DIA_DIEM}}  
**Thời lượng cho phép:** {{SO_PHUT}}  
**Người trình bày / hỗ trợ:** {{HO_TEN_VA_VAI_TRO}}

> Chọn luồng có thể trình diễn trong thời gian cho phép và ghi rõ kết quả cần quan sát. Bằng chứng quay sẵn phải có nhãn riêng khi dùng. Xem [cách dùng bộ mẫu](README.md).

## 1. Mục tiêu trình diễn

- **Người xem:** {{GIANG_VIEN_KHACH_HANG_HOAC_NHOM}}
- **Thông điệp chính:** {{BAI_TOAN_VA_GIA_TRI_CAN_CHUNG_MINH}}
- **Chức năng và yêu cầu cần chứng minh:** {{CAC_F_NF_ID}}
- **Điều kiện kết thúc thành công:** {{CAC_KET_QUA_NGUOI_XEM_CAN_THAY}}
- **Phần chưa triển khai / giới hạn cần nói rõ:** {{NOI_DUNG}}

## 2. Chuẩn bị trước buổi demo

| Hạng mục | Cần chuẩn bị / kiểm tra | Người phụ trách | Trạng thái / bằng chứng |
|---|---|---|---|
| Mô hình và nguồn | {{BOARD_CAM_BIEN_TAI_DAY_CAP_NGUON_DU_PHONG}} | {{HO_TEN}} | {{CHUA_KIEM_TRA_HOAC_KET_QUA}} |
| Mạng và dịch vụ | {{MANG_BROKER_SERVER_DIA_CHI_VA_QUYEN_TRUY_CAP}} | {{HO_TEN}} | {{KET_QUA}} |
| Cấu hình và dữ liệu mẫu | {{TAI_KHOAN_THU_NGUONG_LICH_SU_TRANG_THAI_BAN_DAU}} | {{HO_TEN}} | {{KET_QUA}} |
| Thiết bị trình chiếu | {{MAN_HINH_TRINH_DUYET_CAP_VA_CO_CHU}} | {{HO_TEN}} | {{KET_QUA}} |
| Tài liệu hỗ trợ | {{SLIDE_SO_DO_VIDEO_VA_BANG_CHUNG_TESTING}} | {{HO_TEN}} | {{KET_QUA}} |

**Cách đưa hệ thống về trạng thái bắt đầu:** {{CAC_BUOC_KEM_CACH_XAC_NHAN}}.  
**Thời gian khởi động và ổn định:** {{THOI_LUONG_DA_TAP_THU}}.

## 3. Kịch bản theo thời gian

Thay các mốc bên dưới bằng thời lượng thực tế; tổng thời gian gồm phần hỏi đáp nếu được yêu cầu.

| Thời điểm / thời lượng | Người thực hiện | Lời dẫn / thao tác | Kết quả người xem cần thấy | ID yêu cầu / bằng chứng |
|---|---|---|---|---|
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | Giới thiệu {{BAI_TOAN_VA_MUC_TIEU}} | {{GIA_TRI_CUA_SAN_PHAM}} | {{SLIDE}} |
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | {{TAO_THAY_DOI_TREN_CAM_BIEN}} | {{DU_LIEU_THUC_VA_THOI_DIEM_CAP_NHAT}} | {{F_ID_TC_ID}} |
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | {{GUI_LENH_TU_GIAO_DIEN}} | {{TAI_HOAT_DONG_VA_XAC_NHAN_TREN_UI}} | {{F_ID_TC_ID}} |
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | {{THU_TINH_HUONG_LOI_DA_CHON_NEU_AP_DUNG}} | {{PHAT_HIEN_LOI_VA_KHOI_PHUC}} | {{NF_ID_TC_ID}} |
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | {{NEU_KET_QUA_DO_HAN_CHE_VA_HUONG_PHAT_TRIEN}} | {{SO_LIEU_CO_BANG_CHUNG}} | {{TESTING_REPORT}} |
| {{MOC_THOI_GIAN}} | {{HO_TEN}} | {{HOI_DAP}} | {{CAU_TRA_LOI_VA_TAI_LIEU_DOI_CHIEU}} | {{TAI_LIEU}} |

**Tổng thời lượng dự kiến:** {{SO_PHUT}}. **Khoảng dự phòng:** {{SO_PHUT}}.

## 4. Phương án khi gặp sự cố

| Sự cố | Cách nhận biết | Cách xử lý / thời gian tối đa | Phương án trình bày thay thế |
|---|---|---|---|
| Mạng hoặc dịch vụ không hoạt động | {{DAU_HIEU}} | {{THAO_TAC_DA_TAP_THU}} | {{MANG_DU_PHONG_HOAC_VIDEO_CO_NHAN}} |
| Thiết bị hoặc cảm biến lỗi | {{DAU_HIEU}} | {{THAO_TAC_VA_GIOI_HAN}} | {{THIET_BI_DU_PHONG_HOAC_BANG_CHUNG_CU}} |
| Không đủ thời gian | {{MOC_CAN_CAT_GON}} | {{CAC_BUOC_UU_TIEN}} | {{CHUYEN_PHAN_PHU_SANG_HOI_DAP}} |

**Video / log dự phòng:** {{DUONG_DAN_NGAY_QUAY_COMMIT_VA_DIEU_KIEN_THU}}. Nêu rõ khi chuyển từ demo trực tiếp sang dữ liệu hoặc video đã ghi.

## 5. Slide và câu hỏi dự kiến

| Slide / chủ đề | Nội dung chính | Tài liệu hoặc bằng chứng hỗ trợ |
|---|---|---|
| {{SO_SLIDE_VA_TEN}} | {{NOI_DUNG_NGAN}} | {{DUONG_DAN}} |

| Câu hỏi dự kiến | Ý chính cần trả lời | Người trả lời | Tài liệu đối chiếu |
|---|---|---|---|
| {{CAU_HOI}} | {{CAU_TRA_LOI_DUA_TREN_THIET_KE_HOAC_KET_QUA_DO}} | {{HO_TEN}} | {{TAI_LIEU}} |

## 6. Ghi nhận tập thử và kết thúc

| Ngày tập | Phiên bản | Thời lượng thực tế | Lỗi / phần khó quan sát | Việc cần sửa / người phụ trách |
|---|---|---|---|---|
| {{NGAY}} | {{COMMIT_CAU_HINH}} | {{SO_PHUT}} | {{GHI_NHAN}} | {{HANH_DONG_VA_HO_TEN}} |

**Sau demo:** {{DUNG_TAI_DANG_XUAT_THU_GON_LUU_PHAN_HOI_VA_CAC_DAU_VIEC_TIEP_THEO}}.
