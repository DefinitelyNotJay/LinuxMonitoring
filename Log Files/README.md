<h1>Log Files</h1>
<p>Log Filesคือไฟล์ทั้งหมดที่อยู่ใน /var/log โดยการที่ระบบจะเก็บการกระทำ, กิจกรรม </p>
<h2>กลุ่มLog fileหลัก</h2>
<h3>/var/log/messages(Linux) หรือ /var/log/syslog(Ubuntu)</h3>
<ul><li>เป็นไฟล์ที่เก็บmessage, activitiesทั้งหมดของระบบในระดับ global</li></ul>
<p>ตัวอย่าง</p>
<img width="1470" alt="Screenshot 2567-02-06 at 10 43 48" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/d6ffaef0-f6fb-491a-9060-7eb5c21adbf6">
<p style="font-size : 10px; color: red;" align = "center">การอ่านsyslogไฟล์โดยใช้ vi</p>
<img width="1470" alt="Screenshot 2567-02-07 at 12 09 00" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/2c9b6c08-7d88-49f7-a3f0-14ca8294aa73">
<p align="center">ตัวอย่าง การอ่านไฟล์โดยใช้ tail</p>
<hr>
<h2>กลุ่มการเข้าถึงและการยืนยันตัวตน(Access and Authentication)</h2>

<h3>/var/log/auth.log</h3>
<ul><li>เป็นlog fileที่แสดงการAuthentication(login), AuthorizationของUser</li></ul>
<img width="1114" alt="Screenshot 2567-02-06 at 11 20 35" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/c8cce327-910e-4af6-a8c6-81e38afedb74">
<p align="center">การอ่านไฟล์auth ซึ่งแสดงการสร้างsessionให้ผู้ที่เข้าสู่ระบบ</p>  

<h3>/var/log/lastlog</h3>
<ul>
  <li>เป็นlog fileที่แสดงการAuthentication(login), AuthorizationของUser</li>
  <li>lastlogไฟล์อาจมีขนาดที่ใหญ่ขึ้นอยู่กับจำนวนUserที่มีในระบบ หากเป็นlastlogไฟล์ในserverจะมีขนาดใหญ่มาก แต่มันไม่ได้ใช้พื้นที่เท่าที่มันแสดงจริงๆ</li>
  <li>เป็นไฟล์ที่ไม่ใช่ASCII</li>
  <li>ใช้คำสั่ง lastlogในการอ่าน</li>
</ul>
<img width="1470" alt="Screenshot 2567-02-06 at 11 26 55" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/830e9ec6-9aff-4dd2-9d5e-045e17af1859">
<p align = "center">lastlogในUbuntuที่เปิดด้วย vi</p>
<img width="683" alt="Screenshot 2567-02-06 at 11 41 58" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/d6f627be-6322-4ee1-9147-c3c3a156c538">
<p align = "center">การอ่านไฟล์โดยการใช้คำสั่งlastlog</p>

<h3>/var/log/btmp10</h3>
<ul>
  <li>เก็บข้อมูลการพยายามloginที่failed</li>
  <li>ใช้คำสั่งlastเพื่อแสดง</li>
  <li>sudo last -f btmp</li>
  <li>ต้องเป็น root จึงจะมีสิทธิ์ดูได้</li>
</ul>

<p align="center">การอ่านไฟล์โดยการใช้คำสั่ง last</p>

<h3>/var/log/wtmp หรือ /var/log/utmp</h3>
<ul>
  <li>เก็บข้อมูลการ logins/logouts</li>
</ul>

<p align="center">การอ่านwmtpไฟล์โดยการใช้คำสั่ง last</p>

<p align="center">การอ่านไฟล์โดยการใช้คำสั่ง last</p>

<h3>/var/log/faillog</h3>
<ul>
  <li>เก็บlog การloginที่ไม่สำเร็จของusers</li>
</ul>

<p align="center">การอ่านwmtpไฟล์โดยการใช้คำสั่ง last</p>





