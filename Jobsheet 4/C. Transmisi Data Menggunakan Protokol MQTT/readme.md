# C. Transmisi Data Menggunakan Protokol MQTT

## 1. Alat dan Bahan
1. Node-RED
2. ESP32
3. XAMPP

## 2. Source Code

1. Code JSON Multi-Protocol IoT Server dapat dilihat <a href="https://github.com/ArthZ01/System-Embedded/blob/56e9a384948c7094115b371713c101f8607528e6/Jobsheet%204/B.%20Transmisi%20Data%20Menggunakan%20Protokol%20HTTP/flow%20program%20Multi-Protocol%20IoT.json">disini</a>
2. Program ESP32 dapat dilihat <a href="https://github.com/ArthZ01/System-Embedded/blob/56e9a384948c7094115b371713c101f8607528e6/Jobsheet%204/C.%20Transmisi%20Data%20Menggunakan%20Protokol%20MQTT/program%20transmisi%20mqtt/program%20transmisi%20mqtt.ino">disini</a>


## 3. Flow Program
![Flow Program](https://github.com/ArthZ01/System-Embedded/assets/91934953/c94b9604-a98c-4036-9df2-14c0a48a964d)

## 4. Hasil & Pembahasan
### Dokumentasi Hasil

1. Flow chart 

   ![Flow Chart](https://github.com/ArthZ01/System-Embedded/assets/91934953/63f63cb6-2e40-4b09-99ff-3b8c2c7e574b)
   
3. Output serial monitor
   
   ![2  Output serial monitor](https://github.com/ArthZ01/System-Embedded/assets/91934953/160587e7-6981-4552-ac6f-e0521c7a23ec)

4. Debug Node-RED
   
   ![3  Debug Node-RED](https://github.com/ArthZ01/System-Embedded/assets/91934953/2feaf087-a882-402b-b27e-2a4fc712dbce)
   
5. Dashboard Node-RED

   <img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/8f6d7a42-4854-496c-a174-496ae3b73e0f" width=80% height=80%>
   
6. Tabel database MySQL
   
   ![image](https://github.com/ArthZ01/System-Embedded/assets/91934953/b6e71433-c1e9-4338-8658-50a975f8fb39)


### Source Code
![Penjelasan Kode](https://github.com/ArthZ01/System-Embedded/assets/91934953/bce2d89a-1422-4f42-99e6-76cb8ad0fb6d)

### Pembahasan
1. Bagian Awal:
   * Memasukkan library yang diperlukan:
     * `WiFi.h` untuk mengakses fungsi Wi-Fi.
     * `PubSubClient.h` untuk komunikasi MQTT.
     * `ArduinoJson.h` untuk menangani format JSON.
   * Deklarasi variabel:
     * `ssid` dan `password` untuk menyimpan nama dan password Wi-Fi.
     * `mqtt_server` untuk menyimpan alamat server MQTT.
     * `espClient` untuk membuat koneksi TCP/IP ke server MQTT.
     * `client` untuk komunikasi MQTT.

2. Fungsi `setup_wifi()`:
   * Menghubungkan board Arduino ke jaringan Wi-Fi dengan nama dan password yang telah ditentukan.
   * Menampilkan informasi IP Address yang didapatkan oleh board Arduino.
     
3. Fungsi `reconnect()`:
   * Mencoba menghubungkan board Arduino ke server MQTT.
   * Jika gagal, mencoba kembali setiap 5 detik.

4. Fungsi `setup()`:
   * Menginisialisasi Serial Monitor untuk menampilkan pesan.
   * Menghubungkan board Arduino ke Wi-Fi.
   * Mengatur server MQTT yang akan dituju

5. Fungsi loop():
   * Memeriksa apakah koneksi MQTT masih tersambung.
   * Jika terputus, memanggil fungsi `reconnect()` untuk menyambung kembali.
   * Menangani proses MQTT secara berkala.
   * Mempersiapkan data yang akan dikirimkan dalam format JSON.
   * Menerbitkan data ke topic "flood/node1" pada server MQTT.
   * Menunggu 10 detik sebelum mengirimkan data berikutnya.

Catatan:
   * Kode ini menggunakan protokol MQTT untuk mengirimkan data sensor atau informasi lain dari board Arduino ke server secara berkala.
   * Interval pengiriman data diatur dalam fungsi `loop()` (10 detik dalam kode ini).
   * Data yang dikirimkan dalam format JSON.
   * Server MQTT yang digunakan adalah `broker.hivemq.com`.
   * Kode ini dapat digunakan untuk aplikasi IoT yang membutuhkan komunikasi dua arah yang ringan dan efisien.
