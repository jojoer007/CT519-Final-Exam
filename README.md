(40 คะแนน) Final Exam
Chaiyaporn Khemapatapan
•
09:10 (แก้ไข 11:41)
40 คะแนน
ครบกำหนด 12:20
ให้นักศึกษาใช้งานระบบ Cloud ของ AWS เพื่อสร้างการให้บริการ ด้วย Docker / Docker Compose ที่มีสถาปัตยกรรมตามรูปแบบนี้
                     
                                                             +-------[Web 1]
                                                             |   
Internet -------------------- [NginX]------+-------[Web2]
                                                             |
                                                            +-------[Web3]

โดยกำหนดให้ Landing page  (https://CT519_XXX.ck2all.com  ) แสดงข้อมูล ดังนี้

       Student ID: XXXXXXX,  This is landing page from Web Server [1 / 2 / 3]
        - About              Redirect ไปยัง https://CT519_XXX.ck2all.com/about  บน Web1
        -  My research  Redirect ไปยัง https://CT519_XXX.ck2all.com/myresearch  บน Web2 
        -  CT519            Redirect ไปยัง https://CT519_XXX.ck2all.com/ct519 บน Web3
        -  Github            Redirect ไปยังลิ้งของ Github ของงานที่ทำข้อสอบนี้ (อย่าลืม public share)

โดยมาจากการทำ Reverse Proxy แบบ Roud Robin ไปยั้ง Web server ทั้ง 3 เครื่อง (Web1, Web2, Web3) 

สำหรับ Link ให้แสดงข้อมูลดังนี้
https://CT519_XXX.ck2all.com/about              แสดงข้อมูลรูปภาพและรายละเอียดส่วนตัวของนักศึกษา
https://CT519_XXX.ck2all.com/myresearch   แสดงข้อมูลรูปภาพและแนวทางการวิจัยของนักศึกษา
https://CT519_XXX.ck2all.com/ct519              แสดงข้อมูลรูปภาพและสรุปความรู้ในการดำเนินการข้อสอบนี้

ให้นักศึกษาสมัครใช้งาน Elastic IP เพื่อใช้งาน IP จริง โดยนักศึกษาต้องแจ้งหมายเลข IP ของแต่ละคนใน comment 

ให้นักศึกษาทำการร้องขอ certificate ที่ Let encrypt เพื่อสร้างการใช้งานโพรโทคอล HTTPS โดยชี้ไปยัง domain 
       CT519_XXX.ck2all.com  

เมื่อ XXX คือรหัส 3 ตัวหลังของนักศึกษา