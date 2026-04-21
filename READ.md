# Reflection Notes - Modul 6 Concurrency

## Commit 1 Reflection Notes

Dalam fungsi `handle_connection`, terdapat beberapa hal yang terjadi untuk memproses koneksi yang masuk.
Pertama, ada **BufReader**, ini untuk membungkus `TcpStream` ke dalam `BufReader`. Ini dilakukan untuk meningkatkan efisiensi pembacaan data. Dibandingkan membaca data byte-per-byte langsung dari stream, `BufReader` melakukan manajemen buffer di memori.
Kedua, ada **.lines()** untuk membagi aliran data/ stream menjadi baris-baris teks berdasarkan karakter *newline*.
Ketiga, ada **.map(|result| result.unwrap())**, karena setiap baris hasil pembacaan bisa saja gagal/ error, kita melakukan `unwrap` untuk mengambil string aslinya.
Keempat, ada **.take_while(|line| !line.is_empty())**, ini adalah HTTP Request yang selalu diakhiri dengan baris kosong. Kode ini memberitahu program untuk berhenti membaca setelah menemukan baris kosong tersebut agar tidak menunggu selamanya.
Terakhir, ada **.collect()** yang mengumpulkan semua baris teks yang telah diproses ke dalam sebuah Vector (`Vec<_>`).
