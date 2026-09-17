# Test Plan — ระบบติดตามกระบวนการฝึกงานนักศึกษา

เอกสารสรุปกลยุทธ์การทดสอบภาพรวมของโปรเจกต์ (1 ไฟล์ต่อโปรเจกต์) อ้างอิง [feature-list](../design/feature-list.md),
[user-journey](../design/user-journey.md), [backlog](../requirements/backlog.md) และ [acceptance-criteria](./acceptance-criteria.md) เป็นแหล่งความจริง โปรเจกต์นี้ยังอยู่ในขั้น
requirements/design **ยังไม่มีซอร์สโค้ด** ดังนั้น test plan ฉบับนี้เขียนไว้ล่วงหน้าเพื่อเตรียมความ
พร้อมก่อนเริ่มพัฒนาจริง โดยไม่ผูกกับ tech stack ใดๆ

## 1. Scope (ขอบเขตการทดสอบ)

### อยู่ในขอบเขต

ทดสอบทั้ง 10 ฟีเจอร์ตาม [feature-list](../design/feature-list.md) ครบทุกฟีเจอร์ (ฟีเจอร์ 1–9 = Must have, ฟีเจอร์ 10 =
Should have):

| # | ฟีเจอร์ | MoSCoW |
|---|---|---|
| 1 | [ติดตามสถานะกระบวนการฝึกงาน](../design/feature-list.md) | Must have |
| 2 | [ยื่นเสนอสถานประกอบการและขออนุมัติ](../design/feature-list.md) | Must have |
| 3 | [ตรวจสอบคุณสมบัติด้านการอบรม](../design/feature-list.md) | Must have |
| 4 | [จัดการเอกสารตอบรับการฝึกงาน 3 ฉบับ](../design/feature-list.md) | Must have |
| 5 | [ปักหมุดสถานประกอบการ วางแผนเส้นทาง และมอบหมายอาจารย์นิเทศ](../design/feature-list.md) | Must have |
| 6 | [ให้คะแนนและบันทึกผลสัมภาษณ์ระหว่างนิเทศ](../design/feature-list.md) | Must have |
| 7 | [ยืนยันการบันทึกข้อมูลกับระบบ internship หลัก](../design/feature-list.md) | Must have |
| 8 | [สิ้นสุดการฝึกงานและเอกสารขอบคุณสถานประกอบการ](../design/feature-list.md) | Must have |
| 9 | [บันทึกและติดตามกรณีปัญหาระหว่างฝึกงาน](../design/feature-list.md) | Must have |
| 10 | [แจ้งเตือนกำหนดการนำเสนอและนิเทศ](../design/feature-list.md) | Should have |

รวม FR-01–FR-20, FR-22–FR-29, FR-31–FR-35 และ NFR-01–NFR-07 ทั้งหมด (FR-21, FR-30 = Deprecated
ตั้งแต่ 2026-09-16 จึงไม่อยู่ในขอบเขตการทดสอบอีกต่อไป — ดูรายละเอียดที่ [backlog](../requirements/backlog.md))

### นอกขอบเขต (ตาม [spec หัวข้อ 2](../requirements/spec.md))

- การบันทึก task ประจำวันระหว่างฝึกงาน และการที่สถานประกอบการเข้าดูความคืบหน้า — เป็นหน้าที่ของ
  "ระบบ internship หลัก" ที่มีอยู่แล้ว **ไม่ทดสอบในแผนนี้** (ระบบนี้ทดสอบเพียงจุดเชื่อมต่อแบบ
  self-declare ตาม FR-22–FR-23 เท่านั้น)
- การเซ็นเอกสารแบบดิจิทัล/e-signature
- การจ่ายค่าตอบแทน/สวัสดิการนักศึกษาฝึกงาน
- การเชื่อมต่อ API จริงกับระบบ internship หลัก (ยังเป็นสมมติฐานที่ยังไม่ยืนยัน — ดู
  [สมมติฐานข้อ 2](../requirements/spec.md))

## 2. ประเภทการทดสอบ

### 2.1 Functional Testing (ต่อกลุ่ม FR)

| กลุ่ม FR (ตาม spec) | ฟีเจอร์ที่เกี่ยวข้อง | ประเภทการทดสอบ |
|---|---|---|
| กลุ่ม A (FR-01–FR-02) | ฟีเจอร์ 1 | Functional Testing — การแสดงสถานะ/แดชบอร์ด, การกรอง |
| กลุ่ม B (FR-03–FR-07) | ฟีเจอร์ 2 | Functional Testing — workflow อนุมัติ/วนซ้ำ (state transition) |
| กลุ่ม C (FR-08–FR-10) | ฟีเจอร์ 3 | Functional Testing — การตรวจสอบเกณฑ์/การอัปโหลดไฟล์ |
| กลุ่ม D (FR-11–FR-15) | ฟีเจอร์ 4 | Functional Testing — การอัปโหลดเอกสาร/การแจ้งเตือน |
| กลุ่ม E (FR-16–FR-20, FR-32–FR-34; FR-21, FR-30 = Deprecated) | ฟีเจอร์ 5, 6 | Functional Testing — แผนที่/มอบหมายอาจารย์นิเทศ 1:1 ตามกลุ่มเส้นทาง (FR-32)/ยืนยันก่อนแทนที่การมอบหมายเดิม (FR-34)/การกำหนดรูปแบบนิเทศ online-onsite ต่อครั้ง (FR-33)/การให้คะแนน-สัมภาษณ์ |
| กลุ่ม F (FR-22–FR-23) | ฟีเจอร์ 7 | Functional Testing — self-declare confirmation |
| กลุ่ม G (FR-24–FR-25, FR-35) | ฟีเจอร์ 8 | Functional Testing — เปลี่ยนสถานะอัตโนมัติ/สร้างเอกสารจากแม่แบบ/แจ้งเตือนนักศึกษาเมื่อสถานประกอบการประเมินผลเสร็จสิ้น (FR-35 — milestone คู่ขนาน ไม่ block การเปลี่ยนสถานะ) |
| กลุ่ม H (FR-26–FR-28) | ฟีเจอร์ 9 | Functional Testing — บันทึกกรณีปัญหา/ไทม์ไลน์ |
| กลุ่ม I (FR-29, FR-31) | ฟีเจอร์ 10 | Functional Testing — การแจ้งเตือนตามกำหนดเวลา/นโยบายเวลาล่วงหน้าที่ปรับได้ |

### 2.2 Non-Functional Testing (ต่อ NFR)

| รหัส | ด้าน | ประเภทการทดสอบ |
|---|---|---|
| [NFR-01](./acceptance-criteria.md) | ความปลอดภัย/สิทธิ์การเข้าถึงข้อมูล | Security Testing — ทดสอบสิทธิ์การเข้าถึงเอกสาร/ไฟล์ตามบทบาท (access control / authorization) |
| [NFR-02](./acceptance-criteria.md) | การตรวจสอบย้อนหลัง (Audit) | Audit/Traceability Testing — ทดสอบว่าทุกการเปลี่ยนสถานะสำคัญถูกบันทึกผู้ทำรายการและเวลาไว้ครบ |
| [NFR-03](./acceptance-criteria.md) | การใช้งานภาคสนาม | Usability/Reliability Testing (Field & Offline Conditions) — ทดสอบการบันทึกข้อมูลผ่านอุปกรณ์พกพาภายใต้สัญญาณอินเทอร์เน็ตไม่เสถียร |
| [NFR-04](./acceptance-criteria.md) | ประสิทธิภาพการแสดงผลแผนที่ | Performance Testing — ทดสอบความหน่วงของการแสดงผลแผนที่เมื่อมีจำนวนหมุดมาก |
| [NFR-05](./acceptance-criteria.md) | ความถูกต้องของเอกสารที่สร้างอัตโนมัติ | Output/Document Verification Testing — ทดสอบความถูกต้องของข้อมูลและรูปแบบเอกสารที่ระบบสร้างอัตโนมัติ |
| [NFR-06](./acceptance-criteria.md) | ความถูกต้องของไฟล์ที่อัปโหลด (File Validation) | Security/Input Validation Testing — ทดสอบการปฏิเสธไฟล์ผิดประเภท/เกินขนาด/ไฟล์เสียทันทีทุกจุดที่ให้อัปโหลด (certificate, เอกสารตอบรับ 3 ฉบับ) |
| [NFR-07](./acceptance-criteria.md) | การทำงานแบบออฟไลน์และการซิงก์ข้อมูล (Offline Draft & Auto-Sync) | Reliability/Offline Testing — ทดสอบการเก็บ local draft ไม่จำกัดเวลา, auto-retry เมื่อสัญญาณกลับมา, และแบนเนอร์แจ้งเตือนข้อมูลค้างซิงก์ |

## 3. Environment (สภาพแวดล้อมการทดสอบ)

`docs/02-design/02-technical/technology-stack.md` **ยังไม่มีไฟล์/ยังว่างเปล่า** ณ วันที่เขียนแผนนี้
(2026-09-16) — **รอกำหนด tech stack ก่อน** จึงยังไม่สามารถระบุ environment เชิงเทคนิค (เช่น เวอร์ชัน
browser/OS, ฐานข้อมูลทดสอบ, CI pipeline) ได้ในขณะนี้ เมื่อมีการตัดสินใจ tech stack แล้ว ให้กลับมา
ปรับปรุงหัวข้อนี้ให้ระบุ:
- Environment ระดับ dev/staging/production (ถ้ามี)
- อุปกรณ์ที่ต้องทดสอบจริงสำหรับ NFR-03 (มือถือ/แท็บเล็ตภาคสนาม พร้อมจำลองสัญญาณอินเทอร์เน็ตไม่เสถียร
  — บังคับเฉพาะรอบนิเทศแบบ **onsite** ตาม FR-33 เท่านั้น; รอบนิเทศแบบ **online** ทดสอบด้วยอุปกรณ์/
  อินเทอร์เน็ตปกติแทน ไม่ต้องจำลองสัญญาณไม่เสถียร)
- บัญชีทดสอบของแต่ละบทบาท (นักศึกษา, อาจารย์ที่ปรึกษา, อาจารย์นิเทศ, เจ้าหน้าที่ประสานงานฝึกงาน)
- ข้อมูลตัวอย่าง (seed data) ที่ครอบคลุมทุกสถานะในวงจรชีวิตของนักศึกษาฝึกงาน

## 4. Entry Criteria (เกณฑ์เริ่มทดสอบ)

- มีซอร์สโค้ด/ฟีเจอร์ที่พัฒนาเสร็จตามขอบเขตที่ระบุใน detailed-design ของฟีเจอร์นั้น (เมื่อเริ่ม
  พัฒนาจริง)
- มี test case ที่เกี่ยวข้องใน `test-cases/{feature-slug}.md` ครบและได้รับการทบทวนแล้ว
- Environment พร้อมใช้งานตามที่ระบุในหัวข้อ 3 (รอ tech stack)
- มีบัญชีทดสอบครบทุกบทบาทที่เกี่ยวข้องกับฟีเจอร์นั้น

## 5. Exit Criteria (เกณฑ์ผ่านการทดสอบ)

- Test case ทั้งหมดของฟีเจอร์ที่มีระดับความสำคัญ "สูง" (MVP) ต้องผ่าน 100%
- Test case ของฟีเจอร์ระดับ "กลาง"/"ต่ำ" ผ่านอย่างน้อยตามเกณฑ์ที่ทีมตกลงกันไว้ก่อนปล่อยใช้งานจริง
  (defect ที่พบต้องได้รับการจัดลำดับความสำคัญและมีแผนแก้ไขก่อนปิดรอบทดสอบ)
- ไม่มี defect ระดับ Critical/Blocker ค้างอยู่ในฟีเจอร์ที่เป็น Must have
- ผลการทดสอบ Non-functional (Security, Audit, Field/Offline, Performance, Document Accuracy)
  ผ่านตามเกณฑ์ที่กำหนดใน [acceptance-criteria](./acceptance-criteria.md) ของ NFR แต่ละตัว

## 6. บทบาทผู้ทดสอบ

ทดสอบตามบทบาทผู้ใช้จริงของระบบ (อ้างอิง [spec หัวข้อ 3](../requirements/spec.md) และ [user-journey](../design/user-journey.md)):

| บทบาท | ขอบเขตการทดสอบหลัก |
|---|---|
| นักศึกษา | ยื่นสถานประกอบการ, อัปโหลด certificate/เอกสาร, ปักหมุด Google Map, ยืนยันตนเองกับระบบ internship หลัก, ดูสถานะตนเอง |
| อาจารย์ที่ปรึกษา/ผู้อนุมัติการฝึกงาน | นัดวันนำเสนอ, บันทึกผลผ่าน/ไม่ผ่าน, ดูแดชบอร์ดภาพรวม, รับการแจ้งเตือน |
| อาจารย์นิเทศ (1 ท่านต่อบริษัท ตามกลุ่มเส้นทางที่ได้รับมอบหมาย — ปรับปรุง 2026-09-16) | ดูตำแหน่งปักหมุด/วางแผนเส้นทาง, กำหนดรูปแบบการนิเทศ online/onsite ต่อครั้ง, บันทึกคะแนน/ผลสัมภาษณ์ (ผ่านอุปกรณ์พกพาเฉพาะกรณี onsite), บันทึกกรณีปัญหา |
| เจ้าหน้าที่ประสานงานฝึกงาน | ตรวจสอบคุณสมบัติ/เอกสาร, ดูแดชบอร์ดภาพรวม, บันทึก/ติดตามกรณีปัญหา, สร้างหนังสือขอบคุณ |

## 7. ตารางสรุปฟีเจอร์ ↔ ไฟล์ test case ↔ จำนวน AC ที่ครอบคลุม

| # | ฟีเจอร์ | ไฟล์ test case | จำนวน AC ที่ครอบคลุม |
|---|---|---|---|
| 1 | ติดตามสถานะกระบวนการฝึกงาน | [internship-status-tracking](./test-cases/internship-status-tracking.md) | 5 (FR-01 ×2, FR-02 ×2, NFR-02 ×1) |
| 2 | ยื่นเสนอสถานประกอบการและขออนุมัติ | [company-proposal-approval](./test-cases/company-proposal-approval.md) | 7 (FR-03, FR-04, FR-05 ×2, FR-06, FR-07, NFR-02) |
| 3 | ตรวจสอบคุณสมบัติด้านการอบรม | [training-qualification](./test-cases/training-qualification.md) | 10 (FR-08 ×2, FR-09, FR-10 ×2, NFR-01, NFR-06 ×4) |
| 4 | จัดการเอกสารตอบรับการฝึกงาน 3 ฉบับ | [acceptance-documents](./test-cases/acceptance-documents.md) | 10 (FR-11, FR-12, FR-13, FR-14 ×2, FR-15, NFR-01, NFR-06 ×3) |
| 5 | ปักหมุดสถานประกอบการ วางแผนเส้นทาง และมอบหมายอาจารย์นิเทศ | [company-map-pinning](./test-cases/company-map-pinning.md) | 11 (FR-16 ×2, FR-17, FR-32 ×2, FR-34 ×4, NFR-02 ×1, NFR-04) |
| 6 | ให้คะแนนและบันทึกผลสัมภาษณ์ระหว่างนิเทศ | [supervision-scoring](./test-cases/supervision-scoring.md) | 13 (FR-18 ×2, FR-19 ×2, FR-20 ×2, FR-33 ×3, NFR-03, NFR-07 ×3; FR-21/FR-30 = Deprecated ไม่นับรวม) |
| 7 | ยืนยันการบันทึกข้อมูลกับระบบ internship หลัก | [main-system-confirmation](./test-cases/main-system-confirmation.md) | 3 (FR-22, FR-23, NFR-02) |
| 8 | สิ้นสุดการฝึกงานและเอกสารขอบคุณสถานประกอบการ | [internship-completion](./test-cases/internship-completion.md) | 6 (FR-24, FR-25, FR-35 ×2, NFR-02, NFR-05) |
| 9 | บันทึกและติดตามกรณีปัญหาระหว่างฝึกงาน | [problem-case-tracking](./test-cases/problem-case-tracking.md) | 5 (FR-26 ×2, FR-27, FR-28, NFR-02) |
| 10 | แจ้งเตือนกำหนดการนำเสนอและนิเทศ | [schedule-notifications](./test-cases/schedule-notifications.md) | 4 (FR-29 ×2, FR-31 ×2) |

รวมทั้งหมด 74 AC ครอบคลุม FR-01–FR-20, FR-22–FR-29, FR-31–FR-35 และ NFR-01–NFR-07 ครบทุกรหัส active
(FR-21, FR-30 = Deprecated ตั้งแต่ 2026-09-16 ไม่นับรวมในจำนวนนี้แล้ว — ดู
*(Deprecated — FR-21/FR-30 ยกเลิกจาก scope)*) (รายละเอียดแต่ละ AC ดูที่
[acceptance-criteria](./acceptance-criteria.md))

## เอกสารที่เกี่ยวข้อง

- [feature-list](../design/feature-list.md) — รายการฟีเจอร์ทั้งหมดพร้อม MoSCoW
- [user-journey](../design/user-journey.md) — flow การใช้งานจริงตามบทบาท
- [backlog](../requirements/backlog.md) — สรุป FR/NFR ทั้งหมดพร้อมระดับความสำคัญ
- [acceptance-criteria](./acceptance-criteria.md) — เกณฑ์ยอมรับรายรหัส
- [spec](../requirements/spec.md) — เอกสาร spec ต้นทาง
