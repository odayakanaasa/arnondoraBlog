---
title: "[Dev Tip] Package Control + แนะนำ Package เจ๋งๆ ใน Sublime Text!!"
image: "./devtip_package_control_sign.png"
category: Tutorial
excerpt: "Sublime Text ก็เป็น Editor ตัวหนึ่งที่หลายๆ คนเลือกใช้กันเพราะว่า มันค่อนข้างที่จะทำอะไรได้หลายอย่าง และก็ใช้ง่ายด้วย ตอนแรกผมก็เฉยๆ นะแต่พอมาลองเล่นดูจริงๆ มันทำอะไรได้เยอะมากๆ"
date: 2015-08-12T23:56:55.000
author: arnondora
template: full-width
type: post
isFeatured: false
status: published
---

Sublime Text ก็เป็น Editor ตัวหนึ่งที่หลายๆ คนเลือกใช้กันเพราะว่า มันค่อนข้างที่จะทำอะไรได้หลายอย่าง และก็ใช้ง่ายด้วย ตอนแรกผมก็เฉยๆ นะแต่พอมาลองเล่นดูจริงๆ มันทำอะไรได้เยอะมากๆ
เมื่อก่อน ก่อนที่ผมจะมาใช้ Sublime ส่วนใหญ่จะใช้ Vim เป็น Editor ตัวหลักๆ เพราะมันสามารถปรับอะไรได้เยอะมากๆ และอีกอย่างมันก็มี Plugin ให้เราเลือกเล่นเยอะมากๆ ตอนนั้นเลยติดใจมาก และวันนึงก็มาเจอเจ้า Sublime Text นี่แหละ มันทำได้คล้ายๆ Vim เลยแล้วมันเป็น GUI ด้วยเลยมาลองเล่นดู ปรากฏว่า มันส์มาก ถึงจะมันส์ไม่เท่า Vim แต่ก็ทำงานได้เร็วขึ้นเยอะเลย
แต่โดยปกติแล้ว ถ้าเราติดตั้ง Sublime Text มาเพียวๆ เลยการติดตั้ง Plugin จะค่อนข้างยากสักหน่อย เลยมีคนทำ Package Control มาให้เราใช้

## การติดตั้ง Package Control
ก่อนอื่นให้เรากดเปิดหน้า Console ขึ้นมาก่อน (View \> Show Console) ในที่นี้ผมจะใช้ Sublime Text 3 ในการติดตั้ง ให้เรา Copy คำสั่งด้านล่างนี้ลงไปแปะใน Console เราได้เลย

    import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

จากนั้นกด Enter เราก็จะได้ Package Control เป็นอันเรียบร้อย จากนั้นก็ให้ปิดโปรแกรมแล้วเปิดใหม่จะดีมาก

## มาติดตั้ง Package กัน
วิธีติดตั้งก็ไม่ยากให้เรา**กด Super Key** ถ้าไม่ได้ไปปรับอะไรก็จะเป็น Command + Shift + p หรือถ้าเป็นฝั่ง Windows ก็จะเป็น Ctrl + Shift + p แทน แล้วให้เราพิมพ์คำว่า Install Package แล้วกด Enter มันจะเข้าไปหา Package ที่เราติดตั้งได้ทั้งหมด แล้ว เราก็สามารถพิมพ์ชื่อ Package เพื่อค้นหาได้เลย เมื่อหา Package ที่เราต้องการได้แล้วก็กด Enter ก็จะเป็นการติดตั้ง Package ที่เราได้เลือกไว้ ก็เป็นอันเสร็จสิ้น!!!
Package ของ Sublime มีเยอะมากๆ ตั้งแต่เครื่องมือในการ Compile, Compression Code ยัน Snippet เลยทีเดียวซึ่งก็มีให้เราเลือกใช้เยอะมากๆ เลยจริงๆ วันนี้ผมจะยกอันที่ผมกำลังใช้อยู่มาให้อ่านกันล่ะกัน

* **Emmet -** ตัวนี้ขาดไม่ได้เลยจริงๆ ตัวนี้ผมเคย [Review][0] ไปแล้วรอบนี้ มันทำให้เราไม่ต้องมานั่งไล่เขียนทีล่ะด้วย อยากได้ 3 ชุด ก็พิมพ์ \*3 ได้เลยทีเดียว ฟินมาก แต่ถ้าไม่เคยอ่าน Document นี่ก็ งง เหมือนกันอะไรว้าา อารมณ์ประมาณนี้เลยทีเดียว
* **Bracket Highlighter - **อันนี้เอาไว้ใช้เวลาเราเขียนโปรแกรมที่มี Tag เยอะๆ ซับซ้อน งงๆ เจ้านี้มันจะบอกเราว่า Tag อันนี้ เปิด ปิดตรงไหน เจ๋งมากๆ เลย
* **Sublime ColorPicker - **อันนี้เหมาะกับคนที่เขียนพวกโค๊ตสี เมื่อก่อนเราต้องมานั่งหาโค๊ตสีมากรอกลงในโค๊ตเรา แต่จะดีแค่ไหนที่เราสามารถเลือกสี แล้วให้มันมาแปลงเป็น Hex Color ให้เราในตัวได้เลย เจ้านี่มันทำได้ง่ายมาก ทำให้เราเราเสร็จไวขึ้นเยอะเลย
* **Twitter Bootstrap 3 Snippet - **อันนี้น่าจะเหมาะกับคนที่ใช้ Bootstrap โดยเฉพาะเลย เพราะมันก็ตามชื่อเลยมันเป็น Snippet ของ Bootstrap ทั้งหมดเลย เท่าที่ใช้มาก็แอบ งง นิดหน่อย เวลาใช้ร่วมกับ Emmet นี่มึนเลยทีเดียว ชินกับ Emmet มากกว่า
* **YUI Compressor -** นี่เลยตัวจี๊ดที่ผมใช้เลยมันจะช่วยให้เราสามารถ Compress ไฟล์ js กับ css ของเราให้เล็กลงได้เยอะเลย หรือที่เราเรียกมันว่า minify นี่เอง ทีเด็ดคือ มันง่ายมาก เหมือนกับเราสั่ง Compile แค่กด Command + B หรือ Ctrl + B เอง
* **TrailingSpaces - **อันนี้มันจะช่วย Highlight พวก Whitespace เปล่าๆ ที่มันไม่ได้มีประโยชน์อะไรเลย และเราสามารถกดครั้งเดียวเพื่อลบมันออกไปเลยได้ด้วย สะดวกดีเหมือนกัน กับงานที่มีโค๊ตเยอะมากๆ
* **DocBlockr -** ช่วยให้เราจัดการกับ Comment ได้ง่ายขึ้น แนะนำให้ใช้เลย ทำให้เราสร้าง Mini Document ใน Code เราได้เร็วขึ้นเยอะเลย
* **Javatar -** อารมณ์เหมือน Eclipse ที่เราใช้เขียน Java เลยแต่แค่ย้ายจาก GUI ที่ต้องใช้ Mouse คลิกๆ ไปเป็นเล่นกับ Keyboard ซึ่งแน่นอนว่าผมทำงานกับ Java เป็นส่วนใหญ่มากๆ ทำให้ได้ใช้ Package นี้เยอะสุดเลย ชอบมากๆ เพราะไม่ค่อยถูกกับ Eclipse กับ Netbean สักเท่าไหร่ ไว้ว่างๆ เดี๋ยวจะมา Review ให้อ่านกัน
นี่คือทั้งหมดที่ผมใช้รวมๆ กันและ มันอาจจะดูเยอะ แต่พอใช้เข้าจริงๆ มันทำให้เราทำงานได้เร็วขึ้นมากเลยล่ะ เอาจริงๆ ต่างจาก Vim นิดเดียวเองที่ไม่มี arpeggio กระโดดไปมาใน Code ทำให้ต้องเอื้อมมือไปจับเมาส์อยู่บ่อยๆ ทำให้หงุดงิดมาก อยากให้ arpeggio มาลง Sublime มาก ส่วนที่เหลือก็จะเป็น Theme อันนี้ก็ตามที่เราชอบเลย ส่วนตัวตอนนี้ผมใช้ Seti\_UI อยู่ เพราะมันออกโทนสีฟ้าที่ผมชอบ แล้วมันดูสบายตาดีด้วย
ก็ถ้าใครมี Package เด็ดๆ มาแนะนำก็ Comment ไว้ข้างล่างได้เลยนะครับ แล้วถ้าอยากให้ Review Package ไหนก็บอกได้เลย เดี๋ยวจัดให้ (ถ้ามีเวลานะ จะเปิดเทอมแล้ว เสียจุย....)

[0]: http://www.arnondora.in.th/reviewemmetplugin/
