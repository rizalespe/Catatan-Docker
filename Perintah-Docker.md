# Perintah pada Docker CLI

Sebelum mulai menjalankan perintah pada Docker, pastikan bahwa Docker daemon/service telah berjalan (catatan ini dibuat untuk sistem operasi CentOS Linux 7):
```
service docker status
```
Apabila service belum berjalan, maka jalankan service terlebih dahulu:
```
service docker start
```
Untuk menampilkan panduan penggunaan Docker, jalankan perintah help:
```
docker --help
```
Lebih spesifik untuk mengetahui panduan pada perintah/command tertentu jalankan perintah berikut ini:
```
docker COMMAND --help
```
Pada Docker terdapat dua entitas penting yang perlu dipahami:
1. **Docker Images** merupakan semacam "cetakan" paket yang terdiri dari beberapa lapis/tumpukan apapun yang mendukung agar sistem dapat berjalan yang terdiri dari kode program, runtime, libraries, environment variable, dan file konfigurasi.

2. **Docker Container** container merupakan hasil instansiasi dari docker image yang berjalan pada runtime memory. Dari satu docker image yang sama dapat diinstansiasi menjadi lebih dari satu container dengan konfigurasi yang berbeda-beda. Ketika container dijalankan, maka akan dijalankan secara terpisah dengan proses yang ada pada host (masing-masing container dapat dikonfigurasi secara khusus untuk memiliki akses pada file dan port host). 

sumber: [Penjelasan terkait Images dan Container](https://docs.docker.com/v17.09/get-started/#a-brief-explanation-of-containers) 

## Docker Images
Secara umum terdapat 2 cara untuk membuat mendapatkan image yang nantinya akan diinstansiasi menjadi container, yaitu:
1. Membuat image mulai dari awal atau turunan dari image lain sesuai kebutuhan kita sesuai [panduan](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
2. Memanfaatkan docker image yang tersedia di repositori image yang telah di-deploy sebelumnya seperti pada [Docker Hub](https://hub.docker.com/search?q=&type=image)

### Mendapatkan docker image dari repositori
Untuk mendapatkan image dari repositori yang tersedia, jalankan perintah berikut ini:
```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]; # Contoh: docker pull hello-world
```
### Menampilkan images yang telah ada pada local environment
```
sudo docker images -a
```
## Docker Container
### Instansiasi docker images menjadi docker container
```
sudo docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
sebagai contoh, kita akan melakukan instansiasi pada image ```hello-world``` dengan perintah di bawah ini:
```
sudo docker run --name my-hello-world hello-world 
```
Berikut adalah contoh lain untuk docker image miniconda: 
```
docker pull continuumio/miniconda
```
Selanjutnya, instansiasi dari images untuk menjadi container dimana ketika container dijalnkan pada runtime memiliki gui web based jupyter, perintah yang dijalankan sebagai berikut:  
```
docker run --name conda-no-gui -i -t -p 80:80 continuumio/miniconda3
```
Instalasi package jupyterlab:
```
conda install -c conda-forge jupyterlab
```
menjalankan service untuk jupyter lab:
```
jupyter lab --port 80 --ip 0.0.0.0 --allow-root
```
Ketiga perintah di atas dapat dieksekusi dalam satu perintah sebagai berikut:
```
docker run --name conda-python3.6-gui -i -t -p 80:80 continuumio/miniconda3 /bin/bash -c "/opt/conda/bin/conda install -c conda-forge jupyterlab -y --quiet && /opt/conda/bin/jupyter lab --ip='0.0.0.0' --port=80  --allow-root"
```
pada console akan muncul hasil perintah yang dijalankan seperti berikut:

```
To access the notebook, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/nbserver-1-open.html
    Or copy and paste one of these URLs:
        http://73bf86954abf:80/?token=c82f9e74c4a24f18d1fe0c72d6c4c51fdfa0149d37c973cX
     or http://127.0.0.1:80/?token=c82f9e74c4a24f18d1fe0c72d6c4c51fdfa0149d37c973cX
```
Untuk memulai menggunakan jupyter, gunakan browser dan akses pada alamat ```http://127.0.0.1:80/?token=c82f9e74c4a24f18d1fe0c72d6c4c51fdfa0149d37c973cX``` atau ```http://<IP_ADDRESS>:80/?token=c82f9e74c4a24f18d1fe0c72d6c4c51fdfa0149d37c973cX```

### Menampilkan container yang telah terinstansiasi
Menampilkan container yang sedang berjalan (running)
```
sudo docker ps
```
Menampilkan seluruh container (baik yang sedang berjalan dan berhenti)
```
sudo docker ps -a
```
### Menghapus container yang telah terinstansiasi
```
sudo docker rm CONTAINER
```
### Menghapus images yang ada pada local environment
```
docker rmi IMAGE
```
## Docker Compose
merupakan salah satu komponen Docker yang digunakan untuk menyusun Docker images sesuai dengan kebutuhan kita.
### Instalasi docker compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```
