# Supervisor-Linux
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
  
Memeriksa log dari proses tertentu:

    sudo supervisorctl tail -f <nama_program>
    
Gantilah <nama_program> dengan nama program yang diawasi oleh Supervisor.

Perintah sudo supervisorctl memungkinkan Anda untuk berinteraksi dengan Supervisor secara interaktif dalam shell untuk mengendalikan proses yang diawasi. Gunakan perintah tersebut untuk memulai, menghentikan, merestart, dan melihat status serta log proses yang diatur dalam konfigurasi Supervisor. Pastikan Anda memiliki izin sudo untuk menjalankan perintah ini.
