META-ENV is Vulnerable Environment which consist Vulnerable Application.
Installation :
1. Install Drupal 7.57 (Vulnerable #1)
   - tar -xfv drupal-7.57.tar.gz
   - sudo cp -r drupal-7.57/. /var/www/html
   - sudo chmod -R 755 /var/www/html/*
   - sudo chown -R www-data:www-data /var/www/html/*
   - check IP (username, password, dan db_name)

2. Install vsftpd 2.3.4 (Vulnerable #2)
   - sudo apt-get install build-essential
   - cd vsftpd-2.3.4/
   - nano Makefile
     tambahkan -lcrypt pada LINK = (line 9)
   - make
   - sudo useradd nobody
   - sudo mkdir /usr/share/empty
   - sudo cp vsftpd /usr/local/sbin/vsftpd
   - sudo cp vsftpd.8 /usr/local/man/man8
   - sudo cp vsftpd.conf.5 /usr/local/man/man5
   - sudo cp vsftpd.conf /etc
   - nano /etc/vsftpd.conf
     sesuaikan local_enable=YES
   - sudo mkdir /var/ftp/
   - useradd -d /var/ftp ftp
   - sudo chown root:root /var/ftp
   - sudo chmod og-w /var/ftp
   - sudo /usr/local/sbin/vsftpd &
   - sudo crontab -e
   - add :
     * * * * * /usr/local/sbin/vsftpd
   - reboot
     
3. Install proftpd 1.3.3c (Vulnerable #3)
   - tar -xvf backdoored_proftpd-1.3.3c.tar.gz
   - cd backdoored_proftpd-1.3.3c
   - ./configure
   - make && sudo make install
   - sudo nano /usr/local/etc/proftpd.conf
     modified Port
   - sudo /usr/local/sbin/proftpd -c /usr/local/etc/proftpd.conf
   - sudo crontab -e
     * * * * * /usr/local/sbin/proftpd -c /usr/local/etc/proftpd.conf

