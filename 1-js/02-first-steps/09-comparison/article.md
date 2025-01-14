# การเปรียบเทียบ

เรารู้จักโอเปอเรเตอร์ที่ใช้เปรียบเทียบมากมายจากคณิตศาสตร์

ในจาวาสคริปต์ก็เหมือนกันพวกมันมีหน้าตาแบบนี้:

- มากกว่าและน้อยกว่า: <code>a &gt; b</code>, <code>a &lt; b</code>.
- มากกว่าหรือเท่ากับและน้อยกว่าหรือเท่ากับ: <code>a &gt;= b</code>, <code>a &lt;= b</code>.
- เท่ากับ: `a == b` อย่าลืมว่าเครื่องหมายสองเท่ากับ `==` หมายถึงเท่ากับ, แต่เท่ากับตัวเดียว `a = b` หมายถึงการกำหนดค่าตัวแปร
- ไม่เท่ากับ: ในวิชาคณิตศาสตร์จะใช้สัญลักษณ์ <code>&ne;</code> แต่ในจาวาสคริปต์จะเขียนว่า <code>a != b</code>.

ในบทความนี้เราจะมาเรียนรู้ตัวเปรียบเทียบต่างๆ หน้าตาของแต่ละตัวในจาวาสคริปต์ และคุณสมบัติพิเศษที่เพิ่มเติมขึ้นมาจากคณิตศาสตร์

บทตอนท้าย เราจะพบบทเรียนสำคัญที่ช่วยให้เราหลีกเลี่ยง ความประหลาดๆในจาวาสคริปต์ได้

## ผลลัพธ์เป็นบูลีน

โอเปอเตอร์ที่ใช้เปรียบเทียบจะส่งค่ากลับเป็นบูลีนเสมอ:

- `true` -- หมายถึง "ใช่", "ถูก" หรือ "จริง".
- `false` -- หมายถึง "ไม่", "ผิด" or "เท็จ".

ดั่งตัวอย่าง:

```js run
alert( 2 > 1 );  // true (ถูก)
alert( 2 == 1 ); // false (ผิด)
alert( 2 != 1 ); // true (ถูก)
```

เราสามารถนำตัวแปรมารับตัวผลลัพธ์ที่เกิดจากตัวเปรียบเทียบได้:

```js run
let result = 5 > 4; // กำหนดให้ result เป็นผลลัพธ์ของ 5 มากกว่า 4
alert( result ); // ได้ true เพราะ 5 มากกว่า 4
```

## การเทียบสตริง

ในจาวาสคริปต์เราสามารถเทียบสตริงกับสตริง จาวาสคริปต์จะใช้ลำดับของ "dictionary" หรือ "lexicographical" เพื่อเทียบสตริงฝั่งใดอยู่ลำดับที่สูงกว่า

กล่าวอีกนัยหนึ่งคือ สตริงจะถูกเทียบแบบตัวอักษรต่อตัวอักษร

ดั่งตัวอย่าง:

```js run
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```

อัลกอริทึมที่ใช้เทียบสตริงนั้นทำงานดังนี้:

1. เทียบอักษรตัวแรกของสตริงทั้งสอง
2. หากอักษรตัวแรกอยู่ลำดับที่สูงกว่าหรือต่ำกว่าก็ตาม จากนั่นก็สตริงตัวแรกยาวหรือสั้นกว่าสตริงตัวที่สอง เมื่อหาตัวที่มากกว่าหรือน้อยกว่าได้แล้ว ถือว่าจบการทำงาน
3. หากตัวอักษรตัวแรกของทั้งสองสตริงเป็นตัวเดียวกัน ก็จะเทียบอักษรตัวที่สองด้วยวิธีเหมือนกัน
4. จะเทียบกันไปเรื่อยๆ จนกว่าจะถึงตัวอักษรสุดท้ายของสตริงตัวใดตัวหนึ่ง
5. หากสตริงทั้งสองยาวเท่ากัน แสดงว่าทั้งสองเท่ากัน หากไม่ใช่สตริงที่ยาวกว่าจะถือว่ามากกว่า

จากตัวอย่างด้านบน การเทียบระหว่าง `'Z' > 'A'` จะได้ผลลัพธ์ตั้งแต่ขั้นตอนแรกก

ตัวที่สอง `'Glow'` and `'Glee'` จะใช้ขั้นตอนที่มากขึ้น เพราะต้องเทียบกันทีละตัว

1. `G` เหมือนกับ `G`
2. `l` เหมือนกับ `l`
3. `o` มากกว่า `e` การทำงานจะจบตรงนี้ หมายความว่าสตริงตัวแรกมีค่ามากกว่า

```smart header="ไม่ใช่พจนานุกรมจริง แต่เป็นไปตามลำดับ Unicode"
อัลกอริธึมจะใช้การเปรียบเทียบดั่งตัวอย่างด้านบน เหมือนกับวิธีการที่พจนานุกรมใช้เรียงตัวอักษรจาก A-Z และสมุดโทรศัพท์จาก 0-9 แต่วิธีการเรียงลำดับนั้นไม่เหมือนกัน

ตัวอย่างเช่น ตัวพิมพ์ใหญ่ `"A"` ไม่เท่ากับตัวพิมพ์เล็ก `"a"` แต่อันไหนมากกว่ากันล่ะ? คำตอบคือตัวพิมพ์เล็ก `"a"` ทำไมกันล่ะ? เนื่องจากอักขระตัวพิมพ์เล็กมีดัชนีมากกว่าในตารางการเข้ารหัสภายในที่ JavaScript ใช้ (Unicode) เราจะลงลึกเรื่องนี้อีกทีในบท <info:string>
```

## เปรียบเทียบประเภทต่างๆ

เมื่อเปรียบเทียบค่าประเภทต่างๆ JavaScript จะแปลงค่านั้นๆเป็นตัวเลข

For example:

```js run
alert( '2' > 1 ); // true, สตริง '2' จะกลายเป็นเลข 2
alert( '01' == 1 ); // true, สตริง '01' จะกลายเป็นเลข 1
```

สำหรับค่าบูลีน `true` กลายเป็น `1` และ `false` กลายเป็น `0`

ตัวอย่างเช่น:

```js run
alert( true == 1 ); // true
alert( false == 0 ); // true
```

````smart header="ผลลัพธ์แบบฮาๆ"
เป็นไปได้ว่าในเวลาเดียวกัน:

- ค่าสองค่าเท่ากัน
- หนึ่งในนั้นคือ `true` เป็นบูลีนและอีกอันเป็น `false` เป็นบูลีน

ตัวอย่างเช่น:

```js run
let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!
```

จากมุมมองของ JavaScript ผลลัพธ์นี้ไม่ได้แปลกอะไร การตรวจสอบความเท่าเทียมกันจะแปลงค่าโดยใช้การแปลงตัวเลข (ดังนั้น `"0"` จะกลายเป็น `0`) ในขณะที่การแปลง `Boolean` ตรงๆจะแปลงเป็น `true` เพราะว่าสตริง `b` ไม่ได้เป็นสตริงเปล่า ดังนั้นเมื่อนำทั้ง `a` และ `b` มาเทียบกับ จึงได้ว่า `true == true` ผลลัพธ์จึงได้ `true`
````

## เท่ากันทั้งค่าและชนิดข้อมูล (Strict equality)

การตรวจสอบความเท่ากันแบบปกติ `==` มันมีปัญหา มันไม่สามารถแยกความแตกต่าง `0` กับ `false` ได้:

```js run
alert( 0 == false ); // true
```

สิ่งเดียวกันนี้เกิดขึ้นกับสตริงว่าง:

```js run
alert( '' == false ); // true
```

สิ่งนี้เกิดขึ้นเนื่องจากตัวถูกดำเนินการประเภทต่าง ๆ จะถูกแปลงเป็นตัวเลขโดยตัวดำเนินการความเท่าเทียมกัน `==` สตริงว่าง จะเหมือนกับ `false` นั่นก็คือจะกลายเป็นศูนย์

ทีนี้จะทำอย่างไรถ้าเราต้องการแยกความแตกต่างระหว่าง `0` กับ `false`

**ตัวดำเนินการเท่ากันทั้งค่าและชนิดข้อมูล (Strict equality) `===` จะตรวจสอบความเท่าเทียมกันโดยไม่ต้องแปลงค่าต่างๆเป็นตัวเลข**

กล่าวอีกนัยหนึ่ง หาก `a` และ `b` เป็นข้อมูลคนละประเภทกัน `a === b` จะส่งกลับค่า `false` ทันทีโดยไม่แปลงค่า

มาลองดูกัน:

```js run
alert( 0 === false ); // false, เพราะว่าข้อมูลคนละประเภทกัน อีกตัวเป็นตัวเลข อีกตัวเป็นบูลีน
```

นอกจากนี้ยังมีโอเปอเรเตอร์ไม่เท่ากันทั้งค่าและชนิดข้อมูล "strict non-equality" หรือ `!==` ซึ่งคล้ายกับ `!=`

ตัวดำเนินการเท่ากันทั้งค่าและชนิดข้อมูล ใช้เวลาพิมพ์นานขึ้นนิดหน่อย แต่ทำให้เห็นชัดเจนว่าเกิดอะไรขึ้น และทำให้เกิดข้อผิดพลาดน้อยลง

## การเทียบ null กับ undefined

การเทียบ `null` หรือ `undefined` กับค่าประเภทอื่นๆจะผิดธรรมชาติ จึงต้องอาศัยการจำหลักการเพิ่มเติม

สำหรับเท่ากันทั้งค่าและชนิดข้อมูล `===`
: ค่าเหล่านี้แตกต่างกันเนื่องจากแต่ละค่าเป็นประเภทที่แตกต่างกัน

    ```js run
    alert( null === undefined ); // false
    ```

สำหรับไม่เท่ากันทั้งค่าและชนิดข้อมูล `==`
: มีกฎพิเศษ ทั้งสองตัวนี้้เป็น "คู่รักแสนหวาน": เพราะพวกมันเท่ากัน (ในความหมายของ `==`)

    ```js run
    alert( null == undefined ); // true
    ```

สำหรับการเปรียบเทียบทางคณิตศาสตร์ `< > <= >=`
: `null/undefined` ทั้งคู่จะถูกแปลงเป็นตัวเลข `null` เป็น `0`, ในขณะที่ `undefined` เป็น `NaN`.

ทีนี้มาดูเรื่องตลก ๆ ที่เกิดขึ้นเมื่อเรานำกฎด้านบนไปใช้กัน และที่สำคัญกว่านั้นคือทำอย่างไรไม่ให้ตกหลุมพรางสองตัวนี้

### ผลลัพธ์แปลกๆจาก: null vs 0

มาเทียบ `null` กับเลขศูนย์กันดู:

```js run
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) *!*true*/!*
```

ในทางคณิตศาสตร์ มันแปลก ที่ผลลัพธ์สุดท้ายท่ีระบุว่า `null` มากกว่าหรือเท่ากับศูนย์" ทั้งๆที่เราลองให้ `null` มากกว่าศูนย์ ได้ `false` และ `null` เท่ากับศูนย์ก็ได้ `false` ในทางตรรกะศาสตร์แล้วจึงเป็นไปไม่ได้ที่ false กับ false สองตัวจะกลายเป็น true ได้

เหตุผลก็คือการตรวจสอบความเท่าเทียมกัน `==` และการเปรียบเทียบ `> < >= <=` ทำงานต่างกัน การเปรียบเทียบแปลง `null` เป็นตัวเลข โดยถือว่าเป็น `0` นั่นเป็นสาเหตุที่คำสั่งที่สาม `null >= 0` เป็นจริงและคำสั่งแรก `null > 0` เป็นเท็จ

ในทางกลับกัน การตรวจสอบความเท่าเทียมกัน `==` สำหรับ `undefined` และ `null` ถูกกำหนดให้ไม่มีการแปลงใดๆ พวกมันทั้งคู่จะเท่ากันเองและไม่เท่ากับค่าอื่นๆเลย นั่นเป็นสาเหตุที่ (2) `null == 0` เป็นเท็จ

### undefined เทียบกับอะไรไม่ได้เลย ยกเว้น null

โดยปกติแล้วเราจะไม่เทียบ `undefined` กับค่าใดๆ:

```js run
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```

แม้จะเทียบกับศูนย์ก็ยังได้ false

เราได้รับผลลัพธ์เหล่านี้เนื่องจาก:

- การเปรียบเทียบ `(1)` และ `(2)` คืนค่า `false` เนื่องจาก `undefined` ถูกแปลงเป็น `NaN` และ `NaN` เป็นค่าตัวเลขพิเศษที่คืนค่า `false' เมื่อไปเทียบกับอะไรก็ตาม
- ส่วน `==` แบบ `(3)` คืนค่า `false` เนื่องจาก `undefined` เท่ากับ `null` เท่านั้น `undefined` ตัวเดียวจึงไม่เท่ากับค่าใดๆเลย

### วิธีหลีกเลี่ยงปัญหา

ทำไมเราจึงไม่ข้ามตัวอย่างด้านบน? เราควรท่องจำตัวอย่างด้านบนให้ขึ้นใจหรือไม่? ก็ ไม่ขนาดนั้นนะ ที่จริงแล้ว เมื่อเราทำงานกับ JavaScript ไปเรื่อยๆ เราจะเริ่มชินและคุ้นเคยกับตัวอย่างด้านบน แต่เราก็มีวิธีที่ช่วยหลีกเลี่ยงปัญหาด้่านบนได้อย่างหยั่งยืนเช่นกัน

- ควรเทียบความเท่ากันของค่า `undefined/null` ด้วย `===`
- อย่าไปใช้ตัวเปรียบเทียบ `>= > < <=` กับตัวแปรที่อาจจะเป็น `undefined/null` ได้ เว้นแต่ว่าเรามั่นใจจริงๆว่ากำลังทำอะไรอยู่ หากตัวแปรเป็น `undefined/null` ให้เพิ่มคำสั่งขึ้นมาเพื่อตรวจสอบตะหาก

## สรุป

- ตัวดำเนินการเปรียบเทียบจะส่งค่าที่เป็นบูลีนกลับ
- สตริงจะถูกเปรียบเทียบทีละตัวอักษรในลำดับ "Unicode"
- เมื่อเปรียบเทียบค่าประเภทต่างๆ ค่าเหล่านั้นจะถูกแปลงเป็นตัวเลข (ยกเว้น strict equality `===`)
- ค่า `null` และ `undefined` จะเท่ากันหากเทียบด้วย `==` และไม่เท่ากับค่าอื่นใด
- ระวังเมื่อใช้การเปรียบเทียบ เช่น `>` หรือ `<` กับตัวแปรอาจเป็น `null/undefined` ได้การตรวจสอบ `null/undefined` แยกกันจะดีกว่า
