# A. Setting SSID dan Password Wi-Fi ESP32 melalui Web Server

## 1. Alat dan Bahan
1) ESP32
2) Arduino IDE

## 2. Source Code

<img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/2db0b857-5e73-4955-a12c-b65fec459779" height=1000rem>


## 3. Flowchart

<img src="https://github.com/ArthZ01/System-Embedded/assets/91934953/8286f7b0-52ad-4662-9eb9-9feac8efd2d0" height=700rem>

## 4. Hasil dan Pembahasan
### Dokumentasi Hasil
1. Tampilan Awal Serial Monitor Sebelum Dihubungkan

   ![1  Tampilan Awal Serial Monitor Sebelum Dihubungkan](https://github.com/ArthZ01/System-Embedded/assets/91934953/00a64629-aaed-4876-8403-c0e9d0839872)

2. Tampilan Web

   ![2  tampilan web](https://github.com/ArthZ01/System-Embedded/assets/91934953/b1f7d66e-bfef-45f3-a4d7-6b5a824b09e2)

3. Serial Monitor Setelah Memasukkan SSID dan PASS

   ![SSID dan Pass](https://github.com/ArthZ01/System-Embedded/assets/91934953/371172c6-b42d-47f1-953c-8e28cff1680d)

   ![3  serial monitor setelah memasukan ssid dan pass](https://github.com/ArthZ01/System-Embedded/assets/91934953/51e90c6f-72ea-468b-b1d5-dcd2800f2f56)
   
4. Serial Monitor Setelah Berhasil Terhubung

   ![4  Serial Monitor Setelah Berhasil Terhubung](https://github.com/ArthZ01/System-Embedded/assets/91934953/6bb90203-f938-451f-8f63-ec08a626a5ed)


### Pembahasan

  1. Bagian Awal:
  * Memasukkan library yang diperlukan:
     * 'WiFi.h': untuk mengakses fungsi Wi-Fi.
     * Membaca kredensial WiFi yang tersimpan di EEPROM.
     * Mencoba menghubungkan ke WiFi menggunakan kredensial tersebut.

  2. Loop Utama:
  * Jika terkoneksi ke WiFi:
    * Mencetak pesan konfirmasi koneksi.
  * Jika tidak terkoneksi ke WiFi:
    * Mengecek status tombol untuk memaksa mode AP (Access Point).
    * Jika tombol tidak ditekan dan koneksi gagal, memulai mode AP dan membuat halaman web untuk konfigurasi WiFi.
    * Menunggu hingga terkoneksi ke WiFi.

  3. Fungsi testWifi:
  * Mencoba menghubungkan ke WiFi selama 10 detik.
  * Mengembalikan nilai 'true' jika terkoneksi, 'false' jika tidak.

  4. Fungsi launchWeb:
  * Mencetak informasi IP address perangkat (local dan softAP jika ada).
  * Menjalankan fungsi createWebServer untuk membuat halaman web konfigurasi WiFi.

  5. Fungsi setupAP:
  * Mengatur perangkat sebagai Access Point (AP) dengan nama "MiSREd IoT".
  * Mencari jaringan WiFi di sekitar dan menyimpan daftarnya dalam variabel st.
  * Menjalankan fungsi launchWeb untuk menampilkan halaman konfigurasi WiFi.

  6. Fungsi createWebServer:
  * Menangani permintaan ke halaman web:
    * '/' : Menampilkan halaman utama dengan daftar jaringan WiFi yang ditemukan dan formulir untuk memasukkan kredensial WiFi baru.
    * '/scan' : Memindai ulang jaringan WiFi dan menampilkan hasilnya.
    * '/setting' : Menerima kredensial WiFi baru, menyimpannya ke EEPROM, dan me-restart perangkat.
  
### Kesimpulan:
Kode ini dirancang untuk memudahkan konfigurasi WiFi pada perangkat dengan menyediakan antarmuka web yang dapat diakses dari perangkat lain. Pengguna dapat mengubah kredensial WiFi tanpa perlu mengubah kode secara langsung.
