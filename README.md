# Tiger Zone Tracker

Tiger ki location (latitude, longitude) aur kab dekha gaya, ye daalo.
Page batata hai ki tiger abhi kitne km ke andar ho sakta hai, aur map par circle dikhata hai.

## VS Code mein kaise chalayein

1. Zip ko extract karo.
2. VS Code kholo → File → Open Folder → `tiger-zone-tracker` folder chuno.
3. "Live Server" extension install karo (VS Code khud suggest karega).
4. `index.html` par right-click → **Open with Live Server**.
5. Browser mein page khulega. Internet chalu ho to Satellite map bhi dikhega.

Bina Live Server ke: `index.html` ko seedha Chrome mein double-click karke bhi khol sakte ho.

## Files

| File | Kaam |
| --- | --- |
| `index.html` | Page ka dhancha (form, result, map) |
| `css/style.css` | Rang, font, layout |
| `js/app.js` | Saari logic: doori ka hisaab, map, satellite animation, awaaz |

## Hisaab kaise hota hai (js/app.js → `analyze()`)

- Do location ke beech doori: haversine formula (lat-long se km).
- Speed = doori ÷ time (km/din). 4 ya zyada location hon to tiger ki apni speed, warna default (Speed setting).
- Peela circle (zyada sambhavna) = aam speed × last sighting ke baad ka time + 0.5 km.
- Laal circle (zyada se zyada) = tez speed (sabse tez 10% movements) × time + 0.5 km. Hadd 60 km.
- 60 km/din se tez movement ko galat entry maan kar speed ke hisaab se hata diya jata hai.

## Badalne layak cheezein

- Default speed: `js/app.js` mein `sampleState()` → `set:{avg:5,max:15}`
- Radius ki hadd: `CAP=60` (km), GPS error: `FLOOR=0.5` (km)
- Satellite map: `LAYERS.sat` (Esri World Imagery). Production mein apni map API key wali service lagayein.

## Dhyan rakhein

- Data abhi sirf usi browser ke localStorage mein save hota hai. Team ke liye server + database chahiye (agla step).
- Tiger location sensitive data hai, public website par login ke bina mat daalein.
- Ye sambhavna batata hai, pakki location nahi.
