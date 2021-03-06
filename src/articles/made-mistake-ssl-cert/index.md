---
title: "งานเกิด ! เมื่อขอ Certificate จาก Let's Encrypt แล้วพลาด !"
image:
category: My Life
excerpt: "เมื่อไม่กี่วันที่ผ่านมา ระหว่างที่ผมเข้าเน็ต เล่นเว็บอะไรไปเรื่อย ๆ ก็ไปเจอว่า Let's Encrypt เปิดในบริการในช่วง Public Beta แล้ว"
date: 2015-12-05T22:41:12.000
author: arnondora
template: full-width
type: post
isFeatured: false
status: published
---

เมื่อไม่กี่วันที่ผ่านมา ระหว่างที่ผมเข้าเน็ต เล่นเว็บอะไรไปเรื่อย ๆ ก็ไปเจอว่า "Let's Encrypt เปิดในบริการในช่วง Public Beta แล้ว !!"**ก็ดีใจหน้าตั้งสิครับ !** และหยุดอ่านหนังสือ และทำการบ้านทันที (นี่จะสอบอยู่วันอังคารแล้ว !!) เพราะว่ารอมานานมากแล้วตั้งแต่ Close Beta ที่สมัครไม่ทัน รอบนี้เลยเร็วมาก รีบทำซะ !

## Let's Encrypt คืออะไร ?
เล่าสั้น ๆ ล่ะกัน เพราะว่า เดี๋ยวพอทำเสร็จแล้วจะมาเขียนให้อ่านกันอีกรอบนึง Let's Encrypt เป็นโครงการตัวนึง ที่ต้องการให้เว็บหลาย ๆ เว็บที่กำลังเปิดให้ใช้อยู่ทุกวันนี้ เริ่มที่จะใช้กระบวนการเข้ารหัสทั้งหมด เพื่อความปลอดภัย แต่เมื่อก่อนนั้นการขอใบรับรองพวกนี้ จะต้องมีค่าใช้จ่าย แต่ Let's Encrypt นั้นไม่มีค่าใช้จ่ายใด ๆ และมีการเซ็นใบรับรองแบบอัตโนมัติด้วย เลยทำให้เรื่องพวกนี้เป็นเรื่องที่ง่ายขึ้นมาก ๆ เลย ซึ่งอย่างที่บอกไปว่า ตอนนี้โครงการ Let's Encrypt ได้เปิดให้บริการในช่วง Public Beta แล้ว (นั่นคือไม่จำเป็นต้องใช้ Invite เหมือนตอนช่วง Close Beta) ทำให้ใครก็ได้สามารถเข้าไปขอใบรับรองได้เลย
ขั้นตอนมันง่ายมากจริง ๆ เพียงแค่เราไป Clone Git มาและทำการติดตั้ง เพียงแค่นี้เราก็จะได้ใบรับรองที่ไม่มีค่าใช้จ่ายใด ๆ ทั้งสิ้น แต่ในบทความนี้จะมาเล่าถึงปัญหาที่เกิดขึ้นในตอนนี้
ถ้าใครได้เข้าเว็บนี้มาตั้งแต่วันที่ 4 ธันวาคม ในช่วงเย็นถึงตอนนี้ (วันที่ 5 ธันวาคม) จะสังเกตได้ว่าที่ช่อง Address Bar มีคำว่า https ขึ้นมา แต่เป็นรูปกากบาท ปัญหาตัวนี้หลังจากที่ได้เข้าไปถามใน Twitter ก็มีชายขี่ม้าข้าวมาช่วย Support ให้ปรากฏว่า ตอนที่ผมขอใบรับรองนั้น ผมไปขอใบรับรองให้กับ arnondora.in.th ไม่ใช่ www.arnondora.in.th ที่เราเข้ากัน ทำให้ตัวระบบ ไม่สามารถเซ็นใบรับรองให้ได้ เลยเกิดปัญหาขึ้น

![made-ssl-mistake-1](./made-ssl-mistake-1.png)

## การแก้ไข
จากการไปสอบถาม ชายอังกฤษนิรนามที่ตอบกลับมาอย่างรวดเร็ว สรุปสุดท้ายแล้ว ก็ต้องรอต่อไปจนถึงวันที่ 11 ธันวาคม หรือนับไปอีก 7 วันหลังจากที่เราขอใบรับรอง (เพราะว่า ในตัวระบบมันมีการจำกัดการขอใบรับรองอยู่ ทำให้ไม่สามารถขอใหม่ได้เลย) เพื่อทำการขอใบรับรองอันใหม่มา (หวังว่าจะไม่พลาดเหมือนครั้งนี้อีกแล้วนะ)
เพราะฉะนั้นสุดท้ายแล้ว ตอนนี้ก็ทำได้เพียง **รอ **แล้วค่อยขอใบรับรองใหม่อีกครั้ง ดังนั้นจึงขอย้ำอีกครั้งว่า ถ้าใครเข้าเว็บตอนนี้แล้วมีปัญหาเรื่องของความปลอดภัยเกิดขึ้น สามารถ Ignore มันได้เลยเพราะว่า เป็นแค่เรื่องของใบรับรองมันผิดพลาดเฉย ๆ
