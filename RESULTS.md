# UI lab results

Tool part ที่เลือก: Part 3 Robot Framework และ Part 4 Cypress

## Part 0

- Step 0.1, เวอร์ชันของ Chrome: 157.0.8103.79 (Official Build) (64-bit)
- Step 0.3, เวอร์ชันของ ChromeDriver: ChromeDriver 157.0.8103.79 (6dc9bc3bdaea5c35ed6d41fceab2f7a3a2227c4f-refs/branch-heads/8103@{#1574})
- Step 0.4, locator ของปุ่ม Pizza, Please!: `button[name="pizza-please"]` (CSS) เจอ 1 element
- Step 0.4, locator ของ Excluded tools: `//label[normalize-space()='Excluded tools']/following-sibling::select` (XPath) เจอ 1 element ส่วน `select` ก็เจอ 1 เช่นกันเพราะเป็น list เดียวในหน้า ข้อสังเกตคือ label มี `for="countries_multiple"` แต่ select ไม่มี id นี้ label จึงไม่ได้ผูกกับ select จริง
- Step 0.4, locator ของ Must be vegetarian: `#default-checkbox` เจอ 1 element
- Step 0.4, locator ของ Custom Pizza Name: `input#pizza-name` เจอ 1 element (ถ้าใช้ `#pizza-name` อย่างเดียวจะเจอ 2 ตัวหลังจากคำตอบแสดงขึ้นมา)
- Step 0.4, `$$("#floating_filled").length` ได้ 3 และ `$x("//label[normalize-space()='Max Calories per Slice']/preceding-sibling::input")` เจอ 1
- Step 0.5, ชื่อพิซซ่า, tool และ calories จากการรันด้วยมือ: Lab Pizza 20261123-202400, tool Pizza cutter, 500 calories per slice (รันวันที่ 23 พฤศจิกายน 2026 บน Chrome 157)

| Step | Actual result | Pass or fail |
|------|---------------|--------------|
| 1    | heading แสดงข้อความ "Looking to break out of your pizza routine?" | Pass |
| 2    | หลังเปิด Advanced ช่อง Max Calories per Slice, Excluded tools, Must be vegetarian และ Custom Pizza Name แสดงขึ้นมา (ช่อง Max Calories มีค่า 1000 อยู่ก่อนแล้ว) | Pass |
| 3    | ช่องต่าง ๆ แสดงค่า 600, เลือก Knife, ติ๊ก Must be vegetarian และชื่อ Lab Pizza 20261123-202400 | Pass |
| 4    | ผ่านไปครู่หนึ่งคำตอบแสดง Name: Lab Pizza 20261123-202400, Dough: Thick, ingredients 8 อย่าง, Tool: Pizza cutter (ไม่ใช่ Knife), Calories per slice: 500 (≤ 600) | Pass |
| 5    | กด Love it! แล้วมีข้อความ "Please log in first." ขึ้นใต้ปุ่ม | Pass |
| 6    | ที่หน้า /admin ทั้งสองช่องมีคำว่า admin อยู่แล้ว หลังกด Sign in หน้าแสดง "Latest pizza recommendations" | Pass |
| 7    | ในรายการมีบรรทัด "Lab Pizza 20261123-202400 (tool=Pizza cutter, ingredients_number=8)" tool ตรงกับ step 4 โดยอยู่บรรทัดที่ 13 มีพิซซ่าของผู้ใช้คนอื่นอยู่ด้านบน 12 อัน | Pass |

## Part 3: Robot Framework

- robot --version: Robot Framework 7.5.1 (Python 3.11.9 on win32)
- Step 3.2, ข้อความ failure เมื่อใส่ title ผิด: `Title should have been 'Web Form' but was 'Web form'.`
- Step 3.8, run 1 ผลลัพธ์, elapsed time และชื่อพิซซ่า: PASS (1 test, 1 passed, 0 failed), 00:00:11.875, Lab Pizza 20261123-201915 (tool Scissors, 550 calories per slice)
- Step 3.8, run 2 ผลลัพธ์, elapsed time และชื่อพิซซ่า: PASS (1 test, 1 passed, 0 failed), 00:00:11.796, Lab Pizza 20261123-201928 (tool Scissors, 375 calories per slice)

## Part 4: Cypress

- node --version, npm --version และ npx cypress version: v24.14.0, 11.9.0, Cypress package 16.2.1 / binary 16.2.1 (Electron 41.7.0, bundled Node 24.15.0)
- Step 4.3, ข้อความ failure เมื่อใส่ title ผิด: `Timed out retrying after 10000ms` / `+ expected - actual` / `-'Web form'` / `+'Web Form'`
- Step 4.6, tool และ calories ในคำตอบของ POST /api/pizza: run 1 ได้ tool Pizza cutter, 500 calories per slice (หน้าเว็บแสดงค่าเดียวกัน ซึ่ง test ตรวจสอบไว้แล้ว)
- Step 4.7, บรรทัดในรายการ admin ที่แสดงพิซซ่าของเรา: `Lab Pizza 20261123-201552 (tool=Scissors, ingredients_number=7)` (run 2 โดยมีพิซซ่า "The High Capricciosa" ของผู้ใช้อื่นเข้ามาอยู่ด้านบนและมีป้าย (newest))
- Step 4.8, run 1 ผลลัพธ์, duration และชื่อพิซซ่า: All specs passed (2 tests, 2 passing), 00:14 (pizza-scenario 00:11, web-form 00:03), Lab Pizza 20261123-201502
- Step 4.8, run 2 ผลลัพธ์, duration และชื่อพิซซ่า: All specs passed (2 tests, 2 passing), 00:14 (pizza-scenario 00:11, web-form 00:02), Lab Pizza 20261123-201552
- Step 4.9 (optional), browser และผลลัพธ์: ไม่ได้ทำ

## Part B

1. กล่องตัวเลขทั้งสามกล่องของ QuickPizza คือ Max Calories per Slice, Min Number of Toppings และ Max Number of Toppings ใช้ id เดียวกันคือ `floating_filled` ตอนเช็คใน Console คำสั่ง `$$("#floating_filled").length` ได้ 3 จึงใช้ id แยกกล่องไม่ได้ แต่ข้อความของ label ไม่ซ้ำกัน ทั้งสอง test จึงเริ่มหาจาก label โดย Robot ใช้ `xpath://label[contains(.,'Max Calories')]/../input` และ Cypress ใช้ `cy.contains('label', 'Max Calories per Slice').siblings('input')` สิ่งที่ควรขอให้ developer แก้คือให้แต่ละกล่องมี id ไม่ซ้ำ เช่น `id="max-calories"` (และ `name="maxCaloriesPerSlice"` ซึ่งตรงกับชื่อ field ใน request body ของ POST /api/pizza อยู่แล้ว) แบบนี้ test จะใช้ `id:max-calories` หรือ `#max-calories` ได้ ซึ่งสั้นกว่า เร็วกว่า และไม่พังเมื่อข้อความ label หรือ layout รอบ ๆ เปลี่ยน อีกทั้งยังแก้ข้อผิดพลาดของ HTML ที่ id ต้องไม่ซ้ำ และทำให้ `<label for>` ผูกกับกล่องได้จริงสำหรับ screen reader

2. Step 7 เป็น consistency oracle คือไม่รู้ล่วงหน้าว่า tool ที่ถูกต้องคืออะไร แต่เทียบผลลัพธ์สองจุดของระบบเดียวกันที่ต้องตรงกัน ได้แก่คำแนะนำในหน้าแรกกับบรรทัดในรายการของ admin จากที่รันจริง tool ออกมาแบบสุ่ม เช่น Pizza cutter ใน Cypress run 1 และ Scissors ใน Robot run 1 และ run 2 จึงกำหนด expected value ตายตัวไม่ได้ ต้องใช้การเทียบเท่านั้น check นี้จะจับ fault ที่ server บันทึกพิซซ่าคนละอันกับที่ส่งกลับมา เช่น รายการ admin เก็บ tool ของ request อื่น หรือบันทึกพิซซ่าด้วย tool ค่า default นอกจากนี้ยังจับ fault ที่ชื่อ custom ไปผูกกับพิซซ่าผิดอันได้ด้วย เพราะ test หาบรรทัดจากชื่อแล้วตรวจ tool ในบรรทัดเดียวกันนั้น

3. หน้าเว็บแสดงแค่ชื่อ, dough, ingredients, tool และ calories แต่ไม่บอกว่าพิซซ่าเป็นมังสวิรัติหรือไม่ test ที่ดูแค่ UI จึงตรวจเรื่องนี้ตรง ๆ ไม่ได้ เมื่อเปิดแท็บ Network ใน developer tools จะเห็นว่าคำตอบของ POST /api/pizza มี `"vegetarian": true` ของทั้งพิซซ่า และ ingredient แต่ละตัวก็มี flag ของตัวเอง เช่น `{"name":"Feta cheese","caloriesPerSlice":100,"vegetarian":true}` ใน Cypress จึงเพิ่ม `expect(response.body.vegetarian).to.be.true` ในบล็อก `cy.get('@pizza')` ได้ และตรวจด้วยว่าทุกรายการใน `response.body.pizza.ingredients` มี `vegetarian` เป็น true และชื่อ ingredient บนหน้าเว็บตรงกับในคำตอบ วิธีที่รัดกุมกว่าคือไม่เชื่อ flag ของ server อย่างเดียว แต่เทียบ ingredient ที่แสดงกับรายการวัตถุดิบที่เป็นเนื้อสัตว์และอาหารทะเลซึ่งได้มาจาก requirements โดยอิสระ แล้วให้ fail ถ้าพบวัตถุดิบเหล่านั้น สำหรับ Robot ก็ต้องใช้แหล่งข้อมูลที่สองเช่นกัน คือคำตอบของ API ผ่าน library อย่าง RequestsLibrary หรือรายการวัตถุดิบที่ไม่ใช่มังสวิรัติเก็บไว้ใน resource file

4. Robot Framework จะรอเฉพาะจุดที่เราสั่ง ด้วย keyword อย่าง `Wait Until Element Is Visible    css:h1`, `Wait Until Element Contains    id:recommendations    Name:` และ `Wait Until The Page Is Ready` ก่อน login หน้า admin โดยตั้ง `timeout=10s` ส่วน Cypress รอเองอัตโนมัติ เพราะทุก `cy.get` และ `should` จะลองซ้ำได้นานสุดตาม `defaultCommandTimeout` คือ 10 วินาที ต้องสั่งรอเองแค่ network ด้วย `cy.wait('@pizza')` และรอ `#svelte-announcer` ก่อน login เวลาที่ใช้รัน QP-01 ใกล้เคียงกัน คือ Robot 11.9 และ 11.8 วินาที ส่วน Cypress 00:11 ทั้งสองรอบ การเขียน QP-01 ด้วย Cypress เร็วกว่าเล็กน้อยเพราะไม่ต้องติดตั้ง driver และไม่ต้องคิดเรื่องการรอ ในขณะที่ Robot ต้องใช้ ChromeDriver 157 ให้ตรงกับ Chrome 157 และต้องตั้งตัวแปร CHROMEDRIVER ด้านการอ่านผล log.html ของ Robot ละเอียดที่สุด เห็นทุก keyword, argument, ค่าอย่าง `${tool} = Scissors` และ `${calories} = 550` และ screenshot ตรง step ที่ถ่าย ส่วน Cypress ให้ตารางสั้น ๆ ใน terminal กับวิดีโอ mp4 ที่แสดง Command Log คู่กับหน้าเว็บ ซึ่งเอาไปให้คนอื่นดูง่ายกว่าแต่ค้นหาข้อมูลยากกว่า และข้อความ failure ของ Cypress ก็ชัดเจน คือแสดง `- 'Web form'` และ `+ 'Web Form'` หลังจาก time out ที่ 10000 ms

5. เลือก Cypress สำหรับ automated UI test ของ Project 2 เหตุผลแรกคือ Cypress รอ element ให้อัตโนมัติ test จึงไม่ค่อย fail เพราะหน้าร้านค้าหรือโรงแรมวาดเนื้อหาช้าไปเล็กน้อย และไม่ต้องใช้ ChromeDriver ที่ต้องอัปเดตทุกครั้งที่ Chrome อัปเดต  เหตุผลที่สองคือ `cy.intercept` ทำให้ตรวจ request และคำตอบเบื้องหลังหน้าเว็บได้ (status 200, `maxCaloriesPerSlice` เท่ากับ 600 และ tool กับ calories ตรงกับที่หน้าเว็บแสดง) ซึ่งจับ fault ที่การตรวจแค่หน้าเว็บมองไม่เห็น และวิดีโออัตโนมัติก็ใช้เป็นหลักฐานการรันเต็มได้ทันที แต่ถ้าในกลุ่มมีคนที่ไม่ได้เขียน JavaScript และต้องอ่าน test ด้วย Robot Framework จะเหมาะกว่า เพราะ keyword อ่านเหมือน test case ที่เขียนไว้

6. (Part 3) แก้ 1 บรรทัด คือตัวแปร `${MAX CALORIES}    xpath://label[contains(.,'Max Calories')]/../input` ในส่วน Variables ของ `resources/quickpizza.resource` เพราะ keyword `Turn On Advanced` และ `Fill In The Pizza Request` ใช้ตัวแปรนี้ ส่วน `pizza_scenario.robot` แค่เรียก keyword เช่น `Fill In The Pizza Request    600    Knife    ${name}` และไม่มี locator อยู่ในไฟล์เลย ไฟล์ test จึงไม่ต้องแก้ ยังอ่านเหมือนขั้นตอนของ QP-01 เหมือนเดิม และ test อื่นทุกตัวที่ import resource file นี้ก็ได้รับการแก้ไปพร้อมกันจากการแก้บรรทัดเดียว

7. (Part 4) Cypress ล้าง cookie, local storage และ session storage ก่อนทุก test ทำให้ `it` แต่ละอันเริ่มเหมือนเปิด browser ใหม่ QuickPizza รันอยู่บนหลาย server และใช้ cookie เพื่อให้ browser หนึ่งอยู่กับ server เดิม โดยรายการ admin แสดงเฉพาะพิซซ่าของ server นั้น ถ้าแยก step 6 และ 7 เป็น test ที่สอง test นั้นจะเริ่มโดยไม่มี cookie อาจถูกส่งไป server อื่น แล้วหา `Lab Pizza 20261123-201552` ในรายการ admin ไม่เจอทั้งที่ step 4 สร้างไว้แล้ว ทำให้ test fail แบบสุ่ม นอกจากนี้ test ที่สองยังเสียค่าจาก test แรกไปด้วย เพราะ `pizzaName` เป็นตัวแปร local ของ test แรก และ alias `@tool` ถูก reset ระหว่าง test ทำให้ step 7 ไม่รู้ว่าต้องหาพิซซ่าชื่ออะไรและ tool อะไร
