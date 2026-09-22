# Project IoT

## Các chủ đề có thể tham khảo:

### * Hệ thống An ninh nhà thông minh

* **Mô tả ngắn:** Node cảm biến (PIR + cảm biến cửa + đầu đọc RFID/bàn phím) phát hiện chuyển động/truy cập, gửi ngay lệnh còi báo/đèn qua ESP-NOW đến node chấp hành mà không cần Internet (đáp ứng yêu cầu 1). Đồng thời dữ liệu và sự kiện được đẩy lên Firebase để xem trên web, nhận push notification qua Telegram khi có xâm nhập, có đăng nhập phân quyền cho web quản lý.
* **Thành phần phần cứng**:
  * Vi mạch: 2× ESP32 (1 làm node cảm biến, 1 làm node chấp hành/gateway WiFi)
  * Input: PIR sensor, module RFID RC522, keypad 3×4 (tùy chọn)
  * Output: Relay điều khiển khóa điện, còi buzzer, màn hình OLED 0.96", LED trạng thái
    Module khác: Firebase RTDB, WiFiManager (cấu hình WiFi ban đầu)
* **Kiến trúc hệ thống:**

PIR/RFID → ESP32 (node cảm biến) → ESP-NOW → ESP32 (node chấp hành) → Relay/Buzzer/OLED
                                        ↓ (qua WiFi)
                                    Firebase RTDB + Auth
                                        ↓
                              Web Dashboard (log, điều khiển, cảnh báo)
                                        ↓
                              Telegram Bot Push Notification

* **Các nguồn tham khảo**
  * "Home Security System" (RFID + keypad + LCD + dashboard Adafruit.io) — [https://ocw.cs.pub.ro/courses/iothings/proiecte/2021/homesecurity](https://ocw.cs.pub.ro/courses/iothings/proiecte/2021/homesecurity)
  * "Security System with ESP32" (2021), "Smart Home Security System" (2022, 2023), "WiFi-controlled surveillance system" (2022) — đều nằm trong danh mục [https://ocw.cs.pub.ro/courses/iothings/proiecte/](https://ocw.cs.pub.ro/courses/iothings/proiecte/)
  * Ví dụ hệ thống có Blynk + dashboard: [https://www.hackster.io/VJ-Embedded-Tech/iot-based-home-monitoring-and-device-control-using-esp32-95c601](https://www.hackster.io/VJ-Embedded-Tech/iot-based-home-monitoring-and-device-control-using-esp32-95c601)
  * Video demo dự án tương tự (ESP32 + Firebase + app điều khiển thiết bị): [https://youtu.be/SxM_EhIoMEc](https://youtu.be/SxM_EhIoMEc)
* **Tìm kiếm tham khảo trên YouTube theo từ khóa** "ESP32 home security system RFID relay", "ESP32 door lock RFID Firebase project", "ESP-NOW security alarm ESP32 demo"


### * Hệ thống giám sát & tưới vườn thông minh

**Mô tả ngắn:** Node ngoài trời đo độ ẩm đất/nhiệt độ, khi độ ẩm dưới ngưỡng thì gửi lệnh trực tiếp (ESP-NOW) đến node bơm để tưới ngay mà không phụ thuộc Internet. Dữ liệu định kỳ đẩy lên Firebase, hiển thị biểu đồ trên web, cảnh báo qua Telegram khi cây "khát nước" hoặc cảm biến lỗi, có mô hình đơn giản dự đoán xu hướng khô đất.

**Thành phần phần cứng:**

* Vi mạch: 2× ESP32
* Input: Cảm biến độ ẩm đất (capacitive), DHT11, LDR (tùy chọn đo ánh sáng)
* Output: Relay điều khiển máy bơm nước mini, LED/quạt (tùy chọn điều hòa nhiệt độ)
* Module khác: WiFiManager, Firebase RTDB
* **Kiến trúc hệ thống:**

Soil moisture/DHT11 → ESP32 (node vườn) → ESP-NOW → ESP32 (node bơm) → Relay → Máy bơm
								↓ (qua WiFi)
						Firebase RTDB
								↓
		Web Dashboard (biểu đồ độ ẩm, lịch sử tưới)
								↓
		Telegram Push Notification (cảnh báo khô đất)

* **Nguồn tham khảo thực tế**:
  * "Automated Irrigation System" — ESP32 + soil moisture + DHT11 + Firebase + web app biểu đồ, có link mã nguồn zip và video demo YouTube: https://youtu.be/jzyOkNfnHeY (trang dự án: https://ocw.cs.pub.ro/courses/iothings/proiecte/2022/automated_irrigation_system)
  * "Garden X" — ESP32 + DHT11 + soil moisture + LDR + MQ135 + Firebase + app Kodular, dự án dự thi có mô tả chi tiết phần cứng: https://circuitdigest.com/contest/india-automation-challenge-2021/garden-x
  * Dự án nông nghiệp thông minh dùng Firebase + app MIT App Inventor: https://www.hackster.io/atharva-kaplay/iot-based-smart-farming-system-92f50e
  * Các đồ án cùng trường có chủ đề tương tự để tham khảo thêm: "Smart Irrigation System" (2021), "Smart Garden" (2022-2023), "Smart Plant Monitoring System" (2023), "ESP32 Plant Care System" (2025) — trong danh mục https://ocw.cs.pub.ro/courses/iothings/proiecte/

**Từ khóa tìm YouTube thêm:** "ESP32 smart irrigation Firebase demo", "ESP32 soil moisture automatic watering project", "smart garden ESP32 app demo"
