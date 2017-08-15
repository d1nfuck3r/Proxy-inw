# Proxy-inw
ดิ้นนนน เข้าไป เอาให้ไข่ถลอก

# วิธีติดตั้ง
```
#1.ติดตั้ง สิ่งที่จำเป็น
apt-get install build-essential nano

#2.เพิ่มกรุ๊ป
groupadd squid

#3.เพิ่ม User ลงกรุ๊ป
useradd -g squid -s /dev/null squid

#4.สร้างโฟลเดอร์
mkdir /downloads

#5.ไปที่ 
cd /downloads

#6.ดาวโหลด
wget http://www.squid-cache.org/Versions/v3/3.4/squid-3.4.6.tar.gz

#7.แตกไฟล์
tar -zxvf squid-3.4.6.tar.gz

#8.ไปที่
cd squid-3.4.6

#9.เช็ค
./configure --enable-default-err-language=English

#10.รวมไฟล์และติดตั้ง
make && make install

#11.ลบ squid.conf
mv /usr/local/squid/etc/squid.conf

#12.ไปที่
cd /usr/local/squid/etc/

#13.เพิ่ม squid.conf ใหม่


#14.สร้างโฟลเดอร์
mkdir /usr/local/squid/var/cache

#15.สร้างโฟลเดอร์
mkdir /usr/local/squid/var/logs

#16.เปลี่ยนสิทธิ์
chown squid.squid /usr/local/squid/ -R

#17.รัน cache
/usr/local/squid/sbin/squid -z

#18.
/usr/local/squid/sbin/squid -d10

#19.Enable IP_Forward
sysctl net.ipv4.ip_forward=1

#20.iptables
iptables -A PREROUTING -i eth0 -p tcp -m tcp --dport 443 -j REDIRECT --to-ports 3128

iptables -A PREROUTING -i eth0 -p tcp -m tcp --dport 80 -j REDIRECT --to-ports 3128



#คำสั่ง หยุด
/usr/local/squid/sbin/squid -k kill

#คำสั่งใช้งาน
/usr/local/squid/sbin/squid

```

