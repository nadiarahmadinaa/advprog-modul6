# Reflection Modul 6
## Commit 1 Reflection Notes
Method handle_connection berfungsi untuk menghandle request dari TCP stream.
Method ini mengambil input TcpStream, melakukan proses parsing terhadap request, dan mencetak request HTTPnya.
Pertama, kita inisiasi dua variabel,  `buf_reader` untuk membaca input, dan `http_request` untuk menyimpan output.
`http_request` akan diisi oleh buffer dari `buf_reader` yang di-unwrap oleh `.map(|result| result.unwrap())` hingga ditemukan empty line. Kemudian, hasil request yang sudah di-parse ini akan di cetak.

## Commit 2 Reflection Notes
![Commit 2 screen capture](/assets/images/screenshot_commit2.jpg)
Pada commit ini, method handle_connection telah dimodifikasi dengan tiga variabel baru.
Variabel pertama adalah `status_line` yang mengandung status code dari response HTTP yang akan di return.
Variabel kedua adalah `contents` yang mengandung isi dari hello.html sebagai string.
Variabel ketiga adalah `length` yang berisi hasil penghitungan panjang string tersebut.
Variabel keempat adalah `response` yang mengandung HTTP response secara utuh. Variabel ini terdiri dari tiga variabel sebelumnya, yang sudah di-format sesuai dengan response HTTP.