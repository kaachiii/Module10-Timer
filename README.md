# Module 10 - Timer

* Nama  : Ischika Afrilla
* NPM   : 2306227955

## Refleksi
### Experiment 1.2: Understanding how it works.
![Experiment 1.2: Understanding how it works.](images/Screenshot%202025-05-12%20204308.png)

Berdasarkan gambar di atas, terlihat bahwa `Chika' Computer: hey hey` dieksekusi terlebih dahulu dibandingkan dengan `Chika' Computer: howdy!` dan `Chika' Computer: done!`. Hal ini terjadi karena `Chika' Computer: hey hey` berada di luar fungsi `async`, sehingga dieksekusi secara langsung oleh thread utama sebelum eksekusi asinkron dimulai. Sementara itu, blok kode yang berisi `Chika' Computer: howdy!` dan `Chika' Computer: done!` merupakan bagian dari task asinkron yang dijalankan oleh executor melalui spawner. Karena sifat asynchronous tersebut, task tersebut tidak langsung dijalankan saat fungsi `spawn` dipanggil, melainkan dijadwalkan untuk dieksekusi kemudian oleh `executor`. Setelah perintah `println!("Chika' Computer: hey hey");` selesai, barulah executor mulai menjalankan task yang tertunda, yaitu mencetak `Chika' Computer: howdy!` dan menunggu selama dua detik menggunakan `TimerFuture` untuk mencetak `Chika' Computer: done!`.

### Experiment 1.3: Multiple Spawn and removing drop
Multiple spawns with drop spawner
![Multiple spawns with drop spawner](images/Screenshot%202025-05-12%20215005.png)

Multiple spawns without drop spawner
![Multiple spawns without drop spawner](images/Screenshot%202025-05-12%20210227.png)

Berdasarkan kedua gambar di atas, terlihat bahwa output `howdy` dan `done` dari masing-masing task tidak tercetak secara langsung berurutan. Hal ini disebabkan oleh adanya delay selama dua detik yang diatur menggunakan `TimerFuture`, sehingga setiap task akan menunggu sebelum mencetak `done`. Selain itu, urutan kemunculan output `howdy` dan `done` bisa berbeda tergantung bagaimana executor menjadwalkan task asinkron yang sudah dikirim melalui `spawner`. Selain itu, jika baris `drop(spawner)` dihapus, maka program tidak akan pernah selesai atau berhenti. Hal ini terjadi karena `executor` terus menunggu kemungkinan adanya task baru, dan tanpa `drop(spawner)`, ia tidak mengetahui bahwa semua task telah selesai dikirim sehingga tidak akan keluar dari loop eksekusinya.