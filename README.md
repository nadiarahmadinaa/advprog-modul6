# Reflection Modul 6
## Commit 1 Reflection Notes
Method handle_connection berfungsi untuk menghandle request dari TCP stream.
Method ini mengambil input TcpStream, melakukan proses parsing terhadap request, dan mencetak request HTTPnya.
Pertama, kita inisiasi dua variabel,  `buf_reader` untuk membaca input, dan `http_request` untuk menyimpan output.
`http_request` akan diisi oleh buffer dari `buf_reader` yang di-unwrap oleh `.map(|result| result.unwrap())` hingga ditemukan empty line. Kemudian, hasil request yang sudah di-parse ini akan di cetak.