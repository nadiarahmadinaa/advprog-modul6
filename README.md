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

## Commit 3 Reflection Notes
![Commit 3 screen capture](/assets/images/screenshot_commit3.jpg)
Pada commit ini, saya telah melakukan refactoring terhadap method handle_connection, yang sebelumnya:
``` 
    if request_line == "GET / HTTP/1.1" {
        let status_line = "HTTP/1.1 200 OK";
        let contents = fs::read_to_string("hello.html").unwrap();
        let length = contents.len();

        let response = format!(
            "{status_line}\r\nContent-Length: {length}\r\n\r\n{contents}"
        );

        stream.write_all(response.as_bytes()).unwrap();
    } else {
        let status_line = "HTTP/1.1 404 NOT FOUND";
        let contents = fs::read_to_string("404.html").unwrap();
        let length = contents.len();

        let response = format!(
            "{status_line}\r\nContent-Length: {length}\r\n\r\n{contents}"
        );

        stream.write_all(response.as_bytes()).unwrap();
    }
```
menjadi
```
let (status_line, filename) = if request_line == "GET / HTTP/1.1" {
        ("HTTP/1.1 200 OK", "hello.html")
    } else {
        ("HTTP/1.1 404 NOT FOUND", "404.html")
    };

    let contents = fs::read_to_string(filename).unwrap();
    let length = contents.len();

    let response =
        format!("{status_line}\r\nContent-Length: {length}\r\n\r\n{contents}");

    stream.write_all(response.as_bytes()).unwrap();
```
Refactor ini diperlukan untuk menghindari code duplication yang terdapat pada kedua if-else case. Terdapat logic yang sama pada penulisan status_line, mendapatkan contents, mendapatkan length, dan merakit response. Dari if else case tersebut, hanya perlu dimasukkan status_line dan filename yang berbeda dari masing-masing case. Refactor ini memberikan readability yang lebih baik dan menghindari repetisi, serta memberikan ruang untuk code extension.