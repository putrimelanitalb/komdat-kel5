# Aplikasi Web WBO

<p align="center">
  <img width="200" src="https://user-images.githubusercontent.com/57716837/111347150-809c6a80-86b1-11eb-9111-296800d26426.jpg")
</p>
  
## Anggota
|   | NIM | Nama |
| - | --- | ---- |
| 1 | G64180034 | Tia Isnawati Noor |
| 2 | G64180038 | Elina Eprida |
| 3 | G64180053 | Putri Melanita Londong Bua |
| 4 | G64180085 | Mutia Marcha Fatika |

---

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:

## Sekilas Tentang
[`^ kembali ke atas ^`](#)

**WBO** adalah *whiteboard online* kolaboratif yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan akan diperbarui secara *real time* untuk semua pengguna yang terhubung, dan statusnya selalu dipertahankan. Aplikasi ini dapat digunakan untuk berbagai tujuan, termasuk seni, hiburan, desain, ataupun pengajaran. Untuk berkolaborasi gambar secara *real time* dengan seseorang, cukup kirimkan saja URL-nya.

## Instalasi
[`^ kembali ke atas ^`](#)

### Membuat VM Ubuntu Server
....

### Kebutuhan Sistem
- Windows
- Git 2.25+
- Node.js 10.0+
- NPM 6.14+
- VIM 8.1+

### Proses Instalasi
**1. Instalasi Kebutuhan Sistem**
* Pastikan seluruh paket sistem dalam versi *up-to-date*.
  ```
  $ sudo apt update
  ```
* Install `git`, `node.js`, `npm`, dan `vim`.
  ```
  $ sudo apt install git
  $ sudo apt install nodejs
  $ sudo apt install npm
  $ sudo apt install vim
  ```
#### 2. Unduh dan Install WBO
* Pertama, unduh WBO dengan cara clone repository.
  ```
  $ sudo git clone https://github.com/lovasoa/whitebophir.git
  ```
* Pindah ke direktori `whitebophir`.
  ```
  $ cd whitebophir
  ```
* Install `dependencies` untuk WBO
  ```
  $ sudo npm install --production
  ```
* Terakhir, sudah dapat memulai server pada *port* 5001
  ```
  $ sudo PORT=5001 npm start
  ```
  Setelah memulai server, aplikasi WBO dapat langsung dijalankan pada komputer di `http://localhost:50` dan akan diteruskan ke *port* 5001 di VM.
  
## Konfigurasi
[`^ kembali ke atas ^`](#)

## Cara Pemakaian
[`^ kembali ke atas ^`](#)
    
## Pembahasan
[`^ kembali ke atas ^`](#)

## Referensi
[`^ kembali ke atas ^`](#)

Original Repository : [https://github.com/lovasoa/whitebophir](https://github.com/lovasoa/whitebophir)
