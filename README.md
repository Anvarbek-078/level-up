# LEVEL UP

## Backendni ishga tushirish (Windows)

Python 3.9 yoki yangiroq versiyani o‘rnating. Loyiha papkasida PowerShell ochib, admin hisobini muhit o‘zgaruvchilari orqali belgilang:

```powershell
$env:ADMIN_USERNAME = "admin"
$env:ADMIN_PASSWORD = "kamida-6-belgili-maxfiy-parol"
python server.py
```

So‘ng `http://127.0.0.1:8000` manzilini oching. `ADMIN_USERNAME` va `ADMIN_PASSWORD` birinchi ishga tushishda admin foydalanuvchisini yaratadi. Admin hisobini avval bazaga yozib bo‘lgach, parolni o‘zgartirish profil orqali amalga oshiriladi.

## Ma’lumotlar bazasi

SQLite bazasi avtomatik ravishda `levelup.sqlite3` faylida yaratiladi. Unda o‘quvchi profillari va parol xeshlari, muddati bor login sessiyalari, hamda test/mashq natijalari va mavzu kesimidagi statistika saqlanadi. Hisoblar orasidagi parollar PBKDF2-HMAC-SHA256 bilan xeshlanadi. O‘quvchilar reytingdagi umumiy XP va aniqlikni ko‘radi; urinishlar tarixi faqat o‘quvchining o‘ziga va admin’ga beriladi.

Avvalgi versiyada brauzerning `localStorage`’ida saqlangan hisoblar va natijalar bazaga avtomatik ko‘chirilmaydi. Serverni ommaga chiqarishda HTTPS reverse proxy, muntazam SQLite zaxira nusxasi va so‘rovlar tezligini cheklashni sozlang.

## API

- `POST /api/register` va `POST /api/login` hisob ochadi yoki kirishni tasdiqlaydi.
- `GET /api/bootstrap` joriy profil, reyting va ruxsat etilgan natijalarni qaytaradi.
- `POST /api/results` test natijasini saqlaydi.
- `POST /api/password` parolni yangilaydi.
- `POST /api/students` hamda `DELETE /api/students/{login}` admin uchun o‘quvchi hisoblarini boshqaradi.
- `POST /api/logout` sessiyani yopadi.
- `GET /api/health` server holatini tekshiradi.

Natija yozish API’si hisoblangan foiz, XP va mavzu jami ko‘rsatkichlarini tekshiradi. Savollar va javob kaliti hozir frontendda bo‘lgani sababli, bu versiyada API mustaqil ravishda to‘g‘ri javoblarni tasdiqlamaydi; natijani ataylab soxtalashtirishdan himoya qilish uchun savollarni serverga ko‘chirish kerak bo‘ladi.