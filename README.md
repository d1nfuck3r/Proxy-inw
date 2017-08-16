# Proxy-inw
ดิ้นนนน เข้าไป เอาให้ไข่ถลอก

# วิธีติดตั้ง
```
# 1.ติดตั้ง สิ่งที่จำเป็น
apt-get update && apt-get upgrade

apt-get install build-essential nano

# 2.เพิ่มกรุ๊ป
groupadd squid

# 3.เพิ่ม User ลงกรุ๊ป
useradd -g squid -s /dev/null squid

# 4.สร้างโฟลเดอร์
mkdir /downloads

# 5.ไปที่ 
cd /downloads

# 6.ดาวโหลด
wget http://www.squid-cache.org/Versions/v3/3.4/squid-3.4.6.tar.gz

# 7.แตกไฟล์
tar -zxvf squid-3.4.6.tar.gz

# 8.ไปที่
cd squid-3.4.6

# 9.เช็ค
./configure --enable-default-err-language=English

# 10.รวมไฟล์และติดตั้ง
make && make install

# 11.ลบ squid.conf
rm /usr/local/squid/etc/squid.conf

# 12.ไปที่
cd /usr/local/squid/etc/

# 13.เพิ่ม squid.conf ใหม่
wget https://raw.githubusercontent.com/d1nfuck3r/Proxy-inw/master/squid.conf

# 14.สร้างโฟลเดอร์
mkdir /usr/local/squid/var/cache

# 15.สร้างโฟลเดอร์
mkdir /usr/local/squid/var/logs

# 16.เปลี่ยนสิทธิ์
chown squid.squid /usr/local/squid/ -R

# 17.รัน cache
/usr/local/squid/sbin/squid -z

# 18.
/usr/local/squid/sbin/squid -d10

# 19.Enable IP_Forward
sysctl net.ipv4.ip_forward=1

# 20.iptables
iptables -A PREROUTING -i eth0 -p tcp -m tcp --dport 443 -j REDIRECT --to-ports 3128

iptables -A PREROUTING -i eth0 -p tcp -m tcp --dport 80 -j REDIRECT --to-ports 3128



# คำสั่ง หยุด
/usr/local/squid/sbin/squid -k kill

# คำสั่งใช้งาน
/usr/local/squid/sbin/squid


```

# วิธีกำหนด ให้ไอพีที่สามารถเชื่อมต่อได้ 
```
# 1.เปิดไฟล์
nano /usr/local/squid/etc/squid.conf

# 2.มองหาบรรทัดนี้
acl REDE_INTERNA src 192.168.0.0/24

# 3.แล้ว Enter 1ครั้ง แล้วเพิ่มคำสั่งนี้ลงไป
acl proxy url_regex -i "/usr/local/squid/etc/proxy.txt"

# 4.มองหาบรรทัดนี้
http_access allow REDE_INTERNA

# 5.แล้ว Enter 1 ครั้ง แล้วเพิ่มคำสั่งนี้ลงไป
http_access allow proxy

# 6.มองหาบรรทัดนี้
http_access allow all

# 7.แก้ให้เป็นแบบนี้ เสร็จแล้วบันทึก
http_access deny all

# 8.สร้างไฟล์สำหรับเพิ่มไอพี ให้เชื่อมต่อได้
nano /usr/local/squid/etc/proxy.txt

# 9.หยุด และ สั่ง รัน
/usr/local/squid/sbin/squid -k kill

/usr/local/squid/sbin/squid

```


# อยากให้ไอพีไหนเชื่อมต่อได้ ให้เข้าไปเพิ่มไอพีนั้น ในนี้

```
/usr/local/squid/etc/proxy.txt

```


