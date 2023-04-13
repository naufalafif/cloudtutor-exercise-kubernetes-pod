### Apa Itu Pod

Pod adalah unit paling kecil dalam sistem Kubernetes. Pod terdiri dari satu atau beberapa container yang saling berbagi sumber daya seperti jaringan, penyimpanan, dan lingkungan. Dalam konteks Kubernetes, pod digunakan sebagai unit untuk deploy dan menjalankan aplikasi.

Jika dilihat sekilas, Pod pada Kubernetes memiliki kemiripan dengan Docker Compose. Keduanya sama - sama digunakan untuk menjalankan satu atau lebih container. Perbedaan antara keduanya adalah container pada pod berjalan pada tempat yang sama, seperti halnya menjalankan beberapa aplikasi tanpa container, dimana bisa saling mengakses direktori yang sama, dan jaringan yang sama (localhost).

#### Analogi

Kita bisa mengibaratkan Pod seperti sebuah keluarga yang tinggal dalam satu rumah. Keluarga ini terdiri dari beberapa anggota (container) yang berbagi sumber daya seperti dapur (network), kamar mandi (volume), dan ruang tamu (environment variable). Setiap anggota keluarga mungkin memiliki tanggung jawab dan fungsinya masing-masing, tetapi mereka saling bergantung dan bekerja sama untuk menjalankan rumah secara efisien.

Salah satu contoh multi-container Pod adalah sebuah aplikasi web dijalankan bersama aplikasi monitoring. Ketika berada dalam satu pod, aplikasi monitoring bisa dengan mudah mengakses aplikasi web karena berada dalam tempat yang sama. ex: `django + fluentd`

Kalian bisa akses penjelasan detail dari **Programmer Zaman Now** pada link dibawah

```{.text .copy}
https://youtu.be/-wkpFv3VxFs?list=PL-CtdCApEFH8XrWyQAyRd6d_CKwxD8Ime

```
