---
title: "C Language 101 - Function (EP.7)"
image: "./clangsign7.png"
category: Tutorial
excerpt: "จากตอนที่แล้ว เราก็ได้เรียนเรื่อง การรับข้อมูลเข้าหรือ Input กันไปแล้ว วันนี้เรามาเปลี่ยนเรื่องกันบ้างดีกว่า"
date: 2015-06-12T14:56:47.000
author: arnondora
template: full-width
type: post
isFeatured: false
status: published
---

จากตอนที่แล้ว เราก็ได้เรียนเรื่อง การรับข้อมูลเข้าหรือ Input กันไปแล้ว วันนี้เรามาเปลี่ยนเรื่องกันบ้างดีกว่า ก่อนอื่นอยากถามว่า

## คุณเคยประสบปัญหาแบบนี้มั้ย ?
เราจะต้องเขียนโปรแกรมที่มีโค๊ตซ้ำ ๆ กัน แต่ Loop ก็ช่วยไม่ได้หมด เพราะเราต้องเรียกมันขึ้นมาเป็นระยะ ๆ เจ้า Function จะเข้ามาช่วยเราแก้ปัญหานี้เอง
Function ก็คือกล่องของชุดคำสั่งที่เราเขียนขึ้นมาเพื่อให้ทำงาน หรือ เพื่อให้ได้ Output ตามที่เราต้องการ อย่าง scanf(); ที่เราใช้ไปเมื่อตอนที่แล้ว นั่นก็คือ function นึงเหมือนกัน แต่เป็น function ที่ตัวภาษา C สร้างไว้ให้แล้ว แต่ในตอนนี้ เราจะมาสร้าง function ใช้เองกันบ้าง วิธีสร้างคือ

    return_type function_name (parameter_list)
    {
       //do sth
    }


เราลองมาดูกันทีล่ะส่วนกันเลยดีกว่า
ก่อนอื่น ก็ต้อง Return Type มันจะเป็นตัวกำหนดว่า เวลา function นี้ทำงานจบ มันควรจะค่ากลับไปเป็นแบบไหน เช่น Integer หรือ Double Float อะไรแบบนี้ เป็นต้น
ถัดไปคือ Function Name อันนี้ก็ตามชื่อเลย มันคือชื่อของ Function ที่เราตั้งชื่อขึ้นมาเอง ส่วนใหญ่เราก็จะตั้งชื่อให้สัมพันธ์กับสิ่งที่ function นี้มันทำ (ไม่เอานะตั้งชื่อแปลก ๆ อะ)
และสุดท้าย Parameter List คือค่าที่เราจะต้องส่งมาให้ตัว Function เพื่อให้ Function นำไปใช้งานต่อใน Function ง่าย ๆ เราส่งผ่านค่าไปหาตัว Function แล้วตัว Function ที่ได้รับข้อมูลมาก็สามารถนำไปใช้ได้นั่นเอง
อาจจะยังมองไม่เห็นภาพ ลองมาดูตัวอย่างกันเลยดีกว่า ผมจะสร้าง Function รับค่า int เข้ามา 2 ค่าแล้วให้มันส่งค่ากลับไปเป็นผลบวกของตัวเลข 2 จำนวนล่ะกัน

    int sumNumber (int a, int b)
    {
       return a+b;
    }

จากที่เราเห็นบนตัวอย่างด้านบน ผมกำหนด Return Type เป็น Int เพราะว่า เราแค่ต้องการผลบวกง่าย ๆ ไม่มีอะไร และ Parameter ก็อย่างที่ผมบอกว่า เราต้องการให้เอาตัวเลขเข้าไป 2 ตัว สร้างง่าย ๆ เลยนั่นคือ a กับ b และข้างใน function เราก็บอกว่า ให้มันส่งค่าของ a+b กลับไปหาคนเรียก ทีนี้เราลองมาดูว่า เราจะเรียกใช้ Function ที่เราสร้างได้ยังไง

    #include <stdio.h>

    int sumNumber (int a, int b)
    {
       return a+b;
    }

    int main ()
    {
      int sum = sumNumber(2,1);
      return 0;
    }

วิธีเรียกก็ง่ายมาก ๆ เลย เราก็แค่เขียนชื่อ Function ที่เราต้องการเรียกแล้วก็เติม Parameter ให้ครบเท่านั้นเอง
**คำเตือน !! : คนเรียกจะต้องอยู่ข้างล่าง ตัวที่ถูกเรียก เสมอ ไม่งั้นจะ Compile Error (แต่สามารถใช้ Function Prototype แทนได้)**

## ปัญหาเริ่มเกิด เมื่อเราเรื่องมาก Function Prototype จึงเข้ามา
จากเมื่อกี้ที่ผมเขียนคำเตือนว่า ตัวเรียกจะต้องอยู่ด้านล่างของคนที่ถูกเรียกเสมอ ไม่งั้น Compile Error ทีนี้ ถ้าถามว่าแล้วถ้าเราอยากจะแหกกฏนี้ล่ะ เราจะทำยังไง ?
นี่ล่ะครับเจ้า Function Prototype จะเข้ามาช่วยเราในเรื่องนี้เอง
แต่ก่อนอื่น เราจะต้องมาเข้าใจถึงสาเหตุที่ Function ที่ถูกเรียกจะต้องอยู่ด้านบนกันก่อน มันเป็นเพราะว่าเวลา Compiler มัน Compile มันจะวิ่งจากบนลงล่าง แต่ถ้า Function ที่เราเรียกอยู่ข้างล่าง แปลว่า ณ ตอนที่เราเรียก ตัว Compiler มันจะยังไม่รู้จัก Function ข้างล่าง เลยทำให้เราต้องเขียน Function ที่เป็นคนถูกเรียกไว้ด้านล่างของตัวที่เรียกเสมอ
ถ้ามอง Function Prototype มันทำหน้าที่ตามชื่อเลย มันมาเป็น Function ตัวปลอมบอก Compiler ไว้ก่อนว่า สัญญานะว่า โปรแกรมนี้มี Function นี้อยู่จริง ๆ นะ แต่มันแค่อยู่ข้างล่าง ทำให้ Compiler รู้และปล่อยไป ไม่ให้เกิด Error ขึ้น ทีน้ีต่อมา การประกาศ Function Prototype นั่นก็ไม่มีอะไรเลย เพียงแค่เราก๊อปหัว Function ที่เราต้องการสร้างมาแล้วเติม Semi-Colon เป็นอันจบ เช่นผมจะลองสร้าง Function Prototype ของ sumNumber() เมื่อกี้ล่ะกัน

    int sumNumber (int a, int b);

ทีนี้ถ้าเราประกาศบรรทัดนี้ไว้ข้างบน พอ Main ที่อยู่ข้างล่างของ Function Prototype นี้ก็จะรู้แล้วว่าในโปรแกรมนี้มี sumNumber() อยู่จริง ๆ นะ ให้ Main เรียกได้ ไม่เกิด Error จบและ หน้าที่ของ Function Prototype มีแค่นี้ล่ะ เรามาลองเขียนโปรแกรมเมื่อกี้อีกที แต่รอบนี้เราจะใส่ Function Prototype เข้าไปด้วย

    #include <stdio.h>

    //function prototype will be here
    int sumNumber (int a, int b);
    int main ()
    {
      int sum = sumNumber(2,1);
      return 0;
    }



    int sumNumber (int a, int b)
    {
       return a+b;
    }



แค่นี้เราก็สามารถเอา Function ที่ถูกเรียกไว้หลัง Function ที่เรียกได้แล้ว ง่ายมาก ๆ เลย แค่นี้ก็จบเรื่องนี้แล้ว สำหรับคนที่กำลังหัดแล้วกำลังอ่านบทความนี้อยู่นะครับ บางทีผมอาจจะอธิบายไม่ละเอียดหรือไม่เข้าใจบ้าง ก็ลองพยายามอ่านดูล่ะกันนะครับ หรือถ้าไม่ได้จริง ๆ ก็คอมเม้นด้านล่างเลย สำหรับวันนี้ไปก่อนครับ พบกันใหม่ตอนหน้า สวัสดีครับ
