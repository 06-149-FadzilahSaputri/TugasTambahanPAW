# Analisis Step 06: Functional Testing

## Apa yang Dilakukan?
Pada langkah ini, kita menambahkan *library* `webtest` ke dalam dependensi pengembangan (`[dev]`) kita. Kita kemudian **memperluas** file `tutorial/tests.py` kita untuk menyertakan *functional test* baru (`TutorialFunctionalTests`) di samping *unit test* (`TutorialViewTests`) yang sudah ada.

*Test* baru ini memverifikasi bahwa *keseluruhan* aplikasi kita (bukan hanya satu fungsi) merespons dengan benar ke permintaan web.

## Konsep

1.  **Unit Test vs. Functional Test**:
    * **Unit Test** (yang lama): `TutorialViewTests` menguji satu "unit" kode (fungsi `hello_world`) secara terisolasi. Kita menggunakan `pyramid.testing.DummyRequest` (permintaan palsu) untuk ini.
    * **Functional Test** (yang baru): `TutorialFunctionalTests` menguji *seluruh* aplikasi. Ini mensimulasikan *browser* nyata yang membuat permintaan HTTP ke aplikasi WSGI kita dan memeriksa responsnya.

2.  **`webtest` (`TestApp`)**:
    Ini adalah *library* kunci untuk *functional testing*.
    * `from webtest import TestApp`: Kita mengimpor "browser" palsu.
    * `app = main({})`: Di dalam `setUp`, kita mengimpor dan memanggil fungsi `main` dari `__init__.py` untuk membangun *seluruh* aplikasi Pyramid kita.
    * `self.testapp = TestApp(app)`: Kita menginisialisasi `TestApp` dengan aplikasi Pyramid kita yang sudah jadi.

3.  **Menjalankan Functional Test**:
    * `res = self.testapp.get('/', status=200)`: Ini adalah *test* yang sebenarnya. `self.testapp.get` bertindak seperti *browser* yang mengunjungi URL `/`. Parameter `status=200` berarti *test* ini akan otomatis **gagal** jika status responsnya bukan 200 (OK).
    * `self.assertIn(b'<h1>Hello World!</h1>', res.body)`: Ini adalah apa yang kita diskusikan di *step* sebelumnya! Di sini, kita benar-benar memeriksa **isi (body)** dari respons HTML untuk memastikan bahwa teks `<h1>Hello World!</h1>` (sebagai `bytes`, ditandai `b'...'`) ada di dalamnya.

4.  **`pytest`**:
    `pytest` cukup pintar untuk secara otomatis menemukan *kedua* *class* tes (`TutorialViewTests` dan `TutorialFunctionalTests`) di dalam file `tests.py` dan menjalankan semua metode `test_...` di dalam keduanya. Inilah sebabnya kita sekarang melihat "2 passed".

## Cara Menjalankan

Langkah ini tidak menjalankan server web. Langkah ini menjalankan *tests*.

1.  Pastikan *virtual environment* (`env`) sudah aktif.
2.  Masuk ke direktori `06-functional-testing`.
3.  Install `webtest` (dependensi `[dev]` baru) dengan meng-install ulang proyek:
    ```bash
    pip install -e ".[dev]"
    ```
4.  Jalankan *test runner* `pytest` (ini akan menjalankan 2 tes):
    ```bash
    pytest tutorial/tests.py -q -W ignore
    ```

## Bukti Screenshot
![alt text](image.png)