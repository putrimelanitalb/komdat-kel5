# Aplikasi WBO

<p align="center">
  <img width="200" src="https://user-images.githubusercontent.com/57716837/111366768-83558a80-86c6-11eb-9bd1-b8fb92ba0b95.jpg")
</p>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:

## Anggota
|   | NIM | Nama |
| - | --- | ---- |
| 1 | G64180034 | Tia Isnawati Noor |
| 2 | G64180038 | Elina Eprida |
| 3 | G64180053 | Putri Melanita Londong Bua |
| 4 | G64180085 | Mutia Marcha Fatika |

## Sekilas Tentang
[`^ kembali ke atas ^`](#)

**WBO** adalah *whiteboard online* kolaboratif yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan akan diperbarui secara *real time* untuk semua pengguna yang terhubung, dan statusnya selalu dipertahankan. Aplikasi ini dapat digunakan untuk berbagai tujuan, termasuk seni, hiburan, desain, ataupun pengajaran. Untuk berkolaborasi gambar secara *real time* dengan seseorang, cukup mengirimkan URL-nya saja.

![wbo-draw](https://user-images.githubusercontent.com/57716837/111366807-95cfc400-86c6-11eb-95f8-576fa2754069.png)

## Instalasi
[`^ kembali ke atas ^`](#)

### Kebutuhan Sistem
Berikut versi dari kebutuhan sistem yang kami install dan gunakan:
* Windows 10
* Oracle VM VirtualBox
* VDI Ubuntu 20.04 LTS
* Git version 2.25.1
* Node.js v10.19.0
* npm 6.14.4
* Vim 8.1

### Setup VM

Kami melakukan instalasi dan menjalankan aplikasi WBO menggunakan VM Ubuntu Server. Oleh karena itu, kami perlu membuat sebuah VM dan melakukan beberapa *setting* agar dapat dijalankan di Windows.

#### 1. Membuat VM Ubuntu Server
* Unduh dan install VM di [sini](https://www.virtualbox.org/wiki/Downloads) dan pilih *Windows hosts*.
* Unduh *virtual disk image* (VDI) untuk instalasi Ubuntu 20.04 LTS di [sini](https://ubuntu.com/download/desktop).
* Buka VM dan klik ikon *New* untuk membuat VM baru.
* Tentukan *Name*, *Machine Folder*, *Type*, dan *Version*. Karena ingin menginstall Ubuntu, untuk *Type* pilih **Linux** dan *Version* pilih **Ubuntu (64-bit)**.
* Alokasikan RAM pada VM dengan rekomendasi minimal 1024 MB.
* Pilih *Create a virtual hard disk now* dan pilih *VDI (VirtualBox Disk Image)*.
* Pilih salah satu opsi sesuai kebutuhan pada *Storage on physical hard disk*.
* Tentukan *File location and size* untuk virtual hard disk (*recommended size* 10 GB).
* VM baru telah dibuat dan dapat memulai VM untuk instalasi Ubuntu.
* Pilih file VDI Ubuntu yang telah diunduh pada *Select start-up disk*.
* Pilih *Install Ubuntu* dan lakukan setup Ubuntu. Tunggu instalasi hingga selesai dan *restart* VM.

#### 2. Setting Port Forwarding VM
Sebelum memulai VM, kami harus mengatur *Port Forwarding* terlebih dahulu agar dapat diakses dari luar melalui alamat Host IP (*localhost*).
* Masuk ke *Settings -> Network -> Advanced -> Port Forwarding*.
* Tambahkan tiga aturan *port forwarding* untuk `http`, `ssh`, dan `wbo` (untuk aplikasi WBO) yaitu:

  | Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
  | ---- | -------- | ------- | --------- | -------- | ---------- |
  | http | TCP |  | 8000 |  | 80 |
  | ssh | TCP |  | 2200 |  | 22 |
  | wbo | TCP |  | 50 |  | 5001 |

* Jika sudah selesai, jalankan VM Ubuntu.
* Buka Terminal di VM, lalu mulai dan aktifkan SSH. Kemudian pastikan SSH sudah aktif.
  ```
  $ sudo systemctl start ssh
  $ sudo systemctl enable ssh
  $ sudo systemctl status ssh
  ```

### Proses Instalasi di Windows
#### 1. Akses VM dari *Host* menggunakan SSH.
* Buka *Command Prompt* di komputer *host* dan akses VM dengan *username* dan *password* VM yang telah di-setup.
  ```
  ssh username@localhost -p 2200
  ```
#### 2. Instalasi Kebutuhan Sistem
* Pastikan seluruh paket sistem dalam versi *up-to-date*.
  ```
  $ sudo apt update
  ```
* Install git, node.js, npm, dan vim.
  ```
  $ sudo apt install git
  $ sudo apt install nodejs
  $ sudo apt install npm
  $ sudo apt install vim
  ```
#### 3. Unduh dan Install WBO
* Pertama, unduh WBO dengan cara clone repository.
  ```
  $ sudo git clone https://github.com/lovasoa/whitebophir.git
  ```
* Pindah ke direktori *whitebophir*.
  ```
  $ cd whitebophir
  ```
* Install *dependencies* untuk WBO
  ```
  $ sudo npm install --production
  ```
* Terakhir, sudah dapat memulai server pada *port* 5001 dan masukkan *password* VM.
  ```
  $ sudo PORT=5001 npm start
  ```
  Setelah memulai server, aplikasi WBO dapat langsung dijalankan pada komputer *host* di `http://localhost:50` dan akan diteruskan ke *port* 5001 di VM.
  
## Konfigurasi
[`^ kembali ke atas ^`](#)

## Cara Pemakaian
[`^ kembali ke atas ^`](#)
    
## Pembahasan
[`^ kembali ke atas ^`](#)

WBO adalah papan tulis kolaboratif online yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan diperbarui secara real time untuk semua pengguna yang terhubung. Sebelum menginstall aplikasi ini dibutuhkan penginstalan node.js atau docker.
* Kelebihan
1. Membagi fitur menjadi 2 kategori yaitu privat dan public
2. Tidak memerlukan memori yang besar sehingga sistem ini ringan untuk digunakan
3. Menampilkan data realtime penggambaran pada board
* Kekurangan
1. Tampilan yang sangat sederhana sehingga terlihat kurang menarik
2. Sistem masih memiliki tools paint yang terbatas

## Referensi
[`^ kembali ke atas ^`](#)

Original Repository : [https://github.com/lovasoa/whitebophir](https://github.com/lovasoa/whitebophir)
