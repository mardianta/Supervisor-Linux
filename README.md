# Supervisor - LINUX/UNIX
Supervisor adalah sebuah sistem pemantauan dan pengendalian proses pada lingkungan UNIX yang sering digunakan untuk mengawasi dan menjalankan proses-proses pada sistem. Supervisor memungkinkan Anda untuk mengelola dan menjalankan proses-proses seperti worker, job queue, atau aplikasi lainnya secara terus menerus (persistent) dan dengan lebih aman.

Supervisor dapat digunakan untuk mengawasi dan menjalankan job queue worker pada Laravel. Dengan menggunakan Supervisor, Anda dapat memastikan bahwa job queue worker terus berjalan dan siap menerima dan menjalankan job-job yang masuk ke dalam antrian.

Supervisor bekerja dengan cara melakukan polling secara berkala untuk memantau status proses-proses yang diatur dalam konfigurasi. Jika ada proses yang berhenti atau gagal, Supervisor akan mencoba untuk memulai ulang proses tersebut agar tetap berjalan sesuai dengan konfigurasi yang telah ditentukan.

Berikut adalah beberapa keuntungan menggunakan Supervisor:

1. *Mengelola Proses*: Supervisor dapat mengelola dan menjalankan proses secara otomatis, memastikan proses-proses tersebut tetap berjalan dan selalu aktif.

2. *Restart Otomatis*: Jika proses mengalami kegagalan atau berhenti bekerja, Supervisor akan mencoba untuk memulai ulang proses tersebut, sehingga dapat menghindari downtime yang tidak diinginkan.

3. *Logging*: Supervisor menyediakan fasilitas untuk melacak log aktivitas dari proses-proses yang diawasi.

4. *Monitoring*: Supervisor memungkinkan Anda untuk memantau status proses secara real-time melalui command line, sehingga memudahkan untuk memeriksa kinerja aplikasi.

5. *Konfigurasi Mudah*: Anda dapat mengatur konfigurasi Supervisor dengan mudah melalui file konfigurasi, yang memungkinkan Anda untuk mengatur banyak proses yang berbeda sesuai kebutuhan.

Supervisor memungkinkan Anda untuk mengelola dan menjalankan proses-proses yang kritis dalam lingkungan produksi dengan lebih baik, memberikan stabilitas dan kehandalan pada aplikasi Anda.

- Install Supervisor

        sudo apt-get install supervisor

  Setelah Supervisor terinstal, buatlah file konfigurasi baru untuk menjalankan queue:work. Biasanya, konfigurasi Supervisor disimpan di direktori /etc/supervisor/conf.d/.
- Buatlah file baru dengan ekstensi .conf, misalnya laravel-worker.conf:

        sudo nano /etc/supervisor/conf.d/laravel-worker.conf
  
- Isi file tersebut dengan konfigurasi berikut (sesuaikan dengan lingkungan Anda):

        [program:laravel-worker]
        process_name=%(program_name)s_%(process_num)02d
        command=php /path/to/your/laravel/artisan queue:work --sleep=3 --tries=3 --daemon
        autostart=true
        autorestart=true
        user=your_username
        numprocs=8
        redirect_stderr=true
        stdout_logfile=/path/to/your/laravel/storage/logs/worker.log
        
  - command: Isi dengan perintah yang sesuai untuk menjalankan queue:work. Anda dapat menambahkan opsi-opsi seperti --sleep, --tries, dan --daemon sesuai kebutuhan.
        user: Ganti dengan nama pengguna (username) di server yang memiliki hak akses untuk menjalankan perintah di atas.
  - numprocs: Tentukan berapa banyak worker yang ingin Anda jalankan secara paralel. Anda dapat menyesuaikan jumlahnya sesuai dengan kapasitas server Anda. Biasanya, jumlah worker sebaiknya disetel sesuai dengan jumlah CPU yang ada pada server.
  - stdout_logfile: Tentukan lokasi file log untuk menyimpan keluaran (output) dari worker.

- Muat Ulang Supervisor:
  Setelah Anda menyimpan konfigurasi Supervisor, muat ulang konfigurasi dengan menjalankan perintah:

        sudo supervisorctl reread
        sudo supervisorctl update

- Mulai Worker:
  Sekarang, Anda dapat memulai worker dengan menjalankan perintah berikut:

        sudo supervisorctl start laravel-worker:*
        
  Hal ini akan memulai semua worker yang telah diatur dalam konfigurasi.

- Memantau Worker:
  Untuk memantau status worker, Anda dapat menjalankan perintah:

        sudo supervisorctl status

  Anda akan melihat output yang menunjukkan status worker, apakah sedang berjalan atau tidak.

  Dengan konfigurasi ini, Supervisor akan memastikan bahwa worker terus berjalan secara otomatis. Jika ada job yang masuk dalam antrian, worker akan menjalankan job tersebut secara asinkronus.

  Pastikan Anda telah mengatur konfigurasi worker sesuai dengan kebutuhan dan kapasitas server Anda. Juga, pastikan untuk mencatat log dari worker sehingga Anda dapat memantau aktivitasnya dan melacak setiap masalah yang mungkin terjadi.

Berikut adalah beberapa perintah yang bisa digunakan pada sudo supervisorctl untuk mengelola proses dengan Supervisor:

- Memulai Supervisor: 
    
        sudo service supervisor start

- Menghentikan Supervisor:
    
        sudo service supervisor stop

- Memulai ulang Supervisor: 
    
        sudo service supervisor restart

- Memuat ulang konfigurasi Supervisor: 
    
        sudo supervisorctl reread

- Mengupdate Supervisor dengan konfigurasi baru: 

        sudo supervisorctl update

- Menampilkan status semua proses yang diawasi oleh Supervisor: 

        sudo supervisorctl status

- Memulai proses tertentu yang diawasi oleh Supervisor: 

        sudo supervisorctl start <nama_program>

  Gantilah <nama_program> dengan nama program yang diawasi oleh Supervisor.

- Menghentikan proses tertentu yang diawasi oleh Supervisor:
    
        sudo supervisorctl stop <nama_program>

  Gantilah <nama_program> dengan nama program yang diawasi oleh Supervisor.

- Merestart proses tertentu yang diawasi oleh Supervisor:

        sudo supervisorctl restart <nama_program>

  Gantilah <nama_program> dengan nama program yang diawasi oleh Supervisor.

- Menghentikan semua proses yang diawasi oleh Supervisor:

        sudo supervisorctl stop all
  
- Merestart semua proses yang diawasi oleh Supervisor:

        sudo supervisorctl restart all
  
- Memeriksa log dari proses tertentu:

        sudo supervisorctl tail -f <nama_program>
    Gantilah <nama_program> dengan nama program yang diawasi oleh Supervisor.

Perintah sudo supervisorctl memungkinkan Anda untuk berinteraksi dengan Supervisor secara interaktif dalam shell untuk mengendalikan proses yang diawasi. Gunakan perintah tersebut untuk memulai, menghentikan, merestart, dan melihat status serta log proses yang diatur dalam konfigurasi Supervisor. Pastikan Anda memiliki izin sudo untuk menjalankan perintah ini.
