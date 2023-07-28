# Supervisor-Linux

- Install Supervisor

        sudo apt-get install supervisor

- Setelah Supervisor terinstal, buatlah file konfigurasi baru untuk menjalankan queue:work. Biasanya, konfigurasi Supervisor disimpan di direktori /etc/supervisor/conf.d/.
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
