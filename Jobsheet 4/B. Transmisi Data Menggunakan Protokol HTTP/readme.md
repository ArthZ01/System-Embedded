# B. Transmisi Data Menggunakan Protokol HTTP
   
## 1. Alat dan Bahan
1. Node-RED
2. ESP32
3. XAMPP

## 2. Source Code

1. Code JSON Multi-Protocol IoT Server dapat dilihat <a href="https://github.com/ArthZ01/System-Embedded/blob/b0a720c8346aca387e8e5960110c174ae2e1a92a/Jobsheet%204/B.%20Transmisi%20Data%20Menggunakan%20Protokol%20HTTP/flow%20program%20Multi-Protocol%20IoT.json">disini</a>
2. Program ESP32 transmisi data dummy menggunakan protokol HTTP metode GET dapat dilihat <a href="https://github.com/ArthZ01/System-Embedded/blob/05864b09d785d0e0f36e0ccaa11523e064d9bc64/Jobsheet%204/B.%20Transmisi%20Data%20Menggunakan%20Protokol%20HTTP/transmisi_data_dummy_keNode-Red_protokol_HTTP_metode_Get/transmisi_data_dummy_keNode-Red_protokol_HTTP_metode_Get.ino">disini</a>
3. Program ESP32 transmisi data dummy menggunakan protokol HTTP metode POST dapat dilihat <a href="https://github.com/ArthZ01/System-Embedded/blob/05864b09d785d0e0f36e0ccaa11523e064d9bc64/Jobsheet%204/B.%20Transmisi%20Data%20Menggunakan%20Protokol%20HTTP/transmisi_data_dummy_ke_Node-Red_protokol_HTTP_metode_POST/transmisi_data_dummy_ke_Node-Red_protokol_HTTP_metode_POST.ino">disini</a>

## 3. Flow Program

![Flow Program](https://github.com/ArthZ01/System-Embedded/assets/91934953/81454a50-29fd-481f-8b8f-3e68c6b977ba)


## 4. Hasil Percobaan Transmisi Data Dummy Menuju Node-Red Menggunakan Protokol HTTP Metode GET
### Dokumentasi Percobaan

1. Flow chart

   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/695f4ce4-01d0-4445-a892-19055b93a334" height=700rem>
   
2. Output serial monitor

   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/930cbfb6-1a76-4706-9b1e-bbe84c709ebf" width=80% height=80%>
   
4. Debug Node-RED
   
   ![3  Debug Node-RED](https://github.com/ArthZ01/System-Embedded/assets/91934953/73dcece1-cbf4-4ebc-8748-51bf9fbec73a)

5. Dashboard Node-RED

   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/013e2f79-fb78-4f0e-8d39-8cacd99390fc" width=80% height=80%>
   
7. Tabel database MySQL
   
   ![5  Tabel database MySQL](https://github.com/ArthZ01/System-Embedded/assets/91934953/2a903d24-d8db-4116-98a3-218aef4c5162)


### Source Code
<img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/eb9d6f11-6eec-48e2-b660-e837d4fae026" height=1000rem>

### Pembahasan
1. Bagian Awal:
   * Memasukkan library yang diperlukan:
     * `WiFi.h` untuk mengakses fungsi Wi-Fi.
     * `HTTPClient.h` untuk membuat permintaan HTTP.
   * Deklarasi variabel:
     * `ssid` dan `password` untuk menyimpan nama dan password Wi-Fi.
     * `serverName` untuk menyimpan alamat server yang akan dituju.
     * `lastTime` untuk menyimpan waktu terakhir pengiriman data.
     * `timerDelay` untuk mengatur interval pengiriman data (dalam milisekon).
2. Fungsi `setup()`:
   * Inisialisasi Serial Monitor:
     * `Serial.begin(115200)` untuk menampilkan pesan di Serial Monitor.
   * Menghubungkan ke Wi-Fi:
     * `WiFi.begin(ssid, password)` untuk menghubungkan board Arduino ke jaringan Wi-Fi.
   * Menunggu hingga tersambung ke Wi-Fi:
     * Program akan menunggu hingga koneksi Wi-Fi berhasil sebelum melanjutkan.
   * Menampilkan informasi IP Address:
     * Program menampilkan IP Address yang didapatkan oleh board Arduino.
     * Menginformasikan pengaturan timer:
     * Program menampilkan pesan yang menunjukkan interval pengiriman data.
3. Fungsi `loop()`:
   * Mengirim data setiap interval tertentu:
     * Program akan memeriksa apakah waktu yang telah berlalu sejak pengiriman data terakhir melebihi timerDelay. Jika iya, maka akan dilakukan pengiriman data.
   * Memeriksa status koneksi Wi-Fi:
     * Jika board Arduino masih terhubung ke Wi-Fi, maka proses pengiriman data akan dilanjutkan.
   * Membuat client HTTP:
     * `WiFiClient client` membuat objek client untuk komunikasi HTTP.
     * `HTTPClient http` membuat objek untuk melakukan permintaan HTTP.
   * Menentukan server tujuan:
     * `http.begin(client, serverName`) menetapkan server yang akan dituju untuk pengiriman data.
   * Menentukan header Content-Type:
     * `http.addHeader("Content-Type", "application/json")` menetapkan format data yang dikirimkan adalah JSON.
   *Mempersiapkan data yang akan dikirimkan:
     * String `httpRequestData` menyimpan data dalam format JSON yang akan dikirimkan. Dalam kode ini, data yang dikirimkan berupa nilai `dev_id`, `level`, `rainfall`, dan `flow`.
   * Mengirim permintaan HTTP GET:
     * `int httpResponseCode = http.GET()` mengirimkan permintaan GET ke server dengan data yang telah disiapkan.
   * Menampilkan kode respons HTTP:
     * Program menampilkan kode respons yang diterima dari server untuk mengetahui status pengiriman data.
   * Menutup koneksi HTTP:
     * `http.end()` menutup koneksi HTTP.
   * Mencatat waktu pengiriman data terakhir:
     * `lastTime = millis()` menyimpan waktu saat ini sebagai waktu terakhir pengiriman data
       
Catatan:
   * Kode ini menggunakan metode GET.
   * Interval pengiriman data diatur dalam variabel `timerDelay` (5 detik dalam kode ini).
   * Data yang dikirimkan dalam format JSON.
   * Server yang dituju adalah `http://192.168.1.7:1880/flood/node1`.

## 5. Hasil Percobaan Transmisi Data Dummy Menuju Node-Red Menggunakan Protokol HTTP Metode POST
### Dokumentasi Percobaan

1. Flow chart 

   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/9c59e274-4da3-4569-a54c-68b341211c1e" height=700rem>

2. Output serial monitor
 
   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/2792706d-a6c1-4e06-8109-b4b315404235" width=80% height=80%>
   
3. Debug Node-RED
   
   ![3  Debug Node-RED](https://github.com/ArthZ01/System-Embedded/assets/91934953/d4095d4f-5805-481c-a097-970f5edfe399)
   
4. Dashboard Node-RED
 
   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/69f41a3e-0c2f-4ef1-af93-529e83ef68ed" width=80% height=80%>

### Source Code
<img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/cc612bab-186e-4932-8c1c-4880c186b777">

### Pembahasan

1. Bagian Awal:
   * Memasukkan library yang diperlukan:
     * `WiFi.h` untuk mengakses fungsi Wi-Fi.
     * `PubSubClient.h` untuk komunikasi MQTT.
     * `ArduinoJson.h` untuk membuat dan memproses data JSON.
   * Deklarasi variabel:
     * `ssid` dan `password` untuk menyimpan nama dan password Wi-Fi.
     * `mqtt_server` untuk menyimpan alamat server MQTT.
     * `espClient` untuk membuat klien Wi-Fi.
     * `client` untuk membuat klien MQTT.
       
2. Fungsi `setup_wifi()`:
   * Menghubungkan board Arduino ke jaringan Wi-Fi.
   * Menampilkan informasi IP Address yang didapatkan.
     
3. Fungsi `reconnect()`:
   * Menghubungkan kembali ke server MQTT jika terputus.
   * Membuat client ID secara acak untuk identifikasi unik.
     
4. Fungsi `setup()`:
   * Menginisialisasi Serial Monitor untuk menampilkan pesan.
   * Menghubungkan ke Wi-Fi menggunakan fungsi `setup_wifi()`.
   * Mengatur server MQTT yang akan dituju.
     
5. Fungsi `loop()`:
   * Memeriksa koneksi MQTT, jika terputus akan memanggil fungsi `reconnect()`.
   * Menangani proses komunikasi MQTT secara otomatis.
   * Mempersiapkan data JSON yang akan dikirimkan:
     * Membuat objek JSON dengan nilai `dev_id`, `level`, `rainfall`, dan `flow`.
     * Mengonversi objek JSON ke string dan menyimpannya dalam variabel payload.
   * Mengirimkan data menggunakan metode PUBLISH ke topic "flood/node1".
   * Menunggu selama 10 detik sebelum mengirimkan data berikutnya.
     
Catatan:
   * Kode ini menggunakan protokol MQTT.
   * Metode yang digunakan adalah POST.
   * Data yang dikirimkan dalam format JSON.
   * Server MQTT yang dituju adalah 192.168.1.7 pada port 1883.
   * Interval pengiriman data diatur 10 detik dalam kode ini.
