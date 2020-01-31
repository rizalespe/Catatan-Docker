# Instalasi Docker Engine
Halaman ini berisi catatan langkah-langkah dan perintah yang dijalankan untuk melakukan instalasi Docker Engine pada sistem operasi CentOS.
1. Kebutuhan sistem operasi: untuk memastikan bahwa sistem operasi sudah sesuai, jalankan perintah ```cat /etc/os-release ``` untuk mengetahui secara detail sistem operasi apa yang sedang berjalan.
2. Pastikan bahwa repositori ```centos-extras``` telah aktif (enabled). Untuk mengetahui daftar repositori yang ada jalankan perintah ```yum repolist```. Apabila ```CentOS-X - Extras``` tercantum dalam daftar, maka dapat melanjutkan pada proses selanjutnya. Jika ```CentOS-X - Extras``` tidak tercantum, maka jalankan perintah ```yum --enablerepo=extras```
3. Apabila terdapat versi Docker Engine sebelumnya, maka kita perlu melakukan uninstall terlebih dahulu dengan menggunakan perintah sebagai berikut: 
```
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```
4. Install packages yang diperlukan:
```
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```
5. Untuk mendapatkan package docker engine, kita harus menambahkan repositori docker versi stable yaitu dengan menjalankan perintah:
```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
6. Jalankan perintah untuk install Docker Engine:
```
sudo yum install docker-ce docker-ce-cli containerd.io
```
7. Setelah berhasil melakukan instalasi langkah selanjutnya adalah menjalankan service docker dengan perintah:
```
sudo systemctl start docker
```
8. Terakhir, untuk melakukan verifikasi apakah Docker Engine telah berhasil di-install, Docker telah menyediakan sebuah images bernama ```hello-world```. Perintah yang digunakan untuk menginstansiasi container dari image tersebut yaitu:
```
sudo docker run hello-world
```

Sumber: [Instalasi Docker pada Centos](https://docs.docker.com/install/linux/docker-ce/centos/)
