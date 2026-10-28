# ĐỀ XUẤT 06 — CHILD ROUTINE MONITORING SYSTEM

**Đề tài:** Thiết bị nhắc lịch và giám sát môi trường phòng trẻ  
**Trường/Khoa/Lớp/Nhóm:** Nhóm bổ sung trước khi nộp  
**Thành viên tạm:** A, B, C  
**Hình thức:** Sản phẩm thật, mô hình điện áp thấp  
**Thời gian dự kiến:** 9 tuần; mỗi người 3 buổi/tuần, 1–2 giờ/buổi cho phiên bản điểm nâng cao tối đa. Bản gốc 3 tuần được giữ làm mốc so sánh khả thi.

Bản khảo sát này theo [Yêu cầu thuyết minh dự án](<docs/CQ_YÊU CẦU THUYẾT MINH DỰ ÁN.pdf>) và [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>). Khi nộp phải điền bìa, họ tên/MSSV, ảnh 3D trong/ngoài, ảnh linh kiện và xuất PDF đúng định dạng. Các chức năng đã cam kết chỉ được đổi tối đa một chức năng sau khi chốt thuyết minh.

## 1. Giới thiệu

### 1.1. Tổng quan

Một node ESP32 đặt trong phòng trẻ đo **mức sáng tương đối** và **biên độ âm thanh tương đối** rồi gửi qua MQTT → backend → website để phụ huynh xem biểu đồ. Phụ huynh đặt ba lịch mẫu “học bài”, “đi ngủ”, “làm việc nhà” trên backend; đến giờ, backend gửi lệnh MQTT để node phát tệp lời nhắc đã thu sẵn qua loa, đồng thời OLED hiện tên việc. Trẻ bấm nút để xác nhận; website ghi thời điểm bấm và trạng thái “trẻ đã xác nhận”, **không suy diễn rằng việc đã hoàn thành**. Một cảm biến nhiệt độ riêng kích buzzer tại chỗ khi vượt ngưỡng thử nghiệm, không cần Internet.

Đây là phiên bản thêm cloud, chart, chatbot, thông báo và LED để ba người có thể đạt trần điểm nâng cao dự kiến. Hệ thống **không tự xác định** trẻ đang dùng điện thoại/PC hoặc đang ngủ: các cảm biến ánh sáng, âm thanh và nút bấm không cung cấp bằng chứng trực tiếp cho hai kết luận ấy. Theo dõi thời gian dùng ứng dụng cần phần mềm và quyền truy cập trên chính điện thoại/PC; ví dụ iOS có [Screen Time API và Family Controls](https://developer.apple.com/documentation/screentimeapidocumentation). Xác định giấc ngủ cũng đòi hỏi thêm tín hiệu và thuật toán; [Sleep API của Android](https://developers.google.com/location-context/sleep) trả về xác suất thay vì khẳng định tuyệt đối. Hai ý tưởng này nằm ngoài bảng chức năng và dự toán hiện tại.

### 1.2. Danh sách chức năng

| ID | Loại, điểm theo PDF | Thiết bị/dịch vụ | Luồng và đầu ra kiểm chứng | Chủ sở hữu |
|---|---|---|---|---|
| F01 | Căn bản input → web | Cảm biến sáng CDS | CDS → ESP32 → MQTT → backend → frontend; hiện và ghi mức sáng tương đối theo thời gian. | A |
| F02 | Căn bản input → web | Cảm biến âm thanh MKE-S06 | Cảm biến → ESP32 → MQTT → backend → frontend; hiện biên độ âm thanh tương đối sau lấy mẫu. | B |
| F03 | Căn bản web → output | Module MP3 JQ8900 + loa tích hợp | Lịch trên backend đến hạn → frontend/backend xác nhận lịch → backend → MQTT → ESP32 → module MP3 phát tệp nhắc tương ứng; OLED phụ trợ hiện tên việc. | C |
| F04 | Nâng cao #1, 1,5 điểm | DS18B20 → buzzer 5V | DS18B20 → ESP32 → buzzer khi nhiệt độ vượt ngưỡng demo; chạy cục bộ khi rút WiFi/Internet. | A |
| F05 | Nâng cao #2, 1,5 điểm | Nút nhấn riêng | Nút → ESP32 → MQTT → backend → frontend ghi thời gian xác nhận việc đang được nhắc. | C |
| F06 | Nâng cao #10, 2,0 điểm | Website tự xây + SQLite cục bộ | Backend/frontend cho lịch nhắc, nút phát thử, trạng thái xác nhận và vùng chart F09; SQLite lưu lịch cục bộ; không dùng Node-RED. | B |
| F07 | Nâng cao #4, 1,5 điểm | Firebase RTDB | A lưu mức sáng/âm và lịch sử xác nhận có dấu thời gian lên cloud. | A |
| F08 | Nâng cao #12, 1,0 điểm | WiFiManager, sản phẩm thật | A cho đổi WiFi trên ESP32 và thử kết nối lại MQTT. | A |
| F09 | Nâng cao #5, 1,5 điểm | Firebase RTDB | B đọc dữ liệu F07 từ cloud qua backend rồi vẽ chart mức sáng/âm trên web. | B |
| F10 | Nâng cao #8, 0,5 điểm | Chatbot luật điều kiện | B trả lời lịch tiếp theo/lần xác nhận gần nhất bằng các câu hỏi định sẵn. | B |
| F11 | Nâng cao #3, 1,5 điểm | LED xanh riêng | C làm nút web bật/tắt LED trạng thái → backend → MQTT → ESP32 → LED; khác loa/OLED/buzzer. | C |
| F12 | Nâng cao #6, 1,0 điểm | Telegram Bot | C gửi thông báo nhanh cho phụ huynh khi quá giờ nhắc mà chưa có xác nhận, có chặn lặp. | C |

**Kiểm tra thiết bị:** F01 = CDS; F02 = MKE-S06; F03 = module phát MP3/loa; F04 = DS18B20 **và** buzzer riêng; F05 = nút nhấn; F11 = LED xanh riêng. Bảy thiết bị input/output dùng để chấm ở các yêu cầu khác nhau đều riêng biệt. OLED chỉ là hiển thị phụ trong F03, không dùng lại ở yêu cầu khác. F06–F10 và F12 là phần mềm/dịch vụ; F07 lưu cloud, F09 đọc cloud để tính chart, còn SQLite của F06 giữ lịch và tài khoản cấu hình cục bộ. Mỗi ID nâng cao có một chủ sở hữu. Đây là sản phẩm thật; nếu đổi sang giả lập phải kiểm giới hạn một thiết bị thay thế. Cần xác nhận cách hiểu quy tắc nếu giảng viên xem việc cloud/chart/thông báo dùng lại dữ liệu cảm biến là trùng thiết bị.

**Giới hạn đo:** CDS không đo lux chuẩn nếu chưa hiệu chuẩn; MKE-S06 đọc biên độ analog tương đối, **không tự cho số dB âm học chuẩn**. Biểu đồ chỉ ghi các chỉ số tương đối và thời điểm bấm. Ngưỡng nhiệt F04 chỉ phục vụ **minh họa phản ứng input → output**, không được gọi là thiết bị báo cháy bảo vệ sinh mạng. Để bảo vệ phòng ngủ thực, cần [báo khói chuyên dụng được lắp và kiểm tra đúng cách](https://www.usfa.fema.gov/prevention/home-fires/prepare-for-fire/smoke-alarms/).

## 2. Thiết kế

### 2.1. Bố trí bên ngoài và bên trong

Vỏ hộp đặt trên bàn hoặc tường thấp ngoài tầm nước. CDS hướng về vùng ánh sáng phòng và tránh chính màn hình OLED; micro hướng ra phòng nhưng tách khỏi loa để tránh biểu đồ ghi tiếng nhắc của hệ thống như tiếng môi trường. DS18B20 đặt ở mặt ngoài, xa nguồn nhiệt ESP32/loa. Nút xác nhận và LED xanh F11 ở mặt trước, OLED bên trên nút, loa và buzzer có lỗ âm riêng. ESP32, module MP3, dây nguồn và đầu nối ở trong hộp. Nguồn 5V 2A cấp cho cả board và audio qua đường phù hợp; kiểm tra điện áp từng module, chung mass, không cấp tải loa trực tiếp từ GPIO.

```text
Mặt trước: [OLED phụ F03] [nút xác nhận F05] [LED xanh F11] [loa lời nhắc F03]
Cạnh hộp: [CDS F01] [micro F02] [DS18B20 F04] [buzzer riêng F04]
Bên trong: [ESP32] [module MP3 F03] [dây/đầu nối] [nguồn 5V]
```

Khi hoàn thiện PDF phải dựng hình 3D hai góc nhìn bên ngoài/bên trong, đánh dấu ID từng linh kiện.

### 2.2. Wireframe website

```text
┌─────────────────────────────────────────────────────────────┐
│ PHÒNG TRẺ — ESP32/MQTT online/offline                        │
├─────────────────────────────┬───────────────────────────────┤
│ Mức sáng tương đối F01      │ Mức âm tương đối F02         │
│ Biểu đồ cloud F09          │ Biểu đồ cloud F09   │
├─────────────────────────────┴───────────────────────────────┤
│ Lịch: Học bài / Đi ngủ / Việc nhà F03  | Phát thử F03       │
│ Lần nhấn F05; nút LED F11; cảnh báo Telegram F12             │
│ Ô chat F10: lịch tiếp theo / lần nhấn gần nhất               │
└─────────────────────────────────────────────────────────────┘
```

Không có ô “đang ngủ” hoặc “đang dùng điện thoại” vì không có nguồn dữ liệu đáng tin cậy. Website có thể chạy trên máy của nhóm trong cùng mạng; muốn phụ huynh truy cập từ ngoài nhà cần thêm triển khai mạng/dịch vụ, chưa tính trong phạm vi 9 tuần.

### 2.3. Sơ đồ truyền và nhận dữ liệu

```mermaid
flowchart LR
  L["CDS F01"] --> E["ESP32"]
  S["Micro analog F02"] --> E
  BTN["Nút xác nhận F05"] --> E
  T["DS18B20 F04"] --> E
  E -->|GPIO cục bộ F04| BZ["Buzzer F04"]
  E -->|MQTT: light, sound, ack| MQ["MQTT broker"]
  MQ --> BE["Backend F06 + SQLite"]
  BE --> FE["Frontend F06"]
  FE -->|HTTP: đặt lịch/phát thử F03| BE
  BE -->|MQTT: reminder/play F03| MQ
  MQ --> E
  E --> MP3["Module MP3 + loa F03"]
  E --> OLED["OLED phụ F03"]
  BE -->|lưu theo thời gian F07| DB["Firebase RTDB"]
  DB -->|đọc F09| BE
  BE -->|chart/chat F09/F10| FE
  FE -->|HTTP: LED F11| BE
  BE -->|MQTT: status-led/set| MQ
  E --> LED["LED xanh F11"]
  BE -->|thông báo F12| TG["Telegram"]
  PHONE["Điện thoại cấu hình WiFi F08"] --> E
```

Lịch chạy trên backend: có Internet/mạng tới broker thì lệnh phát lời nhắc đến node; khi mất kết nối, nhắc việc và xác nhận qua web tạm ngừng. **F04 vẫn hoạt động cục bộ**. Bản này không cần ESP-NOW vì nhiệt kế và buzzer cùng nối một ESP32. Backend lưu thời gian nhận dữ liệu và thời gian nút bấm; F07 ghi cloud, F09 đọc cloud cho chart, F12 báo chậm xác nhận. F08 mở cổng cấu hình WiFi trên thiết bị thật. Nút LED F11, chart cloud, ô chat và trạng thái thông báo đã có trong phác thảo; gắn màu/mẫu mũi tên khác nhau khi xuất PDF.

### 2.4. Dự án tương tự và phần có thể tham khảo

| Nguồn có mã | Hữu ích cho đề xuất | Cần thay đổi |
|---|---|---|
| [Smart Desk — ESP32](https://github.com/dasha-dotcom/smart-desk) | Có mã firmware cho bộ đếm học tập, OLED, nút bấm và xử lý không chặn. | Không thay thế luồng MQTT → backend → frontend của PDF. |
| [Connected Alarm Clock for Children](https://github.com/bl1ndc4m3l/ConnectedAlarmClock) | Đồng hồ trẻ em dùng ESP32, OLED và MQTT để thông báo. | Gốc dùng Home Assistant/buzzer; đề xuất dùng backend tự xây và tệp giọng nói qua loa riêng. |
| [ESP32 Cloud Environment Monitor](https://github.com/saganash-21/ESP32-Cloud-Environment-Monitor) | Tham khảo bố trí cảm biến sáng, âm thanh và cảnh báo cục bộ. | Gốc dùng Arduino IoT Cloud; cần thay bằng MQTT → backend tự xây cho F01/F02. |
| [IoT_Project — ESP32/MQTT/Flask](https://github.com/PhucHuwu/IoT_Project) | Có firmware, backend, frontend, topic MQTT hai chiều và biểu đồ. | Chỉ lấy mẫu tổ chức luồng, không sao chép toàn bộ MongoDB hoặc các LED của dự án gốc. |

Không nguồn nào trong bảng chứng minh hệ thống nhận biết trẻ dùng điện thoại hoặc đang ngủ bằng các cảm biến của bản này; hai chức năng ấy không được đưa vào cam kết.

## 3. Triển khai

### 3.1. Danh sách linh kiện và dự toán

Giá VND tham khảo ngày **28/10/2026**. Link bán hàng có ảnh để đưa vào PDF; giá chưa gồm vận chuyển. Loa của module JQ8900 được mô tả là **tích hợp sẵn**, nên không mua thêm loa rời cho F03.

| STT | Linh kiện | SL | Đơn giá | Thành tiền | Nguồn giá/tình trạng | ID |
|---|---|---:|---:|---:|---|---|
| 1 | ESP32 DevKit V1 | 1 | 140.000 | 140.000 | [Linh Kiện Việt Nam](https://linhkienvietnam.vn/module-node-mcu-32s-esp32-devkitc-dung-module-esp-wroom-32) | F01–F05 |
| 2 | Cảm biến sáng CDS | 1 | 15.000 | 15.000 | [Hshop](https://hshop.vn/cam-bien-anh-sang-quang-tro-2) | F01 |
| 3 | Cảm biến âm thanh analog MKE-S06 | 1 | 45.000 | 45.000 | [Hshop](https://hshop.vn/cam-bien-am-thanh-mke-s06-sound-sensor) | F02 |
| 4 | Module MP3 JQ8900 kèm loa mini | 1 | 145.000 | 145.000 | [Hshop](https://hshop.vn/mach-phat-am-thanh-mke-m11-jq8900-mp3-i2c-module); kiểm tra phiên bản/tệp âm thanh | F03 |
| 5 | OLED I2C 0,96 inch | 1 | 65.000 | 65.000 | [Hshop](https://hshop.vn/lcd-oled-trang-0-96-inch-i2c); hiển thị phụ trong F03 | F03 |
| 6 | DS18B20 | 1 | 35.000 | 35.000 | [Hshop](https://hshop.vn/cam-bien-nhiet-do-chong-nuoc-ds18b20-waterproof-temperature-sensor) | F04 |
| 7 | Buzzer 5V riêng | 1 | 15.000 | 15.000 | [Hshop](https://hshop.vn/coi-buzzer-5vdc); kiểm tra giá lúc mua | F04 |
| 8 | Nút nhấn nhả | 1 | 5.000 | 5.000 | [Hshop, nhóm nút nhấn](https://hshop.vn/dieu-khien-ban-phim-joystick); giá **ước tính** | F05 |
| 9 | Adapter 5V 2A + cáp/đầu cấp nguồn | 1 bộ | 40.000 | 40.000 | [Adapter 30.000đ](https://linhkienvietnam.vn/nguon-adapter-5v-2a-5v2a-kho-b-ka9h14) + cáp ước tính 10.000đ | F01–F05 |
| 10 | Hộp, dây, đầu nối, điện trở/PCB | 1 bộ | 80.000 | 80.000 | **Ước tính**, chọn sau khi đo kích thước | F01–F05 |
| 11 | LED xanh F11 + điện trở | 1 bộ | 8.000 | 8.000 | **Ước tính**, kiểm điện trở khi lắp | F11 |
| | **Tổng tham khảo** | | | **593.000** | Chưa tính vận chuyển, công cụ, hosting ngoài mạng nhà | |

Giá trên Shopee/Lazada có thể thấp hơn nhưng cần kiểm tra biến thể, độ tin cậy người bán và phí giao; các mẫu Hshop ở đây đủ để lập ngân sách sơ bộ. Nếu muốn lời nhắc bằng giọng nói mới được nhập tự do trên web, cần thêm TTS/luồng nạp tệp; **bản này chỉ dùng ba tệp thu sẵn**.

### 3.2. Kế hoạch 9 tuần và đối chiếu mốc nền 3 tuần

**Quỹ nhóm:** 3 người × 3 ngày/tuần × 1–2 giờ/ngày × 3 tuần = **27–54 giờ-người**. Bảng dưới là ước tính khi nhóm đã biết Arduino ESP32, MQTT và Flask cơ bản; chưa kể thời gian giao hàng. Các phần song song nhưng phải tích hợp trước cuối Tuần 2.

| Tuần | ID | Đầu ra kiểm chứng | Chủ sở hữu | Giờ ước tính |
|---|---|---|---|---:|
| 1 | F01, F04 | CDS → MQTT → web; DS18B20 → buzzer và thử ngắt WiFi | A | 9–12 |
| 1 | F02, F06 | Âm thanh → MQTT → web; khung backend/frontend/SQLite | B | 10–14 |
| 1–2 | F03 | Ba tệp MP3, lệnh backend → MQTT → loa; OLED hiện việc đang nhắc | C | 10–14 |
| 2 | F05 | Nút → MQTT → backend → web, ghi đúng việc/thời điểm | C | 5–7 |
| 2–3 | F06 | Lịch chạy trên backend, biểu đồ sáng/âm, trạng thái xác nhận | B | 7–10 |
| 3 | F01–F06 | Tích hợp, kiểm thử mất mạng, đóng hộp, ảnh 3D/linh kiện, PDF, vấn đáp | A điều phối; B/C tham gia | 10–14 |
| | | **Tổng** | | **51–71** |

**Kết luận:** Với 27–54 giờ-người, toàn bộ F01–F06 **không khả thi một cách chắc chắn** trong 3 tuần: ngay cận dưới 51 giờ đã gần chạm mức tối đa 54 giờ, không còn dự phòng. Nếu mỗi người chỉ làm 1 giờ/buổi, quỹ 27 giờ là thiếu rõ rệt. Phần loa MP3/OLED và backend lịch nhắc là hai rủi ro lớn. Muốn nộp đúng phạm vi này, nên tăng thời gian lên khoảng **60–75 giờ-người**, tương đương trung bình 2,2–2,8 giờ/người/buổi, hoặc kéo dài 4 tuần. Với đúng giới hạn 3 tuần, nhóm nên thử loa và MQTT ngay trước khi chốt thuyết minh; nếu chưa chạy được thì thu hẹp chức năng **trước khi nộp**, vì sau đó chỉ được điều chỉnh tối đa một chức năng.

**Phần mở rộng F07–F12 để đạt trần:** F07 Firebase 6–8 giờ (A), F08 WiFiManager 4–6 giờ (A), F09 chart cloud 5–7 giờ (B), F10 chatbot luật 2–3 giờ (B), F11 web → LED 4–6 giờ (C), F12 Telegram 3–5 giờ (C), tích hợp/kiểm thử tăng thêm 5–7 giờ. Tổng cả đề tài **80–113 giờ-người**. Với nhịp 1–2 giờ/buổi, 3 người, 3 buổi/tuần, chọn **9 tuần = 81–162 giờ-người** để cận dưới quỹ giờ vừa bao phủ cận dưới ước lượng. Tuần 4–5 làm F07/F08/F11; Tuần 6–7 làm F09/F10/F12; Tuần 8–9 kiểm thử, đóng hộp, ảnh 3D, PDF và vấn đáp. Dòng tích hợp cuối Tuần 3 ở bảng nền chuyển sang Tuần 8–9. Nếu học kỳ còn ít hơn 9 tuần, không nên cam kết phiên bản tối đa điểm này; phải chốt một phạm vi nhỏ hơn trước khi nộp thuyết minh.

| Tuần mở rộng | ID | Chủ sở hữu | Giờ | Đầu ra kiểm chứng |
|---|---|---|---:|---|
| 4–5 | F07, F08 | A | 10–14 | Lưu Firebase có dấu thời gian; đổi WiFi và nối lại MQTT |
| 6–7 | F09, F10 | B | 7–10 | Chart đọc từ Firebase; chatbot trả lời lịch và lần nhấn |
| 4–7 | F11, F12 | C | 7–11 | Web điều khiển LED riêng; Telegram báo trễ xác nhận |
| 8–9 | F01–F12 | Cả nhóm | 5–7 tăng thêm | Thử toàn luồng và hoàn thiện PDF, ngoài giờ tích hợp nền |

Mốc 9 tuần chỉ vừa đủ ở trường hợp mỗi người làm đúng 1 giờ/buổi và mọi việc đạt cận dưới ước lượng; nên giữ nhịp gần 1,5 giờ/buổi để có dự phòng.

Phạm vi đầy đủ ban đầu, có **nhận biết dùng điện thoại/PC và xác định ngủ**, còn đòi hỏi ứng dụng/agent hoặc cảm biến và thuật toán riêng; chưa có thiết bị, công việc hay giờ công cho hai khả năng này. Không nên ghi chúng vào danh sách chức năng chấm điểm của bản 3 tuần.

## 4. Tổng kết và phân chia công việc

Theo C.1 của [Quy định đồ án cuối kỳ](<docs/CQ_QUY ĐỊNH ĐỒ ÁN CUỐI KỲ.pdf>), mỗi thành viên phụ trách một luồng căn bản qua MQTT/backend/frontend; khi làm, tích hợp và giải thích được có thể đạt **4 điểm chức năng + 1 điểm nhóm**. C.2 cho tối đa **4 điểm nâng cao/người**; điểm dưới đây chỉ là dự kiến từ các ID đăng ký. Biểu đồ F09 phải đọc dữ liệu từ Firebase F07 qua backend để được xem xét cho #5; SQLite F06 chỉ giữ lịch cục bộ. Điểm báo cáo tối đa 1 và cộng xét sản phẩm thật tối đa 1 tính riêng; điểm cuối kỳ còn nhân hệ số hiểu bài K.

| Thành viên | ID và phần bàn giao | Căn bản gồm nhóm | Nâng cao | Tổng tạm tính chưa gồm báo cáo |
|---|---|---:|---:|---:|
| A | F01; F04 nhiệt độ → buzzer 1,5 + F07 cloud 1,5 + F08 WiFi 1,0 | 5,0 | 4,0 | 9,0 |
| B | F02; F06 website 2,0 + F09 chart cloud 1,5 + F10 chatbot 0,5 | 5,0 | 4,0 | 9,0 |
| C | F03; F05 nút → web 1,5 + F11 web → LED 1,5 + F12 Telegram 1,0 | 5,0 | 4,0 | 9,0 |

**Rà soát trước nộp:** bảy thiết bị F01–F05/F11 đôi một khác nhau giữa các yêu cầu, kể cả DS18B20 và buzzer của F04; một chủ sở hữu/ID; không gắn nhãn “đã hoàn thành” cho nút nhấn, “lux/dB chuẩn” cho chỉ số chưa hiệu chuẩn, hay “báo cháy thật” cho ngưỡng nhiệt demo; thêm ảnh 3D ngoài/trong, ảnh linh kiện có ID, sơ đồ một trang có mũi tên phân biệt; xuất PDF tên `MANHOM_MSSV1_MSSV2_MSSV3_PROPOSAL.PDF`, Times New Roman 13, giãn dòng 1,15, canh đều.
