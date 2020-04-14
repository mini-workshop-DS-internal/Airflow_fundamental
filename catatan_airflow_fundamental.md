## Airflow Fundamental
### Konsep dasar airflow bekerja

- Komponen
<p align="center">
	<img src="airflow_img/1_im.png">
</p>

- Konsep Kunci dalam Aliran Udara
<p align="center">
	<img src="airflow_img/2_im.png">
</p>

- manfaat aliran udara
<p align="center">
	<img src="airflow_img/3_im.png">
</p>

- ini bukan
<p align="center">
	<img src="airflow_img/4_im.png">
</p>

- Kasing untuk utilitas aliran udara
<p align="center">
	<img src="airflow_img/5_im.png">
</p>

- Bagaimana mengelola begitu banyak jenis pipa
<p align="center">
	<img src="airflow_img/6_im.png">
</p>

- arsitektur menggunakan satu node
<p align="center">
	<img src="airflow_img/7_im.png">
</p>

- arsitektur menggunakan banyak node
<p align="center">
	<img src="airflow_img/8_im.png">
</p>

- membandingkan dengan Google Composer
<p align="center">
	<img src="airflow_img/architecture_composer_gcp.svg">
</p>

- scheduler pertama membaca folder dan melihat apakah skripnya memenuhi kriteria
<p align="center">
	<img src="airflow_img/9_im.png">
</p>

- jika bertemu maka buat DagRun di DB, daftarkan skripnya maka DagRun Sedang Berjalan
<p align="center">
	<img src="airflow_img/10_im.png">
</p>

- jadwalkan TaskInances untuk dijalankan kemudian TaskInstance Dijadwalkan
<p align="center">
	<img src="airflow_img/11_im.png">
</p>

- Penjadwal mengirim TaskInstance ke Executor, Executor mengirim TaskInstance ke Sistem Antrian kemudian TaskInstance Diantri
<p align="center">
	<img src="airflow_img/12_im.png">
</p>

- Pelaksana mengeluarkan TaskInstance kemudian memperbarui TaskInstance di MetaDB untuk dijalankan, jadi kemudian Worker yang mengeksekusi TaskInstance
<p align="center">
	<img src="airflow_img/13_im.png">
</p>

- Setelah Tugas Selesai, Pelaksana akan memperbarui TaskInstance ke Sukses tetapi DagRun masih berjalan ke tugas berikutnya dalam Dag itu
<p align="center">
	<img src="airflow_img/14_im.png">
</p>

- Setelah Semua Tugas Selesai dalam Dag, Penjadwal akan memperbarui ke Sukses MetaDB DagRun, atau jika satu tugas gagal sehingga DagRun akan memperbarui ke Gagal
<p align="center">
	<img src="airflow_img/15_im.png">
</p>

- Web Server membaca MetaDB ke Pembaruan UI
<p align="center">
	<img src="airflow_img/16_im.png">
</p>

- Ringkasan
<p align="center">
	<img src="airflow_img/18_im.png">
</p>

1. Penjadwal membaca folder DAG
2. DAG Anda diuraikan oleh proses untuk membuat DagRun berdasarkan parameter penjadwalan DAG Anda
3. TaskInstance digunakan untuk setiap Tugas yang perlu dieksekusi dan ditandai ke "Dijadwalkan" dalam database metadata
4. Penjadwal mendapatkan semua TaskInstance yang ditandai "Dijadwalkan" dari metadata database, mengubah status menjadi "Antri" dan mengirimkannya ke pelaksana yang akan dieksekusi.
5. Pelaksana mengeluarkan Tugas dari antrian (tergantung pada pengaturan eksekusi Anda), mengubah status dari "Antri" menjadi "Berjalan" dan Pekerja mulai mengeksekusi TaskInstances
6. Ketika Tugas selesai, Pelaksana mengubah status tugas tersebut ke status finalnya (sukses, gagal, dll) dalam database dan DagRun diperbarui oleh Penjadwal dengan status "Sukses" atau "Gagal" tentu saja , server web secara berkala mengambil data dari metadaDB untuk memperbarui UI
