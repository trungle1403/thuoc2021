DNS:
bind/named.conf.local / options
zone "vlute.com" {
type master;
file "/etc/bind/db.vlute.com";
};
zone "56,168,192.in-addr.arpa" {
type master;
file "/etc/bind/db.192";
};
bind/db.local db.vlute.com
bind/db.127 192
sudo nano /etc/resolv.conf
search vltue.com
WEB
chown -R $USER:$USER /var/www/intranet
chmod -R 755
MYSQL
alter user 'root'@'localhost' identified with mysql_native_password by 'password';
mysql -u root -p
create table acc(
id int(6) auto_increment primary key,
username varchar(30) not null
);
insert into acc
value
(null,"trung","123"),
(null,"trung","123");

RAID
sudo mdadm -C /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
cat /proc/mdstat
sudo mkfx.ext4 /dev/md0
sudo mkdir raid0
sudo mount /dev/md0 raid0
df -h raid0

OTHER
sudo add-apt-repository ppa:oguzhaninan/stacer -y
sudo apt-get update
sudo apt-get install stacer -y

PRINTER
nano /etc/samba/smb.conf
security = user
sudo apt install cups
nano /etc/cups/cupsd.conf
port 631
allow all
ip:631/admin


Đổi tên: sudo nano /etc/hostname
Coppy 2 file vao thu muc K46:
 
Sudo cp file1.txt file2.txt /home/fit/vlute/k64
Di chuyen 1 file (KNN_VLUTE.txt) vao nhieu thu muc: K43,K44
Sudo tee k43/knn_vlute.txt k44/knn_vlute.txt
 
Font chữ : sudo apt-get install ttf-mscorefonts-installer (tohamo lên mạng tải)
Tạo cây thư mục k41, k42, k43
•	Cd/home/fit
•	Sudo mkdir -p <tên thư mục> /{k41,k42,k43…} nếu trong k41 còn thư mục thì {k41{a,b,…},k42,k43}
•	Coppy file knn.txt vào thư mục k43, k44: sudo tee k43 /knn.txt k44/knn.txt
•	Xoá thư mục: sudo rm -r <tên thư mục>
•	Cấp quyền cho thư mục: sudo chmod 777 <tên thư mục>
PHÂN QUYỀN THƯ MỤC
       + Thông số:
	r (read) = 4, w (write) = 2, x (excute) = 1, - = 0
       + ls -l : Xem tất cả quyền của thư mục or file
       + Câu lệnh phân quyền:
       + $ sudo chmod <thông số> <Tên thư mục or file>
	Ví dụ: $ sudo chmod 764 vidu
	-> Có nghĩa là: 
		+ Ở thư mục ' vidu '  -> Owner có quyền là 7.
				-> Group có quyền 6.
				-> Other có quyền 4.
	+ Thay đổi quyền:
	u: owner
	g: group
	o: other
	ugo hoặc a: cho tất cả.
	Ví dụ:
		+ Ở thư mục ' vidu '  -> Owner có quyền là 7.
				-> Group có quyền 6.
				-> Other có quyền 4.
	Câu 2.4 đề 1:Ta thay đổi quyền Owner từ 7 thành 6:
		$ sudo chmod u=rw <filename>

Thay đổi quyền thư mục:
Yêu cầu: Change the ownership in the other directory for the VLUTE group:
•	Sudo chown -R username:groupname /tenthumuc
Ví dụ: sudo chown -R user1:VLUTE /home/fit/KNN_SV/orther
•	username: Nếu giữ nguyên thì không cần ghi
Ví dụ: sudo chown -R :VLUTE /home/fit/KNN_SV/orther

Xem danh sách user: cat /etc/passwd
Xem danh sách group: cat /etc/group hoặc getent group



TẠO FILE
      + cat > filename
      + echo ""  filename
      + sudo nano filename
	B1: gõ sudo nano filename để tạo fil
	B2: bấm enter rồi bấm del
	B3: Crtl + X  xong gõ Y rồi bấm Enter.

Create folder: sudo mkdir -p TenThuMuc9/{Thumuccon,Thumuccon}
 





ĐỀ1: CÂU 2.4 	
 

CÂU 2.5 
Tạo 1 file pp lưu vào thư mục Sales. Nếu lưu không được là do không có quyền. Sửa lại như sau:
 	
Nhớ sửa lại về mặc định để ko mất điểm







TẠO USER VÀ GROUP
•	Tạo user
•	Tạo user kèm theo password để đăng nhập
sudo adduser <tenuser>
•	Tạo user ko có password
sudo useradd <tenuser>
•	Tạo group
     sudo groupadd <tengroup>
•	Thêm user vào group
•	Tạo user và thêm vào group đã tồn tại
sudo useradd -G <tengroup> <tenuser>
•	Thêm user đã có vào group đã có
sudo usermod -G <tengroup> <tenuser>
•	Xoá group
Sudo groupdel <tengroup>
•	Xoa user
Sudo userdel <tenuser>
Sudo deluser <tenuser>
Xoa user ra khoi group: sudo deluser <tenuser> <tengroup>
Xem group: cat/etc/<tengroup> hoặc getent group
Xem tat cả user: cat/etc/passwd hoặc getent passwd
Đặt pass cho user: sudo passwd <ten user>
		


https://sinhvientot.net/huong-dan-quan-tri-user-group-tren-linux/
 
Tao tree
 
3. DHCP
Đầu tiên để NAT để cài đặt hết tất cả các dịch vụ.
B1: Network: NAT, Ipv4: Automatic
B2: sudo apt-get update
B3: sudo apt-get install isc-dhcp-server
B4: Vaò setting cài đặt IP tĩnh: 192.168.56.100 (Ko đặt default
B5: sudo nano /etc/dhcp/dhcpd.conf
B6:
Xoá # Authoritative
 subnet 192.168.56.0 netmask 255.255.255.0 {
	range 192.168.56.60 192.168.56.220;
	option routers 192.168.56.100;
	option domain-name-servers 8.8.8.8;
}
B7: sudo systemctl restart isc-dhcp-server.service
Hoặc sudo service isc-dhcp-server restart
B8: sudo systemctl status isc-dhcp-server.service
Hoặc sudo service isc-dhcp-server status
B9: Chỉnh Network: internal network
B10: Test Client Network: internal network





4. SAMBA
Đầu tiên để NAT để cài đặt hết tất cả các dịch vụ.
B1: Network: NAT, Ipv4: Automatic
B2: sudo apt-get update
B3:  cd /home/tenmay (Ví dụ: fit)
B4: sudo mkdir <share-data>
B5: sudo apt install tasksel
B6: sudo tasksel install samba-server
B7: sudo cp /etc/samba/smb.conf /etc/samba/smb.conf_backup
B8:  sudo nano /etc/samba/smb.conf
 [share-data]
comment = hello
path = /home/fit/share-data
read only = no
guest ok = yes
B9: sudo /etc/init.d/smbd restart  hoac sudo systemctl restart smbd.service
B10: gõ ls -l để xem quyền của thư mục share-data
B11: sudo chmod 777 <name> ví dụ (share-data)
B11: Lưu ý: Network: internal network,  ( nếu chưa có DHCP thì đặt IP tĩnh)
B12: Test Client Network: internal network, IP: Cùng lớp mạng với server
B13: vào run gõ : \\<ip server> ví dụ: \\192.168.56.100




WEB-SERVER
https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04
B1: sudo apt-get update
B2: sudo apt install apache2
B3: sudo ufw app list
B4: sudo ufw allow ‘Apache’
B5: sudo ufw status
B6: sudo ufw enable
B7: sudo ufw status
 

B8: sudo systemctl status apache2
B9: hostname -I
B10: curl -4 icanhazip.com
 
B11:sudo apt install curl (ko có curl nên install curl)
B12: B10
B13: sudo mkdir /var/www/myweb(tự đặt tên vd là myweb)
B14: sudo chown -R $USER:$USER  /var/www/myweb
B15: sudo chmod -R 755 /var/www/ myweb
B16:  sudo nano /var/www/ myweb /index.html
<html>
    <head>
        <title>Welcome to Your_domain!</title>
    </head>
    <body>
        <h1>Success!  The your_domain virtual host is working!</h1>
    </body>
</html>
B17: sudo nano /etc/apache2/sites-available/ myweb.conf
•	Dan lenh nay vao:

<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	ServerName myweb
	ServerAlias www.myweb
	DocumentRoot /var/www/myweb
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

B18: sudo a2ensite myweb.conf
B19: sudo a2dissite 000-default.conf
B20: sudo apache2ctl configtest
B21: sudo systemctl restart apache2
RÙI LÊN GOOLE TEST : 10.0.2.15














FTP-SERVER
Tham khảo:
https://tel4vn.edu.vn/blog/how-to-install-ftp-server-use-vsftpd-with-ssl-tls/

B1: sudo apt-get update
B2: sudo apt install vsftpd
Cấu hình tưởng lửa cho vsftpd
B3: sudo ufw enable
Thực hiện mở các port 20 (FTP command port), 21 (FTP data port), 990 (TLS FTP data port) và dải port 35000-40000:
B4: sudo ufw allow 20:21/tcp
B5: sudo ufw allow 990/tcp
B6: sudo ufw allow 35000:40000/tcp
B7: sudo ufw status
Cấu hình vsftpd
B8: sudo nano /etc/vsftpd.conf
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
pasv_min_port=35000
pasv_max_port=40000
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
sudo systemctl restart vsftpd.service
sudo systemctl status vsftpd.service

Cấu hình thư mục người dùng
B9: sudo adduser <username>
	Chỉ cần đặt passord, fullname, còn lại enter
B10: thêm user vừa tạo vào file vsftpd.userlist
	Echo ‘username’ | sudo tee -a /etc/vsftpd.userlist
B11: sudo mkdir /home/username/ftp
B12: sudo chown nobody:nogroup /home/username/ftp
B13: sudo chmod a-w /home/username/ftp
B14: sudo ls -al /home/username/ftp
tạo thư mục có quyền write để có thể lưu các file tải lên:
B15: sudo mkdir /home/username/ftp/upload
B16:  sudo chown username:username /home/username/ftp/upload
B17: sudo ls -al /home/username/ftp
B18: Để tiện cho việc test thử, bạn nên tạo một file test.txt ttrong thư mục upload:
echo “vsftpd test file” | sudo tee /home/username/ftp/upload/test.txt
B19: Kiểm tra: ftp -p <địa chỉ ip máy>
•	Nhập username
•	Nhập password




MYSQL-SERVER
https://www.linuxtopic.com/2016/03/how-to-configure-mysql-server-in-linux.html
B1: sudo apt-get update
B2: sudo apt install mysql-server
B3: sudo mysql_secure_installation
	Y, 0, y, n, y, n, y
B4: sudo mysql
B5: SELECT user, authentication_string, plugin,host from mysql.user;
B6: ALTER USER ‘root’@’localhost’ IDENTIFIED WITH mysql_native_password BY ‘password’;
B7: FLUSH PRIVILEGES;
Nếu bị thoát ra khỏi mysql thì làm bước 9
B9:mysql -u root -p
Nhập mật khẩu là: password
Tạo bảng
	Create database <tendatabase>;  -> tạo database.
Ví dụ: create database users;
	Show databases; -> xem database hiện có.
	use <database>; -> chọn dùng database;
Ví dụ: use users;
	Và tạo table như hình
 

show tables; -> xem chơi table của database hiện tại
 

	describe <tentable>; -> xem chơi các cột của table-> 
Ví dụ: describe acc;
 
	thêm dữ liệu vào table
 
	Select ra mấy cái vừa thêm
 
Gõ exit để out ra ngoài 
B10: systemctl status mysql.service
Mấy bước sau dòng này khỏi làm. Vì đề k y/c.
B11: sudo mysqladmin -p -u root version
B12: download mysql workbench
https://dev.mysql.com/downloads/repo/apt/
cai dat:
sudo apt install ./<tenfile_tai_ve.deb
ok
ok
B13: sudo apt update
B14: sudo apt install mysql-workbench-community


3.1. Performance Monitoring and Optimization(cài ứng dụng toi uu)
Sudo add-apt-repository ppa:oguzhaninan/stacer -y
Sudo apt-get update
Sudo apt-get install stacer -y
 



Lưu ý: Cần thêm ổ đĩa vào trước khi làm:
 
Để làm raid khác thì 1 là thêm ổ mới 
2 là xoá raid trước đó : ( Cách này chưa test)
sudo mdadm --remove /dev/md0
sao đó vào: sudo nano /etc/mdadm/mdadm.conf
đánh dấu # mấy thằnd raid
RAID0:

B1: sudo apt-get update
B2: sudo apt-get install mdadm
B3: lsblk 
 
B4:sudo mdadm -C  /dev/md0 --level=0 --raid-devices=2 /dev/sdc /dev/sdb
B5:cat /proc/mdstat
	Sudo mdadm -E /dev/sdb /dev/sdc
Hoặc viết tắt sudo mđam -E /dev/sd[b-c] để xem  Raid level coi đúng k
B6: sudo mkfs.ext4  /dev/md0
Nếu lỗi thì:  sudo apt-get install xfsprogs rồi làm lại B6
B8: sudo mkdir raid0 
B9:sudo mount /dev/md0 raid0
B10:df -h raid0 để xem kết quả






RAID 1: Y chang raid0 nhưng sửa level=1
https://www.linuxbabe.com/linux-server/linux-software-raid-1-setup
B1: sudo apt-get update
B2: sudo apt-get install mdadm
B3: lsblk 
 
B4:sudo mdadm -C  /dev/md0 --level=1 --raid-devices=2 /dev/sdc /dev/sdb
B5:cat /proc/mdstat
	sudo mdadm -E /dev/sdb /dev/sdc
Hoặc viết tắt sudo mđam -E /dev/sd[b-c] để xem  Raid level coi đúng k
B6: sudo mkfs.ext4  /dev/md0 (nếu trc đó đã tạo md0 làm rai0 thì sửa /dev/md1)
Nếu lỗi thì:  sudo apt-get install xfsprogs rồi làm lại B6
B8: sudo mkdir radi1
B9: sudo mount /dev/md0  raid1 // sudo mount /dev/md1  raid1
B10:df -h raid1 để xem kết quả

RAID5:
https://www.tecmint.com/create-raid-5-in-linux/
B1: sudo apt-get update
B2: sudo apt-get install mdadm
B3: lsblk 
 
B4:sudo mdadm -C  /dev/md0 --level=5 --raid-devices=3 /dev/sdc /dev/sdb /dev/sdd
B5:cat /proc/mdstat
	Sudo mdadm -E /dev/sdb /dev/sdc /dev/sdd
Hoặc viết tắt sudo mdadm -E /dev/sd[b-d] để xem  Raid level coi đúng k
B6: sudo mkfs.ext4  /dev/md0
Nếu lỗi thì:  sudo apt-get install xfsprogs rồi làm lại B6
B8: sudo mkdir raid5
B9:sudo mount /dev/md0 raid5
B10:df -h raid5 để xem kết quả
Xoa lock 
Sudo rm /var/lib/dpkg/lock























   DNS
https://askubuntu.com/questions/558449/how-to-configure-two-domains-with-bind9-arpa
B1:sudo apt-get update
B2:sudo dpkg --configure -a (khỏi cũng đc)
B3:sudo apt-get install bind9 dnsutils (dnsutils khỏi can cai)
B4: 
chỉnh address: ví dụ: 192.168.56.100 255.255.255.0
DNS: 192.168.56.100
B5:sudo nano /etc/bind/named.conf.options 
 
B6:sudo nano /etc/bind/named.conf.local
Nhập 2 cái zone vào:
 
B7: sudo cp /etc/bind/db.local  /etc/bind/db.abc.com
B8:sudo nano /etc/bind/db.abc.com
sửa lại, đề y.c làm 1 tên miền thì bỏ nguyên dòng ems.abc.com. ….  .. 
còn y/c làm 3 4 tên miền thì thêm vô:
ví dụ cit.abc.com IN A 192.168.56.x (x tuỳ ý).
 
B9: sudo cp  /etc/bind/db.127  /etc/bind/db.192
B10:sudo nano /etc/bind/db.192
sửa lại cho giống: Làm mấy địa chỉ thì ghi bấy nhiu.
 
B11:sudo nano /etc/resolv.conf
sửa lại:
 
b12:sudo systemctl restart bind9
b13:sudo systemctl status bind
B13:ktra  gõ nslookup 
 gõ >192.168.56.10
    
PRINTER-SERVER
B1: sudo apt-get update
B2: 
Sudo apt install tasksel
sudo tasksel install samba-server
B3: sudo cp /etc/samba/smb.conf  /etc/samba/smb.conf.copy ( Khỏi cũng được)
B4: sudo nano /etc/samba/smb.conf
Tìm và sửa như hình
 

B5: sudo systemctl restart smbd.service nmbd.service
B6: sudo apt install cups
B7: sudo cp /etc/cups/cupsd.conf  /etc/cups/cupsd.conf.copy (khỏi cũng đc)
B8: sudo nano /etc/cups/cupsd.conf
Tim` va` sua? Lai. nhu hinh`
 

 

B9: sudo systemctl restart cups
B10: ip a  
Mở trình duyệt gõ ip máy: ví dụ: 192.168.56.100:631/admin
 
Bấm add printer
 
Bấm như hình


Sau đó bấm lại add printer
 
Rồi nhập tài khoản mật khẩu lúc đầu đăng nhập
Chọn như hình bấm countinue
 
 
Chọn 1 make rồi bấm continue
 
Chọn 1 em rồi add
 
Chọn Set default options
 
B11: qua client gõ ip máy server nhớ 2 máy cùng lớp mạng và internal network
 



















		NFS SERVER
https://www.tecmint.com/install-nfs-server-on-ubuntu/
[UBUNTU-SERVER]:
B1: sudo apt update
B2: sudo apt install nfs-kernel-server
	Ip-server: 192.168.56.100 255.255.255.0 
B3: sudo mkdir -p nfs-server (mặc định ở home/<tentk>)
(tạo xong nó là /home/fit/nfs-server : ghi nhớ)
B4: sudo chown nobody:nogroup nfs-server
B5: sudo chmod 777 nfs-server
B6: sudo nano /etc/exports
	Thêm dòng này vào:
/home/fit/nfs-server 192.168.56.0/24(rw,sync,no_subtree_check)
B7: sudo exportfs -a
B8: sudo systemctl restart nfs-kernel-server
B9: sudo ufw allow from 192.168.56.0/24 to any port nfs
B10: sudo nano nfs-server/abc.txt (gõ 1 ký tự rồi ctrol + x bấm y rồi enter để tạo file để test)
[UBUNTU-CLIENT]:
B1: sudo apt update
B2: sudo apt install nfs-common
Ip-client: nếu chưa có dhcp thì tự ghi: 192.168.56.110
B3: sudo mkdir -p nfs-client (/home/fit/nfs-client ghi nhớ)
B4: sudo mount 192.168.56.100:/home/fit/nfs-server /home/fit/nfs-client
			Ip server
B5: sudo ls -l nfs-client (xem coi có file txt hồi nãy tạo k
Câu lệnh cài đặt dịch vụ
Install tất cả các dịch vụ: Mạng NAT
Sudo apt-get install update
*DHCP
Sudo apt-get install isc-dhcp-server
*SAMBA
Sudo apt install tasksel
Sudo tasksel install Samba-server
*Web-server
Sudo apt install apache2
*FTP-server
Sudo apt install usftpd
*My SQL
Sudo apt install mysql-server
*RAID
Sudo apt-get install mdadm
*print server
- Sudo apt install cups
Sudo systemctl start cups 
*DNS
Sudo apt-get install bind9
*NFS-server
Sudo apt-get install nfs-kernel-server


