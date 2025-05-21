# MODULE 10 - Tutorial 02

## 2.1
![Running 3 clients and 1 server](/image/image.png)

Program ini mengimplementasikan sistem chat sederhana menggunkana WebSocket di Rust. Server berjalan pada alamat 127.0.0.1:2000 dan dapat menangani banyak klien secara bersamaan. Setiap klien yang berjalan akan memiliki prot berbeda-beda, tetapi terhubung ke port 2000 dan bisa mengirim pesan, dan pesan tersebut akan diteruskan oleh server ke semua klien lain, termasuk dirinya sendiri. Proses ini dilakukan dengan menggunakan channel broadcast dari tokio untuk mengirimkan pesan secara real-time.

Untuk menjalankan, pertama jalankan server terlebih dahulu dengan `cargo run --bin server`, lalu buka tiga terminal berbeda dan jalankan klien di masing-masing terminal denga  `cargo run --bin client`. Ketik pesan dikirim salah satu klien, maka kita akan melihat pesan itu muncul di semua terminal termasuk klien pengirim. Gambar di atas adalah contoh ketika menjalankan program.

## 2.2
![Modify server port to be 8080](/image/image%20copy.png)

```rust
\\ server.rs
    let listener = TcpListener::bind("127.0.0.1:8080").await?;
    println!("listening on port 8080");
```
baris pertama memberitahu server untuk mendengarkan koneksi TCP pada port 8080, bukan 2000. Baris kedua diubah agar pesan yang ditampilkan sesuai dengan port yang didengarkan.


```rust
\\ client.rs
    let (mut ws_stream, _) = ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
                            .connect()
                            .await?;
```
port diubah ke 8080 agar terhubung ke port yang sama dengan port yang digunakan server.

## 2.3
![Add sender IP and port to message](/image/image%20copy.png)
```rust
\\ server.rs
    if let Some(text) = msg.as_text() {
        println!("From client {addr:?} {text:?}");
        bcast_tx.send(format!("{addr}: {text}"))?;
    }
```
Baris kedua membuat format teks yang dicetak dalam server menampilkan address dan port client. Baris ketiga memformat pesan yang dikirimkan ke client untuk mengandung address pengirim.
