---
title: "How to get data from Facebook Graph API in an optimised way"
image: "./get-data-facebook-graph-api-sign.png"
category: Tutorial
excerpt: "เนื่องจากช่วงนี้ผมใช้ Facebook Graph API เยอะมาก ๆ แล้วได้อ่าน Document ไปเจออยู่พอตัว แรก ๆ ที่ใช้เวลาผมอยากได้ของสักอย่างนึง ผมต้องเรียก API 2-3 ครั้งกว่าจะได้ข้อมูลที่ต้องการทั้งหมด"
date: "2017-10-15T22:12:03.284Z"
author: arnondora
template: normal
type: post
isFeatured: false
status: published
---

เนื่องจากช่วงนี้ผมใช้ **Facebook Graph API** เยอะมาก ๆ แล้วได้อ่าน Document ไปเจออยู่พอตัว แรก ๆ ที่ใช้เวลาผมอยากได้ของสักอย่างนึง ผมต้องเรียก API 2-3 ครั้งกว่าจะได้ข้อมูลที่ต้องการทั้งหมด นั่นทำให้เราเสียเวลาเยอะมาก ๆ อย่างน้อยก็ 2 RTT (Round-Trip-Time หรือเวลาที่ใช้ในการรับและตอบของ Server) มันทำให้ Application ของเราช้ากว่าที่ควรจะเป็น วันนี้เลยจะมาอธิบายว่า ถ้าเราต้องการข้อมูลจาก Facebook Graph API แบบเจ๋ง ๆ รันรอบเดียวจบเราจะทำได้ยังไง

## ทำความเข้าใจกันก่อน

![](./get-lots-data-facebook-graph-api-overall-graph.png)

ชื่อมันก็บอกว่า **Facebook Graph API** ฉะนั้นการแสดงผลข้อมูลมันจะออกมาในรูปแบบของกราฟ ซึ่งถ้าใครที่เรียนมาเราก็จะรู้ว่า Graph มีอยู่ 2 องค์ประกอบดังนี้ Node

![](./get-lots-data-facebook-graph-api-nodes.png)

Node ถ้านึกภาพคือมันก็เป็นก้อนกลม ๆ ลอยอยู่ ถ้านึกภาพเป็นข้อมูลใน Facebook ก็จะเป็นพวก **Page** หรือ **User** อะไรเทือกนั้น มองลึกลงไปอีกก็จะเป็น **Post กับ Comment ของ Parents Node** Edge

![](./get-lots-data-facebook-graph-api-edges-03-e1508080220841.png)

ในเมื่อเรามี Node แล้วอีกสิ่งที่จะขาดไม่ได้เลยคือ Edge เพราะข้อมูลในแต่ละ Node ล้วนมีความสัมพันธ์ทั้งนั้น ซึ่ง Edge นี่แหละเป็นสิ่งที่เชื่อมแต่ละ Node เอาไว้ เช่นถ้าเราถามว่า Comment ของ Post A คืออะไรบ้าง มันก็คือ เราถามหา Child Node ของ A ซึ่งมันก็ต้องวิ่งเข้าไปดูว่า Node A มีลูกเป็นใครบ้าง แล้วโยนกลับมาให้เรา

## วิธีที่ผมใช้ตอนแรก

ช่วงแรก ๆ ผมก็อ่าน Document ไปพอควรอยู่สุดท้ายมาจบที่ การเรียกหลายครั้งมาก ๆ มันก็ทำให้ Application ของผมมันช้า ช้ามาก ๆ ณ ตอนนั้นสมมุติว่าผมต้องการได้ Post และ Comment มาวิธีที่ผมทำคือ

`GET /{source_id}/posts GET /{post_id}/comments GET /{post_id}/likes`

ผมต้องเรียก Post ครั้งนึงและในแต่ละ Post ผมต้องเรียก Comment ทีละอันอีก นอกจากนั้นถ้าเรายังต้องการยอดไลค์ หรือต้องการ List ของคนที่ Like Post หรือ Comment นั้น ๆ เราก็ยังต้องเรียกอีกรอบนึง สรุปแล้วถ้าเราต้องการ Post ของ Source นั้น ๆ รวมถึง Comment และยอด Like ของ Post และ Comment นั้น ๆ เราต้องเรียกโคตรจะหลายรอบมาก ๆ กว่าจะได้ข้อมูลทั้งหมดที่เราต้องการ นอกจากนั้นเรายังสามารถกำหนด Field ที่ต้องการส่งมาได้ด้วย ทำให้เราสามารถ**ลดขนาด**ของข้อมูลที่รับกลับมา ทำให้เวลาในการรับข้อมูลน้อยลง และลดขนาดของหน่วยความจำที่เราใช้ในการจัดการข้อมูลอีกด้วย โดยการใส่ Argument ลงไปเช่น `GET /{source_id}/posts?fields=id,message` เวลาได้ค่ากลับมา เราก็จะได้แค่ **ID และ Message กลับมาเท่านั้น**ไม่มีอย่างอื่น ก็จะช่วยให้เราจัดการกับข้อมูลได้ง่ายขึ้นเยอะเลย

## รู้จักกับ Field Expansion

นอกจากที่เรายังจะสามารถเลือกขอ Field ที่อยู่ใน Node นั้น ๆ ได้แล้ว เรายังสามารถที่จะขอข้ามยันแต่ละ Edge ได้เลย เช่นจากเหตุการณ์ที่ยกตัวอย่างไม่เมื่อครู่ที่เราต้องการ Post จาก Page หนึ่ง และ Comment ของแต่ละ Post มองในรูปแบบของ Graph Page ที่เราต้องการก็คือ Node นึง ที่เชื่อมไปในแต่ละ Node ที่เป็น Post และแต่ละ Post ก็เชื่อมไปแต่ละ Comment ที่เป็น Node เช่นกัน ปกติถ้าเราต้องการ Post จาก Page เราก็ต้องเรียก Post แล้วเรียก Comment เป็น 2 ครั้ง แต่ถ้าผมบอกว่า **ผมสามารถจัดการทั้งหมดนี้ได้ด้วยการเรียกเพียงรอบเดียวละครับ !** แน่นอนว่าทำได้ (ถ้าไม่ได้จะมาเขียนแบบนี้มั้ย !!) พระเอกของงานนี้คือ **Field Expansion** ที่เป็นฟีเจอร์ที่อยู่ใน Graph API มานานละ ขอยกตัวอย่างก่อนเลยละกัน สมมุติว่า เราต้องการ Post ที่มี ID และ Body และ Comment จากเพจสัก ID นึงเราก็สามารถเรียกได้ดังนี้ `GET /{source_id}/posts?fields=id,message,comments{id,message}` สังเกตว่าผมเติม Argument fields ลงไปโดย 2 ตัวแรกก็ไม่น่าจะแปลกอะไรก็คือเอา id และ message จาก Post มา แต่ตรง **comments{id,message}** นี่สิ ส่วนนี้มันคือ Field Expansion ถ้าเราลองเอาไปรันดู เราจะเห็นว่ามันมี Post ของ Source นั้น ๆ ออกมาจริง ๆ แถม Comment ของ Post แต่ละ Post ออกมาด้วย **ฉะนั้นวิธีการใช้ Field Expansion คือการเติมชื่อ Edge ที่เราต้องการลงไป ในตัวอย่างนี้คือ Comment แล้วตามด้วยปีกกา ตามด้วย Field ที่เราต้องการของตัวลูก และปิดปีกกาให้เรียบร้อยก็เป็นอันเสร็จ** ถ้าเทียบ Field Expansion เป็น SQL มันก็น่าจะเหมือนกับคำสั่ง Join ที่ Join Child Node เข้ามาในผลด้วย

## Multiple IDs Request

ทีนี้ ลองมาดูอีกสถานการณ์กัน ในรอบนี้เราต้องการ Comment ของแต่ละ Post โดยที่เรามี ID ของ Post ทั้งหมดแล้ว ถ้าปกติเราก็อาจจะใช้เป็น `GET /{post_id}/comments` แต่ถ้ามี 112 Post เราก็จะต้องเรียกแบบนี้ทั้งหมด 112 ครั้งกันเลยทีเดียว ถ้ายังเรียกแบบนี้เยอะๆ อยู่ผมอาจจะติดคุกก็ได้ (ถ้าไม่เก็ดก็นึกถึงมาตรา 112 ไว้นะ) เอาเป็น 100 เดียวละกัน ก็ต้องเรียกแบบนี้ 100 ครั้งก็คงไม่สนุกเท่าไหร่ API จึงอนุญาติให้เราเรียกข้อมูลหลาย ๆ Node พร้อมกันได้โดยการใส่ Argument ที่เขียนว่า **ids** เช่นเราต้องการข้อมูลของ Node ID 111, 222, 333 พร้อม ๆ กันในรอบเดียวเราก็จะเขียนเป็น

`GET /?ids=111,222,333`

ซึ่งจะเทียบเท่ากับเราเรียก 3 รอบ

`GET /111 GET /222 GET /333`

 มันก็จะช่วยให้เราประหยัดเวลาในการรอข้อมูลกลับมาได้มาเลย งั้นลองกันต่อ แล้วถ้าเราต้องการ Child Nodes จาก 3 Nodes นี้ละจะทำยังไง ? เช่น 3 Nodes นี้เป็น Post แล้วเราต้องการ Comment เราก็สามารถที่จะทำได้เช่นกัน

 `GET /comments?ids=111,222,333`

 มันจะเทียบเท่ากับ

 `GET /111/comments GET /222/comments GET /333/comments` ม

 ันก็จะช่วยเราได้เยอะ ถ้าเทียบกับ SQL มันก็คงจะคล้าย ๆ กับ WHERE แต่เป็น WHERE ID เท่ากับค่าสักค่าไปเลยมากกว่า ไม่ใช่เงื่อนไขในอารมณ์นั้นซะทีเดียว แต่วิธีนี้ก็มีข้อจำกัดเหมือนกันนั่นคือ สิ่งที่เราต้องการจากแต่ละ Node จะต้องเหมือนกัน เช่น Node แรกเป็น Post แล้วเราต้องการ Comment และ Node ถัดไปเป็น Page จะเอา Post มันก็จะไม่ได้

## Batch Requests

เพื่อให้สามารถที่จะเรียกของต่างกันใน Request เดียวกันได้ **Batch Request จึงเป็นพระเอกขี่ม้าขาวมาช่วยเราในงานนี้** เพียงแค่เราป้อนสิ่งที่เราต้องการลงไปใน Request Body และส่งเป็น POST Method โดยใช้ดังตัวอย่างนี้

`{ "batch": [ { "method":"GET", "relative_url":"141108613290_10155957553153291/comments" }, { "method":"GET", "relative_url":"141108613290_10155957553153291/likes" } ] }`

 ในตัวอย่างนี้ผมได้ขอไป 2 Request คือการขอ Comment และ Like ของ Node นึง จะเห็นว่า ผมสามารถขอ 2 อย่างนี้พร้อม ๆ กันใน Request เดียวได้ โดยที่ไม่ต้องเรียกแยกเป็น 2 Request ถ้า งง มันจะเทียบเท่ากับ 2 Request นี้

 `GET /141108613290_10155957553153291/comments GET /141108613290_10155957553153291/likes`

  นอกจากนั้นเรายังสามารถตั้งชื่อแต่ละ Sub Request ที่เราส่งได้ด้วยโดยการเติมส่วนของ Name เข้าไปใน Sub Request นั้น ๆ เช่น

  `{ "method":"GET", "name":"Mycomment" "relative_url":"10204866996135140?fields=id,name" }`

   และ Sub Request อื่น ๆ ก็จะมาสามารถใช้ผลของ Request ที่เราตั้งชื่อได้โดยการใช้ **ชื่อ Sub Request:$.ชื่อ Field** ก็เรียบร้อยแล้ว

## สรุป

ทั้งหมดนี้ก็เป็นวิธีง่าย ๆ ที่จะทำให้เราประหยัดเวลาในการเรียก **Facebook Graph API** ได้มากขึ้นจากที่เราค่อย ๆ เรียกทีละ Request เราก็สามารถมัดรวมกันแล้วส่งไปทีเดียว เราก็จะเสียเวลาในการรอข้อมูลส่ง Request และรับ Response น้อยลง เท่าที่ลองมันเร็วขึ้นแบบเห็นผลมาก **เพราะมันลด Request ลงไปจาก Exponential กลายเป็นเหลือแค่ n เท่านั้น** ก็เอาไปลองกันได้นะ สวัสดี ~
