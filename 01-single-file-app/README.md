# Analisis Step 01: Single-File Web Applications

## Apa yang Dilakukan?
Pada langkah ini, kita membuat aplikasi web Pyramid sederhana menggunakan satu file Python (`app.py`). Aplikasi ini dijalankan menggunakan server `waitress` dan menampilkan teks "Hello World!" sebagai HTML `<h1>` ketika seseorang mengakses halaman utama (`/`).


## Konsep

1.  **Waitress (`from waitress import serve`)**:
    Ini adalah server WSGI yang *production-grade* (siap untuk produksi). Berbeda dengan `simple_server` bawaan Python, `waitress` dirancang untuk menangani lalu lintas web yang sebenarnya. Kita meng-import fungsi `serve` darinya.

2.  **View Callable (`hello_world`)**:
    Fungsi Python yang menerima `request` dan mengembalikan `Response`. Kali ini, `Response` berisi string HTML (`'<body><h1>Hello World!</h1></body>'`), yang akan di-render oleh *browser* sebagai teks tebal (heading).

3.  **Configurator (`with Configurator() as config:`)**:
    Objek utama Pyramid untuk mendaftarkan semua rute, view, dan pengaturan.

4.  **Route & View (`.add_route` dan `.add_view`)**:
    Logikanya tetap sama:
    * `config.add_route('hello', '/')`: Memetakan URL `/` ke nama rute `hello`.
    * `config.add_view(hello_world, route_name='hello')`: Menghubungkan nama rute `hello` ke fungsi `hello_world`.

5.  **Menjalankan Server (`serve(app, ...`)**:
    Alih-alih menggunakan `make_server(...).serve_forever()`, kita hanya memanggil fungsi `serve` dari `waitress` dan memberinya aplikasi (`app`) kita, serta `host` dan `port` yang diinginkan.

## Cara Menjalankan

1.  Pastikan *virtual environment* (`env`) sudah aktif.
2.  Pastikan Anda telah meng-install `waitress`:
    ```bash
    pip install waitress
    ```
3.  Masuk ke direktori yang berisi file `app.py`:
    ```bash
    cd 01-single-file-app
    ```
4.  Jalankan file Python-nya:
    ```bash
    python app.py
    ```
5.  Buka *browser* dan kunjungi alamat `http://localhost:6543`.

## Bukti Screenshot
![alt text](image.png)