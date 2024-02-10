<h1>Log Collection / Server🌐</h1>
<p>เป็นส่วนสำคัญในการบริหารจัดการบันทึก (logs) ที่ระบบทำการสร้างขึ้นในทุก ๆ กิจกรรมของระบบคอมพิวเตอร์
<ol>
  <li>
    <b>Log Collection</b> เป็นกระบวนการที่เกี่ยวข้องกับการรวบรวมข้อมูลบันทึกจากระบบหลาย ๆ แหล่งไปเก็บไว้ในที่เดียว เพื่อให้ง่ายต่อการจัดการ ตรวจสอบ และวิเคราะห์ ข้อมูลบันทึกที่รวบรวมนั้นสามารถมีทั้งข้อมูลการเข้าถึงระบบ ข้อผิดพลาด และกิจกรรมอื่นๆ ที่เกิดขึ้นในระบบ
  </li>
  <li>
    <b>Log Server</b> เป็นเซิร์ฟเวอร์ที่ใช้เก็บรวบรวมข้อมูลบันทึกจากระบบต่าง ๆ ที่เชื่อมต่อมา โดยทั่วไป log server จะมีซอฟต์แวร์ที่จัดการกับการรับ เก็บ และนำเสนอข้อมูลบันทึกในรูปแบบที่ง่ายต่อการทำความเข้าใจ เช่น การแสดงผลในรูปแบบกราฟ ตาราง และรายงาน เป็นต้น
  </li>
</ol>
</p>
<h2>บทบาทและหน้าที่</h2>
<ul>
  <li>เก็บข้อมูลบันทึก</li>
  <li>การจัดเก็บข้อมูล</li>
  <li>การส่งข้อมูล</li>
  <li>การคัดกรองข้อมูล</li>
  <li>การรักษาความปลอดภัย</li>
</ul>
<h2>พื้นฐานหรือหลักการทำงานของ log collection บน Linux</h2>
<ol>
  <li><b>การสร้าง Logs</b>
    ระบบปฏิบัติการและแอปพลิเคชันต่าง ๆ บน Linux สร้าง logs เพื่อบันทึกข้อมูลเหตุการณ์ทเกิดขึ้นในระบบ Logs เหล่านี้มักถูกเขียนลงในไฟล์ที่ตั้งไว้ล่วงหน้า
  </li>
  <li><b>Log Rotation</b>
    เนื่องจากข้อมูล logs มีขนาดใหญ่และมีการเขียนอย่างต่อเนื่อง การจัดการขนาดและการจัดเก็บ logs เป็นสิ่งสำคัญ Log rotation เป็นกระบวนการที่หลับตามโดยทำให้ logs เก่าถูกบีบอัด ย้าย หรือลบเพื่อทำให้พื้นที่ไม่เต็ม
  </li>
  <li><b>Log Collection Agents</b>
    บางครั้งจะมีตัวแทน (agents) ที่ทำหน้าที่เก็บ logs จากระบบและแอปพลิเคชันที่ต่างกันไป Agents นี้สามารถส่ง logs ไปยังตำแหน่งที่กำหนดได้ เช่น central log server หรือ log aggregator
  </li>
  <li><b>Centralized Log Server</b>
    การนำ logs มาเก็บไว้ที่ตำแหน่งเดียวกัน (centralized log server) เป็นแนวคิดที่พึงสำคัญ สิ่งนี้ทำให้ผู้ดูแลระบบสามารถจัดการ logs จากหลายแหล่งในที่เดียว ช่วยในการวิเคราะห์ข้อมูล ค้นหาข้อผิดพลาด และดำเนินการต่อไป
  </li>
  <li><b>Log Formats</b>
    ข้อมูล logs มักจะถูกจัดเก็บในรูปแบบที่เป็นทางการ (standardized format) เพื่อทำให้ง่ายต่อการอ่านและวิเคราะห์ รูปแบบทั่วไปที่ใช้กันมากคือ syslog และ JSON
  </li>
  <li><b>Security and Access Controls</b>
    การควบคุมการเข้าถึง logs เพื่อความปลอดภัยมีความสำคัญ สิทธิ์และการตรวจสอบความปลอดภัยควรถูกกำหนดให้เพียงพอเพื่อป้องกันการเข้าถึงที่ไม่ถูกต้อง
  </li>
  <li><b>Log Analysis Tools</b>
    มีเครื่องมือต่าง ๆ ที่ใช้ในการวิเคราะห์ logs เพื่อหาข้อมูลที่มีประโยชน์ เครื่องมือเหล่านี้สามารถช่วยในการตรวจสอบปัญหา ค้นหาแนวโน้ม และเพิ่มประสิทธิภาพของระบบ
  </li>
  <li><b>การแจ้งเตือน (Alerting)</b>
    การตั้งค่าระบบแจ้งเตือนเพื่อแจ้งเตือนผู้ดูแลระบบเมื่อเหตุการณ์ที่สำคัญเกิดขึ้น นี้ช่วยในการตอบสนองได้เร็วต่อปัญหาหรือเหตุการณ์ที่มีความสำคัญ
  </li>
</ol>
<h2>การเรียกใช้งาน</h2>
<p>
  <h4>สามารถเรียกใช้งานด้วยคอมมานด์ syslogd หรือ rsyslog</h4>
  <b>syslogd</b> daemon อ่าน Datagram Socket และส่งแต่ละบรรทัดข้อความไปยังปลายทางที่อธิบายโดยไฟล์ configuration <b>/etc/syslog.conf</b> 
  <p><b>syslogd</b> daemon อ่านไฟล์ configuration เมื่อเปิดใช้งานและเมื่อได้ hangup signal</p>
</p>
<h2>syslogd [option]</h2>
<table>
  <tr>
    <th>option</th>
    <th>describe</th>
    <th>example</th>
  </tr>
  <tr>
    <td>-V</td>
    <td>print  หมายเลขเวอร์ชัน</td>
    <td>syslogd -V</td>
  </tr>
  <tr>
    <td>--help</td>
    <td>แสดงข้อมูลความช่วยเหลือ</td>
    <td>syslogd --help</td>
  </tr>
  <tr>
    <td>--usage</td>
    <td>แสดงข้อมูลการใช้คำสั่งต่างๆ ของ syslogd</td>
    <td>syslogd --usage</td>
  </tr>
  <tr>
    <td>-d</td>
    <td>เข้าสู่โหมดแก้ไขข้อบกพร่อง(debug mode) syslogd ไม่ได้ใส่ตัวเองในพื้นหลัง ไม่แยกและแสดงข้อมูลการดีบัก</td>
    <td>syslogd -d</td>
  </tr>
  <tr>
    <td>-a</td>
    <td>ระบุ socket เพิ่มเติมจากที่ syslogd ต้องรับฟัง นี่เป็นสิ่งจำเป็นถ้าคุณจะปล่อยให้ daemon บางตัวทำงานภายในสภาพแวดล้อม chroot()'ed คุณสามารถระบุ socket เพิ่มเติมได้สูงสุด 19 ช่อง</td>
    <td>syslogd -a [SOCKET]</td>
  </tr>
  <tr>
    <td>-f, --rcfile=FILE</td>
    <td>ระบุชื่อ path ของ configuration file สำรอง มีค่าเริ่มต้นคือ system specific และแสดงใน output วิธีใช้</td>
    <td>syslogd -f [FILE]</td>
  </tr>
  <tr>
    <td> --rcdir=DIR</td>
    <td>ระบุชื่อ path ของ configuration directory สำรอง ค่าเริ่มต้นคือ system specific และแสดงใน output วิธีใช้</td>
    <td>syslogd --rcdir=DIR</td>
  </tr>
  <tr>
    <td>-h, --hop</td>
    <td>เปิดใช้งานการส่งต่อข้อความระยะไกล โดยค่าเริ่มต้น syslogd จะไม่ส่งต่อข้อความนั้นที่ได้รับจาก host ระยะไกล</td>
    <td>syslogd --hop</td>
  </tr>
  <tr>
    <td>-l</td>
    <td>รายชื่อ host ที่คั่นด้วยเครื่องหมาย colon(:) ซึ่งควรได้รับการพิจารณาว่าเป็น local โดยจะถูกบันทึกไว้โดยใช้ host name แทนโดย FQDN</td>
    <td>syslogd -l [HOSTLIST]</td>
  </tr>
  <tr>
    <td>-m, --mark=INTERVAL/fP</td>
    <td>เลือกจำนวนนาทีระหว่างข้อความ `` ทำเครื่องหมาย '' ค่าเริ่มต้นคือ 20 นาที หากตั้งเป็น 0 คือการปิดใช้งาน time stamp</td>
    <td>syslogd -m [INTVAL]</td>
  </tr>
  <tr>
    <td>-n, --no-detach</td>
    <td>ระงับการทำงานเบื้องหลังและการปลด daemon จากการควบคุม terminal</td>
    <td>syslogd -n</td>
  </tr>
  <tr>
    <td>-p, --socket=PATH</td>
    <td>ระบุชื่อ path ของ socket log สำรอง</td>
    <td>syslogd -p [FILE]</td>
  </tr>
  <tr>
    <td>-r, --inet</td>
    <td>เปิดใช้งานเพื่อรับข้อความระยะไกลโดยใช้ internet domain socket</td>
    <td>syslogd -r</td>
  </tr>
  <tr>
    <td>-s</td>
    <td>list ของ domain name ซึ่งควรแยกออกจาก FQDN ของ host เมื่อ logging</td>
    <td>syslogd -s [DOMAINLIST]</td>
  </tr>
  <tr>
    <td>--no-klog</td>
    <td>อย่าฟังอุปกรณ์บันทึกเคอร์เนล(kernel log device)</td>
    <td>syslogd --no-klog</td>
  </tr>
  <tr>
    <td>--no-unixaf</td>
    <td>อย่าฟัง unix domain socket ใดๆ</td>
    <td>syslogd --no-unixaf</td>
  </tr>
  <tr>
    <td>--no-forward</td>
    <td>ห้ามส่งต่อข้อความใดๆ</td>
    <td>syslogd --no-forward</td>
  </tr>
</table>
<blockquote>เพิ่มเติม file dir</blockquote>
<ul>
  <li>/etc/syslog.conf     	  <blockquote>ไฟล์ configuration</blockquote></li>
  <li>/var/run/syslog.pid  	  <blockquote>process id ของ syslogd ปัจจุบัน</blockquote></li>
  <li>/dev/log             	  <blockquote>ชื่อของ UNIX domain datagram log socket</blockquote></li>
  <li>/dev/klog, /proc/kmsg	  <blockquote>อุปกรณ์บันทึก kernel</blockquote></li>
</ul>
