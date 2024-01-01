# D. Akuisi Data dan Kendali Perangkat IoT Menggunakan Protokol MQTT
   
## 1. Alat dan Bahan
1. Node-RED
2. ESP32
3. Kabel jumper
4. LED
5. XAMPP

## 2. Source Code

1. Code JSON Multi-Protocol IoT Server dapat dilihat <a href="https://github.com/JustBadrun/Embeded_System/blob/dd513af13ce3906220b904cf8b1522e06d7a0c23/Jobsheet%204/B.%20Transmisi%20Data%20Menggunakan%20Protokol%20HTTP/flow%20program%20Multi-Protocol%20IoT.json">disini</a>
2. Program ESP32 kontrol nyala LED melalui dashboard Node-RED dapat dilihat <a href="https://github.com/JustBadrun/Embeded_System/blob/5de87485d941e0818fd193cdf1d823249256daca/Jobsheet%204/D.%20Akuisi%20Data%20dan%20Kendali%20Perangkat%20IoT%20Menggunakan%20Protokol%20MQTT/akuisisi/akuisisi.ino">disini</a>


## 3. Flow Program
![image](https://github.com/ArthZ01/System-Embedded/assets/91934953/5a4526ba-f8e2-4cdd-b02a-6704872a7403)


## 4. Hasil & Penjelasan Percobaan Kontrol Nyala LED Melalui Dashboard Node-RED
### Dokumentasi Percobaan

1. Flow chart program ESP32
   
  ![image](https://github.com/ArthZ01/System-Embedded/assets/91934953/7db33564-d846-4c57-ad71-42562765d82c)

2. Dokumentasi
   
   ![WhatsApp Image 2023-12-22 at 08 21 04_01c9056c](https://github.com/JustBadrun/Embeded_System/assets/128286595/13547144-2d63-43d3-8adb-016d78373858)

4. Output serial monitor
   
   ![serialmonitor1](https://github.com/JustBadrun/Embeded_System/assets/128286595/72266af7-a40f-45fc-933c-ce0a4062d98a)

5. Debug Node-RED
   
   <img src="https://github.com/brianrahma/system-embedded/assets/82065700/6f42ea1e-cc21-48d6-8e28-a84fb027c729" height="500">
   
6. Dashboard Node-RED
   
  ![WhatsApp Image 2023-12-22 at 08 22 13_1d17d3e7](https://github.com/JustBadrun/Embeded_System/assets/128286595/473009bc-0983-4b1b-9a15-ea96e908a5a0)

### Kode
![carbon (2)](https://github.com/ArthZ01/System-Embedded/assets/91934953/afaeef6d-5159-4916-89c9-98757bc551f4)

### Pembahasan


Kode di atas adalah program ESP32 yang menggunakan modul WiFi untuk mengukur suhu dan mengontrol LED melalui protokol MQTT. Berikut penjelasan singkat untuk setiap bagian dari kode tersebut:

1. **Inklusi Library:**
   ```cpp
   #include <WiFi.h>
   #include <PubSubClient.h>
   #include <ArduinoJson.h>
   ```
   Library WiFi.h digunakan untuk mengelola koneksi WiFi, library PubSubClient.h untuk mengimplementasikan klien MQTT, dan library ArduinoJson.h untuk memproses dan membangun data JSON.

2. **Konfigurasi Koneksi WiFi dan MQTT Server:**
   ```cpp
   const char* ssid = "ZTE_2.4G_TuYTR4";
   const char* password = "kasnaman1";
   const char* mqtt_server = "broker.emqx.io";
   ```
   Nama dan kata sandi WiFi, serta alamat MQTT broker yang digunakan.

3. **Inisialisasi Objek Klien WiFi dan MQTT:**
   ```cpp
   WiFiClient espClient;
   PubSubClient client(espClient);
   ```

4. **Definisi GPIO dan Topik MQTT:**
   ```cpp
   const char led = 2;
   #define TEMP_TOPIC "flood/node2"
   #define LED_TOPIC "flood/node2/led"
   ```

   GPIO pin untuk LED dan topik MQTT yang digunakan.

5. **Fungsi Callback untuk Menerima Pesan MQTT:**
   ```cpp
   void receivedCallback(char* topic, byte* payload, unsigned int length) {
     // ...
   }
   ```

   Fungsi ini akan dipanggil ketika perangkat menerima pesan dari topik yang telah di-subscribe.

6. **Fungsi Koneksi MQTT:**
   ```cpp
   void mqttconnect() {
     // ...
   }
   ```

   Fungsi ini mencoba untuk terhubung ke broker MQTT dan melakukan subscribe ke topik yang diinginkan.

7. **Fungsi Setup:**
   ```cpp
   void setup() {
     // ...
   }
   ```

   Fungsi setup yang pertama kali dijalankan saat perangkat dinyalakan. Menginisialisasi serial, koneksi WiFi, pin LED, dan mengatur server MQTT serta fungsi callback.

8. **Fungsi Loop:**
   ```cpp
   void loop() {
     // ...
   }
   ```

   Fungsi loop yang berjalan terus-menerus setelah fungsi setup selesai. Jika koneksi MQTT terputus, akan mencoba kembali terhubung. Melakukan loop untuk mendengarkan pesan MQTT dan mengukur suhu setiap 5 detik.

9. **Pengiriman Data MQTT:**
   ```cpp
   if (now - lastMsg > 5000) {
     // ...
   }
   ```

   Bagian ini mengirimkan data sensor (dalam bentuk objek JSON) ke topik MQTT "flood/node2" setiap 5 detik. Data suhu dan status LED dikirim bersamaan dalam bentuk JSON.
