# ĐỀ XUẤT 03 — SMART CLASSROOM MONITORING SYSTEM

**Đề tài:** Hệ thống giám sát môi trường phòng học  
**Trường/Khoa/Lớp/Nhóm:** Nhóm bổ sung trước khi nộp  
**Thành viên tạm:** A, B, C  
**Hình thức:** Sản phẩm thật, mô hình điện áp thấp  
**Thời gian:** 5 tuần; mỗi thành viên 3 buổi/tuần, 2–3 giờ/buổi. Bản tối đa điểm nâng cao thay thế mốc 4 tuần trước.

Bản này theo [Yêu cầu thuyết minh dự án](<docs/CQ_YÊU CẦU THUYẾT MINH DỰ ÁN.pdf>) và [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>). Đây là phương án **ưu tiên theo quỹ thời gian**, chưa phải bản PDF nộp chính thức: cần bổ sung bìa, thông tin thành viên, ảnh 3D ngoài/trong, ảnh linh kiện và định dạng PDF theo quy định. Vì các chức năng đã cam kết trong thuyết minh chỉ được đổi tối đa một chức năng, nhóm nên xác nhận phạm vi trước khi nộp.

## 1. Giới thiệu

### 1.1. Tổng quan

Một ESP32 giám sát nhiệt độ/độ ẩm và chuyển động trong phòng học, đưa dữ liệu qua MQTT đến backend rồi hiển thị trên website. Người dùng bật/tắt đèn LED mô hình từ web; một cảm biến ánh sáng riêng kích còi khi phòng quá tối theo ngưỡng thử nghiệm. Backend lưu lịch sử lên cloud và gửi cảnh báo nhanh khi có chuyển động trong chế độ canh gác. Sản phẩm giúp người quản lý theo dõi trạng thái phòng từ xa và kiểm chứng hai chiều dữ liệu IoT với mô hình nhỏ, rẻ, dễ đóng hộp.

### 1.2. Danh sách chức năng

| ID | Loại, điểm tối đa theo C.1/C.2 | Thiết bị/dịch vụ | Luồng và kết quả kiểm chứng | Chủ sở hữu |
|---|---|---|---|---|
| F01 | Căn bản: input → web | DHT11 | DHT11 → ESP32 → MQTT → backend → frontend; hiện nhiệt độ, độ ẩm, thời điểm đo. | A |
| F02 | Căn bản: input → web | PIR HC-SR501 | PIR → ESP32 → MQTT → backend → frontend; hiện chuyển động/cập nhật mới nhất. | B |
| F03 | Căn bản: web → output | LED xanh | Frontend → backend → MQTT → ESP32 → LED; trả trạng thái bật/tắt thực tế. | C |
| F04 | Nâng cao #1, 1,5 điểm | Cảm biến ánh sáng CDS → buzzer | CDS → ESP32 → buzzer khi tối; thử ngưỡng tại chỗ, độc lập với LED F03. | C |
| F05 | Nâng cao #4, 1,5 điểm | Firebase RTDB | Backend lưu bản ghi DHT11/PIR và sự kiện LED theo thời gian. | A |
| F06 | Nâng cao #10, 2,0 điểm | Website tự xây | Tự xây backend/frontend, trang số đo, nút LED, trạng thái kết nối; không dùng Node-RED. | B |
| F07 | Nâng cao #6, 1,0 điểm | Telegram Bot | Backend gửi thông báo nhanh khi PIR báo chuyển động lúc bật chế độ canh gác, có chặn lặp. | C |
| F08 | Nâng cao #9, 1,5 điểm | SQLite tài khoản | A làm đăng ký/đăng nhập, băm mật khẩu và bảo vệ nút LED cùng trang lịch sử. | A |
| F09 | Nâng cao #12, 1,0 điểm | WiFiManager, sản phẩm thật | A cho phép nhập WiFi mới từ cổng cấu hình ESP32, kiểm tra kết nối lại MQTT. | A |
| F10 | Nâng cao #5, 1,5 điểm | Firebase RTDB | B đọc dữ liệu theo thời gian từ cloud F05 qua backend và vẽ chart trên website. | B |
| F11 | Nâng cao #8, 0,5 điểm | Chatbot luật điều kiện | B cho ô chat trả lời số đo/trạng thái mới nhất từ backend theo câu hỏi định sẵn. | B |
| F12 | Nâng cao #2, 1,5 điểm | Nút nhấn riêng → web | C đọc nút xác nhận phòng đã kiểm tra → ESP32 → MQTT → backend → frontend, hiện thời điểm. | C |

**Đối chiếu thiết bị:** F01 = DHT11, F02 = PIR, F03 = LED xanh, F04 = CDS **và** buzzer, F12 = nút nhấn riêng. Sáu thiết bị input/output vật lý này **đôi một khác nhau**. F05–F11 là dịch vụ/chức năng phần mềm, không đăng ký thêm luồng thiết bị; mỗi yêu cầu nâng cao có đúng một chủ sở hữu. ESP32 là board trung gian. Sản phẩm thật nên quy tắc thay thế trong giả lập không áp dụng. Cần xác nhận với giảng viên nếu quy định “thiết bị khác nhau” được hiểu bao gồm cả việc các dịch vụ cloud/chart/thông báo dùng lại dữ liệu cảm biến.

## 2. Thiết kế

### 2.1. Bố trí ngoài và trong

Mặt hộp có lỗ thoáng cho DHT11, cửa sổ hướng nhìn của PIR, lỗ ánh sáng cho CDS, LED, nút xác nhận F12 và lỗ âm của buzzer. ESP32, dây tín hiệu và đầu nối đặt trong hộp; nguồn USB 5V cấp qua cổng của board. Không điều khiển tải điện lưới. DHT11 tránh gần nguồn nhiệt; PIR hướng về vùng cửa, CDS tránh bị LED F03 chiếu trực tiếp.

```text
Mặt ngoài: [DHT11 F01] [PIR F02] [CDS F04] [LED xanh F03] [buzzer F04] [nút F12]
Mặt trong: [ESP32] [dây + điện trở LED] [đầu nối] [cổng USB cấp nguồn]
```

Trước khi xuất PDF: dựng **hai hình 3D ngoài/trong** và đánh dấu từng vị trí F01–F04 và F12; đây là đầu ra của Tuần 5, chưa có trong bản khảo sát này.

### 2.2. Wireframe website

```text
┌──────────────────────────────────────────────────────────┐
│ GIÁM SÁT PHÒNG HỌC | ESP32/MQTT online/offline | F08     │
├─────────────────────────────┬────────────────────────────┤
│ Nhiệt độ/độ ẩm F01         │ Chuyển động F02            │
│ Cập nhật lần cuối           │ Cập nhật lần cuối          │
├─────────────────────────────┴────────────────────────────┤
│ Bật/tắt LED F03 | Bật/tắt chế độ canh gác cho F07       │
│ Lịch sử F05; biểu đồ cloud F10; thông báo F07            │
│ Nút xác nhận F12 và thời điểm; ô chat điều kiện F11       │
└──────────────────────────────────────────────────────────┘
```

Website F06 có vùng F01–F03, F05, F07–F08 và F10–F12. Chế độ canh gác là thiết lập phần mềm của cảnh báo F07, không thêm một thiết bị output.

### 2.3. Sơ đồ dữ liệu chung

```mermaid
flowchart LR
  DHT["DHT11 F01"] --> ESP["ESP32"]
  PIR["PIR F02"] --> ESP
  CDS["CDS F04"] --> ESP
  ESP --> BUZ["Buzzer F04"]
  ESP -->|MQTT: room/telemetry, room/motion| MQ["Broker MQTT"]
  MQ --> BE["Web backend F06"]
  BE --> FE["Web frontend F06"]
  FE -->|HTTP: LED on/off F03| BE
  BE -->|MQTT: room/led/set| MQ
  MQ --> ESP
  ESP --> LED["LED xanh F03"]
  ESP -->|MQTT: room/led/state| MQ
  BE -->|bản ghi có thời gian F05| DB["Firebase RTDB"]
  BE -->|cảnh báo F07| TG["Telegram"]
  BTN["Nút xác nhận F12"] --> ESP
  BE --> AUTH["SQLite tài khoản F08"]
  DB -->|đọc F10| BE
  BE -->|chart/chat F10/F11| FE
  PHONE["Điện thoại cấu hình WiFi F09"] --> ESP
```

MQTT chỉ truyền dữ liệu qua backend trước khi đến frontend. ESP32 công bố trạng thái LED thực sau lệnh để phân biệt lệnh gửi và tác động đã xảy ra. Khi broker mất kết nối, còi F04 vẫn chạy nội bộ; website hiển thị trạng thái mất kết nối.

F09 cấu hình WiFi tại ESP32 thật; F08 bảo vệ website, F10 hiển thị chart lấy từ Firebase, F11 trả lời theo luật điều kiện. Nút F12, mục xác nhận, chart và chat đã có trong bản phác thảo; khi xuất PDF tô màu/mẫu mũi tên theo từng luồng.

### 2.4. Một số dự án ESP32 có mã nguồn đã khảo sát

| Dự án gốc | Có thể tham khảo | Khác biệt so với hai PDF |
|---|---|---|
| [Smart Classroom: MQTT + Flask](https://github.com/221110/IoT-Based-Smart-Classroom-Environment-Monitoring-and-Alert-System-With-Real-Time-Dashboard) | Có mã backend Flask và giao diện mẫu cho phòng học. | README xác nhận đây chỉ là bản giữa kỳ, MQTT dùng dữ liệu **mô phỏng**, chưa có phần cứng ESP32; chỉ tham khảo khung backend, phải tự làm firmware và kiểm chứng MQTT thật. |
| [SmartHome — ESP32 + MQTT + Flask](https://github.com/anjulameegalla/Group-Project-BTDT_24_51) | Có firmware, `app.py`, trang web; README mô tả cả chiều cảm biến → MQTT → Flask → web và web → Flask → MQTT → LED/relay. Đây là mẫu **gần nhất với C.1** của PDF quy định. | Repo dùng broker công khai và nhiều thiết bị; tách quyền sở hữu từng yêu cầu, không dùng lại input/output giữa F01–F04, giữ cấu hình mạng bí mật. |
| [IoT_Project — ESP32 + MQTT + Flask](https://github.com/PhucHuwu/IoT_Project) | Có thư mục `hardware`, `backend`, `frontend`, mã `.ino` và topic MQTT telemetry/control/action-history; hữu ích cho F01–F03 và F06. | Bản gốc dùng MongoDB, nhiều LED; đề xuất này giữ một LED cho F03 và Firebase RTDB cho F05, không sao chép nguyên kiến trúc nặng. |
| [Greenhouse Monitor — MQTT + Node.js](https://github.com/danieladarve/greenhouse-monitor) | Có firmware ESP32, backend, dashboard và Telegram với giới hạn tần suất; tham khảo cách kiểm thử F07 và xử lý bản ghi có thời gian. | Dự án gốc dùng ba ESP32 và Raspberry Pi; đề xuất phòng học chỉ cần một ESP32 và backend chạy trên máy nhóm. |
| [Smart Greenhouse System — ESP32 mô phỏng](https://github.com/Devenford/smart-greenhouse-system) | Có backend Node.js/MQTT và dữ liệu lịch sử, là mẫu tham khảo luồng cloud/dashboard. | README nói node cảm biến chạy trên Wokwi; không coi đây là bằng chứng vận hành phần cứng thật. |
| [EdgeGuard ESP32](https://github.com/AyushmanRaha/EdgeGuard-ESP32) | Firmware DHT11, cảm biến khác, điều khiển relay, giao diện web và kiểm thử logic. | Web gốc chạy trên ESP32 qua HTTP; không thay thế backend/MQTT bắt buộc của C.1. |
| [Smart Home IoT](https://github.com/DavidKShi/smart-home-iot) | DHT11, PIR, LED và dashboard đơn giản; phù hợp lắp mẫu đầu tiên. | Cần dựng backend trung gian và MQTT, phân quyền sở hữu từng chức năng. |
| [Smart Dustbin](https://github.com/shm230605/Smart-Dustbin-System) | Phương án khác: thùng rác tự mở nắp, đo mức đầy, có firmware và mô phỏng. | Cần bổ sung backend MQTT và một output web độc lập; cơ khí nắp tăng rủi ro lịch 4 tuần. |
| [Car Parking System](https://github.com/O2sa/Car-Parking-System) | Phương án khác: HC-SR04, servo, mô hình bãi xe và code ESP32. | Mẫu gốc dùng web server trên ESP32, không có backend MQTT; hai cảm biến/servo và cơ khí làm phương án này nặng hơn. |

**Xếp hạng theo quỹ giờ:** phòng học (ưu tiên) → thùng rác → bãi xe. Đây là suy luận từ số linh kiện, công cơ khí và mức sửa kiến trúc cần thiết; không phải kết quả thử nghiệm độc lập. Nhờ hai repo SmartHome và IoT_Project, phương án phòng học có nguồn tham khảo rõ cho luồng C.1, nhưng nhóm vẫn phải tự triển khai, kiểm thử và ghi nguồn trong báo cáo để bảo đảm tính trung thực.

## 3. Triển khai

### 3.1. Linh kiện và dự toán

Giá tham khảo tra ngày **28/10/2026**, đơn vị VND. Link sản phẩm có ảnh linh kiện để nhóm chèn vào PDF. Giá vận chuyển và vật tư mô hình chưa được xác minh.

| STT | Linh kiện | SL | Đơn giá | Thành tiền | Nguồn giá/tình trạng | ID |
|---|---|---:|---:|---:|---|---|
| 1 | ESP32 DevKit V1 | 1 | 140.000 | 140.000 | [Linh Kiện Việt Nam](https://linhkienvietnam.vn/module-node-mcu-32s-esp32-devkitc-dung-module-esp-wroom-32) | F01–F04 |
| 2 | DHT11 ASAIR | 1 | 27.000 | 27.000 | [Hshop](https://hshop.vn/cam-bien-do-am-nhiet-do-dht11) | F01 |
| 3 | PIR HC-SR501 | 1 | 27.000 | 27.000 | [Hshop](https://hshop.vn/cam-bien-chuyen-dong-pir-5v-2) | F02 |
| 4 | LED xanh + điện trở | 1 bộ | 8.000 | 8.000 | **Ước tính**, chọn đúng điện trở khi lắp | F03 |
| 5 | CDS Light Sensor | 1 | 15.000 | 15.000 | [Hshop](https://hshop.vn/cam-bien-anh-sang-quang-tro-2) | F04 |
| 6 | Buzzer 5VDC | 1 | 15.000 | 15.000 | **Ước tính**, [mẫu tham khảo](https://hshop.vn/coi-buzzer-5vdc) | F04 |
| 7 | Adapter 5V 2A | 1 | 30.000 | 30.000 | [Linh Kiện Việt Nam](https://linhkienvietnam.vn/nguon-adapter-5v-2a-5v2a-kho-b-ka9h14); cần dây/đầu USB phù hợp | F01–F04 |
| 8 | Hộp, dây, breadboard hoặc PCB đục lỗ | 1 bộ | 60.000 | 60.000 | **Ước tính**, chọn kích thước sau khi bố trí | F01–F04 |
| 9 | Nút nhấn F12 | 1 | 5.000 | 5.000 | **Ước tính**, [nhóm sản phẩm Hshop](https://hshop.vn/dieu-khien-ban-phim-joystick) | F12 |
| | **Tổng tham khảo** | | | **327.000** | Chưa gồm vận chuyển, công cụ và dịch vụ | |

Firebase và Telegram dự kiến dùng mức miễn phí nếu phù hợp hạn mức thực tế. Không cấp trực tiếp buzzer/LED vượt khả năng GPIO; kiểm tra dòng, điện trở và driver theo linh kiện mua được.

### 3.2. Kế hoạch thực hiện và kiểm tra sức chứa thời gian

Giả định mỗi người tăng thêm một giờ so với mức 1–2 giờ/ngày trước đó: **3 người × 3 buổi/tuần × 2–3 giờ/buổi × 4 tuần = 72–108 giờ-người** (mức giữa **90 giờ-người**). Ước lượng dưới đây là giờ làm tập trung, không tính chờ giao hàng; một số phần chạy song song.

| Tuần | ID | Công việc và đầu ra kiểm chứng | Chủ sở hữu | Ước giờ |
|---|---|---|---|---:|
| 1 | F01 | Lắp DHT11, firmware publish MQTT, backend nhận và frontend hiện số đo | A | 6–8 |
| 1 | F02 | Lắp PIR, publish MQTT, backend/frontend hiện sự kiện; dựng khung website F06 | B | 6–8 |
| 2 | F03 | Lệnh từ frontend qua backend/MQTT tới LED, nhận trạng thái xác nhận | C | 5–7 |
| 2 | F04 | CDS → buzzer, thử ngưỡng và thử khi ngắt WiFi | C | 3–5 |
| 2–3 | F05 | Lưu bản ghi theo thời gian trên Firebase, đọc lại mẫu dữ liệu | A | 5–7 |
| 2–3 | F06 | Hoàn thiện website tự xây, cập nhật online/offline, tích hợp API của A/C | B | 7–9 |
| 3 | F07 | Telegram Bot, chế độ canh gác và giới hạn gửi lặp | C | 3–5 |
| 4 | F01–F07 | Tích hợp, kiểm thử toàn luồng, đóng hộp, ảnh 3D, ảnh linh kiện, thuyết minh/PDF, tập vấn đáp | A điều phối; B/C cùng làm | 10–14 |
| | | **Tổng ước tính** | | **45–63** |

**Phạm vi nền F01–F07** cần 45–63 giờ-người theo bảng trên. Các dòng tích hợp của Tuần 4 được chuyển sang Tuần 5 khi thêm F08–F12; đây là ước lượng công việc, không phải giờ đã đo thực tế.

**Kế hoạch nâng cao để đạt trần dự kiến:** F08 đăng nhập 7–10 giờ (A), F09 WiFiManager 4–6 giờ (A), F10 chart cloud 5–7 giờ (B), F11 chatbot luật 2–3 giờ (B), F12 nút → web 4–6 giờ (C); tích hợp và vấn đáp thêm 4–6 giờ. Tổng mới **71–101 giờ-người**. Quỹ 4 tuần 72–108 giờ chỉ đủ ở phía thuận lợi; để có dự phòng, kéo sang **5 tuần = 90–135 giờ-người**. Tuần 4 làm F08/F09/F10/F12, Tuần 5 làm F11 và kiểm thử toàn hệ thống/PDF. Bảng tuần 1–4 phía trên là lịch nền của F01–F07; mốc tích hợp cuối cùng chuyển sang Tuần 5.

| Tuần mở rộng | ID | Chủ sở hữu | Giờ | Đầu ra kiểm chứng |
|---|---|---|---:|---|
| 4 | F08, F09 | A | 11–16 | Đăng nhập có băm mật khẩu; cấu hình lại WiFi và MQTT |
| 4 | F10 | B | 5–7 | Chart đọc bản ghi Firebase qua backend |
| 5 | F11 | B | 2–3 | Chatbot trả lời theo luật và dữ liệu mới nhất |
| 4 | F12 | C | 4–6 | Nút riêng hiện thời điểm trên web qua MQTT |
| 5 | F01–F12 | Cả nhóm | 4–6 tăng thêm | Kiểm thử tích hợp và vấn đáp, ngoài giờ tích hợp nền đã chuyển sang Tuần 5 |

## 4. Tổng kết và phân chia công việc

Theo C.1 của [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>), mỗi người có một luồng căn bản qua MQTT, backend và frontend; tối đa **4 điểm chức năng + 1 điểm tích hợp nhóm** nếu làm và giải thích được. C.2 cho phép tối đa **4 điểm nâng cao/người**, nhưng điểm dự kiến ở đây chỉ cộng những yêu cầu đã phân công; không coi điểm là được bảo đảm. Điểm báo cáo cuối kỳ tối đa 1 và khoản cộng xét tối đa 1 cho sản phẩm thật nằm ngoài bảng. Công thức cuối kỳ còn nhân hệ số hiểu bài **K** theo vấn đáp.

| Thành viên | ID và phần bàn giao chính | Căn bản gồm nhóm | Nâng cao | Tổng tạm tính chưa gồm báo cáo |
|---|---|---:|---:|---:|
| A | F01; F05 cloud 1,5 + F08 bảo mật 1,5 + F09 WiFi 1,0 | 5,0 | 4,0 | 9,0 |
| B | F02; F06 web 2,0 + F10 chart cloud 1,5 + F11 chatbot 0,5 | 5,0 | 4,0 | 9,0 |
| C | F03; F04 CDS → buzzer 1,5 + F07 Telegram 1,0 + F12 nút → web 1,5 | 5,0 | 4,0 | 9,0 |

**Rà soát trước nộp:** xác nhận cách chấm dữ liệu F05/F07/F10; đo giờ thực tế nhóm có thể làm; kiểm tra sáu thiết bị của F01–F04/F12 không trùng; thử mọi luồng qua MQTT/backend/frontend; chèn ảnh 3D ngoài/trong, ảnh linh kiện có ID, màu mũi tên phân biệt trong sơ đồ; điền bìa và xuất PDF đúng tên `MANHOM_MSSV1_MSSV2_MSSV3_PROPOSAL.PDF`, Times New Roman 13, giãn dòng 1,15, canh đều.
