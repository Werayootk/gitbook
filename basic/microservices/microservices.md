---
description: "\U0001F914 ออกแบบ Microservices Architecture ยังไงถึงจะถือว่าดี ?"
---

# Microservices ที่ดีมีลักษณะยังไง

จากบทความที่แล้วเราก็จะพอเห็นไอเดียวแล้วว่า **Microservices Arhictectures** นั้นมีหัวใจหลักเรื่องอะไรบ้าง และเพื่อนๆบางคนก็อาจจะเคยได้ลองเล่น architecture นี้ไปบ้างแล้ว แต่เคยนึกสงสัยไหมว่า การออกแบบ architecture แบบนี้นั้นมันควรจะต้องเป็นยังไง? ดังนั้นในรอบนี้เราจะไปดู**ลักษณะเฉพาะตัว**ของ Microservices Architecture หรือสิ่งที่เรียกว่า **Characteristic** กัน

{% hint style="success" %}
**แนะนำให้อ่าน**  
บทความนี้เป็นส่วนหนึ่งของบทความ [👶 Microservices พื้นฐาน](https://saladpuk.gitbook.io/learn/basic/microservices) หากเพื่อนๆสนใจอยากรู้ประวัติความเป็นมาและข้อมูลเบื้องต้นของ Microservices architecture ก็สามารถกดเข้าไปอ่านจากลิงค์สีฟ้าๆได้เลยนะครับ
{% endhint %}

{% hint style="info" %}
**อ้างอิง**  
บทความนี้ถอดความรู้มาจากมหาเทพ [James Lewis](https://twitter.com/boicy) และ [Martin Fowler](https://martinfowler.com/) โดยสามารถเข้าไปดูบทความหลักได้จากลิงค์นี้เลยครับ [Microservices ](https://martinfowler.com/articles/microservices.html)
{% endhint %}

## Characteristics of a Microservice Architecture

ลักษณะเฉพาะตัวของเจ้า microservice นั้นมหาเทพได้กล่าวว่ามันควรจะมีองค์ประกอบด้านล่างนี้ครบถึงจะถือว่าดี แต่ถึงจะมีไม่ครบก็ยังเป็น microservice ได้อยู่นะ แต่มันจะขาดคุณสมบัติบางอย่างไป ดังนั้นลองไปไล่กันดูเลยละกันว่ามันมีอะไรบ้าง

## 🔥 เซอร์วิสต้องขาดออกจากกัน

หลักในการออกแบบ microservice คือให้มองของต่างๆเป็น**ส่วนประกอบ**หรือที่เราเรียกกันว่า **Component** โดยในแต่ละ component นั้นจะต้องแยกขาดออกจากกันแบบสุดโต่ง

**อธิบายให้เห็นภาพ**  
เพื่อให้เห็นภาพที่ชัดเจนขึ้นให้เรามองมองว่าแต่ละ component คือชิ้นเลโก้ เพราะเลโก้แต่ละชิ้นมันไม่มีความเกี่ยวข้องอะไรกันเลย เราไม่ชอบชิ้นไหนก็สามารถถอดเปลี่ยนไปใช้ชิ้นอื่นเมื่อไหร่ก็ได้

![](../../.gitbook/assets/image%20%28342%29.png)

สาเหตุที่ต้องออกแบบให้แต่ละ component ขาดออกจากกันก็เพราะ เราจะได้สามารถแยกทำอะไรกับแต่ละ component ได้อิสระโดยไม่ไปกระทบกับ component อื่นๆเลยนั่นเอง เช่น อยากใช้ภาษาอะไรกับ component นั้นก็ใช้ไป วันดีคืนดีอยากเปลี่ยนภาษาก็เปลี่ยนได้เลย อยาก re-deploy ใหม่ก็ทำไป **เพราะแต่ละส่วนมันแยกขาดออกจากกัน**

ส่วนถ้ามันจะต้องไปทำงานร่วมกับ component อื่นก็ขอแค่เรียกใช้งานผ่าน **Web service request** แทนนั่นเอง โดยแต่ละ service จะต้องมี **Component Interface** ที่มั่นคงของมันเอง

{% hint style="danger" %}
**ข้อเสีย**  
แต่ละ component จะติดต่อทำงานร่วมกันได้ช้ากว่าปกติเพราะมันคุยกันผ่าน web service request ทุกครั้งนั่นเอง และมันจะเป็นเรื่องใหญ่มากถ้าเราต้องการจะย้ายหน้าที่การรับผิดชอบข้าม component กัน
{% endhint %}

## 🔥 ดูแลเฉพาะเรื่องของมัน

ในการทำ microservice architecture นั้น เราควรจะแยกทีมทำงานในรูปแบบของ microservice ด้วย โดย service หนึ่งตัวก็ควรจะมีทีมดูแลทีมเดียว และคนภายในทีมควรจะเป็นแบบ **cross-functional team** ด้วย หรือพูดง่ายๆคือคนในทีมต้องทำงานหลากหลายเป็น เช่น มีทั้งฝั่ง back-end, front-end, database บลาๆ อยู่ภายในทีมเดียวกันตามรูปด้านล่าง

![](../../.gitbook/assets/image%20%2814%29.png)

และที่สำคัญคือแต่ละทีมที่ดูแล service นั้นจะต้องดูแลแค่เพียงกลุ่มงานเดียวเท่านั้น หรือที่เราเรียกกันว่า **Bounded context** นั่นเอง เพราะถ้าทีมต้องดูแลกลุ่มงานมากกว่า 1 ตัว มันจำทำให้เราสับสนหรือไม่สามารถ focus ตัวงานได้ดี และผลเสียก็จะรวมถึงตัว service ด้วย เพราะมันดูแลงานมากกว่า 2 เรื่องทำให้ถ้ามีการแก้เรื่องใดเรื่องหนึ่งมันก็จะส่งผลกระทบกับอีกเรื่องด้วย ไม่ทางตรงก็ทางอ้อม

## 🔥 มันคือชิ้นงาน

โดยปกติเวลาที่เราทำงานเสร็จ เราก็จะปิดงานนั้นๆแล้วยุบทีมไปรวมกับทีมอื่น เพื่อช่วยกันทำงานชิ้นถัดไป แต่ในการทำ Microservices นั้นจะไม่ทำแบบนั้น แต่เขาจะใช้หลักการว่า **มึงสร้างมึงก็ดูแลด้วย** ดังนั้นทีมที่ดูแล component นั้นๆทำงานเสร็จก็ต้องรับผิดชอบดูแลมันต่อ เอางานขึ้น production ดูแล เพิ่มเติมแก้ไขกันไปจนตายกันไปข้าง และไม่ใช่แค่ทำให้มันเสร็จเท่านั้น แต่จะต้องเอาใจใส่เหมือนลูกเพื่อมองว่า**เราจะทำให้มันดีขึ้นได้ยังไง**อีกด้วย เพราะตัว service มันไม่ใช่ตัว project แต่มันคือชิ้นส่วนตัวนึงของงานทั้งหมดนั่นเอง

## 🔥 การคุยกันทำให้มันง่าย

การคุยกันระหว่าง service นั้นจะต้องเรียบง่าย โดยการทำงานผ่าน **HTTP protocol** โดยสนับสนุนให้ใช้ **REST** นั่นเอง เพราะทุกคนก็สามารถเรียกใช้งานได้โดยไม่มีข้อจำกัดในเรื่องของภาษา หรือจะให้มันง่ายจนกระทั่งมันอยู่แค่ภายใน router เลยก็ได้

## 🔥 ดูแลแต่ละเซอร์วิสแยกกัน

ในการจัดการแต่ละ service นั้นควรแยกให้แต่ละทีมรับผิดชอบกันเอง เช่น ทีมจะเลือกใช้ภาษาอะไร ก็ปล่อยให้ทีมจัดการไป เพราะแต่ละ component นั้นแยกขาดออกจากกันอยู่แล้ว และงานแต่ละแบบก็จะมีเครื่องมือหรือภาษาที่เหมาะสมกับหน้างานของมันเองอยู่แล้วนั่นเอง

{% hint style="danger" %}
**ข้อควรระวัง**  
การที่เราปล่อยให้ service เป็นอิสระก็ไม่ให้หมายความว่าให้ใช้อะไรก็ได้มั่วซั่วนะ แต่ทีมแต่ละทีมควรจะมีการแชร์กันเรื่อง tools ต่างๆ ข้อดีข้อเสียที่ได้เรียนรู้มา เพื่อให้สามารถพัฒนาความรู้และเทคนิกต่างๆให้ไปด้วยกันได้ ไม่ใช่ปล่อยให้ทีมนึงโดดไปใช้อะไรก็ไม่รู้แล้วก็ส่งงานไม่ได้ และการที่จะทำ features อะไรออกมาในแต่ละ iteration ก็ต้องให้มันสอดคล้องกับทีมอื่นๆด้วยนะ
{% endhint %}

## 🔥 ดูแลข้อมูลแยกกัน

service แต่ละตัวถ้าแยกกัน component แล้ว เราก็สามารถจะให้แต่ละ service แยกจัดการกับข้อมูลของมันเองได้อิสระเลย เช่น จะใช้ MongoDB หรือใช้ SQL ก็ได้ทั้งนั้น และรวมถึงการออกแบบด้วย เพราะถ้าย้อนกลับไปดูเรื่อง **Bounded Context** จากหลักของ **Domain Driven Design \(DDD\)** แล้วเราจะพบว่า ของอย่างเดียวกันแต่มันอยู่ต่างเรื่องกัน อาจจะกลายเป็นของคนละโลกเลยก็ได้ ดังนั้นแต่ละ service จะต้องดูละจัดการข้อมูลตามหน้างานของมันเอง

**ยกตัวอย่างให้เห็นภาพ**  
คำว่า **ผู้ใช้** ในมุมของ developer ทีม กับมุมของ marketing ทีม ก็ดูผิวเผินอาจจะคล้ายกัน แต่พอไปคุยรายละเอียดจริงๆเราจะพบว่าจริงๆทั้งสองทีมนี้มองคำว่าผู้ใช้กันคนละโลกเลย \(จริงๆนะ\)

![](../../.gitbook/assets/image%20%28138%29.png)

## 🔥 ต้องทำ Automation ได้

งานที่ทำทุกอย่างมันต้องไว ทั้งการเอาขึ้นเซิฟเวอร์ การเทส ต่างๆ ดังนั้นตัว service แต่ละตัวก็ต้องมีโครงสร้างที่รองรับการทำ **Build pipeline** ได้เช่นพวก **Continuous Integration \(CI\)** และ **Continuous Delivery \(CD\)** และงานก็ต้องมี automated tests ทั้ง code และ UI ครบสมบูรณ์ เพราะสมัยนี้การให้คนไปคอยนั่งเทสหรือที่เราเรียกว่า Monkey test นั้นจะหายไปแล้วโดยเปลี่ยนบทบาทมาเป็น **UX test** แทน

![](../../.gitbook/assets/image%20%28349%29.png)

{% hint style="info" %}
**สรุปสั้นๆแบบไม่มีศัพท์เทคนิคเลย**  
ตัว microservice นั้นจะต้องรองรับให้มีระบบอื่นมาช่วยเอางานขึ้นเซิฟเวอร์ เอางานเราไปตรวจว่ามีข้อผิดพลาดหรือ bug หรือเปล่า และรวมถึงการทดสอบในอีกหลายๆเรื่องด้วยนั่นเอง
{% endhint %}

![](../../.gitbook/assets/image%20%28160%29.png)

## 🔥 รับมือกับการล่มได้

ตัว Microservice ต้องถูกออกแบบให้รองรับสถานะการณ์ที่ **service อื่นนั้นไม่สามารถใช้งานได้ด้วยและรวมถึงตัวมันเองก็พังด้วยเช่นกัน** เพราะเราไม่สามารถการันตีได้ว่า service จะทำงานได้ตลอดเวลานั่นเอง ดังนั้นแต่ละ service จะต้องมีวิธีการรับมือในการรับมือกับสถานะการณ์ที่ติดต่อ service อื่นไม่ได้ เช่นการใช้ค่า default ไปก่อน หรือมีระบบในการตรวจเช็คสถานะของ service ที่เกี่ยวข้องกับมันว่ายังสามารถใช้งานได้อยู่หรือเปล่านั่นเอง ดังนั้นเราจะต้องมีระบบที่คอยดูแต่ละ services ตลอดเวลารวมถึงการทำ log เพื่อหาสิ่งผิดปกติด้วย

## 🔥 ยืนหยุ่นต่อการเปลี่ยนแปลง

ในการทำ Microservice ก็จะมีการปรับเปลี่ยนให้มันดีขึ้นไปเรื่อยๆ ทั้งในการทำงาน การออกแบบทั้งหลาย เพื่อให้มันสามารถรองรับความสามารถใหม่ๆเข้าไปได้เรื่อยๆโดยที่ไม่ทำให้ความเร็วในการพัฒนาลดลง และรวมถึงการโละทิ้ง service ที่เคยใช้ด้วย

## 🎯 บทสรุป

การนำ Microservices Architecture ไปใช้นั้น มันไม่ใช่แค่การออกแบบเพียงอย่างเดียว แต่มันจะต้องมี**วิธีการคิด**ในรูปแบบของมันอีกด้วย อีกทั้งกระบวนการจัดการก็จะไม่เหมือนแบบทั่วไปที่เคยทำ เพราะเราต้องดูแล services หลายๆตัวที่แตกต่างกัน ภาษาไม่เหมือนกัน เก็บข้อมูลคนละแบบกัน บลาๆ ดังนั้นทีมก็ต้องปรับวิธีการคิดในการใช้ architecture นี้ให้เหมาะสมกับมันด้วย
