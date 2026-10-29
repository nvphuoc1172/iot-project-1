# Báo cáo tổng kết — {{TEN_DU_AN}}

**Trường / đơn vị:** {{TEN_DON_VI}}  
**Môn học / khách hàng:** {{THONG_TIN}}  
**Nhóm và thành viên:** {{HO_TEN_MSSV_HOAC_VAI_TRO}}  
**Giảng viên / người hướng dẫn:** {{HO_TEN}}  
**Phiên bản sản phẩm / commit:** {{PHIEN_BAN}}  
**Trạng thái báo cáo:** {{NHAP_DANG_RA_SOAT_DA_CHOT}}  
**Người phụ trách:** {{HO_TEN}}  
**Cập nhật:** {{YYYY-MM-DD}}

> Tổng hợp kết quả từ tài liệu thiết kế và bằng chứng kiểm thử. Phân biệt rõ mục tiêu ban đầu, phần đã làm và phần chưa kiểm chứng. Điều chỉnh bố cục, trang bìa và định dạng xuất PDF theo yêu cầu nơi nhận. Xem [cách dùng bộ mẫu](README.md).

## Tóm tắt

{{TOM_TAT_BAI_TOAN_GIAI_PHAP_PHAM_VI_KET_QUA_CHINH_VA_HAN_CHE_TRONG_MOT_DOAN}}

**Từ khóa:** {{CAC_TU_KHOA}}.

**Mục lục:** {{TAO_SAU_KHI_CHOT_BO_CUC_VA_SO_TRANG}}.

## 1. Giới thiệu và mục tiêu

- **Bối cảnh và vấn đề:** {{VAN_DE_THUC_TE_VA_DOI_TUONG_SU_DUNG}}
- **Mục tiêu ban đầu:** {{KET_QUA_MONG_MUON_KEM_CHI_SO}}
- **Phạm vi thực hiện:** {{THIET_BI_DIA_DIEM_SO_NGUOI_DUNG_THOI_GIAN}}
- **Ràng buộc:** {{NGAN_SACH_HA_TANG_THOI_GIAN}}
- **Yêu cầu làm căn cứ:** {{THAM_CHIEU_REQUIREMENTS_VA_PHIEN_BAN}}

## 2. Cơ sở và khảo sát giải pháp

Chỉ trình bày kiến thức cần để hiểu thiết kế. Dẫn nguồn cho thông số, phương pháp và nội dung tham khảo.

| Giải pháp / nguồn | Phần liên quan | Ưu điểm / giới hạn | Phần dự án kế thừa hoặc điều chỉnh |
|---|---|---|---|
| {{TEN_VA_NGUON}} | {{THANH_PHAN_HOAC_PHUONG_PHAP}} | {{NHAN_XET_CO_CO_SO}} | {{DONG_GOP_CUA_NHOM}} |

## 3. Phân tích yêu cầu

**Tài liệu yêu cầu chi tiết:** {{DUONG_DAN}}.

| ID | Yêu cầu tóm tắt | Tiêu chí nghiệm thu | Ưu tiên | Thay đổi so với đề xuất |
|---|---|---|---|---|
| {{F_NF_ID}} | {{NOI_DUNG}} | {{NGUONG_VA_DIEU_KIEN}} | {{MUC_UU_TIEN}} | {{THAY_DOI_VA_LY_DO_HOAC_KHONG_CO}} |

## 4. Thiết kế hệ thống

### 4.1. Kiến trúc và luồng xử lý

{{SO_DO_TONG_THE_VA_GIAI_THICH_TRACH_NHIEM_TUNG_THANH_PHAN}}

**Quyết định thiết kế chính và lý do:** {{TOM_TAT_CAC_ADR_QUAN_TRONG}}.  
**Tham chiếu:** {{TAI_LIEU_ARCHITECTURE}}.

### 4.2. Phần cứng và mô hình

{{SO_DO_MACH_ANH_MO_HINH_VA_CAC_THONG_SO_QUAN_TRONG}}

**BOM và chi phí phần cứng:** {{TOM_TAT_VA_THAM_CHIEU_HARDWARE}}.  
**Giới hạn giả lập / phần cứng thật:** {{NOI_DUNG}}.

### 4.3. Phần mềm, dữ liệu và giao tiếp

{{CAC_KHOI_FIRMWARE_BACKEND_UI_LUU_TRU_VA_LUONG_LENH_PHAN_HOI}}

**Tham chiếu hợp đồng API/MQTT và schema:** {{TAI_LIEU_INTERFACES}}.

## 5. Triển khai thực tế

- **Công nghệ và phiên bản đã dùng:** {{DANH_SACH_NGAN}}
- **Môi trường triển khai:** {{THIET_BI_MANG_DICH_VU}}
- **Chức năng đã tích hợp:** {{CAC_F_ID_KEM_ANH_VA_CHU_THICH}}
- **Khó khăn và cách giải quyết:** {{VAN_DE_NGUYEN_NHAN_CACH_SUA_VA_KET_QUA}}
- **Cách tái lập:** {{THAM_CHIEU_SETUP_COMMIT_CAU_HINH_KHONG_CHUA_BI_MAT}}

## 6. Kiểm thử và đánh giá

**Phương pháp và môi trường:** {{TOM_TAT_DIEU_KIEN_DO_CONG_CU_SO_MAU}}.  
**Nhật ký và dữ liệu thô:** {{THAM_CHIEU_TESTING_VA_BANG_CHUNG}}.

| Yêu cầu / chỉ số | Mục tiêu | Kết quả thực tế | Test case / bằng chứng | Đánh giá |
|---|---|---|---|---|
| {{F_NF_ID}} | {{NGUONG_VA_DIEU_KIEN}} | {{KET_QUA_HOAC_CHUA_DO}} | {{TC_ID_VA_DUONG_DAN}} | {{DAT_KHONG_DAT_CHUA_DU_CO_SO}} |

**Phân tích:** {{Y_NGHIA_KET_QUA_SAI_LECH_SO_VOI_MUC_TIEU_VA_GIOI_HAN_PHEP_DO}}.

## 7. Tổ chức thực hiện và chi phí

| Thành viên | Phần thực hiện | Đầu ra kiểm chứng | Chênh lệch với phân công ban đầu |
|---|---|---|---|
| {{HO_TEN}} | {{F_ID_VA_CONG_VIEC}} | {{COMMIT_TAI_LIEU_TC_HOAC_MACH}} | {{NOI_DUNG_VA_LY_DO}} |

**Tiến độ và chi phí dự kiến so với thực tế:** {{TOM_TAT_THAM_CHIEU_PROJECT_PLAN_VA_BOM}}.

## 8. Kết luận và hướng phát triển

- **Mục tiêu đã đạt:** {{CAC_ID_VA_BANG_CHUNG_CHINH}}
- **Mục tiêu chưa đạt / chưa kiểm chứng:** {{CAC_ID_NGUYEN_NHAN_VA_ANH_HUONG}}
- **Hạn chế khi dùng thực tế:** {{GIOI_HAN_QUY_MO_DO_TIN_CAY_VA_DIEU_KIEN_SU_DUNG}}
- **Bài học rút ra:** {{BAI_HOC_CU_THE_TU_DU_AN}}
- **Hướng phát triển:** {{HANG_MUC_UU_TIEN_VA_DIEU_KIEN_CAN_CO}}

## 9. Tài liệu tham khảo

| Mã | Tác giả / đơn vị | Tên tài liệu và liên kết | Phiên bản / ngày truy cập | Phần được sử dụng / giấy phép nếu có |
|---|---|---|---|---|
| REF01 | {{DON_VI}} | {{TEN_VA_URL}} | {{PHIEN_BAN_NGAY}} | {{NOI_DUNG_VA_DIEU_KIEN_SU_DUNG}} |

## 10. Phụ lục và hồ sơ bàn giao

| Hạng mục | Đường dẫn / phiên bản | Ghi chú |
|---|---|---|
| Mã nguồn và bản phát hành | {{REPO_TAG_COMMIT}} | {{HUONG_DAN_LAY_MA}} |
| Thiết kế mạch và mô hình | {{TEP_GOC_VA_ANH}} | {{REVISION}} |
| Hướng dẫn cài đặt và sử dụng | {{SETUP_VA_USER_GUIDE}} | {{DOI_TUONG_DOC}} |
| Dữ liệu và bằng chứng kiểm thử | {{TESTING_EVIDENCE}} | {{GIOI_HAN_CHIA_SE_NEU_CO}} |
| Kịch bản / video demo | {{DEMO_SLIDE_VIDEO}} | {{NGAY_VA_PHIEN_BAN}} |
| Tài liệu vận hành | {{OPERATIONS_HOAC_KHONG_AP_DUNG}} | {{DAU_MOI_BAN_GIAO}} |
