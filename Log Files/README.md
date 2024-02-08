<h1>Log Files</h1>
<p>Log Filesคือไฟล์ที่เก็บการกระทำ, กิจกรรม, สิ่งต่างๆที่เกิดขึ้นกับระบบไม่ว่าจะเกิดขึ้นจาก ผู้ใช้งาน, kernel, package ฯลฯ Log Filesส่วนใหญ่จะถูกจัดเก็บอยู่ใน /var/log 
  โดยการอ่านไฟล์อ่านทำได้โดยการใช้คำสั่ง เช่น less, last, cat, vi, หรือคำสั่งเฉพาะไฟล์เช่น lastlog ประโยชน์ของLog Filesคือการทำให้ผู้ใช้สามารถย้อนดูสิ่งผิดปกติที่เกิดขึ้น เช่น การเรียกดูการAuthentication ของUserในช่วงระยะเวลานึง, การเลือกดูเฉพาะคำสั่งบางคำสั่งที่ทำโดยPackage Manager
</p>
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
<img width="697" alt="Screenshot 2567-02-06 at 12 20 55" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/957f437f-9a81-4773-9af9-9ce776133210">
<p align="center">การอ่านไฟล์โดยการใช้คำสั่ง last</p>

<h3>/var/log/wtmp หรือ /var/log/utmp</h3>กด
<ul>
  <li>เก็บข้อมูลการ logins/logouts</li>
</ul>
<img width="687" alt="Screenshot 2567-02-06 at 12 25 06" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/3baa37be-d739-4685-99b4-4fc1b2812a56">
<p align="center">การอ่านwmtpไฟล์โดยการใช้คำสั่ง last</p>

<h3>/var/log/faillog</h3>
<ul>
  <li>เก็บlog การloginที่ไม่สำเร็จของusers</li>
</ul>
<img width="401" alt="Screenshot 2567-02-06 at 12 44 03" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/e249c0ec-8212-4a09-ba93-fa0d57221968">
<p align="center">การอ่านwmtpไฟล์โดยการใช้คำสั่ง last</p>

<h2>กลุ่ม Package Install/uninstall</h2>
<h3>/var/log/dpkg.log</h3>
<ul>
  <li>เก็บทุกการกระทำที่ทำโดยDebian package manager เช่น package installations, upgrades, uninstall</li>
</ul>

<img width="819" alt="Screenshot 2567-02-06 at 23 08 24" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/0cf1f89f-39c0-4a27-a268-a9fa5c96fab5">
<p align = "center">ข้อมูลในdpkg.log</p>
<img width="813" alt="Screenshot 2567-02-06 at 23 15 00" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/0503b5bb-b72f-44a5-a03d-e2b5025aede9">
<p align = "center">การหาstatus unpackedในdpkg.log file โดยใช้ grep</p>

<h2>กลุ่มSystem log files</h2>
<h3>/var/log/kern.log</h3>
<ul>
  <li>เก็บmessagesที่เกี่ยวกับkernel ช่วยให้การtroubleshooting ปัญหาที่เกิดขึ้นกับstartup, hardware, kernel</li>
</ul>
<img width="1470" alt="Screenshot 2567-02-08 at 13 03 44" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/8cd07571-b6ad-4a68-b69e-b949ec2c7c4b">
<p align = "center">ไฟล์kern.logที่เปิดโดยใช้ vi</p>

<h3>/var/log/dmesg</h3>
<ul>
  <li>เก็บข้อมูลที่เกี่ยวกับmessageของkernelที่ได้มาจากkernel ring buffer</li>
  <li>โดยที่ring bufferเก็บข้อมูลเกี่ยวกับhardware, driverเริ่มต้นของอุปกรณ์, messageจากkernel modulesที่ทำงานตอนstartup</li>
</ul>
<img width="840" alt="Screenshot 2567-02-08 at 13 09 16" src="https://github.com/DefinitelyNotJay/LinuxMonitoring/assets/81279337/c7ffefe3-1ed4-410d-8f7f-4ca87b9e337c">

<p align = "center">ไฟล์dmesgที่อ่านโดยการใช้คำสั่งlast</p>







