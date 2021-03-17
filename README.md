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

**WBO** adalah papan tulis kolaboratif online yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan akan diperbarui secara *real time* untuk semua pengguna yang terhubung, dan statusnya tetap. Aplikasi ini dapat digunakan untuk berbagai tujuan, termasuk seni, hiburan, desain, ataupun pengajaran. Untuk berkolaborasi gambar secara *real time* dengan seseorang, cukup hanya mengirimkan URL-nya saja.

![wbo-draw](https://user-images.githubusercontent.com/57716837/111366807-95cfc400-86c6-11eb-95f8-576fa2754069.png)

## Instalasi
[`^ kembali ke atas ^`](#)

### Kebutuhan Sistem
Berikut versi dari kebutuhan sistem yang kami install dan gunakan :
* Windows 10
* Oracle VM VirtualBox
* VDI Ubuntu 20.04 LTS
* Git version 2.25.1
* Node.js v10.19.0
* npm 6.14.4
* Vim 8.1

### Setup VM

Kami melakukan instalasi dan menjalankan aplikasi WBO menggunakan VM Ubuntu Server. Oleh karena itu, kita perlu membuat sebuah VM dan melakukan beberapa *setting* agar dapat dijalankan di Windows.

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
Sebelum memulai VM, kita harus mengatur *Port Forwarding* terlebih dahulu agar dapat diakses dari luar melalui alamat Host IP (*localhost*).
* Masuk ke *Settings -> Network -> Advanced -> Port Forwarding*.
* Tambahkan tiga aturan *port forwarding* untuk `http`, `ssh`, dan `wbo` (untuk aplikasi WBO) yaitu :

  | Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
  | ---- | -------- | ------- | --------- | -------- | ---------- |
  | http | TCP |  | 8000 |  | 80 |
  | ssh | TCP |  | 2200 |  | 22 |
  | wbo | TCP |  | 50 |  | 5001 |

* Jika sudah selesai, jalankan VM Ubuntu.
* Buka Terminal di VM, lalu unduh informasi *packages* yang terbaru dari repositori.
  ```
  $ sudo apt-get update
  ```
* Install openSSH server.
  ```
  $ sudo apt-get install openssh-server
  ```
* Jalankan SSH, serta pastikan SSH sudah aktif.
  ```
  $ sudo systemctl enable ssh
  $ sudo systemctl start ssh
  $ sudo systemctl status ssh
  ```

### Proses Instalasi di Windows
#### 1. Akses VM dari *Host* menggunakan SSH.
* Buka *Command Prompt* di komputer *host* dan akses VM dengan *username* dan *password* VM yang telah di-setup.
  ```
  ssh username@localhost -p 2200
  ```
#### 2. Instalasi Kebutuhan Sistem
* Install git, node.js, npm, dan vim.
  ```
  $ sudo apt install git
  $ sudo apt install nodejs
  $ sudo apt install npm
  $ sudo apt install vim
  ```
#### 3. Unduh dan Install WBO
* Pertama, unduh WBO dengan cara clone dari original repository.
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
* Terakhir, memulai server pada *port* 5001 dan masukkan *password* VM.
  ```
  $ sudo PORT=5001 npm start
  ```
  Setelah memulai server, aplikasi WBO dapat langsung dijalankan pada komputer *host* di `http://localhost:50` dan akan diteruskan ke *port* 5001 di VM.
  
## Konfigurasi
[`^ kembali ke atas ^`](#)

Saat memulai server WBO, server akan memuat konfigurasinya dari beberapa variabel. Kita dapat melihat daftar variabel ini di `configuration.js`. Beberapa variabel diantaranya :
1. `WBO_HISTORY_DIR`: berfungsi untuk mengkonfigurasi direktori tempat papan disimpan. *Default*-nya adalah `./server-data/`.
2. `WBO_MAX_EMIT_COUNT`: jumlah maksimum pesan yang dapat dikirim per unit waktu. Biasanya digunakan agar kualitas gambar yang dihasilkan dapat lebih halus. Secara *default*, unit kuantitasnya sebesar pesan per 4 detik, dan nilai *default*-nya adalah `192`.

### Translation
WBO tersedia dalam berbagai bahasa. Terjemahan disimpan di `server/translations.json`. Kita dapat menambahkan terjemahan WBO ke dalam bahasa yang belum tersedia. Berikut langkah-langkahnya :

1. Edit isi file server/translations.json.
   ```
   $ sudo vim server/translations.json
   ```
2. Tambahkan isi terjemahan bahasa yang baru di bawah bahasa lain. Misal, menambahkan Bahasa Indonesia ke dalam WBO.
   ```
   "id": {
    "hand": "Tangan",
    "loading": "Memuat",
    "tagline": "Alat menggambar kolaboratif online gratis dan open-source. Buat sketsa ide baru bersama-sama di WBO!",
    "configuration": "Konfigurasi",
    "collaborative_whiteboard": "Papan tulis kolaboratif",
    "size": "Ukuran",
    "zoom": "Perbesar",
    "tools": "Alat",
    "rectangle": "Persegi panjang",
    "square": "Persegi",
    "circle": "Lingkaran",
    "ellipse": "Elips",
    "click_to_toggle": "klik untuk beralih",
    "menu": "Menu",
    "text": "Teks",
    "mover": "Penggerak",
    "straight_line": "Garis lurus",
    "pencil": "Pensil",
    "grid": "Kisi",
    "click_to_zoom": "Klik untuk memperbesar\nTekan shift and klik untuk memperkecil",
    "keyboard_shortcut": "pintasan keyboard",
    "mousewheel": "mouse wheel",
    "opacity": "Opasitas",
    "color": "Warna",
    "eraser": "Penghapus",
    "White-out": "White-out",
    "index_title": "Selamat datang di papan tulis online gratis WBO!",
    "introduction_paragraph": "WBO adalah papan tulis kolaboratif online <a href=\"https://github.com/lovasoa/whitebophir\" title=\"Bebas seperti dalam kebebasan berbicara, bukan bir gratis. Perangkat lunak ini dirilis di bawah lisensi AGPL\">gratis dan open-source</a> yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan akan diperbarui secara real time untuk semua pengguna yang terhubung, dan statusnya tetap. Ini dapat digunakan untuk berbagai tujuan, termasuk seni, hiburan, desain dan pengajaran.",
    "share_instructions": "Untuk berkolaborasi pada gambar secara real time dengan seseorang, cukup hanya mengirimkan URL-nya saja.",
    "public_board_description": "<b>Papan publik</b>dapat diakses oleh semua orang. Ini adalah kekacauan yang menyenangkan dan tidak terorganisir di mana Anda dapat bertemu dengan orang asing yang tidak dikenal dan berkumpul bersama. Segala sesuatu di sana hanya sementara.",
    "open_public_board": "Menuju papan publik",
    "private_board_description": "Anda dapat membuat <b>papan pribadi</b> dengan nama random, yang hanya dapat diakses melalui tautannya. Gunakan ini jika Anda ingin berbagi informasi pribadi.",
    "create_private_board": Buat papan privat",
    "named_private_board_description": "Anda juga dapat <strong>menamai papan pribadi</strong> dengan URL khusus, yang akan dapat diakses oleh semua orang yang mengetahui namanya.",
    "board_name_placeholder": "Nama papan…",
    "view_source": "Sumber kode dari GitHub"
   },
   ```

## Cara Pemakaian
[`^ kembali ke atas ^`](#)

Cara pemakaian WBO sangat mudah karena tampilannya yang sangat sederhana sehingga mudah dimengerti. Berikut lebih jelasnya :
1. Halaman utama.
![1](https://user-images.githubusercontent.com/57716837/111383984-8e66e580-86db-11eb-88f4-71c92610ac26.png)

2. Terdapat beberapa pilihan bahasa yang tersedia sehingga memudahkan kita dalam menggunakannya.
![2](https://user-images.githubusercontent.com/60084871/111375164-86ee0f00-86d0-11eb-8ea0-28b854f4e0e4.png)

3. Tersedia **“Public Board”** dimana nantinya kita dapat menggambar dengan siapapun tanpa mengetahui nama dari setiap pengguna.
![3](https://user-images.githubusercontent.com/60084871/111375214-90777700-86d0-11eb-8a51-501acffeb318.png)

4. Tersedia **“Private Board”** dimana kita dapat membuat *board* pribadi dengan nama random, dan *board* ini pun hanya bisa diakses melalui link tautannya.
![4](https://user-images.githubusercontent.com/60084871/111375229-94a39480-86d0-11eb-9767-e5f54e06288d.png)

5. Tersedia **“Named Private Board”** dimana kita dapat membuat *board* dengan nama yang sesuai kita inginkan, dan kita juga dapat berbagi link tautan *board* tersebut.
![5](https://user-images.githubusercontent.com/60084871/111375246-98371b80-86d0-11eb-9e2a-5228b4a4ef23.png)

6. Tampilan *board*, pada bagian ini terdapat beberapa *tools paint* yang dapat kita gunakan dalam berkolaborasi.
![6](https://user-images.githubusercontent.com/60084871/111375260-9b320c00-86d0-11eb-99b8-5ba44c541f09.png)

## Pembahasan
[`^ kembali ke atas ^`](#)

**WBO** adalah papan tulis kolaboratif online yang memungkinkan banyak pengguna menggambar secara bersamaan di papan virtual besar. Papan akan diperbarui secara *real time* untuk semua pengguna yang terhubung. Sebelum menginstall aplikasi ini, dibutuhkan penginstalan node.js.

### 1. Pendapat tentang Aplikasi WBO
* Kelebihan
  * Membagi fitur menjadi dua kategori, yaitu *public board* dan *private board*.
  * Tidak memerlukan memori yang besar, sehingga sistem ini ringan untuk digunakan.
  * Menampilkan data *real time* penggambaran pada *board*.
* Kekurangan
  * Tampilan yang sangat sederhana, sehingga terlihat kurang menarik.
  * Sistem masih memiliki *tools paint* yang terbatas.

### 2. Perbandingan Aplikasi *Whiteboard* Lainnya
#### a. Jamboard
**Jamboard** adalah papan tulis digital yang memungkinkan tim yang lokasinya berjauhan untuk berkolaborasi membuat atau melakukan diskusi dengan menggambar pada papan secara *real time*.  
Kelebihan :
1. Dapat mengambil gambar dari penelusuran Google dengan cepat.
2. Dapat menyimpan pekerjaan ke Cloud secara otomatis.
3. Menggunakan fitur pengenalan bentuk dan tulisan tangan yang mudah dibaca.

#### b. Open Board
**Open Board** adalah papan tulis interaktif dan revolusioner yang dirancang khusus untuk sekolah dan universitas.  
Kelebihan :
1. Tersedia untuk *mobile*, macOS, Linux, dan Windows.
2. Merupakan solusi *open-source* di bawah GPLv3 dan dikelola komunitas GitHub.
3. Terintegrasi dengan *browser web*.

#### c. Stormboard
**Stormboard** adalah solusi perencanaan dan *brainstorming online* interaktif yang memungkinkan individu dan perusahaan untuk membangun proyek dan berpartisipasi dalam pertemuan jarak jauh dengan lebih mudah.  
Kelebihan :
1. Terintegrasi dengan Google, Microsoft, Trello, dan Pipedrive.
2. Memiliki data keamanan bersertifikat dengan koneksi SSL 256 bit dari internet.
3. Sistem berbasis Cloud yang didukung dengan jam *online* dan bisnis.

## Referensi
[`^ kembali ke atas ^`](#)

Original Repository : [https://github.com/lovasoa/whitebophir](https://github.com/lovasoa/whitebophir)

Artikel Pendukung : https://www.ruangparabintang.com/2020/07/kumpulan-white-board-virtual-terbaik-di.html
