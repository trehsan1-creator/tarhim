# 🕊️ یادبود سید جعفر محمددوست

> مجلس هفتم — جمعه ۳ مهرماه — رستوران عابدین‌زاده

این یک دعوت‌نامه‌ی یادبود تک‌صفحه‌ای، موبایل‌فرست و بدون مرحله‌ی ساخت است. با لمس پاکت، کارت باز می‌شود، نوای پس‌زمینه تلاش می‌کند پخش شود و پیام‌های تسلیت در دیوار یادبود نمایش داده می‌شوند.

## ✨ ویژگی‌ها
- ✉️ پاکت سه‌بعدی تعاملی با انیمیشن باز شدن
- 🕯️ شمع SVG متحرک و ذرات آرام پس‌زمینه
- 🔤 ترکیب IranNastaliq، Amiri و Sahel
- 🎵 پخش خودکار نوای محلی با باز شدن پاکت
- 📸 عکس مرحوم به صورت لوکال (بدون نیاز به هاست خارجی)
- 💬 دیوار یادبود آنلاین با Supabase و fallback به localStorage
- 📱 طراحی کاملاً موبایل‌فرست با safe area آیفون
- 🗺️ مسیریابی مستقیم گوگل‌مپ و نشان

## 🚀 شروع سریع
1. ریپو را کلون کنید.
2. عکس مرحوم را با نام دقیق `portrait.jpg` در `assets/` قرار دهید.
3. فایل آهنگ را با نام دقیق `audio.mp3` در `assets/` قرار دهید.
4. `index.html` را مستقیماً در مرورگر باز کنید یا پوشه را روی GitHub Pages، Vercel یا Netlify منتشر کنید.

> تصاویر تزئینی تولیدشده در `assets/` قرار دارند و همه‌ی مسیرهای عکس و صدا محلی هستند. فایل‌های نمونه‌ی موجود برای پیش‌نمایش‌اند؛ عکس و نوای خانوادگی را جایگزین کنید.

## 📸 تنظیم عکس مرحوم
- فرمت JPG یا PNG، ترجیحاً JPG
- حداقل ۴۰۰×۴۰۰ و حداکثر ۱۲۰۰×۱۲۰۰ پیکسل
- نسبت مربعی (۱:۱)، چون در کارت به شکل دایره‌ای برش می‌خورد
- حجم پیشنهادی کمتر از ۵۰۰ کیلوبایت
- نام فایل دقیقاً `portrait.jpg` و مسیر دقیقاً `assets/portrait.jpg` باشد

اگر عکس خراب یا حذف شود، `portrait-placeholder.webp` نمایش داده می‌شود و در صورت نبودن آن، زمینه‌ی قاب همچنان قابل استفاده است.

## 🎵 تنظیم آهنگ
یک MP3 آرام (نوای نی، تلاوت یا موسیقی بی‌کلام محترمانه) را با نام `audio.mp3` در `assets/` بگذارید. صدا در اولین لمس پاکت با حجم پیش‌فرض ۰٫۳۵ آغاز می‌شود، loop است و دکمه‌ی شناور برای توقف/پخش دارد. اگر فایل وجود نداشته باشد، صفحه بدون خطا و بدون صدا کار می‌کند.

## 🗄️ فعال‌سازی دیوار یادبود آنلاین (Supabase)
1. در [supabase.com](https://supabase.com) ثبت‌نام کنید و یک پروژه بسازید.
2. در SQL Editor این دستور را اجرا کنید:

```sql
CREATE TABLE condolences (
  id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name TEXT NOT NULL,
  message TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE condolences ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Anyone can read" ON condolences FOR SELECT USING (true);
CREATE POLICY "Anyone can insert" ON condolences FOR INSERT WITH CHECK (true);
ALTER PUBLICATION supabase_realtime ADD TABLE condolences;
```

3. `index.html` را باز کنید و فقط این دو مقدار را در `CONFIG` پر کنید:

```js
supabaseUrl: "https://xxxxx.supabase.co",
supabaseKey: "eyJhbGciOi..."
```

اگر هر دو مقدار خالی باشند، پیام‌ها بی‌صدا در `localStorage` با کلید `memorial_mohammaddoost-haftom-1403` ذخیره می‌شوند. سه پیام نمونه نیز برای حالت محلی نمایش داده می‌شوند.

## 📦 دیپلوی
- **GitHub Pages:** Settings → Pages → شاخه‌ی اصلی و پوشه‌ی root
- **Vercel:** Import repository → Deploy
- **Netlify:** پوشه را Drag & Drop کنید

صفحه با باز کردن مستقیم `index.html` هم کار می‌کند. برای قابلیت آنلاین Supabase و اشتراک‌گذاری عمومی، آن را روی یکی از سرویس‌های بالا منتشر کنید.

## 🛠️ ساختار
```text
index.html
assets/
├── portrait.jpg
├── audio.mp3
├── bg-atmosphere.webp
├── ornament-frame.webp
├── floral-divider.webp
└── portrait-placeholder.webp
```

## 📄 لایسنس
MIT — استفاده‌ی آزاد برای خانواده‌ها 🖤

---

# 🕊️ Digital Memorial — Seyyed Jafar Mohammaddoost

> Seventh-day memorial — Friday, 3 Mehr — Abedin-Zadeh Restaurant

A zero-build, single-file Persian memorial invitation designed mobile-first for sharing through WhatsApp and Telegram. The envelope interaction, local assets, audio gesture, animated portrait frame, structured event details, map links, and condolence wall are all contained in `index.html`.

## Quick setup
1. Put the family photo at `assets/portrait.jpg`.
2. Put a respectful MP3 at `assets/audio.mp3`.
3. Open `index.html`, or deploy the folder as a static site.
4. Optional: add Supabase URL and anon key to the documented `CONFIG` object.

The page has no build step and falls back silently to localStorage when Supabase or audio is unavailable. Keep family media local and review the Supabase RLS policies before public deployment.

## License
MIT.
