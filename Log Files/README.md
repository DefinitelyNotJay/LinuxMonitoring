<h1>Log Files</h1>
<h2>กลุ่มLog fileหลัก</h2>
<h3>/var/log/messages(Linux) หรือ /var/log/syslog(Ubuntu)</h3>
<ul><li>เป็นไฟล์ที่เก็บmessage, activitiesทั้งหมดของระบบในระดับ global</li></ul>
<p>ตัวอย่าง</p>
<img width="1470" alt="Screenshot 2567-02-06 at 10 43 48" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/d6ffaef0-f6fb-491a-9060-7eb5c21adbf6">
<p style="font-size : 10px; color: red;" align = "center">การอ่านsyslogไฟล์โดยใช้ vi</p>
<img width="1470" alt="Screenshot 2567-02-07 at 12 09 00" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/2c9b6c08-7d88-49f7-a3f0-14ca8294aa73">
<p align="center">ตัวอย่าง การอ่านไฟล์โดยใช้ tail</p>
---------------
---------------
<h2>กลุ่มการเข้าถึงและการยืนยันตัวตน(Access and Authentication)</h2>
<h3>/var/log/auth.log</h3>
<ul><li>เป็นlog fileที่แสดงการAuthentication(login), AuthorizationของUser</li></ul>
<img width="1114" alt="Screenshot 2567-02-06 at 11 20 35" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/c8cce327-910e-4af6-a8c6-81e38afedb74">
<p align="center">การอ่านไฟล์auth ซึ่งแสดงการสร้างsessionให้ผู้ที่เข้าสู่ระบบ</p>  

