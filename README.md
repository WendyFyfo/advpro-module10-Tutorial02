# MODULE 10 - Tutorial 02

## 2.1
![Running 3 clients and 1 server](/image/image.png)

Program ini mengimplementasikan sistem chat sederhana menggunkana WebSocket di Rust. Server berjalan pada alamat 127.0.0.1:2000 dan dapat menangani banyak klien secara bersamaan. Setiap klien yang berjalan akan memiliki prot berbeda-beda, tetapi terhubung ke port 2000 dan bisa mengirim pesan, dan pesan tersebut akan diteruskan oleh server ke semua klien lain, termasuk dirinya sendiri. Proses ini dilakukan dengan menggunakan channel broadcast dari tokio untuk mengirimkan pesan secara real-time.

Untuk menjalankan, pertama jalankan server terlebih dahulu dengan `cargo run --bin server`, lalu buka tiga terminal berbeda dan jalankan klien di masing-masing terminal denga  `cargo run --bin client`. Ketik pesan dikirim salah satu klien, maka kita akan melihat pesan itu muncul di semua terminal termasuk klien pengirim. Gambar di atas adalah contoh ketika menjalankan program.