---
title: "[Dev Tip] TDD คืออะไร ?"
image: "./whatistddsign.png"
category: Tutorial
excerpt: "เมื่อก่อน จนถึงตอนนี้ Dev อย่างเรา ๆ เวลาทำงานส่วนใหญ่ เราก็จะลงมือ Design แล้ว มาเขียน แล้วค่อย Test แต่งานมันไปงอกตรง"
date: 2015-06-28T23:13:39.000
author: arnondora
templete: full-width
type: post
isFeatured: false
status: published
---

เมื่อก่อน จนถึงตอนนี้ Dev อย่างเรา ๆ เวลาทำงานส่วนใหญ่ เราก็จะลงมือ Design แล้ว มาเขียน แล้วค่อย Test แต่งานมันไปงอกตรง Test นี่แหละ ยิ่ง Test ยิ่งแก้ Bug มันก็ยิ่งงอกออกมาเรื่อย ๆ จนพูดกันว่า

## "การ Debug คือการเอา Bug เข้าไปใส่เพิ่มนั่นเอง"
จากเหตุการณ์นี้ มันเลยมีการ Development แบบ TDD หรือ Test Driven Development เลยงอกออกมาเพื่อแก้ปัญหานี้

## Test Driven Development (TDD) คืออะไร ?
ง่าย ๆ เลย มันคือการเอา Workflow ปกติที่เราทำงานมากลับหัว จากเมื่อก่อน เราจะต้อง

## Design -\> Code -\> Test
แต่อันนี้ เราจะต้องสร้าง Test ขึ้นมาก่อนจาก Requirement ที่เราได้รับมา จับมันแยกย่อยออกมาเป็นหลาย ๆ Test ให้เรามองว่า Test เหมือนกับกล่องอะไรสักอย่างที่เราใส่ Input แบบนี้ เราจะต้องได้ Output แบบนั้น มองให้มันเรียบง่ายที่สุด
**ข้อสำคัญ อย่าคิดแทนลูกค้าเด็ดขาด เพราะเราไม่รู้เลยว่าเขาจะเห็นดีกับสิ่งที่เราทำรึเปล่า ? และจำไว้ว่า Test ที่ดีนั้นจะต้อง เล็ก และมีจุดประสงค์ในการ Test ที่ชัดเจน**
หลังจากที่เราเขียน Test ขึ้นมาแล้ว เราก็ลงมือเขียน Code เพื่อให้รัน Test ที่เราสร้างไว้ผ่าน ถ้าไม่ผ่านก็กลับไปเขียนใหม่ซะ !
หลังจากที่เราเขียน Code และรัน Test ผ่านแล้ว ขั้นตอนสุดท้ายนั่นคือการ จัดการกับ Code ของเราให้ สั้นลง กระชับมากขึ้น ทำงานเร็วขึ้น อ่านง่ายมากขึ้น และลดความซับซ้อนของ Code เราจะเรียกกระบวนการทั้งหมดนี้กว่า การ Code refactoring
จากนั้น เราก็เอา Code ที่เราได้จากการ Refactor มารันตัว Test เพื่อยืนยันว่า Code ที่เราทำ Code refactoring ยังถูกต้องตาม Requirement ที่เราต้องการอยู่มั้ย ?  ถ้าผ่านอยู่ก็เป็นอันเรียบร้อยสำหรับโปรแกรมของเรา เย้ ๆ
เพราะฉะนั้น Process ที่เราทำใน TDD คือ

## Test  -\> Code -\> Refactor
ฉะนั้นการพัฒนาโปรแกรมแบบ TDD ทำเหมือนกับเราทำย้อนกลับ Process แบบปกตินั่นเอง แต่จริง ๆ แล้วการสลับตำแหน่ง Process เพียงเท่านี้ ช่วยให้เราไม่หลงประเด็นของสิ่งที่เราต้องการจากโปรแกรมเลย และเวลาที่ใช้ในการ Test  ก็น้อยกว่าปกติด้วย เพราะว่าในระหว่างขั้นตอนการเขียน เราก็ทำการ Test อยู่ตลอด และทำให้เราอุ่นใจได้อีกว่า Code ที่เราเขียนยังถูกต้องตามที่เรากำหนดไว้อยู่
นอกจากที่ทำให้เราลดเวลาในการทำงานและ ความผิดพลาดที่อาจจะเกิดขึ้น ได้แล้ว ยังช่วยทำให้ Requirement ของเราไม่หายไปไหน เราก่อนที่เราจะเขียนตัวโปรแกรม เราจับมันแยกย่อยออกมาเป็นส่วน ๆ ไว้ก่อนแล้ว ทำให้เราไม่ลืมมันง่าย ๆ หรอก