# Panduan Penggunaan NAS Lab

Dokumentasi ini berisi panduan penggunaan NAS Lab untuk seluruh anggota lab. NAS digunakan sebagai tempat penyimpanan file bersama, folder pribadi mahasiswa, serta tempat upload file untuk kebutuhan print tanpa perlu mengirim file melalui email lab.

---

## 1. Fungsi NAS Lab

NAS Lab digunakan untuk:

1. Menyimpan file pribadi mahasiswa.
2. Memberikan jatah penyimpanan untuk setiap mahasiswa.
3. Berbagi file antar anggota lab.
4. Mengirim file print tanpa perlu menggunakan email lab.
5. Mengakses file dari komputer/laptop yang terhubung ke jaringan lab.

---

## 2. Informasi Akses NAS

Setiap anggota lab akan mendapatkan:

```text
Username : username masing-masing
Password : password masing-masing
```

Alamat NAS:

```text
\\10.4.89.190
```

Share utama yang dapat digunakan:

| Nama Share     | Alamat                         | Fungsi                                             |
| -------------- | ------------------------------ | -------------------------------------------------- |
| Folder Pribadi | `\\10.4.89.190\mahasiswa`      | Penyimpanan pribadi masing-masing user             |
| Folder Bersama | `\\10.4.89.190\folder-bersama` | Folder sharing bersama anggota lab                 |
| TA Archive     | `\\10.4.89.190\ta-archive`     | Arsip TA/referensi, jika tersedia                  |
| ISO            | `\\10.4.89.190\iso`            | File ISO, installer, atau tools lab, jika tersedia |

---

## 3. Akses dari Windows

### 3.1 Akses Folder Pribadi

1. Pastikan Laptop sudah terhubung dengan jaringan ITS, jika tidak sedang di ITS, gunakan VPN ITS.
2. Buka **File Explorer**.
3. Klik address bar di bagian atas.
4. Masukkan alamat berikut:

```text
\\10.4.89.190\mahasiswa
```

5. Masukkan username dan password yang diberikan oleh admin lab.
6. Setelah berhasil login, user akan masuk ke folder penyimpanan pribadi.

Contoh:

```text
Username : susilo
Password : ********
```

---

### 3.2 Akses Folder Bersama

Buka File Explorer, lalu masukkan:

```text
\\10.4.89.190\folder-bersama
```

Folder ini digunakan untuk berbagi file antar anggota lab.

---

### 3.3 Upload File untuk Print

Untuk mengirim file yang ingin diprint, buka folder:

```text
\\10.4.89.190\folder-bersama
```

Jika tersedia folder `Print`, masuk ke:

```text
\\10.4.89.190\folder-bersama\Print
```

Lalu copy file yang ingin diprint ke folder tersebut.

Contoh penggunaan:

```text
File laporan.docx
→ copy
→ \\10.4.89.190\folder-bersama\Print
→ paste
```

Dengan cara ini, file print tidak perlu dikirim melalui email lab.

---

## 4. Akses dari Ubuntu/Linux

### 4.1 Akses Folder Pribadi

1. Buka **Files / File Manager**.
2. Tekan `Ctrl + L`.
3. Masukkan alamat berikut:

```text
smb://10.4.89.190/mahasiswa
```

4. Masukkan username dan password masing-masing.
5. Pada bagian `Domain`, jika muncul, biarkan default atau isi:

```text
WORKGROUP
```

---

### 4.2 Akses Folder Bersama

Buka File Manager, tekan `Ctrl + L`, lalu masukkan:

```text
smb://10.4.89.190/folder-bersama
```

Login menggunakan username dan password masing-masing.

---

## 5. Batas Kapasitas Penyimpanan

Setiap mahasiswa mendapatkan batas penyimpanan pribadi.

Default quota:

```text
Soft limit : 20 GB
Hard limit : 22 GB
```

Artinya:

* User disarankan menyimpan file maksimal sekitar 20 GB.
* Jika melewati batas hard limit, user tidak dapat menambahkan file baru.
* Jika penyimpanan penuh, hapus file lama atau hubungi admin lab.

---

## 6. Aturan Penggunaan

1. Gunakan folder pribadi untuk file masing-masing.
2. Gunakan folder bersama hanya untuk file yang memang perlu dibagikan.
3. Jangan menghapus file milik orang lain.
4. Jangan menyimpan file yang tidak berkaitan dengan kebutuhan akademik/lab.
5. Jangan membagikan username dan password kepada orang lain.
6. Jika menggunakan komputer umum/lab, logout dari NAS setelah selesai.
7. Untuk file print, letakkan file di folder `Print` jika tersedia.

---

## 7. Logout dari NAS di Windows

Jika menggunakan komputer bersama, logout dari NAS setelah selesai.

### Cara 1: Menggunakan Command Prompt

Buka **Command Prompt**, lalu jalankan:

```cmd
net use * /delete /y
```

Command ini akan memutus koneksi SMB/NAS yang sedang aktif.

---

### Cara 2: Hapus Credential Tersimpan

Jika Windows masih otomatis login menggunakan akun lama:

1. Buka **Control Panel**.
2. Masuk ke:

```text
Credential Manager
→ Windows Credentials
```

3. Cari credential yang berhubungan dengan:

```text
10.4.89.190
```

4. Hapus credential tersebut.
5. Buka ulang File Explorer dan akses NAS lagi.

---

## 8. Logout dari NAS di Ubuntu/Linux

Jika Ubuntu masih otomatis login dengan akun lama, tutup File Manager lalu jalankan:

```bash
gio mount -l | grep smb
```

Jika ada koneksi ke NAS, matikan cache SMB:

```bash
killall nautilus
killall gvfsd-smb
killall gvfsd-smb-browse
```

Jika muncul pesan `no process found`, abaikan.

Jika credential masih tersimpan, hapus melalui aplikasi **Passwords and Keys**.

Install jika belum ada:

```bash
sudo apt install seahorse -y
```

Buka aplikasi:

```bash
seahorse
```

Cari credential yang berhubungan dengan:

```text
10.4.89.190
smb
```

Lalu hapus credential tersebut.

---

## 9. Troubleshooting

### 9.1 Tidak Muncul Form Login

Penyebab umum:

* Komputer sudah pernah login ke NAS sebelumnya.
* Credential masih tersimpan di Windows atau Ubuntu.

Solusi Windows:

```cmd
net use * /delete /y
```

Lalu hapus credential di:

```text
Control Panel
→ Credential Manager
→ Windows Credentials
```

Solusi Ubuntu:

```bash
killall nautilus
killall gvfsd-smb
killall gvfsd-smb-browse
```

Jika masih otomatis login, hapus credential dari **Passwords and Keys**.

---

### 9.2 Login Gagal Padahal Password Benar

Kemungkinan penyebab:

1. Password yang dimasukkan bukan password NAS/Samba.
2. Username salah ketik.
3. Credential lama masih tersimpan.
4. Akun belum diaktifkan oleh admin.

Solusi:

* Pastikan username dan password sesuai.
* Hapus credential lama.
* Coba login ulang.
* Jika masih gagal, hubungi admin lab.

---

### 9.3 Windows Menampilkan Error Multiple Connections

Jika muncul error seperti:

```text
Multiple connections to a server or shared resource by the same user,
using more than one user name, are not allowed.
```

Artinya Windows masih tersambung ke NAS menggunakan user lain.

Solusi:

Buka Command Prompt:

```cmd
net use * /delete /y
```

Lalu buka ulang:

```text
\\10.4.89.190\mahasiswa
```

Masukkan username dan password yang benar.

---

### 9.4 Tidak Bisa Upload File

Kemungkinan penyebab:

1. Kuota penyimpanan sudah penuh.
2. User tidak memiliki akses tulis ke folder tersebut.
3. File sedang terbuka di aplikasi lain.
4. Koneksi jaringan bermasalah.

Solusi:

* Coba upload ke folder pribadi.
* Hapus file yang tidak diperlukan.
* Pastikan ukuran file tidak terlalu besar.
* Hubungi admin jika masih gagal.

---

### 9.5 Folder Pribadi Tidak Terlihat

Pada share `mahasiswa`, user hanya dapat mengakses folder yang sesuai dengan akun masing-masing.

Contoh:

```text
User susilo → folder susilo
User zaky   → folder zaky
```

Jika folder pribadi tidak terlihat atau tidak bisa dibuka, hubungi admin lab.

---

### 9.6 Akses NAS Lambat

Kemungkinan penyebab:

1. Menggunakan Wi-Fi yang tidak stabil.
2. File yang dicopy berjumlah sangat banyak dan kecil-kecil.
3. Jaringan sedang ramai.
4. Komputer belum menggunakan koneksi gigabit.

Solusi:

* Gunakan kabel LAN jika memungkinkan.
* Untuk banyak file kecil, kompres menjadi `.zip` terlebih dahulu.
* Hindari upload file besar saat jaringan ramai.
* Cek koneksi jaringan.

Kecepatan normal jaringan lokal 1 Gbps biasanya sekitar:

```text
80–110 MB/s
```

Jika hanya sekitar:

```text
8–12 MB/s
```

kemungkinan koneksi hanya 100 Mbps atau menggunakan Wi-Fi lambat.

---

### 9.7 Tidak Bisa Membuka NAS dari Windows

Pastikan alamat ditulis dengan benar:

```text
\\10.4.89.190\mahasiswa
```

Bukan:

```text
//10.4.89.190/mahasiswa
```

Untuk Windows gunakan backslash `\`.

---

### 9.8 Tidak Bisa Membuka NAS dari Ubuntu

Pastikan alamat ditulis dengan benar:

```text
smb://10.4.89.190/mahasiswa
```

Untuk Ubuntu/Linux gunakan format `smb://`.

---

## 10. Panduan Singkat

### Windows

Folder pribadi:

```text
\\10.4.89.190\mahasiswa
```

Folder bersama:

```text
\\10.4.89.190\folder-bersama
```

Logout NAS:

```cmd
net use * /delete /y
```

---

### Ubuntu/Linux

Folder pribadi:

```text
smb://10.4.89.190/mahasiswa
```

Folder bersama:

```text
smb://10.4.89.190/folder-bersama
```

Reset cache SMB:

```bash
killall nautilus
killall gvfsd-smb
killall gvfsd-smb-browse
```

---

## 11. Informasi yang Harus Diberikan Admin ke Anggota Lab

Admin cukup memberikan informasi berikut:

```text
Alamat folder pribadi:
\\10.4.89.190\mahasiswa

Alamat folder bersama:
\\10.4.89.190\folder-bersama

Username:
username masing-masing

Password:
password masing-masing
```

Untuk Ubuntu/Linux:

```text
smb://10.4.89.190/mahasiswa
smb://10.4.89.190/folder-bersama
```

---

## 12. Catatan Penting

* Jangan membagikan username dan password.
* Jangan menyimpan file pribadi di folder bersama.
* File print cukup diletakkan di folder `Print` jika tersedia.
* Jika menggunakan komputer bersama, logout dari NAS setelah selesai.
* Jika terjadi error login, hapus credential lama terlebih dahulu.
* Jika kuota penuh atau folder tidak bisa diakses, hubungi admin lab.
