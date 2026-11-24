# ui-lab

Lab การทดสอบ UI แบบอัตโนมัติ (Automated UI Testing) วิชา ITDS362 Software Quality Assurance and Testing

Tool part ที่เลือก: **Part 3 Robot Framework** และ **Part 4 Cypress**

ทั้งสอง part ทดสอบ web form ของ Selenium และทำ test case **QP-01 A custom pizza reaches the admin list**
บน QuickPizza (https://quickpizza.grafana.com) ให้เป็นแบบอัตโนมัติ
ผลการรันและคำตอบ Reflection อยู่ใน [RESULTS.md](RESULTS.md)

## robot/ (Part 3, Robot Framework)

test ของ Robot Framework ที่ใช้ SeleniumLibrary โดย `first.robot` และ `web_form.robot` ทดสอบ web form,
`pizza_scenario.robot` ทำ QP-01 แบบอัตโนมัติ และ `resources/quickpizza.resource` เก็บ locator กับ keyword
ของหน้า QuickPizza ไว้ที่เดียว ส่วน `results/run1` และ `results/run2` เก็บ log, report และ screenshot
ของการรันเต็ม 2 รอบไว้เป็นหลักฐาน

ต้องใช้ Python 3.10 ขึ้นไป, แพ็กเกจใน `requirements.txt` และตัวแปร environment `CHROMEDRIVER`
ที่ชี้ไปยัง ChromeDriver รุ่นเดียวกับ Chrome ให้รันจากโฟลเดอร์ `robot/` โดยเปิด virtual environment ไว้:

```
robot -d results/run1 -v BROWSER:headlesschrome pizza_scenario.robot
```

## cypress/ (Part 4, Cypress)

โปรเจกต์ Cypress 16 โดย `cypress/e2e/web-form.cy.js` ทดสอบ web form,
`cypress/e2e/pizza-scenario.cy.js` ทำ QP-01 แบบอัตโนมัติ และ `cypress/support/commands.js`
มี custom command ชื่อ `adminLogin` ส่วน `cypress/videos` และ `cypress/screenshots`
เก็บวิดีโอและภาพของการรันเต็มไว้เป็นหลักฐาน

ต้องใช้ Node.js 22 ขึ้นไป ให้รัน `npm install` ในโฟลเดอร์ `cypress/` ครั้งแรกครั้งเดียว แล้วรัน:

```
npx cypress run --browser chrome
```
