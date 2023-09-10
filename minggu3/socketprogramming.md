# Socket Programming

### Server_single.c:

1. **Pendahuluan**:
   - Program ini adalah contoh server sederhana yang menggunakan pendekatan single-threaded untuk melayani koneksi klien.
   
2. **Header Files**:
   - Kode ini menggunakan beberapa header files standar dalam bahasa C seperti `<stdio.h>`, `<stdlib.h>`, `<netdb.h>`, `<netinet/in.h>`, dan `<string.h>`.
   - Header files ini menyediakan definisi dan fungsi yang diperlukan untuk operasi input/output, manipulasi string, dan berinteraksi dengan jaringan.

3. **Inisialisasi**:
   - Server ini menginisialisasi struktur `sockaddr_in` yang merepresentasikan alamat dan port tempat server akan mendengarkan.
   - Menetapkan nomor port dan alamat IP dengan `INADDR_ANY` (artinya akan mendengarkan semua antarmuka yang tersedia).

4. **Socket Creation**:
   - Server membuat soket dengan memanggil `socket(AF_INET, SOCK_STREAM, 0)`. Ini menciptakan soket menggunakan protokol IPv4 dan jenis soket TCP (SOCK_STREAM).

5. **Binding**:
   - Server mengikat soket ke alamat yang telah diinisialisasi sebelumnya menggunakan `bind`.
   - Jika binding gagal, server mencetak pesan kesalahan dan keluar.

6. **Listening**:
   - Server memulai mendengarkan koneksi dari klien menggunakan `listen`. Dalam contoh ini, server dapat menangani hingga 5 koneksi secara bersamaan.

7. **Menerima Koneksi**:
   - Ketika klien terhubung, server memanggil `accept` untuk menerima koneksi.
   - Ini menghasilkan soket baru (`newsockfd`) yang akan digunakan untuk berkomunikasi dengan klien.

8. **Komunikasi dengan Klien**:
   - Server membaca pesan dari klien menggunakan `read` dan meresponsnya dengan mengirim pesan yang sama menggunakan `write`.
   - Jika pesan dari klien adalah "quit", server keluar dari loop dan program berakhir.

### Server.c:

1. **Pendahuluan**:
   - Program ini adalah contoh server yang lebih kompleks yang menggunakan pendekatan multi-threaded untuk melayani beberapa koneksi klien secara bersamaan.

2. **Fungsi Tambahan**:
   - Program ini mendefinisikan beberapa fungsi tambahan seperti `bzero`, `bcopy`, `init_sockaddr_in`, dan `process_operation`.
   - `bzero` dan `bcopy` digunakan untuk menginisialisasi dan menyalin memori. Meskipun sekarang jarang digunakan, mereka adalah bagian dari versi lama dari pustaka C.
   - `init_sockaddr_in` menginisialisasi dan mengembalikan struktur `sockaddr_in`.
   - `process_operation` adalah contoh fungsi pengolahan data yang sederhana.

3. **Inisialisasi dan Binding**:
   - Server melakukan inisialisasi dan binding serupa dengan `Server_single.c`.

4. **Mengelola Koneksi**:
   - Server menciptakan proses anak untuk menangani setiap koneksi klien dengan memanggil `fork`. Setiap proses anak memiliki soketnya sendiri untuk berkomunikasi dengan klien.

5. **Timeout**:
   - Server memiliki mekanisme timeout yang memungkinkan server menutup koneksi jika tidak ada aktivitas dari klien selama beberapa waktu.

6. **Mengelola Klien**:
   - Dalam setiap proses anak, server membaca pesan dari klien, memprosesnya, dan mengirimkan respons.

### Client.c:

1. **Pendahuluan**:
   - Program ini adalah contoh klien yang berkomunikasi dengan server yang dijalankan di host lokal pada port tertentu.

2. **Inisialisasi dan Koneksi**:
   - Klien menciptakan soket dan menggunakan `gethostbyname` untuk mendapatkan informasi host server.
   - Selanjutnya, klien terhubung ke server menggunakan `connect`.

3. **Komunikasi dengan Server**:
   - Klien memasukkan pesan yang ingin dikirimkan ke server melalui `scanf`.
   - Pesan dikirim menggunakan `write`.
   - Klien kemudian membaca respons dari server menggunakan `read` dan mencetaknya.

4. **Pesan "quit"**:
   - Klien dapat keluar dari loop dengan memasukkan pesan "quit".

### Hubungan dengan Socket Programming:

Kode-kode ini memanfaatkan fungsi-fungsi dasar dari pustaka socket. Mereka menciptakan, mengikat, mendengarkan, dan menerima koneksi pada sisi server. Pada sisi klien, mereka menciptakan soket, menghubungkan ke server, dan melakukan operasi baca/tulis untuk berkomunikasi. Dengan cara ini, mereka membentuk dasar dari komunikasi jaringan menggunakan protokol TCP/IP melalui socket. Masing-masing contoh menunjukkan berbagai aspek socket programming, dari penanganan koneksi tunggal hingga multi-threading untuk mendukung banyak koneksi secara bersamaan.
