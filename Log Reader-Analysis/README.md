# Log reader & Analysis
Log reader & Analysis คือ การอ่านบันทึกข้อผิดพลาดหรือบันทึกข้อมูล และวิเคราะห์ข้อมูลที่บันทึกไว้ใน log files ของ linux โดย log ที่บันทึกไว้อาจเป็นข้อมูลเกี่ยวกับเหตุการณ์ที่เกิดขึ้นในระบบ เช่น บันทึกการเข้าสู่ระบบ, การเปิดและปิดเซสชัน, การเข้าถึงไฟล์, ข้อผิดพลาดในระบบ เช่น grep, tail, awk, sed

# dmesg
Demgs คือคำสั่งที่ใช้เพื่อแสดงข้อมูลจาก kernel ring buffer ซึ่งเป็นพื้นที่ในหน่วยความจำที่ใช้เก็บข้อมูลเกี่ยวกับเหตุการณ์ต่าง ๆ ที่เกิดขึ้นในระบบเมื่อระบบทำงาน รวมถึงข้อผิดพลาด (errors) และข้อความแจ้งเตือน (warnings) ต่าง ๆ ที่อาจเกิดขึ้นในเวลาที่ระบบเปิดใช้งานหรือในระหว่างการทำงาน[1]<br>
## คำสั่ง dmesg [option][1]
<table>
    <tr>
        <th>Option</th>
        <th>Description</th>
        <th>Examples</th>
    </tr>
    <tr>
        <td><code>-C, --clear</code></td>
        <td>เคลียร์ kernel ring buffer</td>
        <td><code>dmesg -C</code></td>
    </tr>
     <tr>
    <td><code>-c, –read-clear</code></td>
    <td>เคลียร์ kernel ring buffer หลังข้อมูลถูกแสดง</td>
    <td><code>dmesg -c</code></td>
  </tr>
  <tr>
    <td><code>-f, –facility</code></td>
    <td>แสดงผลเฉพาะรายการของสิ่งที่ระบุไว้ในรายการหน่วยงานที่คั่นด้วยเครื่องหมายจุลภาค เช่น kern,user,syslog</td>
    <td><code>dmesg -f syslog</code></td>
  </tr>
  <tr>
    <td><code>-H, –human</code></td>
    <td>แสดงข้อมูลในรูปแบบของ HTML</td>
    <td><code>dmesg -H</code></td>
  </tr>
  <tr>
    <td><code>-L, --color[=auto|never|always]</code></td>
    <td>กำหนดการใช้สีในผลลัพธ์ที่แสดงผล</td>
    <td><code>dmesg –color=auto</code></td>
  </tr>
  <tr>
    <td><code>-l, –level</code></td>
    <td>เข้าถึงบันทึกตามที่ระบุลักษณะความสำคัญของข้อความ เช่น info,err,debug</td>
    <td><code>dmesg -l info</code></td>
  </tr>
  <tr>
    <td><code>--noescape</code></td>
    <td>ปิดใช้ละเว้นตัวอักษรที่ไม่สามารถพิมพ์ได้และอาจเป็นอันตรายได้โดยอัตโนมัติ เช่น ตัวอักษรควบคุม terminal</td>
    <td><code>dmesg --noescape</code></td>
  </tr>
  <tr>
    <td><code>-s, --buffer-size [size]</code></td>
    <td>กำหนดขนาดของ Buffer ขนาดเริ่มต้นคือ 16392</td>
    <td><code>dmesg -s 8192</code></td>
  </tr>
  <tr>
    <td><code>-T, --ctime</code></td>
    <td>แสดง timestamps ที่มนุษย์สามารถอ่านได้</td>
    <td><code>dmesg -T</code></td>
  </tr>
  <tr>
    <td><code>-t, --notime</code></td>
    <td>ไม่แสดง timestamps ของ kernel</td>
    <td><code>dmesg -t</code></td>
  </tr>
  <tr>
    <td><code>--time-format [format]</code></td>
    <td>แสดง timestamps โดยใช้ format เช่น iso,ctime</td>
    <td><code>dmesg –time-format=iso</code></td>
  </tr>
  <tr>
    <td><code>-w, --follow</code></td>
    <td>ติดตามการอัปเดตข้อมูลใหม่ที่ถูกเขียนลงใน buffer อย่างต่อเนื่อง</td>
    <td><code>dmesg -w</code></td>
  </tr>
</table>

>ข้อมูลเพิ่มเติม
- dmesg
    - แสดงผลลัพธ์จากคำสั่ง dmesg ทั้งหมด
- dmesg | less
    - จะแสดงผลลัพธ์จากคำสั่ง dmesg ในหน้าจอที่สามารถเลื่อนได้
- dmesg | grep -i pattern
    - ใช้สำหรับกรองข้อความที่ตรงกับ pattern ที่กำหนด เช่น dmesg | grep -i usb
> code examples
```cmd
  sudo dmesg --time-format=iso
```
แสดงเหตุการณ์ทั้งหมดที่เกิดขึ้นในระบบพร้อมกับเวลาในรูปแบบ ISO 8601 
<img src="iso1.png" width=90%>

```cmd
  sudo - dmesg | grep -i usb
```
แสดงเฉพาะบรรทัดในผลลัพธ์ของคำสั่ง dmesg ที่มีคำว่า "usb" โดยไม่คำนึงถึง case-insensitive
<img src="usb.png" width=90%>

<br>

# last
แสดงรายการของผู้ใช้ที่เข้าสู่ระบบล่าสุด รวมถึงเวลาที่เข้าและออกไปด้วย โดยมักจะแสดงในรูปแบบตารางที่แสดงชื่อผู้ใช้, อุปกรณ์ที่ใช้เข้าสู่ระบบ, ที่อยู่ IP, เวลาที่เข้าและออกจากระบบ, และระยะเวลาการใช้งาน การใช้คำสั่ง "last" สามารถช่วยในการตรวจสอบข้อมูลเกี่ยวกับการเข้าสู่ระบบ[2]
## คำสั่ง last [arguments] [parameters][2]
<table>
  <tr>
    <th>Option</th>
    <th>Description</th>
    <th>Examples</th>
  </tr>
  <tr>
    <td><code>-n, --lines N</code></td>
    <td>กำหนดจำนวนบรรทัดที่แสดง</td>
    <td><code>last -n 10</code></td>
  </tr>
  <tr>
    <td><code>-f, --file FILE</code></td>
    <td>ระบุไฟล์บันทึกที่จะใช้</td>
    <td><code>last -f /var/log/lastlog</code></td>
  </tr>
  <tr>
    <td><code>-i, --ipaddress</code></td>
    <td>แสดงที่อยู่ IP ของผู้ใช้</td>
    <td><code>last -i</code></td>
  </tr>
  <tr>
    <td><code>-R, --reboot</code></td>
    <td>แสดงข้อมูลเกี่ยวกับการรีบูตของระบบ</td>
    <td><code>last -R</code></td>
  </tr>
  <tr>
    <td><code>-x, --details</code></td>
    <td>แสดงรายละเอียดเพิ่มเติมเกี่ยวกับการเข้าสู่ระบบ</td>
    <td><code>last -x</code></td>
  </tr>
</table>

>code examplems
```
last
```
<img src="last.png" width=90%><br>
1. แสดงชื่อของผู้ใช้ที่เข้าสู่ระบบ[3]

2. ระบุว่าผู้ใช้เชื่อมต่อกับระบบอย่างไร เช่น ผ่าน pts (pseudo-terminal) หรือ tty (teletype) แต่ถ้ารีบูตจะแสดงว่า system boot.[3]

3. แสดงที่มาของผู้ใช้ที่เข้าสู่ระบบ[3] เช่น
    - ชื่อโฮสต์หรือที่อยู่ IP - หากผู้ใช้เชื่อมต่อจากคอมพิวเตอร์ระยะไกล
    - ค่าว่าง - หากผู้ใช้เชื่อมต่อผ่าน tty
    - เวอร์ชันของเคอร์เนล - หากreboot
    - ค่าที่เกี่ยวกับแอปพลิเคชันที่เฉพาะเจาะจง
4. แสดงเวลาที่กิจกรรมการเข้าสู่ระบบเกิดขึ้น[3]

5. แสดงเวลาออกจากระบบ[3]
    - ค่าที่อาจพบได้คือ
        - ปัจจุบันเวลา - หากผู้ใช้ออกจากระบบ
        - still running - หากระบบกำลังเริ่มต้นอยู่
        - still logged in - หากผู้ใช้ยังคงเข้าสู่ระบบ
        - down - ระบบปิดการทำงานอย่างปกติ
        - qcrash - หากไม่มีรายการออกจากระบบในไฟล์ "/var/log/wtmp" โดยทั่วไปนี่หมายถึงว่าระบบล้มเหลว

# awk
เป็นคำสั่งที่สามารถใช้แปลง, ค้นหา และ สร้างข้อมูลในรูปแบบ text ที่มีความซับซ้อนตามความต้องการของ user ได้ทุกรูปแบบ[5]
- Awk มักถูกใช้ในการดำเนินการต่างๆ กับข้อมูลข้อความ[6] เช่น
    1. การค้นหาและแสดงข้อมูลที่ตรงตามเงื่อนไขที่กำหนด
    2. การคำนวณค่าหรือการสร้างรายงานจากข้อมูล
    3. การแปลงรูปแบบของข้อมูล เช่น การเปลี่ยนรูปแบบของข้อมูลจากไฟล์ล็อกเข้ารหัสเป็นข้อความที่อ่านได้ง่าย
    4. การประมวลผลข้อมูลในรูปแบบของคอลัมน์และแถว
## คำสั่ง awk 'pattern { action }' input-file[7]
<table>
  <thead>
    <tr>
      <th>Action</th>
      <th>Description</th>
      <th>Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Print</td>
      <td>พิมพ์บรรทัดทั้งหมดที่ตรงกับเงื่อนไขที่กำหนด</td>
      <td><code>awk '/pattern/ { print }' input-file</code></td>
    </tr>
    <tr>
      <td>กำหนดค่า (Assignment)</td>
      <td>กำหนดค่าให้กับตัวแปรตามเงื่อนไขที่กำหนด</td>
      <td><code>awk '/pattern/ { var = $1 }' input-file</code></td>
    </tr>
    <tr>
      <td>เงื่อนไข (Conditional Statements)</td>
      <td>ทำตามเงื่อนไขที่กำหนด</td>
      <td><code>awk '/pattern/ { if ($1 > 10) print $0 }' input-file</code></td>
    </tr>
    <tr>
      <td>Looping</td>
      <td>ทำซ้ำๆ สำหรับแต่ละบรรทัด</td>
      <td><code>awk '{ for (i = 1; i <= NF; i++) print $i }' input-file</code></td>
    </tr>
    <tr>
      <td>BEGIN & END Blocks</td>
      <td>ทำการกระทำก่อนที่จะเริ่มการประมวลผลและหลังจากการประมวลผลสิ้นสุด</td>
      <td><code>awk 'BEGIN { print "เริ่มการประมวลผล" } /pattern/ { print $0 } END { print "การประมวลผลเสร็จสิ้น" }' input-file</code></td>
    </tr>
    <tr>
      <td>ฟังก์ชันที่มีอยู่ใน awk</td>
      <td>ฟังก์ชันที่ให้มาให้ใช้ในการประมวลผลข้อมูล</td>
      <td><code>awk '/pattern/ { len = length($1); print len }' input-file</code></td>
    </tr>
    <tr>
      <td>Arrays</td>
      <td>ใช้ในการจัดเก็บและประมวลผลข้อมูลในรูปแบบของอาร์เรย์</td>
      <td><code>awk '{ count[$1]++ } END { for (word in count) print word, count[word] }' input-file</code></td>
    </tr>
  </tbody>
</table>

>code examples[5]

ใช้ white space เป็นตัวแบ่งข้อมูล field ($) โดย field number จะเริ่มต้นที่ 1 แต่ถ้าจะให้แสดงผลทั้งหมดจะใช้ $0
```
awk '{print $0}' saixiii.txt
```
output
```
line,1,Hello world!
line,2,My name is saixiii
line,3,Good Bye
line,4,Bye
```

ใส่เงื่อนไขในการแสดงผล
```
awk -F',' '{if($2%2==1) {print $0}}' saixiii.txt
```
output
```
line,1,Hello world!
line,3,Good Bye
```

# sed
ใช้สำหรับแก้ไขและประมวลผลข้อมูลข้อความเป็นลำดับ โดยทำงานโดยอ่านข้อมูลจากแหล่งให้ได้ และส่งออกผลลัพธ์ไปยังอีกแหล่งหนึ่ง โดยจะทำการแก้ไขข้อมูลของแถวที่ตรงตามเงื่อนไขที่กำหนดไว้ หรือปฏิบัติการอื่น ๆ ตามคำสั่งที่ระบุ โดยการใช้งานผ่าน command line interface (CLI)[8]

## คำสั่ง sed [options] 'command' file[8]
<table>
  <tr>
    <th>Option</th>
    <th>Description</th>
    <th>Examples</th>
  </tr>
  <tr>
    <td><code>-n</code></td>
    <td>ป้องกันการพิมพ์โดยอัตโนมัติของสเปซแพทเทิร์น</td>
    <td><code>sed -n '1p' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-i</code></td>
    <td>แก้ไขไฟล์ในที่ (ทำการสำรองไฟล์หากมีการระบุนามสกุล)</td>
    <td><code>sed -i.bak 's/old/new/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-e script</code></td>
    <td>เพิ่มสคริปต์ไปยังคำสั่งที่จะประมวลผล</td>
    <td><code>sed -e 's/old/new/' -e 's/foo/bar/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-r</code></td>
    <td>ช้ syntax ของ regular expression แบบขยาย</td>
    <td><code>sed -r 's/regex/replacement/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-f script-file</code></td>
    <td>เพิ่มเนื้อหาของไฟล์สคริปต์ไปยังคำสั่งที่จะประมวลผล</td>
    <td><code>sed -f script.sed file.txt</code></td>
  </tr>
  <tr>
    <td><code>-i.bak</code></td>
    <td>สำรองไฟล์เดิมด้วยนามสกุล .bak ก่อนที่จะแก้ไขในที่</td>
    <td><code>sed -i.bak 's/old/new/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-u</code></td>
    <td>เก็บข้อมูลเขียนจนกว่าจะมีการเกิดการขึ้นของบรรทัดในสเปซแพทเทิร์น</td>
    <td><code>sed -u 's/old/new/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-h</code></td>
    <td>ป้อนเอ็นทรี่ไปยังคำสั่ง sed โดยไม่ระบุชื่อไฟล์ที่อยู่ในหัวข้อ</td>
    <td><code>sed -n 's/old/new/' file.txt</code></td>
  </tr>
  <tr>
    <td><code>-V</code></td>
    <td>แสดงรายละเอียดเวอร์ชันของ sed</td>
    <td><code>sed -V</code></td>
  </tr>
</table>

>ข้อมูลเพิ่มเติม[8]

แทนที่ข้อความเก่าด้วยข้อความใหม่เฉพาะครั้งแรกที่พบในแต่ละบรรทัดของไฟล์
```
sed 's/old_string/new_string/' filename.txt
```
แทนที่ข้อความเก่าด้วยข้อความใหม่ทุกครั้งที่พบ โดยไม่จำกัดเพียงครั้งเดียวต่อบรรทัดเท่านั้น
```
sed 's/old_string/new_string/g' filename.txt
```
แทนที่ข้อความเก่าด้วยข้อความใหม่ในเฉพาะครั้งที่ #(1,2,..) ที่พบ

```
sed 's/old_string/new_string/#' filename.txt
```
แทนที่ข้อความในบรรทัดที่ i-j ตามที่กำหนด
```
sed 'i,j s/old_string/new_string/' filename.txt
```
ลบข้อความในบรรทัดที่กำหนด(# = number)
```
sed '#d' filename.txt
```
ลบข้อความในบรรทัดที่ i-j
```
sed 'i,jd' filename.txt
```
ลบเนื้อหาจากบรรทัดที่กำหนดจนถึงบรรทัดสุดท้ายของ file
```
sed '#,$d' filename.txt
```

# Journalctl

Journalctl  คือ คำสั่งในการที่เรียกดูบันทึกเหตุการณ์ทั้งหมดภายในระบบ ซึ่งเป็นการบันทึกกระบวนการต่างๆ คือ กระบวนการบูตก่อนหน้า, เคอร์เนล, initrd และข้อผิดพลาดของแอปพลิเคชัน [9]


```cmd
journalctl
```
คำสั่ง :


<img src="journalct-main.png">

ผลลัพธ์ :

<img src="journalct2.png"><br>

## คำสั่ง journalctl [option]
<table>
  <tr>
    <th>Option</th>
    <th>Description</th>
    <th>Examples</th>
  </tr>
  <tr>
    <td><code>-b, --boot</code></td>
    <td>แสดงรายการสำหรับบูตปัจจุบันหรือบูตที่กำหนด</td>
    <td><code>journalctl -b</code></td>
  </tr>
  <tr>
    <td><code>--since</code></td>
    <td>แสดงรายการที่เกิดขึ้นตั้งแต่เวลาที่ระบุ</td>
    <td><code>journalctl --since "2024-02-07 10:00:00"</code></td>
  </tr>
  <tr>
    <td><code>--until</code></td>
    <td>แสดงรายการที่เกิดขึ้นก่อนเวลาที่ระบุ</td>
    <td><code>journalctl --until "2024-02-07 12:00:00"</code></td>
  </tr>
  <tr>
    <td><code>-u, --unit</code></td>
    <td>ระบุหน่วยที่ต้องการให้แสดงรายการ</td>
    <td><code>journalctl -u sshd.service</code></td>
  </tr>
  <tr>
    <td><code>-p, --priority</code></td>
    <td>ระบุระดับความสำคัญของข้อความ</td>
    <td><code>journalctl -p err</code></td>
  </tr>
  <tr>
    <td><code>--grep</code></td>
    <td>ค้นหาข้อความที่ตรงกับ pattern ที่กำหนด</td>
    <td><code>journalctl --grep "failed"</code></td>
  </tr>
  <tr>
    <td><code>--user-unit</code></td>
    <td>แสดงรายการที่เกี่ยวข้องกับผู้ใช้งานที่ระบุ</td>
    <td><code>journalctl --user-unit sshd.service</code></td>
  </tr>
  <tr>
    <td><code>--system</code></td>
    <td>แสดงรายการที่เกี่ยวข้องกับระบบทั้งหมด</td>
    <td><code>journalctl --system</td>
  </tr>
  <tr>
    <td><code>--list-boots</code></td>
    <td>แสดงรายการของบูตที่มี</td>
    <td><code>journalctl --list-boots</td>
  </tr>
  <tr>
    <td><code>--disk-usage</code></td>
    <td>แสดงขนาดข้อมูลบันทึกบัญชีข้อผิดพลาดในระบบของเครื่อง</td>
    <td><code>journalctl --disk-usage</td>
  </tr>
</table><br>


>Option ที่น่าสนใจ

```cmd
--since / --until 
```

ใช้ในการเรียกดูบันทึกตามวัน-เวลาที่ต้องการ โดยใช้ since และ until ในรูปเเบบของการกำหนดวันเเละเวลา คือ YYYY-MM-DD HH:MM:SS
Ex. journalctl --since "2015-01-10" --until "2015-01-11 03:00" , 
journalctl --since yesterday, journalctl –since -1d 

คำสั่ง : 

<img src="journalct_sin.png">

ผลลัพธ์ :

<img src="journalct-since-re.png"><br>

```cmd
-p (priority)
```

ใช้ในการเรียกดูบันทึกตามระดับความสำคัญ (priority) ที่สนใจ
- 0 : สถานการณ์ฉุกเฉินที่ต้องการการทำงานเร่งด่วน
- 1 : การแจ้งเตือน ระดับความสำคัญสูงกว่าทั่วไป ต้องเเก้ไขทันที
- 2 : สำคัญ ครอบคลุมการแครช coredumps และความล้มเหลวที่สำคัญในแอปพลิเคชันหลัก มีระดับความสำคัญสูงและต้องตอบสนองโดยเร่งด่วน
- 3 : ข้อผิดพลาด มีการรายงานข้อผิดพลาดที่ต้องการการแก้ไข
- 4 : คำเตือน สถานการณ์ที่อาจก่อให้เกิดปัญหาในอนาคต หากเพิกเฉยอาจกลายเป็นข้อผิดพลาดได้
- 5 : ประกาศ ใช้เพื่อรายงานสถานการณ์ที่น่าสนใจแต่ไม่ใช่ข้อผิดพลาดหรือปัญหาที่ผิดปกติ
- 6 : ข้อมูล ข้อความการดำเนินงานทั่วไป
- 7 : ดีบัก ข้อมูลเพิ่มเติมสำหรับการตรวจสอบปัญหาหรือการทำงานของระบบ โดยข้อความบอกแก้ไขจุดบกพร่อง<br>


ผลลัพธ์ :

<img src = "journalct-p.png"><br>

```cmd
  _COMM 
```
ใช้ในการเรียกดูบันทึกของโปรเเกรมที่สนใจ โดย _COMM  = ชื่อของโปรแกรมที่สร้างบันทึก 

ex. <code>journalctl -f _COMM=geek-app</code>


```cmd
  _PID 
```
ใช้ในการเรียกดูบันทึกเฉพาะกระบวนการที่สนใจ


ex. <code>journalctl _PID=751</code>


```cmd
  _UID
```

ใช้ในการเรียกดูบันทึกที่สร้างโดยผู้ใช้ User ID ที่สนใจ

ex. <code>journalctl _UID=1000</code><br><br>

>เพิ่มเติม

อาจจะใช้ sudo นำหน้าด้วย ความเเตกต่างกัน คือ<br>
journalctl ปกติ มันสามารถดูข้อมูลได้บางส่วน เพราะยังมีบางบันทึกที่กำหนดสิทธิการเข้าถึงที่ผู้ใช้ทั่วไปไม่สามารถดูได้<br>
sudo journalctl จะสามารถเข้าถึงบันทึกได้ทั้งหมด ทั้งข้อมูลที่เป็นความลับหรือข้อมูลที่ต้องมีสิทธิพิเศษในการเข้าถึง เพราะฐานะของผู้ดูแลระบบ<br><br>

# lastcomm
lastcomm เป็นคำสั่งที่ใช้แสดงประวัติการใช้งานของผู้ใช้ ที่บันทึกไว้ใน /var/account/pacct การเเสดงผลจะเรียงตามเวลาล่าสุดที่ทำงานไปก่อนหน้านั้น [10]


การใช้คำสั่ง lastcomm ต้องติดตั้งแพ็กเกจ acct โดยใช้

สำหรับ Ubuntu หรือ Debian :
```cmd
sudo apt update
sudo apt install acct
```

acct ช่วยในการบันทึกข้อมูลเหล่านี้ไว้ เป็นไฟล์ log โดยที่  log พวกนี้อยู่ใน /var/log/account/pacct หรือ /var/account/pacct


ข้อมูลที่ lastcomm เเสดง คือ
- ชื่อคำสั่ง
- สถานะการทำงานของกระบวนการ (Flags) <br>
  ลักษณะของ flags มีดังนี้
  - '<': แสดงว่ากระบวนการทำงานนี้มีการอ่านจากไฟล์
  - '>': แสดงว่ากระบวนการทำงานนี้มีการเขียนลงไปในไฟล์
  - 'C': กระบวนการทำงานเป็นการควบคุมการเข้าถึงข้อมูล (Control process)
  - 'E': กระบวนการทำงานเป็นของระบบการส่งออก
  - 'X': แสดงว่ากระบวนการทำงานถูกติดตั้งเป็น setgid (set group ID)
  - '+' (คำนำหน้า): แสดงว่าโปรแกรมนี้ถูกตรวจสอบสิทธิ์บนเครื่อง
  - 'S': กระบวนการทำงานอยู่ในสถานะพร้อมทำงาน
  - 'D': กระบวนการทำงานอยู่ในสถานะพักการทำงาน (uninterruptible sleep)
  - 'R': กระบวนการทำงานอยู่ในสถานะรอการรัน<br>
  - 'Z': กระบวนการทำงานเป็น zombie <br>
<li>ชื่อผู้ใช้งาน</li>
<li>หมายเลข PID (Process ID)</li>
<li>เวลาที่กระบวนการเริ่มต้น-จบ</li><br>

คำสั่ง:
```cmd
  lastcomm
```
ผลลัพธ์ :

<img src="lastcomm-re.png" width=90%>


## คำสั่ง lastcomm [option]
<table>
  <tr>
    <th>Option</th>
    <th>Description</th>
    <th>Examples</th>
  </tr>
  <tr>
    <td><code>-c</code></td>
    <td>แสดงชื่อของคำสั่งที่ใช้งาน</td>
    <td><code>lastcomm -c 10</code></td>
  </tr>
  <tr>
    <td><code>-d</code></td>
    <td>แสดงชื่อของคำสั่งในวันที่ระบุ</td>
    <td><code>lastcomm -d "2024-02-07"</code></td>
  </tr>
  <tr>
    <td><code>-f</code></td>
    <td>แสดงข้อมูลทั้งหมดที่มีอยู่</td>
    <td><code>lastcomm -f, lastcomm -f filename</code></td>
  </tr>
  <tr>
    <td><code>-h</code></td>
    <td>ไม่เอาส่วนหัวของผลลัพธ์</td>
    <td><code>lastcomm -h</code></td>
  </tr>
  <tr>
    <td><code>-l</code></td>
    <td>แสดงข้อมูลที่เกี่ยวกับ process เช่น uid, gid, tty</td>
    <td><code>lastcomm -l</code></td>
  </tr>
  <tr>
    <td><code>-m</code></td>
    <td>รายงาน process ที่สร้างโดย crontab</td>
    <td><code>lastcomm -m</code></td>
  </tr>
  <tr>
    <td><code>-r</code></td>
    <td>แสดงผลลัพธ์ในย้อนหลัง</td>
    <td><code>lastcomm -r</code></td>
  </tr>
  <tr>
    <td><code>-s</code></td>
    <td>แสดงคำสั่งที่ระบุตามเวลา</td>
    <td><code>lastcomm -s "08:00" -s "17:00"</code></td>
  </tr>
  <tr>
    <td><code>-t</code></td>
    <td>แสดงรายการของคำสั่งที่ระบุ</td>
    <td><code>lastcomm -t "bash"</code></td>
  </tr>
  <tr>
    <td><code>-u</code></td>
    <td>ระบุผู้ใช้งานที่ต้องการให้แสดงผล</td>
    <td><code>lastcomm -u "username"</code></td>
  </tr>
</table><br>

>Option ที่น่าสนใจ

<code>--strict-match</code> ระบุคำสั่งที่ต้องการค้นหา 
ex. <code>lastcomm --strict-match rsync</code><br>
<code>--tty name</code> แสดงรายการของคำสั่งที่ถูกเรียกใช้โดยกรองเฉพาะผู้ใช้ที่ ที่ทำงานบน tty
ex. <code>lastcomm --tty pts/0 name</code><br>

คำสั่ง :

```cmd
  lastcomm --tty pts/0 name
```

ผลลัพธ์:


<img src="lastcomm -tt.png" width=90%><br>


# tail
tail เป็นการเเสดงเนื้อหาของไฟล์จากท้ายสุด เพื่อดูเนื้อหาที่เพิ่มมาใหม่ 
>ประโยชน์ของ tail
 - ช่วยทำให้สามาถติดตามข้อมูลใหม่ได้อย่าง real time  
 - Error Checking ทำให้สามาถตรวจสอบการเขียนล่าสุด เพื่อค้นหาข้อผิดพลาด
 -  General Data Viewing ช่วยให้ดูข้อมูลในไฟล์ขนาดใหญ่ได้เร็วขึ้น โดยไม่ต้องอ่านทั้งหมด ดูเเค่ส่วนท้ายของไฟล์ [11]

คำสั่ง :
```cmd
 tail filename
 ```

ผลลัพธ์ : 

<img src="tail_re.png">

## คำสั่ง tail [option]
<table>
  <tr>
    <th>Option</th>
    <th>Description</th>
    <th>ตัวอย่าง</th>
  </tr>
  <tr>
    <td><code>-n, --lines</code></td>
    <td>แสดงจำนวนบรรทัดที่กำหนด</td>
    <td><code>tail -n 20 myfile.txt</code> (แสดง 20 บรรทัดท้ายสุดของไฟล์ myfile.txt)</td>
  </tr>
  <tr>
    <td><code>-c, --bytes</code></td>
    <td>แสดงจำนวนไบต์ที่กำหนด</td>
    <td><code>tail -c 100 myfile.txt</code> (แสดง 100 ไบต์สุดท้ายของไฟล์ myfile.txt)</td>
  </tr>
  <tr>
    <td><code>-f, --follow</code></td>
    <td>ติดตามการเพิ่มข้อมูลล่าสุดในไฟล์</td>
    <td><code>tail -f access.log</code> (ติดตามการเพิ่มข้อมูลล่าสุดในไฟล์ access.log และแสดงอัปเดตเมื่อมีการเพิ่มข้อมูลใหม่)</td>
  </tr>
  <tr>
    <td><code>--pid=PID</code></td>
    <td>ติดตามการเพิ่มข้อมูลล่าสุดจาก process ที่กำหนด</td>
    <td><code>tail --pid=5555 access.log</code> (ติดตามการเพิ่มข้อมูลล่าสุดในไฟล์ access.log ที่ process หมายเลข 1234 สร้างข้อมูล)</td>
  </tr>
</table>

# grep

grap เป็นคำสั่งที่ใช้ค้นหารูปแบบข้อความ(นิพจน์)ที่อยู่ในไฟล์ และ แสดงบรรทัดในไฟล์ที่ตรงกับรูปแบบนั้น [12]

คำสั่ง : 
```cmd
   grep "string" file name หรือ filename grep "string"
```
ผลลัพธ์ :

<img src="grep.png"><br>

## คำสั่ง grep [options] pattern [FILE][4]
<table>
<tr>
    <th>Option</th>
    <th>Description</th>
    <th>Examples</th>
  </tr>
  <tr>
    <td><code>-i</code></td>
    <td>ไม่สนใจตัวอักษรพิมพ์ใหญ่หรือเล็กใน pattern</td>
    <td><code>grep -i "pattern" filename</code></td>
  </tr>
  <tr>
    <td><code>-r</code></td>
    <td>อ่านไฟล์ทั้งหมดในแต่ละไดเรกทอรีและไดเรกทอรีย่อยๆ</td>
    <td><code>grep -r "pattern" directory</code></td>
  </tr>
  <tr>
    <td><code>-n</code></td>
    <td>เติมหมายเลขบรรทัดของแต่ละบรรทัดในไฟล์เข้าไปด้วย โดยนับจากบรรทัดแรกเป็นบรรทัดที่ 1</td>
    <td><code>grep -n "pattern" filename</code></td>
  </tr>
  <tr>
    <td><code>-v</code></td>
    <td>เลือกบรรทัดที่ไม่ตรงกับpattern</td>
    <td><code>grep -v "pattern" filename</code></td>
  </tr>
  <tr>
    <td><code>-E</code></td>
    <td>ใช้ regular expressions ขั้นสูง (รองรับ ?, +, {}, () เป็นต้น)</td>
    <td><code>grep -E "pattern" filename</code></td>
  </tr>
  <tr>
    <td><code>-w</code></td>
    <td>ตรงกับคำเท่านั้น</td>
    <td><code>grep -w "คำ" filename</code></td>
  </tr>
  <tr>
  <td><code>--color</code></td>
  <td>ทำให้ข้อความที่ตรงกับ pattern มีสีเน้น</td>
  <td><code>grep --color "pattern" filename</code></td>
  <tr>
    <td><code>-c</code></td>
    <td>นับจำนวนบรรทัดที่ตรงกับ pattern</td>
    <td><code>grep -c "pattern" filename</code></td>
   </tr>
  <tr>
    <td><code>-l</code></td>
    <td>แสดงเฉพาะชื่อไฟล์ที่มีข้อมูลที่ตรงกับ pattern</td>
    <td><code>grep -l "pattern" *.txt</code></td>
  </tr>
  <tr>
    <td><code>-f</code></td>
    <td>อ่าน patternจากไฟล์</td>
    <td><code>grep -f patterns.txt filename</code></td>
  </tr>
</table>

>รูปเเเบบการค้นหา Option ที่น่าสนใจ

- นับจำนวนบรรทัดที่ตรงกับ pattern

```c
grep -c "hello" xxx.txt
```

<img src="grep1.png" width=70%><br>

- Ignoring case sensitivity คือ ค้นหา String ในไฟล์ โดย ไม่ต้องคำนึงถึง ตัวพิมพ์ใหญ่ ตัวพิมพ์เล็ก
  ```cmd
    grep -i "String" welcome.txt
  ```
  ex. <code>grep -i "UNix" popo.txt</code>

- Searching for a string recursively in all directories คือ การค้นหา string ที่อยู่ใน current directory ทั้งหมด

  ```cmd
    grep -r "string" *
  ```
  ex. <code>grep -r "linux" *</code>

-  REGEX (regular expressions) คือ การค้นหาแบบซับเซ็ตของข้อความ หรือรูปแบบของข้อความ เช่น
   - ค้นหาข้อความที่มี "apple" หรือ "orange" ในไฟล์ fruits.
   txt: <code>grep "apple\|orange" fruits.txt</code>
    - ค้นหาบรรทัดที่ขึ้นต้นด้วย "apple" ในไฟล์ fruits.txt: <code>grep "^apple" fruits.txt</code>
    - ค้นหาบรรทัดที่มี "banana" ซึ่งตามด้วย "s" หรือ "es" ในไฟล์ fruits.txt: <code>grep "pineapple[s|es]" fruits.txt</code>
    - ค้นหาบรรทัดที่มีตัวอักษร "a", "b", "c" อย่างน้อยหนึ่งครั้งในไฟล์ fruits.txt: <code>grep "[a-c]" fruits.txt</code>
- ค้นหาการติดตั้งแพ็คเกจ
  ```cmd
    dpkg -L | grep "package-name"
  ```
  ex. <code>dpkg -L | grep -i "openssh"</code><br><br>


# rsyslog

The Rocket-fast System for log processing (rsyslog) คือ ยูทิลิตี้สำหรับรวบรวมจัดการข้อมูลเหตุการณ์ โดยการรวบรวมเหตุการณ์จากแอปพลิเคชันต่างๆ และเก็บไว้ในไฟล์บันทึก (log files) หรือส่งไปยังที่เก็บข้อมูล (log storage) หรือตัวจัดการ log เช่น Elasticsearch เพื่อให้จัดการข้อมูลเหตุการณ์ให้มีประสิทธิภาพ [13]

>คำสั่งพื้นฐานของ rsyslog
- Check status of rsyslog service:

```cmd
    sudo systemctl status rsyslog
```
ผลลัพธ์ :

<img src="check rsyslog.png">


- Start rsyslog service to start on boot

```cmd
    sudo systemctl start rsyslog
```


- Enable rsyslog service to start on boot

```cmd
    sudo systemctl enable rsyslog
```


- Restart rsyslog
```cmd
    sudo systemctl restart rsyslog
```

- View rsyslog configuration
```cmd
    cat /etc/rsyslog.conf
```
ผลลัพธ์ :

<img src="rsysconf.png"><br><br>

# logrotate
logrotate คือ เป็นตัวจัดการไฟล์บันทึก(log file) เเละการหมุนเวียนของไฟล์ที่บันทึก อัตโนมัติ เพื่อเเก้ปัญหาหน่วยความจำเต็ม หรือการเก็บข้อมูลที่ไม่จำเป็น ทำให้ลดปัญหาด้านประสิทธิภาพและหน่วยความจำที่เกิดกับเซิร์ฟเวอร์ [14]

>การทำงาน
  - มีการกำหนดเวลาหรือขนาดสูงสุดของไฟล์บันทึก ที่จะหมุนเปลี่ยน เมื่อเกิดที่กำหนด logrotate จะถูกเรียกใช้ จะมีการสร้างไฟล์บันทึกใหม่และส่งไฟล์บันทึกเก่าไปที่กำหนด
  -  logrotate มีบีบอัดไฟล์บันทึกที่ถูกหมุนเปลี่ยนเพื่อประหยัดพื้นที่
  -  logrotate ลบไฟล์บันทึกเก่าที่ไม่ได้ใช้งานออกจากระบบ
  -  แจ้งเตือนผู้ดูแลระบบเมื่อมีการหมุนเปลี่ยนไฟล์หรือเมื่อเกิดปัญหา

ข้อมูลการกำหนดค่าการทำงานของ Logrotate
  - /etc/logrotate.conf
  - /etc/logrotate.d/

<br>

> คำสั่งพื้นฐาน

- เรียกดูการกำหนดค่า Logrotate:
```cmd
cat /etc/logrotate.conf
```
ผลลัพธ์ :

<img src="catlogro.png"><br>

- ตรวจสอบสถานะของการเคลื่อนไหวของ Logrotate
```cmd
sudo logrotate -f /etc/logrotate.conf
```
ผลลัพธ์ :

<img src="sudo_cat_status.png"><br>

- ดู Logrotate ว่าจะทำอะไรกับไฟล์บันทึก
```cmd
  sudo logrotate -d /etc/logrotate.conf
```
ผลลัพธ์ :

<img src="logrotate_-d.png"><br>

- ทดสอบการหมุนเวียนของไฟล์ที่บันทึก

```cmd
  sudo logrotate -vf /etc/logrotate.d/myapp
```
ผลลัพธ์ :

<img src="logro_test.png"><br>

- หมุนเวียนของไฟล์ที่บันทึกสำหรับไฟล์ที่ระบุ
```cmd
  sudo logrotate -d -f /etc/logrotate.conf
```

>คำเเนะนำ

logrotate ต้องมีสิทธิ์การเข้าถึงข้อมูลในไดเร็กทอรีและไฟล์ที่ต้องการจัดการ ด้วยการ sudo หรือเป็นผู้มีสิทธิ์เท่านั้น


>Reference

[1]https://phoenixnap.com/kb/dmesg-linux<br>
[2]https://ioflood.com/blog/last-linux-command/<br>
[3]https://www.baeldung.com/linux/last-command<br>
[4]https://www.hostinger.com/tutorials/grep-command-in-linux-useful-examples/<br>
[5]https://saixiii.com/awk-linux-command/<br>
[6]https://th.linux-console.net/?p=17513<br>
[7]https://linuxize.com/post/awk-command/<br>
[8]https://phoenixnap.com/kb/linux-sed<br>
[9] https://www.howtogeek.com/499623/how-to-use-journalctl-to-read-linux-system-logs/ <br>
[10] https://www.cyberciti.biz/faq/linux-unix-lastcomm-command-examples-usage-syntax/ <br>
[11] https://phoenixnap.com/kb/linux-tail <br>
[12] https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix <br>
[13] https://www.linkedin.com/pulse/how-install-set-up-rsyslog-server-linux-ubuntu-20041-akshay-sharma<br>
[14] https://betterstack.com/community/guides/logging/how-to-manage-log-files-with-logrotate-on-ubuntu-20-04/
