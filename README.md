# Module 10 - Timer

* Nama  : Ischika Afrilla
* NPM   : 2306227955

## Refleksi
![Experiment 1.2: Understanding how it works.](images/Screenshot%202025-05-12%20204308.png)

Berdasarkan gambar di atas, terlihat bahwa `Chika' Computer: hey hey` dieksekusi terlebih dahulu dibandingkan dengan `Chika' Computer: howdy!` dan `Chika' Computer: done!`. Hal ini terjadi karena `Chika' Computer: hey hey` berada di luar fungsi `async`, sehingga dieksekusi secara langsung oleh thread utama sebelum eksekusi asinkron dimulai. Sementara itu, blok kode yang berisi `Chika' Computer: howdy!` dan `Chika' Computer: done!` merupakan bagian dari task asinkron yang dijalankan oleh executor melalui spawner. Karena sifat asynchronous tersebut, task tersebut tidak langsung dijalankan saat fungsi `spawn` dipanggil, melainkan dijadwalkan untuk dieksekusi kemudian oleh `executor`. Setelah perintah `println!("Chika' Computer: hey hey");` selesai, barulah executor mulai menjalankan task yang tertunda, yaitu mencetak `Chika' Computer: howdy!` dan menunggu selama dua detik menggunakan `TimerFuture` untuk mencetak `Chika' Computer: done!`.