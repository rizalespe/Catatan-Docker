# Dokumentasi inisialisasi web server
Berikut adalah langkah-langkah yang dilakukan untuk menginisiasi web server mulai dari awal:
1. Install perangkat lunak virtualisasi, pada catatan ini saya menggunakan [VirtualBox](https://www.virtualbox.org/)
2. Kemudian langkah selanjutnya adalah instalasi sistem operasi. Saat ini sistem operasi yang saya gunakan adalah linux Centos [ISO](http://isoredirect.centos.org/centos/7/isos/x86_64/)
3. Setelah sistem operasi Linux Centos ter-install, berikut adalah konfigurasi dasar yang perlu dilakukan:
  - Konfigurasi jaringan
      - Ganti mode jaringan pada VirtualBox dari NAT menjadi Bridged Adapter
      - setting network script
          ```
            vi /etc/sysconfig/network-scripts/<nama-interface>
          ```
     
          ```
            BOOTPROTO = static
            ONBOOT = yes
            IPADDR=192.168.0.200 # sesuaikan dengan pola IP address host
            NETMASK=255.255.255.0
            GATEWAY=192.168.0.1 # sesuaikan dengan pola IP address host
            DNS1=1.0.0.1
            DNS2=1.1.1.1
            DNS3=8.8.4.4 
          ```
    - setting machine hostname
        ```
        # nmtui-hostname
        ```
    - setting network interface
        ```
        # nmtui-edit
        ```
    - menyimpan konfigurasi jaringan
        ```
        # nmtui-connect
        ```
    - periksa apakah konfigurasi jaringan telah berjalan
        ```
        # ifconfig enp0s3
        # ip a
        # ping -c2 google.com
        ```
  - Update CentOS system 
      ```
      # yum clean all
      # yum update
      # yum install yum-utils
      ```

  - Konfigurasi repositori
      - install Extra Packages for Enterprise Linux (EPEL)
        ```
        yum -y install epel-release
        yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
        yum install yum-utils
        yum --enablerepo=epel list
        ```

  - Install system utility
    ```
    yum install nano wget curl net-tools lsof bash-completion
    ```

### Apabila akan menggunakan Docker, lanjutkan pada langkah No. 7


4. Install PHP interpreter, pada catatan ini saya melakukan instalasi untuk versi 7.2
  - Turn on Remi repo i.e.remi-php72
    ```
      sudo yum-config-manager --enable remi-php72
    ```
  - Refresh repository
    ```
      sudo yum update
    ```
  - Install PHP
    ```
      sudo yum install php
    ```
  - Install modul yang biasa digunakan
    ```
      sudo yum install php72-php-fpm php72-php-gd php72-php-json php72-php-mbstring php72-php-mysqlnd php72-php-xml php72-php-xmlrpc php72-php-opcache php-intl php-mbstring 
    ```
  - Verifikasi versi PHP
    ```
      php --version
    ```
  - Melihat modul PHP yang terinstall
    ```
      php --modules
    ```
5. Install Apache webserver
  - Update apache
      ```
        yum update httpd
      ```
  - Install apache
      ```
        yum install httpd
      ```
  - Konfigurasi firewall terkait dengan service apache
      ```
        firewall-cmd --permanent --add-service=http
        firewall-cmd --permanent --add-service=https
        firewall-cmd --reload
      ```
6. Uninstall Apache dan PHP
  ```
    yum remove httpd* php*
  ```
7. Install Docker service dengan mengikuti langkah-langkah yang ada pada halaman berikut: [tautan instalasi Docker](https://github.com/rizalespe/Catatan-Docker/blob/master/Instalasi-Docker.md) 
