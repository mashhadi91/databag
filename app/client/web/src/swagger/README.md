# 🎨 Swagger Customization - Ako WorkFlow

این پوشه شامل فایل‌های سفارشی‌سازی Swagger است.

---

## 📁 ساختار فایل‌ها

```
swagger/
├── swagger-custom.css      # فایل CSS سفارشی
├── fonts/                  # فونت‌های فارسی محلی
│   ├── Vazir.eot           # فونت Regular
│   ├── Vazir.ttf
│   ├── Vazir.woff
│   ├── Vazir.woff2
│   ├── Vazir-Thin.*        # فونت نازک (وزن 100)
│   ├── Vazir-Light.*       # فونت سبک (وزن 300)
│   ├── Vazir-Medium.*      # فونت متوسط (وزن 500)
│   └── Vazir-Bold.*        # فونت ضخیم (وزن 700)
└── README.md               # این فایل
```

---

## ✨ ویژگی‌های CSS

### 1️⃣ **فونت‌های محلی (Local Fonts)**

همه فونت‌ها به صورت محلی از پوشه `fonts/` بارگذاری می‌شوند:

```css
@font-face {
    font-family: 'Vazir';
    src: url('./fonts/Vazir.woff2') format('woff2'),
         url('./fonts/Vazir.woff') format('woff'),
         url('./fonts/Vazir.ttf') format('truetype');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}
```

### 2️⃣ **وزن‌های مختلف فونت**

| Font Weight | وزن | استفاده |
|-------------|-----|---------|
| 100 | Thin | متن‌های خیلی نازک |
| 300 | Light | متن‌های سبک |
| 400 | Regular | متن‌های عادی (پیش‌فرض) |
| 500 | Medium | متن‌های متوسط |
| 700 | Bold | متن‌های ضخیم و عناوین |

### 3️⃣ **RTL Support**

```css
/* متن‌های فارسی - راست‌چین */
.opblock-description-wrapper .renderedMarkdown {
    direction: rtl;
    text-align: right;
}

/* کدها - چپ‌چین */
.swagger-ui pre,
.swagger-ui code {
    direction: ltr !important;
    text-align: left !important;
}
```

---

## 🚀 نحوه استفاده

### 1. Configuration در `PipelineConfigurationExtensions.cs`

```csharp
app.UseSwaggerUI(options =>
{
    // Inject custom CSS
    options.InjectStylesheet("./swagger-custom.css?v=2");
    
    // سایر تنظیمات...
});
```

### 2. Static Files در `Program.cs`

```csharp
app.UseStaticFiles(); // قبل از ConfigurePipeline()
```

### 3. مسیرهای فونت

فونت‌ها با مسیر نسبی از CSS بارگذاری می‌شوند:

```
swagger-custom.css  →  ./fonts/Vazir.woff2
```

معادل:

```
/swagger/swagger-custom.css  →  /swagger/fonts/Vazir.woff2
```

---

## 📦 فرمت‌های فونت

### اولویت بارگذاری:

1. **WOFF2** - فشرده‌ترین (بهترین عملکرد)
2. **WOFF** - پشتیبانی گسترده
3. **TTF** - سازگاری بیشتر
4. **EOT** - IE قدیمی

```css
src: url('./fonts/Vazir.eot');  /* IE9 Compat Modes */
src: url('./fonts/Vazir.eot?#iefix') format('embedded-opentype'),  /* IE6-IE8 */
     url('./fonts/Vazir.woff2') format('woff2'),  /* Modern Browsers */
     url('./fonts/Vazir.woff') format('woff'),    /* Modern Browsers */
     url('./fonts/Vazir.ttf') format('truetype'); /* Safari, Android */
```

---

## 🎯 مزایای استفاده از فونت‌های محلی

✅ **سرعت بالا:** بدون نیاز به درخواست خارجی (CDN)  
✅ **بدون وابستگی به اینترنت:** کار کردن Offline  
✅ **کنترل کامل:** نسخه فونت ثابت  
✅ **امنیت بیشتر:** بدون CORS یا Security Issues  
✅ **Privacy:** بدون tracking توسط CDN  

---

## 🔧 سفارشی‌سازی

### تغییر فونت پیش‌فرض:

```css
body,
.swagger-ui {
    font-family: 'Vazir', 'YourFont', sans-serif !important;
}
```

### تغییر وزن فونت‌های خاص:

```css
/* عناوین با فونت Bold */
.swagger-ui .info .title {
    font-weight: 700;
}

/* توضیحات با فونت Light */
.swagger-ui .info .description {
    font-weight: 300;
}
```

### اضافه کردن فونت جدید:

1. فونت را در پوشه `fonts/` قرار دهید
2. `@font-face` را در `swagger-custom.css` اضافه کنید
3. از فونت در `font-family` استفاده کنید

---

## 📊 اندازه فایل‌ها

| Format | Size | Support |
|--------|------|---------|
| WOFF2 | ~37KB | ✅ Modern (95%+) |
| WOFF | ~47KB | ✅ Good (98%+) |
| TTF | ~82KB | ✅ Universal |
| EOT | ~82KB | ⚠️ IE Only |

**توصیه:** WOFF2 برای عملکرد بهینه

---

## 🐛 رفع مشکلات

### فونت بارگذاری نمی‌شود

1. ✅ مسیر فونت را بررسی کنید: `./fonts/Vazir.woff2`
2. ✅ Console مرورگر را چک کنید (F12)
3. ✅ `UseStaticFiles()` را در `Program.cs` فعال کنید
4. ✅ Cache مرورگر را پاک کنید (Ctrl+Shift+R)

### فونت به درستی نمایش نداده نمی‌شود

```css
/* اضافه کردن !important */
body {
    font-family: 'Vazir', sans-serif !important;
}
```

### مشکل CORS

فونت‌های محلی CORS ندارند ✅

اگر از CDN استفاده می‌کنید:

```css
@font-face {
    font-family: 'Vazir';
    src: url('https://cdn.example.com/font.woff2') format('woff2');
    /* نیاز به CORS Header دارد */
}
```

---

## 🔍 بررسی بارگذاری فونت

### در Chrome DevTools:

1. F12 → Network
2. فیلتر Font
3. بررسی Status Code:
   - ✅ 200 OK - موفق
   - ❌ 404 - مسیر اشتباه
   - ❌ CORS Error - مشکل CORS

### در Console:

```javascript
// بررسی فونت بارگذاری شده
document.fonts.check("12px Vazir");  // true یا false
```

---

## 📈 بهینه‌سازی

### 1. استفاده از `font-display: swap`

```css
@font-face {
    font-family: 'Vazir';
    src: url('./fonts/Vazir.woff2') format('woff2');
    font-display: swap;  /* نمایش فونت پیش‌فرض تا بارگذاری */
}
```

### 2. Preload فونت‌های مهم

در `_Host.cshtml` یا HTML اصلی:

```html
<link rel="preload" href="/swagger/fonts/Vazir.woff2" as="font" type="font/woff2" crossorigin>
```

### 3. فقط فونت‌های لازم

اگر فقط Regular و Bold نیاز دارید:

```css
/* حذف Thin, Light, Medium */
@font-face { ... } /* Regular */
@font-face { ... } /* Bold */
```

---

## 📚 منابع

- [Vazir Font on GitHub](https://github.com/rastikerdar/vazir-font)
- [Web Font Best Practices](https://web.dev/font-best-practices/)
- [font-display Property](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display)

---

## 📝 Changelog

### v2.0.0 - 2025-10-04

- ✅ استفاده از فونت‌های محلی (Local Fonts)
- ✅ حذف وابستگی به CDN
- ✅ پشتیبانی از 5 وزن فونت (Thin, Light, Regular, Medium, Bold)
- ✅ بهینه‌سازی با `font-display: swap`
- ✅ پشتیبانی کامل از تمام مرورگرها
- ✅ بهبود عملکرد و سرعت بارگذاری

### v1.0.0 - 2025-10-04

- ✅ استفاده از CDN (Vazirmatn + IRANSans)
- ✅ RTL Support
- ✅ Basic Typography

---

## 📄 License

فونت Vazir تحت لایسنس **OFL-1.1** منتشر شده است.

---

**ساخته شده با ❤️ برای Ako WorkFlow**
