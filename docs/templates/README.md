# Bộ template tài liệu dự án IoT

Bộ mẫu này dùng sau khi nhóm chọn đề tài, từ xác định yêu cầu đến kiểm thử, báo cáo và bàn giao. Đây là khung để điền, chưa mô tả một hệ thống đã triển khai hay kết quả đã được kiểm chứng.

## 1. Danh mục và nơi lưu bản đã điền

| Template | Mục đích | Vị trí gợi ý cho bản đã điền | Khi nào cần |
|---|---|---|---|
| [Đề xuất dự án](PROJECT_PROPOSAL_TEMPLATE.MD) | Trình bày ý tưởng, tính khả thi và dự toán ban đầu | `ideas/` | Trước khi chốt đề tài |
| [Yêu cầu và phạm vi](REQUIREMENTS_TEMPLATE.MD) | Chốt hệ thống phải làm gì và điều kiện nghiệm thu | `docs/requirements.md` | Ưu tiên đầu tiên |
| [Kiến trúc hệ thống](ARCHITECTURE_TEMPLATE.MD) | Thiết kế các thành phần và luồng xử lý | `docs/architecture.md` | Trước khi tích hợp |
| [Thiết kế phần cứng](HARDWARE_TEMPLATE.MD) | Chốt linh kiện, đấu nối, nguồn và hiệu chuẩn | `docs/hardware.md` | Trước khi lắp mạch |
| [Dữ liệu và giao tiếp](INTERFACES_TEMPLATE.MD) | Thống nhất hợp đồng API, MQTT và lưu trữ | `docs/interfaces.md` | Trước khi các phần giao tiếp với nhau |
| [Cài đặt và chạy](SETUP_TEMPLATE.MD) | Giúp thành viên khác dựng lại môi trường | `docs/setup.md` | Cập nhật ngay khi có bản chạy được |
| [Kiểm thử và kết quả](TESTING_TEMPLATE.MD) | Kiểm chứng yêu cầu và lưu bằng chứng | `docs/testing.md` | Lập kế hoạch sớm, điền kết quả khi chạy |
| [Hướng dẫn sử dụng](USER_GUIDE_TEMPLATE.MD) | Hướng dẫn người dùng thao tác | `docs/user-guide.md` | Khi luồng sử dụng ổn định |
| [Kế hoạch và tiến độ](PROJECT_PLAN_TEMPLATE.MD) | Quản lý đầu ra, người phụ trách và rủi ro | `docs/project-plan.md` | Xuyên suốt dự án |
| [Báo cáo tổng kết](REPORT_TEMPLATE.MD) | Tổng hợp thiết kế, kết quả và hạn chế | `docs/report/README.md` | Khi tổng kết đồ án hoặc giai đoạn |
| [Kịch bản demo](DEMO_TEMPLATE.MD) | Chuẩn bị trình diễn có thể lặp lại | `docs/demo.md` | Trước buổi demo/nghiệm thu |
| [Triển khai và vận hành](OPERATIONS_TEMPLATE.MD) | Triển khai, bảo mật, giám sát, khôi phục và bảo trì | `docs/operations.md` | Khi bàn giao hoặc vận hành thực tế |

## 2. Cách sử dụng

1. Sao chép mẫu cần dùng sang vị trí gợi ý. Giữ các mẫu gốc để tái sử dụng cho đề tài khác.
2. Thay các biến `{{TEN_BIEN}}`. Chỉ giữ những mục phù hợp; với mục đã rà soát nhưng không áp dụng, ghi `Không áp dụng — lý do`.
3. Các đoạn có nhãn **Ví dụ minh họa** chỉ giúp hiểu cách điền. Thay bằng thiết kế thực tế trước khi dùng làm tài liệu chính thức.
4. Ghi người phụ trách, phiên bản, ngày cập nhật và trạng thái. Mục chưa chốt phải có người xử lý và hạn hoàn thành.
5. Giữ ID nhất quán: `F01` cho chức năng, `NF01` cho yêu cầu chất lượng, `HW01` cho linh kiện, `TC01` cho kiểm thử, `R01` cho rủi ro.
6. Khi chuyển tài liệu sang thư mục khác, cập nhật đường dẫn tương đối tới ảnh, bằng chứng và tài liệu liên quan.

Một chức năng nên theo dõi được qua chuỗi: `F01 → thành phần/linh kiện → giao tiếp → TC01 → bằng chứng → kết luận nghiệm thu`.

## 3. Thứ tự soạn tài liệu

- **Chốt đề tài:** đề xuất → yêu cầu và phạm vi → kế hoạch.
- **Thiết kế:** kiến trúc → phần cứng và giao tiếp → tiêu chí kiểm thử.
- **Triển khai:** cập nhật hướng dẫn cài đặt, ghi thay đổi thiết kế và kết quả kiểm thử.
- **Bàn giao:** hướng dẫn sử dụng → báo cáo → demo; thêm vận hành nếu hệ thống tiếp tục được sử dụng.

Với nhóm nhỏ, có thể gộp tài liệu nhưng vẫn giữ đủ nội dung cần thiết. Nếu cần bắt đầu gọn, viết trước yêu cầu, kiến trúc, phần cứng, cài đặt và kiểm thử; ghi giao tiếp tối thiểu trong tài liệu kiến trúc rồi tách khi cần.

## 4. Nơi quản lý thông tin chính

| Thông tin | Tài liệu quản lý chính | Cách tài liệu khác sử dụng |
|---|---|---|
| Phạm vi, ID và tiêu chí nghiệm thu | Yêu cầu và phạm vi | Dẫn ID, tránh định nghĩa lại |
| Quyết định và sơ đồ hệ thống | Kiến trúc | Dẫn sơ đồ hoặc mục tương ứng |
| BOM, GPIO, nguồn, hiệu chuẩn | Phần cứng | Báo cáo chỉ trích bản tổng hợp |
| Payload, topic, API, schema | Dữ liệu và giao tiếp | Firmware/backend/frontend cùng đối chiếu |
| Tiến độ, phân công, dự toán tổng | Kế hoạch | Dẫn tới BOM để lấy chi phí linh kiện |
| Kết quả đo và bằng chứng | Kiểm thử | Báo cáo và demo dẫn lại kết quả |

Đối với đồ án môn học, đối chiếu thêm [yêu cầu thuyết minh](<../docs/CQ_YÊU CẦU THUYẾT MINH DỰ ÁN.pdf>) và [quy định đồ án](<../docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>). Các template bổ sung không thay thế biểu mẫu hoặc yêu cầu nộp bài của giảng viên.
