# java-shipment-exercise

แบบฝึกหัด Java OOP — ระบบคำนวณค่าขนส่ง Shipment  
วิชา Object-Oriented Programming | ปีการศึกษา 2569

---

## คำอธิบายโจทย์

บริษัทขนส่งแห่งหนึ่งมีรายการ **Shipment** หลายรายการ  
ให้เขียนโปรแกรม Java คำนวณค่าขนส่งตามน้ำหนักและประเภท แล้วแสดงยอดรวม

**กฎการคำนวณ:**

| ประเภท | อัตรา |
|--------|-------|
| STANDARD (มาตรฐาน) | 40 บาท / กิโลกรัม |
| EXPRESS (ด่วน) | 100 บาท / กิโลกรัม |

---

## 📁 ไฟล์ในโปรเจกต์

```
java-shipment-exercise/
├── pom.xml                              ← Maven config (JUnit 5)
├── src/
│   ├── main/java/com/example/
│   │   ├── ShipmentSection1_Exercise.java
│   │   ├── ShipmentSection2_Exercise.java
│   │   ├── ShipmentSection3_Exercise.java
│   │   └── ShipmentSection4_Exercise.java
│   └── test/java/com/example/
│       └── ShipmentTest.java            ← JUnit 5 test cases
├── ExpectedOutput_Section1.md
├── ExpectedOutput_Section2.md
├── ExpectedOutput_Section3.md
├── ExpectedOutput_Section4.md
└── README.md
```

> เฉลยไม่ได้อยู่ใน repo นี้ — อาจารย์จะแจกให้หลังส่งงาน

---

## 🍴 วิธีเริ่มต้น (Fork & Clone)

### Step 1 — Fork repo นี้

กดปุ่ม **Fork** มุมบนขวาของหน้านี้

> Fork แล้ว repo จะไปอยู่ใน GitHub ของตัวเอง เช่น  
> `https://github.com/your-username/java-shipment-exercise`

---

### Step 2 — Clone ลงเครื่อง

```bash
git clone https://github.com/your-username/java-shipment-exercise.git
cd java-shipment-exercise
```

> แทน `your-username` ด้วย GitHub username ของตัวเอง

---

### Step 3 — เปิดไฟล์ที่ได้รับมอบหมาย

อาจารย์จะแจ้งว่าให้ทำ Section ใด (1, 2, 3 หรือ 4)

```
Section 1 → src/main/java/com/example/ShipmentSection1_Exercise.java
Section 2 → src/main/java/com/example/ShipmentSection2_Exercise.java
Section 3 → src/main/java/com/example/ShipmentSection3_Exercise.java
Section 4 → src/main/java/com/example/ShipmentSection4_Exercise.java
```

เปิด `ExpectedOutput_SectionX.md` ของ Section นั้นไว้คู่กันเสมอ

---

### Step 3.5 — ⚠️ ลบไฟล์ Section อื่นที่ไม่ใช่ของตัวเองออก

> **สำคัญมาก** — หลัง Fork แล้วให้ลบไฟล์ของ Section อื่นออกจาก repo ตัวเองด้วย  
> เพื่อไม่ให้สับสน และป้องกันการส่งงานผิด Section

**ตัวอย่าง: ถ้าได้รับมอบหมาย Section 2**

```bash
git rm src/main/java/com/example/ShipmentSection1_Exercise.java
git rm src/main/java/com/example/ShipmentSection3_Exercise.java
git rm src/main/java/com/example/ShipmentSection4_Exercise.java
git rm ExpectedOutput_Section1.md
git rm ExpectedOutput_Section3.md
git rm ExpectedOutput_Section4.md

git commit -m "remove: ลบ Section ที่ไม่ใช่ของตัวเองออก"
git push origin main
```

> เก็บไว้เฉพาะ Section ของตัวเอง + `pom.xml` + `ShipmentTest.java` + `README.md`

---

### Step 4 — แก้ Bug ตาม TODO

แต่ละ Section มี Bug ที่ต่างกัน — แก้ตามลำดับ TODO ที่ระบุในไฟล์

| Section | บริษัท | Bug หลักที่ซ่อนไว้ |
|:-------:|--------|-------------------|
| 1 | SpeedEx Logistics | enum ขาด, parameter สลับ, อัตราสลับ |
| 2 | FlashMove Express | enum ขาด, assignment สลับ, อัตราผิด |
| 3 | RocketShip Thailand | if-condition สลับ, index ผิด |
| 4 | SwiftCargo Co., Ltd. | return ค่าผิด, loop condition ผิด |

---

### Step 5 — รันด้วย Maven Test

ตรวจสอบก่อนว่ามี Maven ในเครื่อง:

```bash
mvn -version
```

ถ้ายังไม่มี ดาวน์โหลดได้ที่ https://maven.apache.org/download.cgi

#### รัน Test ทั้งหมด

```bash
mvn test
```

#### รัน Test เฉพาะ Section ของตัวเอง

```bash
# Section 1
mvn -Dtest=ShipmentTest#sec1* test

# Section 2
mvn -Dtest=ShipmentTest#sec2* test

# Section 3
mvn -Dtest=ShipmentTest#sec3* test

# Section 4
mvn -Dtest=ShipmentTest#sec4* test
```

#### ผลลัพธ์ที่ต้องการเห็น (ตัวอย่าง Section 1)

```
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.example.ShipmentTest
[INFO]
[INFO] Tests run: 6, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO] BUILD SUCCESS
```

> `Failures: 0` และ `BUILD SUCCESS` = แก้ Bug ถูกต้องทุกจุด ✅

#### ถ้า Test ยังไม่ผ่าน ให้ดูบรรทัดนี้

```
expected: <120.0> but was: <300.0>
```

แปลว่าค่าที่คำนวณได้ไม่ตรงกับที่คาดหวัง — กลับไปแก้ Bug ในไฟล์ Exercise

---

### Step 6 — Push และส่งงาน

เมื่อ `mvn test` ผ่านแล้ว:

```bash
git add src/main/java/com/example/ShipmentSectionX_Exercise.java
git commit -m "fix: แก้ไข TODO Section X เสร็จสมบูรณ์"
git push origin main
```

**ส่ง link repo ให้อาจารย์:**  
`https://github.com/your-username/java-shipment-exercise`

---

## 🧪 Test Cases ใน ShipmentTest.java

ไฟล์ `src/test/java/com/example/ShipmentTest.java` มี test ครอบคลุมทุก Section:

| Test Method | ทดสอบอะไร | ผลที่คาดหวัง |
|-------------|----------|-------------|
| `sec1_standard_3kg` | TH001: 3.0 กก. STANDARD | 120.00 บาท |
| `sec1_express_1_5kg` | TH002: 1.5 กก. EXPRESS | 150.00 บาท |
| `sec1_standard_5kg` | TH003: 5.0 กก. STANDARD | 200.00 บาท |
| `sec1_express_2kg` | TH004: 2.0 กก. EXPRESS | 200.00 บาท |
| `sec1_standard_10kg` | TH005: 10.0 กก. STANDARD | 400.00 บาท |
| `sec1_totalCost` | ยอดรวม SpeedEx | 1,070.00 บาท |
| `sec2_totalCost` | ยอดรวม FlashMove | 1,070.00 บาท |
| `sec3_totalCost` | ยอดรวม RocketShip | 1,240.00 บาท |
| `sec4_totalCost` | ยอดรวม SwiftCargo | 1,310.00 บาท |
| `edge_zeroWeight` | น้ำหนัก 0 กก. | 0.00 บาท |
| `edge_emptyCompany` | ไม่มี Shipment | 0.00 บาท |

---

## ❗ Error ที่พบบ่อย

| Error | สาเหตุ | ดู TODO |
|-------|--------|--------|
| `error: cannot find symbol` | enum ไม่ครบ | A (Sec 1, 2) |
| `NullPointerException` | ลืม `new ArrayList<>()` | E (Sec 1, 2) |
| ทุกรายการได้ `0.00` | `return 0` แทน `return cost` | A (Sec 4) |
| ตัวเลขสลับ STANDARD/EXPRESS | if-condition ผิด | A (Sec 3) |
| ยอดรวมผิด (น้อยกว่าที่ควร) | loop วนไม่ครบ | C (Sec 3, 4) |
| ไม่มีบรรทัดรายการใดแสดง | `printSummary()` ไม่มี loop | G/D |
| `BUILD FAILURE` ใน mvn | มี test ไม่ผ่าน — อ่าน expected/actual | แก้ Bug ต่อ |

---

## ✅ Checklist ก่อนส่ง

- [ ] Fork repo แล้ว
- [ ] Clone ลงเครื่องแล้ว
- [ ] ลบไฟล์ Section อื่นออกแล้ว
- [ ] แก้ TODO ครบทุกจุด
- [ ] `mvn test` ผ่าน — ขึ้น `BUILD SUCCESS`
- [ ] `Failures: 0, Errors: 0`
- [ ] `git push` ขึ้น GitHub แล้ว
- [ ] ส่ง link repo ให้อาจารย์แล้ว
