
```js no-beautify
"" + 1 + 0 = "10" // (1)
"" - 1 + 0 = -1 // (2)
true + false = 1
6 / "3" = 2
"2" * "3" = 6
4 + 5 + "px" = "9px"
"$" + 4 + 5 = "$45"
"4" - 2 = 2
"4px" - 2 = NaN
7 / 0 = Infinity
"  -9  " + 5 = "  -9  5" // (3)
"  -9  " - 5 = -14 // (4)
null + 1 = 1 // (5)
undefined + 1 = NaN // (6)
" \t \n" - 2 = -2 // (7)
```

1. การบวกสตริงว่างกับเลขหนึ่ง `"" + 1` จะแปลงเลข `1` ให้เป็นสตริง : `"" + 1 = "1"` และ เราก็มี `"1" + 0` ต่อ ก็จะใช้กฎเดียวกัน
2. การลบ `-` (จะเหมือนกับดำเนินการทางคณิตฯอื่นๆ) จะทำงานกับตัวเลขเท่านั้น ดังนั้นจะมันจึงแปลงสตริงว่างให้เป็นเลข `0`
3. การบวกกับสตริง จะต่อท้ายเลข `5` กับสตริง
4. การลบจะแปลงทุกอย่างเป็นตัวเลขเสมอ ดังนั้น `"  -9  "` จึงได้เลข `-9` (จะแปลงโดยที่ไม่สนใจ spaces ที่อยู่รอบเลขลบเก้าเลย)
5. `null` จะกลายเป็นเลข `0` หากถูกแปลงเป็นตัวเลข
6. `undefined` จะเป็นกลายเป็น `NaN` หากถูกแปลงเป็นตัวเลข
ึึ7. space หน้าและหลังจะถูกตัดออก หากแปลงสตริงเป็นตัวเลข หากสตริงมีอักขระพิเศษอย่าง `\t`, `\n` และตามด้วย space ด้านหน้าและหลัง การแปลงเป็นตัวเลขจะตัด space หน้าและหลังออก ส่วน `\t`, `\n` จะกลายเป็นเลข `0`