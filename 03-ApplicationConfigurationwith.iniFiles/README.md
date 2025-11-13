# Analisis Step 03: Configuration Files (.ini)

## Apa yang Dilakukan?
Pada langkah ini, kita beralih dari menjalankan aplikasi secara manual (`python ...`) ke cara yang standar dan terkonfigurasi menggunakan `pserve` dan file `.ini`.

Kita melakukan 3 perubahan:
1.  **Refactoring Kode**: Logika aplikasi dipindahkan dari `tutorial/app.py` ke `tutorial/__init__.py` dan file `app.py` dihapus.
2.  **Konfigurasi**: File `setup.py` diperbarui dengan `entry_point`, dan file `development.ini` baru dibuat.
3.  **Eksekusi**: Aplikasi sekarang dijalankan dengan perintah `pserve`.

## Konsep

1.  **`development.ini`**:
    Ini adalah file konfigurasi. File ini memisahkan "apa yang dijalankan" (kode) dari "bagaimana menjalankannya" (konfigurasi).
    * `[app:main]`: Mendefinisikan aplikasi utama. `use = egg:tutorial` memberi tahu `pserve` untuk mencari *entry point* (titik masuk) bernama `main` dari *package* `tutorial`.
    * `[server:main]`: Mendefinisikan server. `use = egg:waitress#main` memberi tahu `pserve` untuk menggunakan `waitress` sebagai server, dan `listen = localhost:6543` memberitahunya untuk berjalan di port 6543.

2.  **`setup.py` dan `entry_points`**:
    Bagian `entry_points` yang baru di `setup.py` adalah "lem" yang menghubungkan semuanya.
    `'main = tutorial:main'` mendaftarkan *package* `tutorial` ke sistem. Ini memberi tahu siapa pun (seperti `pserve`) bahwa "jika Anda mencari 'main' dari 'tutorial', jalankan fungsi `main` yang ada di dalam *package* `tutorial` (yaitu, `tutorial/__init__.py`)."

3.  **`tutorial/__init__.py` (Refactored)**:
    File ini sekarang berisi fungsi `main` yang dicari oleh `entry_point`. Fungsi `main` ini bertindak sebagai "pabrik" (factory) yang menerima konfigurasi dan mengembalikan aplikasi WSGI yang sudah jadi.

4.  **`pserve`**:
    Ini adalah *script* yang disediakan oleh Pyramid untuk menjalankan aplikasi berbasis file `.ini`.
    * `--reload`: Opsi ini sangat berguna. `pserve` akan memonitor file proyek Anda, dan jika ada perubahan yang disimpan, server akan otomatis di-restart.

## Cara Menjalankan

1.  Pastikan *virtual environment* (`env`) sudah aktif.
2.  Masuk ke direktori yang berisi file `setup.py` dan `development.ini`:
    ```bash
    cd "03-ApplicationConfigurationWith.iniFiles"
    ```
3.  Install (atau install ulang) proyek dalam mode *editable* untuk mendaftarkan `entry_point`:
    ```bash
    pip install -e .
    ```
4.  Jalankan server menggunakan `pserve` dan file `.ini`:
    ```bash
    pserve development.ini --reload
    ```
5.  Buka *browser* dan kunjungi alamat `http://localhost:6543`.

## Bukti Screenshot

![alt text](image.png)