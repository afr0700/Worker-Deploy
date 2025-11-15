🚀 Cloudflare Worker Auto-Deployment Guide
GitHub Actions · Zero-Timeout · Multi-Domain Ready

Dokumen ini menjelaskan dua metode deployment Cloudflare Worker yang dapat Anda gunakan langsung di GitHub Actions.
Disusun ulang dengan gaya berbeda, lebih profesional, dan tetap mudah dipahami.

⭐ Apa yang Bisa Dilakukan Panduan Ini?

Deploy Worker ke Cloudflare otomatis

Mendaftarkan route domain & subdomain tanpa ribet

Menghindari error 504 API Timeout

Mendukung ratusan domain melalui sharding

⚠️ Masalah Umum: Cloudflare Timeout 504

Saat Worker memiliki terlalu banyak rute dalam satu deploy, Cloudflare API tidak mampu memproses semua sekaligus → muncul timeout.

Untuk itu tersedia dua pendekatan, masing-masing dibuat untuk kondisi berbeda.

🔍 Perbandingan Dua Pendekatan
Metode	Karakteristik	Cocok Untuk
1. Legacy – Single Worker	Semua rute digabung ke satu Worker	Proyek kecil, <50 rute
2. Sharded – Multi Worker	Setiap domain dibuatkan Worker unik	Proyek besar, ratusan domain
📦 Struktur File Wajib dalam Repository
File	Keterangan	Dipakai Pada
worker.js	Script Cloudflare Worker	Semua metode
customdomain.txt	Daftar prefix subdomain	Semua metode
main_domains.txt	Daftar domain	Khusus metode shard
[Deploy Injektor].yml	Workflow metode Legacy	Legacy
deploy_chunked.yml	Workflow metode Sharded	Sharding
🧰 Metode 1: Legacy Deployment (Single Worker)

Workflow: [Deploy Injektor].yml

Pendekatan ini memakai 1 Worker untuk seluruh domain & subdomain.

✔️ Yang Perlu Disiapkan

worker_name

main_domain

cloudflare_account_id

cloudflare_api_token

🔁 Cara Kerja

Workflow membaca domain utama.

Semua prefix diambil dari customdomain.txt.

Worker menghasilkan satu daftar rute besar.

Deploy dilakukan satu kali.

Catatan: Jika jumlah rute banyak, kemungkinan besar akan timeout.

🧩 Metode 2: Multi-Worker Sharding (Highly Recommended)

Workflow: deploy_chunked.yml

Setiap domain akan diproses sebagai Worker terpisah → tidak ada rute panjang → no timeout.

✔️ Yang Perlu Disiapkan

Hanya dua input:

cloudflare_account_id

cloudflare_api_token

🤖 Bagaimana Workflow Ini Bekerja?
Tahap	Proses	Tujuan
1. Loader	Membaca semua domain di main_domains.txt	Menentukan jumlah Worker
2. Generator	Membuat Worker baru per domain	Tidak ada beban berlebih
3. Route Builder	Prefix dari customdomain.txt digabung otomatis	Setup massal
4. Deploy Serial	Deploy domain satu-per-satu	Mencegah konflik
5. Cooldown	sleep 20 detik antar deploy	Anti-504 Timeout

Dengan metode sharding, deploy 100–500 domain pun tetap stabil.

▶️ Cara Menjalankan Workflow

Buka menu Actions pada repository GitHub

Pilih workflow:

Legacy → [Deploy Injektor]

Sharded → Deploy Chunked Multi-Domain

Klik Run workflow

Isi kredensial Cloudflare

Jalankan → otomatis deploy 🎉
