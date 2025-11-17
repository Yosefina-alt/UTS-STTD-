# UTS-STDT-
Jelaskan teorema CAP dan BASE dan keterkaitan keduannya.jelaskan menggunakan contoh yang pernah anda gunakan:

**1. Teorema CA**
   
CAP theorem menyatakan bahwa dalam sistem terdistribusi, Anda hanya dapat memaksimalkan dua dari tiga properti berikut secara bersamaan:

a. C – Consistency

   Semua node memberikan data yang sama pada waktu yang sama.

b. A – Availability

   Sistem selalu memberikan respons, meskipun responsnya mungkin bukan data terbaru.

c. P – Partition Tolerance

   Sistem tetap berjalan meskipun terjadi kegagalan jaringan antar-node.

Tidak mungkin mendapatkan C, A, dan P secara sempurna sekaligus.

**Contoh yang pernah saya gunakan: Aplikasi Chat Sederhana**

Ketika jaringan antar server terputus (partition), aplikasi chat harus memilih:

a. CA (Consistency + Availability) tidak mungkin karena jika jaringan putus, Anda harus memilih salah satunya.

b. CP (Consistency + Partition-tolerance) → Pesan tidak ditampilkan sampai semua server sinkron.
Pengguna merasa lama karena harus menunggu.

c. AP (Availability + Partition-tolerance) → Pesan tetap terkirim cepat, tapi mungkin muncul dalam urutan yang salah selama beberapa detik.
Ini pilihan WhatsApp/Telegram.

**2. BASE (Basically Available, Soft State, Eventual Consistency)**

BASE adalah pendekan yang menjelaskan pendekatan non-ACID pada database skala besar, terutama NoSQL.

a.Basically Available

Sistem tetap responsif meski datanya mungkin sementara tidak konsisten.

b.Soft State

Data bisa berubah seiring waktu karena proses replikasi.

c.Eventual Consistency

Pada akhirnya, semua node akan konsisten, tetapi tidak harus langsung.

BASE muncul sebagai praktik untuk mewujudkan sistem AP dalam CAP.

Contoh yang pernah saya gunakan: Marketplace (Stok Produk)

Misalnya ada produk "Sepatu A" dengan stok 1:

a.Dua user membeli sekaligus.

b.Karena menggunakan sistem BASE, kedua server mungkin belum sinkron.

c.Kedua user mungkin melihat stok “1” pada waktu yang sama.

d.Tetapi dalam akhirnya, sistem akan konsisten: salah satu order dibatalkan atau diganti.

**3. Keterkaitan CAP dan BASE**

CAP Property	                                          BASE Handling

Availability + Partition Tolerance (AP)	                BASE digunakan karena memberi eventual consistency

Consistency + Partition Tolerance (CP)	                Biasanya pakai ACID, bukan BASE

BASE mengorbankan strong consistency demi skalabilitas	Sesuai dengan pilihan AP pada CAP

**4. Menghubungkan semuanya dengan contoh**
Contoh 1: Aplikasi Chat

a.Mengutamakan Availability → pesan harus terkirim cepat.

b.Tetap berjalan meski jaringan antar data center bermasalah → Partition Tolerance.

c.Konsistensi di-relaksasi → pesan boleh terlambat sinkron.
→ AP → BASE (eventual consistency).

Contoh 2: Sistem marketplace

a.Perubahan stok menyebar sedikit terlambat → BASE.

b.Marketplace memilih Availability karena pengguna tidak bisa menunggu server sinkron.

c.Kompatibel dengan CAP → AP system.
