<link rel="stylesheet" href="./assets/fonts/Estedad-stylesheet.css" />


<p align="center">
  <img src="https://basalam.com/img/basalam-logotype.svg" alt="باسلام">
</p>

# سلام ای.پی.آی (Basalam API)

**[Basalam API](https://developers.basalam.com)** مجموعه‌ای از api‌های سرویس‌های باسلام هست که امکان دسترسی به سرویس‌های باسلام را برای شما فراهم می‌کند. به واسطه api‌های ارائه شده شما می‌توانید با استفاده از استاندارد OAuth2 به اطلاعات کاربران اعم از غرفه‌داران و مشتریان دسترسی پیدا کنید و برنامه‌های خود را بر پایه آنها توسعه دهید.

در این مستندات سعی شده است که توضیحات کاملی برای اتصال به api‌ها داده شود.

---

## فهرست مطالب

* شروع
  * [دریافت توکن](#-شروع-دریافت-توکن-کاربر)
  * [دریافت اطلاعات کاربر](#دریافت-اطلاعات-کاربر)
  * [لیست APIها](#لیست-apiها)

---

## 🚀 شروع (دریافت توکن کاربر)

ابتدا باید از [اینجا](https://developers.basalam.com/clients) یک کلاینت ایجاد کنید.
کلاینت همان برنامه‌ی مدنظر شما جهت پیاده سازی است: [(راهنما)](https://developers.basalam.com/authorization#%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%DA%A9%D9%84%D8%A7%DB%8C%D9%86%D8%AA)

* روی دکمه **ایجاد کلاینت** کلیک کنید.
* **name:** نام کلاینت (برنامه) خود را وارد کنید.
* **redirect_url:** آدرسی از برنامهٔ شما که کاربر بعد از صدور (یا رد) اجازه‌های درخواستی به آن هدایت شود. [(توضیحات بیشتر)](https://developers.basalam.com/authorization#%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%AF%D8%B3%D8%AA%D8%B1%D8%B3%DB%8C-%D8%A7%D8%B2-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1)

بعد از ایجاد کلاینت خود، برای احراز هویت کاربران و گرفتن توکن کاربر لازم است دکمه ای در برنامه‌ی خود ایجاد کنید که کاربران را به لینکی با ساختار زیر هدایت میکند:

```
https://basalam.com/accounts/sso?client_id=[client_id]&scope=[scope]&redirect_uri=[client_redirect_uri]&state=[state]
```

* **client_id:** آی دی کلاینتی که ایجاد کردید. در [این صفحه](https://developers.basalam.com/clients) قابل مشاهده است.
* **scope:** رشته‌ای از [دسترسی‌های](https://developers.basalam.com/scopes) درخواستی که با کاما "," یا فاصله جدا شده‌اند.
* **redirect_uri:** آدرسی که کاربر بعد از اعطای دسترسی به آن هدایت می‌شود، این آدرس باید همان آدرسی باشد که در ایجاد کلاینت قرار داده‌اید.
* **state:** یک رشته دلخواه که در درخواست‌های بعدی به کلاینت شما ارسال می‌شود که براساس آن کاربر بعد از ورود موفق به صفحه‌ی خاصی از برنامه شما هدایت شود یا اکشن خاصی برای کاربر انجام شود. (این پارامتر اختیاری است)

در مرحله بعد که کاربر به لینک redirect_uri شما هدایت شد، اگر اجازه دسترسی را تایید کرده باشد دو پارامتر زیر برای شما ارسال می شود:

* **code:** کد یک‌بار مصرف ایجاد شده توسط سرویس احراز هویت به منظور دریافت توکن
* **state:** مقدار دلخواهی که در مرحله قبل ارسال کرده‌اید

حالا باید با استفاده از code دریافتی ریکوئستی به فرمت زیر ارسال کنید که توکن کاربر را دریافت کنید:

```bash
curl --request POST \
  --url https://auth.basalam.com/oauth/token \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json' \
  --data '{
        "grant_type" : "authorization_code",
        "client_id" : "[client_id]",
        "client_secret" : "[client_secret]",
        "redirect_uri" : "[redirect_uri]",
        "code" : "[code]"
}'
```

* **client_id:** آی دی کلاینتی که ایجاد کردید. در [این صفحه](https://developers.basalam.com/clients) قابل مشاهده است.
* **client_secret:** رمز اختصاص داده شده به کلاینت. در [این صفحه](https://developers.basalam.com/clients) قابل مشاهده است.
* **redirect_uri:** آدرسی که کاربر بعد از اعطای دسترسی به آن هدایت می‌شود، این آدرس باید همان آدرسی باشد که در ایجاد کلاینت قرار داده‌اید.
* **code:** کد یکبار مصرفی که به آدرس ریدارکت شما ارسال شده است.

در صورت صحیح بودن اطلاعات، پاسخ دریافتی به صورت زیر است:

```json
{
  "token_type": "Bearer",
  "expires_in": 31622400,
  "access_token": "...",
  "refresh_token": "..."
}
```

* **token_type:** نوع توکن برگشتی، که نوع Bearer هست.
* **expires_in:** زمان معتبر بودن توکن به ثانیه
* **access_token:** توکن کاربر
* **refresh_token:** توکنی برای دریافت توکن جدید زمانی که توکن کاربر منقضی شده

پس از دریافت توکن، آن را نزد خود ذخیره کنید و برای درخواست های بعدی آنرا در هدر Authorization ارسال کنید.
برای اطلاعات بیشتر [این صفحه](https://developers.basalam.com/authorization#%D9%85%D8%B1%D8%AD%D9%84%D9%87-%D8%B3%D9%88%D9%85-%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%D8%A7%D8%AA-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1) را مشاهده کنید.

## دریافت اطلاعات کاربر

پس از دریافت توکن کاربر، اولین قدم این است که اطلاعات کاربر را دریافت کنید و موارد مورد نیاز مانند شناسه کاربر (id) و شناسه غرفه کاربر (vendor->id) را برای درخواست های بعدی ذخیره کنید:

```bash
curl --request GET \
  --url https://core.basalam.com/v3/users/me \
  --header 'Accept: application/json'
  --header 'Authorization: Bearer [TOKEN]'
```

بجای `[TOKEN]` باید توکن کاربر را که در مراحل قبل بعد از تایید دسترسی توسط کاربر دریافت کردید را قرار دهید.

نمونه ریسپانس:

```json
{
  "id": 0, # شناسه عددی کاربر
  "hash_id": "string", # شناسه هش کاربر
  "username": "string", # نام کاربری
  "name": "string", # نام کامل
  "avatar": { # آبجکت عکس پروفایل
    "id": 0, # کد فایل عکس
    "original": "string", # آدرس عکس در سایز اصلی
    "xs": "string", # آدرس عکس در سایز خیلی کوچک
    "sm": "string", # آدرس عکس در سایز اسمال
    "md": "string", # آدرس عکس در سایز مدیوم
    "lg": "string" # آدرس عکس در سایز لارج
  },
  "marked_type": {
    "name": "string",
    "value": 0,
    "description": "string"
  },
  "user_follower_count": 0,
  "user_following_count": 0,
  "gender": {
    "name": "string",
    "value": 0,
    "description": "string"
  },
  "bio": "string",
  "city": {
    "name": "string",
    "value": 0,
    "province": {
      "name": "string",
      "value": 0,
      "description": "string"
    }
  },
  "created_at": "string",
  "last_activity": "string",
  "referral_journey_enum": {
    "name": "string",
    "value": 0,
    "description": "string"
  },
  "is_banned_in_social": true,
  "ban_user": {},
  "vendor": {
    "id": 0,
    "identifier": "string",
    "title": "string",
    "description": "string",
    "is_active": true,
    "free_shipping_to_iran": 0,
    "free_shipping_to_same_city": 0,
    "worth_buy": "string",
    "created_at": "string",
    "activated_at": "string",
    "order_count": 0,
    "status": 0
  },
  "email": "string",
  "birthday": "string",
  "national_code": "string",
  "mobile": "string",
  "credit_card_number": "string",
  "credit_card_owner": "string",
  "foreign_citizen_code": "string",
  "user_sheba_number": "string",
  "user_sheba_owner": "string",
  "bank_information": "string",
  "bank_information_owner": "string",
  "info_verification_status": {
    "name": "string",
    "value": 0,
    "description": "string"
  },
  "referrer_user_id": 0
}
```

## لیست APIها

معماری باسلام براساس میکروسرویس است و هر بخش آن وبسرویس‌های مجزای خود را دارد که در لیست زیر دردسترس هستند:

* [Core (هسته)](https://developers.basalam.com/services#-%D9%87%D8%B3%D8%AA%D9%87-core)
* [Wallet (کیف پول)](https://developers.basalam.com/services#-%DA%A9%DB%8C%D9%81-%D9%BE%D9%88%D9%84-wallet)
* [Order (سفارش)](https://developers.basalam.com/services#-%D8%B3%D9%81%D8%A7%D8%B1%D8%B4-order)
* [Order Processing (رهگیری سفارش)](https://developers.basalam.com/services#-%D8%B1%D9%87%DA%AF%DB%8C%D8%B1%DB%8C-%D8%B3%D9%81%D8%A7%D8%B1%D8%B4-order-processing)
* [Search (جستجو)](https://developers.basalam.com/services#-%D8%AC%D8%B3%D8%AA%D8%AC%D9%88-search)

