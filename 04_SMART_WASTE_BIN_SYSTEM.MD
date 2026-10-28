# ĐỀ XUẤT 04 — SMART WASTE BIN SYSTEM

**Đề tài:** Thùng rác thông minh giám sát mức đầy  
**Trường/Khoa/Lớp/Nhóm:** Nhóm bổ sung  
**Thành viên tạm:** A, B, C  
**Hình thức:** Sản phẩm thật, điện áp thấp  
**Thời gian:** 4 tuần; 3 buổi/tuần × 2–3 giờ/buổi/người.

Theo [Yêu cầu thuyết minh dự án](<docs/CQ_YÊU CẦU THUYẾT MINH DỰ ÁN.pdf>) và [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>). Đây là bản khảo sát để chọn đề tài; trước khi nộp phải thêm bìa, tên/MSSV, ảnh 3D ngoài/trong, ảnh linh kiện và xuất PDF đúng định dạng. Chỉ được đổi tối đa một chức năng sau khi chốt thuyết minh.

## 1. Giới thiệu

### 1.1. Tổng quan

Mô hình thùng rác đo khoảng cách đến mặt rác để ước lượng mức đầy và phát hiện bàn tay ở gần nắp bằng cảm biến hồng ngoại riêng. Dữ liệu từ ESP32 đi qua MQTT, backend đến website. Người quản lý có thể ra lệnh mở nắp bằng servo từ web; một công tắc từ gắn ở nắp sẽ kích buzzer khi nắp bị giữ mở quá lâu. Backend lưu lịch sử và gửi Telegram khi thùng gần đầy. Mô hình tập trung vào theo dõi trạng thái, điều khiển và cảnh báo; cơ cấu nắp dùng bìa cứng/nhựa nhẹ để giảm tải servo.

### 1.2. Danh sách chức năng

| ID | Loại, điểm theo PDF | Thiết bị/dịch vụ | Luồng và đầu ra kiểm chứng | Chủ sở hữu |
|---|---|---|---|---|
| F01 | Căn bản input → web | HC-SR04 đo mức đầy | Cảm biến → ESP32 → MQTT → backend → frontend hiện khoảng cách/% đầy. | A |
| F02 | Căn bản input → web | Cảm biến vật cản IR | IR → ESP32 → MQTT → backend → frontend hiện có/không có tay gần nắp. | B |
| F03 | Căn bản web → output | Servo SG90 | Frontend → backend → MQTT → ESP32 → servo mở nắp tối đa vài giây rồi đóng; phản hồi trạng thái. | C |
| F04 | Nâng cao #1, 1,5 điểm | Công tắc từ → buzzer | Công tắc từ ở nắp → ESP32 → buzzer nếu nắp mở quá thời gian, chạy cục bộ khi mất mạng. | A |
| F05 | Nâng cao #4, 1,5 điểm | Firebase RTDB | Backend lưu mức đầy và sự kiện mở nắp theo thời gian. | B |
| F06 | Nâng cao #10, 2,0 điểm | Website tự xây | Backend/frontend hiển thị F01–F03, lịch sử F05, nút mở nắp; không dùng Node-RED. | B |
| F07 | Nâng cao #6, 1,0 điểm | Telegram Bot | Backend cảnh báo thùng gần đầy liên tục, giới hạn gửi lặp. | C |

**Kiểm tra thiết bị:** F01 = HC-SR04, F02 = IR, F03 = SG90, F04 = công tắc từ **và** buzzer. Năm thiết bị input/output khác nhau; servo F03 không dùng trong F04. F05–F07 là dịch vụ/website dùng dữ liệu đã phát sinh, không thêm thiết bị vật lý. Mỗi ID có một chủ sở hữu. Đây là sản phẩm thật; nếu chuyển sang giả lập phải kiểm lại quy tắc tối đa một thiết bị thay thế. Việc cloud/thông báo dùng lại dữ liệu F01/F03 cần xác nhận với giảng viên nếu quy tắc “khác thiết bị” được hiểu bao gồm dữ liệu thứ cấp.

## 2. Thiết kế

### 2.1. Bố trí ngoài và trong

HC-SR04 đặt dưới mặt nắp, hướng xuống lòng thùng; IR hướng ra trước để nhận biết tay; công tắc từ gắn giữa nắp và thân, tách khỏi vùng quét IR. Servo nối bản lề nắp nhẹ. ESP32, dây, nguồn và buzzer ở hộp khô phía sau. HC-SR04 loại thông dụng có chân Echo mức 5V; dùng chia áp/level shifter trước chân GPIO ESP32. Servo cấp nguồn 5V riêng phù hợp dòng, nối chung mass với ESP32; không kéo dòng servo từ GPIO.

```text
Ngoài: [IR F02] [nắp + công tắc từ F04] [lỗ âm buzzer F04]
Trong nắp: [HC-SR04 F01 hướng xuống] [servo SG90 F03]
Hộp khô sau thùng: [ESP32] [chia áp Echo] [nguồn 5V] [đầu nối]
```

Khi xuất PDF cần hình 3D cả ngoài và trong, đánh dấu ID của từng linh kiện.

### 2.2. Wireframe website

```text
┌─────────────────────────────────────────────────────────┐
│ THÙNG RÁC THÔNG MINH — MQTT online/offline               │
├───────────────────────┬─────────────────────────────────┤
│ Mức đầy F01           │ Tay gần nắp F02                │
│ Cảnh báo F07          │ Nút MỞ NẮP F03; trạng thái nắp │
├───────────────────────┴─────────────────────────────────┤
│ Lịch sử mức đầy / lần mở nắp F05                        │
└─────────────────────────────────────────────────────────┘
```

### 2.3. Sơ đồ truyền và nhận dữ liệu

```mermaid
flowchart LR
  U["HC-SR04 F01"] --> E["ESP32"]
  IR["IR F02"] --> E
  M["Công tắc từ F04"] --> E
  E --> BZ["Buzzer F04"]
  E -->|MQTT: bin/level, bin/hand| MQ["MQTT broker"]
  MQ --> BE["Backend F06"]
  BE --> FE["Frontend F06"]
  FE -->|HTTP: mở nắp F03| BE
  BE -->|MQTT: bin/lid/set| MQ
  MQ --> E
  E --> S["Servo F03"]
  E -->|MQTT: bin/lid/state| MQ
  BE -->|lưu thời gian F05| DB["Firebase RTDB"]
  BE -->|thông báo F07| TG["Telegram"]
```

Nắp tự đóng theo bộ đếm trên ESP32 dù backend mất mạng. Buzzer F04 cũng chạy cục bộ. Backend gửi trạng thái offline nếu quá thời gian không nhận telemetry.

### 2.4. Dự án tương tự có mã nguồn

| Nguồn | Phần hữu ích | Điều chỉnh theo hai PDF |
|---|---|---|
| [Smart Dustbin System](https://github.com/shm230605/Smart-Dustbin-System) | Có mã ESP32, sơ đồ, Wokwi, HC-SR04, servo và cảnh báo. | Bản gốc không có đúng luồng MQTT → backend → frontend và web → output; phải tự xây F01–F03 theo C.1. |
| [IoT Smart Waste Bin](https://github.com/PamudaUposath/iot-smart-waste-bin) | Firmware ESP32, MQTT, điều khiển nắp và mức đầy. | Dashboard gốc dùng Node-RED; F06 của đề xuất phải là website tự xây. |
| [SmartHome ESP32 + Flask](https://github.com/anjulameegalla/Group-Project-BTDT_24_51) | Mẫu kiến trúc MQTT hai chiều qua backend Flask. | Chỉ tham khảo kiến trúc; thay cảm biến và tách thiết bị theo từng ID của thùng rác. |

Các repo là nguồn học tập, không chứng minh mô hình của nhóm đã chạy; cần tự tích hợp, kiểm thử và trích dẫn trung thực.

## 3. Triển khai

### 3.1. Linh kiện và dự toán

Giá tham khảo tra ngày **28/10/2026**, VND. Link sản phẩm có ảnh để chèn vào PDF. Các khoản ghi “ước tính” cần tra báo giá trước khi mua.

| STT | Linh kiện | SL | Đơn giá | Thành tiền | Nguồn giá/tình trạng | ID |
|---|---|---:|---:|---:|---|---|
| 1 | ESP32 DevKit V1 | 1 | 140.000 | 140.000 | [Linh Kiện Việt Nam](https://linhkienvietnam.vn/module-node-mcu-32s-esp32-devkitc-dung-module-esp-wroom-32) | F01–F04 |
| 2 | HC-SR04 | 1 | 27.000 | 27.000 | [Hshop](https://hshop.vn/cam-bien-sieu-am-srf04) | F01 |
| 3 | IR phát hiện vật cản | 1 | 15.000 | 15.000 | [Hshop](https://hshop.vn/cam-bien-vat-can-hong-ngoai-v1-2) | F02 |
| 4 | Servo SG90 | 1 | 42.000 | 42.000 | [Hshop](https://hshop.vn/dong-co-rc-servo-9g) | F03 |
| 5 | Công tắc từ MC-38 | 1 | 12.000 | 12.000 | [Shopee](https://shopee.vn/C%E1%BA%A3m-bi%E1%BA%BFn-c%E1%BB%ADa-MC-38-%28t%E1%BB%AB-tr%C6%B0%E1%BB%9Dng%29-TH334-i.310609561.3173442342); kiểm tra biến thể | F04 |
| 6 | Buzzer 5V | 1 | 15.000 | 15.000 | **Ước tính**, [mẫu](https://hshop.vn/coi-buzzer-5vdc) | F04 |
| 7 | Adapter 5V 2A + dây/đầu cấp nguồn | 1 bộ | 40.000 | 40.000 | [Adapter 30.000đ](https://linhkienvietnam.vn/nguon-adapter-5v-2a-5v2a-kho-b-ka9h14) + dây ước tính 10.000đ | F01–F04 |
| 8 | Hộp/thùng mô hình, bản lề, dây, chia áp/PCB | 1 bộ | 100.000 | 100.000 | **Ước tính**, cần chọn sau khi đo kích thước | F01–F04 |
| | **Tổng tham khảo** | | | **391.000** | Chưa gồm vận chuyển/công cụ/dịch vụ | |

### 3.2. Kế hoạch 4 tuần

Quỹ nhóm: **3 người × 3 ngày/tuần × 2–3 giờ/ngày × 4 tuần = 72–108 giờ-người**. Dự toán công cho F01–F07 khoảng **60–82 giờ-người**, gồm lắp cơ khí, website, cloud, cảnh báo, kiểm thử và PDF. Mốc dưới 72 giờ vẫn có rủi ro nếu nắp kẹt hoặc giao hàng chậm.

| Tuần | ID | Đầu ra kiểm chứng | Chủ sở hữu | Giờ ước tính |
|---|---|---|---|---:|
| 1 | F01, F04 | Chốt cơ khí; mức đầy MQTT → web; công tắc từ → buzzer | A | 12–16 |
| 1–2 | F02, F05, F06 | IR MQTT → web; khung backend/frontend; lưu lịch sử Firebase | B | 14–19 |
| 2 | F03 | Web → MQTT → servo; tự đóng khi hết thời gian | C | 10–14 |
| 3 | F06, F07 | Tích hợp dashboard, Telegram; thử quá mức đầy/mất kết nối | B cho F06; C cho F07 | 10–13 |
| 4 | F01–F07 | Hoàn thiện nắp/hộp, kiểm tra toàn luồng, hình 3D/ảnh linh kiện, PDF và vấn đáp | A điều phối; B/C hỗ trợ | 14–20 |
| | | **Tổng** | | **60–82** |

Mỗi ID chỉ có một chủ sở hữu; dòng Tuần 4 là công tích hợp chung. Ở mức 108 giờ có dự phòng 26–48 giờ, ở mức 72 giờ có thể thiếu tối đa 10 giờ. Chỉ nên chốt đề tài khi nhóm có thể dành gần **2,5–3 giờ/ngày/người** hoặc đã thử cơ khí nắp trước Tuần 1.

## 4. Tổng kết và phân chia công việc

Theo C.1 của [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>), mỗi người có một luồng căn bản; điểm tối đa khi làm và giải thích được là **4 chức năng + 1 tích hợp nhóm**. C.2 tối đa **4 nâng cao/người**; bản này ưu tiên kịp tiến độ nên chưa đạt trần nâng cao. Điểm báo cáo tối đa 1 và khoản cộng xét sản phẩm thật tối đa 1 tính riêng; điểm cuối kỳ còn phụ thuộc hệ số hiểu bài K.

| Thành viên | ID và bàn giao | Căn bản gồm nhóm | Nâng cao | Tổng tạm tính chưa gồm báo cáo |
|---|---|---:|---:|---:|
| A | F01 cảm biến mức; F04 công tắc từ/buzzer | 5,0 | 1,5 | 6,5 |
| B | F02 IR; F05 Firebase; F06 website | 5,0 | 3,5 | 8,5 |
| C | F03 servo; F07 Telegram | 5,0 | 1,0 | 6,0 |

**Rà soát nộp:** năm thiết bị F01–F04 đôi một khác nhau; một chủ sở hữu/ID; ảnh 3D ngoài/trong và ảnh linh kiện có ID; sơ đồ duy nhất có mũi tên/màu phân biệt; giá có link; thử nắp khi mất MQTT; PDF đúng tên `MANHOM_MSSV1_MSSV2_MSSV3_PROPOSAL.PDF`, Times New Roman 13, giãn dòng 1,15, canh đều.
