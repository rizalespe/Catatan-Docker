# Instalasi MariaDB Server
1. Menambahkan repositori MariaDB
  ```
  sudo yum install wget
  wget https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
  chmod +x mariadb_repo_setup
  sudo ./mariadb_repo_setup
  ```
 2. Instalasi MariaDB server
  ```
  # sudo yum install MariaDB-server
  ```
 3. Start service database server
  ```
  # sudo systemctl start mariadb.service
  ```
 4. Secure installation
  ```
  # sudo mysql_secure_installation
  ```
