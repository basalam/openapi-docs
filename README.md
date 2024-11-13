<link rel="stylesheet" href="./assets/fonts/Estedad-stylesheet.css" />
<link rel="stylesheet" href="./assets/css/highlight/default.min.css" />
<!-- <script src="./assets/js/highlight/highlight.min.js"></script> -->

<div style="text-align: center;">
  <br>
  <img class="oI3ssn" src="https://basalam.com/img/basalam-logotype.svg" alt="باسلام">
  </div>
  <br>
  <div align="right" dir="rtl" style="font-family: 'Estedad', -apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,Arial,sans-serif,'Apple Color Emoji','Segoe UI Emoji','Segoe UI Symbol', sans-serif; text-align: justify; direction: rtl;">
  <p>
  <b style="font-weight:bold">سلام ای.پی.آی (<a href="https://developers.basalam.com" target="_blank">Basalam API</a>)</b> مجموعه‌ای از api‌های سرویس‌های باسلام هست که امکان دسترسی به سرویس‌های باسلام را برای شما فراهم می‌کند. به واسطه api‌های ارائه شده شما می‌توانید با استفاده از استاندارد OAuth2 به اطلاعات کاربران اعم از غرفه‌داران و مشتریان دسترسی پیدا کنید و برنامه‌های خود را بر پایه آنها توسعه دهید.
  در این مستندات سعی شده است که توضیحات کاملی برای اتصال به api‌ها داده شود.
  </p>
  <hr>
  <ul dir="rtl">
    <li> شروع
      <ul>
        <li><a href="#%F0%9F%9A%80-%D8%B4%D8%B1%D9%88%D8%B9-%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%AA%D9%88%DA%A9%D9%86-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1">دریافت توکن</a></li>
        <li><a href="#%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%D8%A7%D8%AA-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1">دریافت اطلاعات کاربر</a></li>
        <li><a href="#%D9%84%DB%8C%D8%B3%D8%AA-api%D9%87%D8%A7">لیست APIها</a></li>
      </ul>
    </li>
  </ul>
  <hr>
  <p>
  <h2 style="font-weight:bold">🚀 شروع (دریافت توکن کاربر)</h2> ابتدا باید از <a href="https://developers.basalam.com/clients" target="_new">اینجا</a> یک کلاینت ایجاد کنید.
  کلاینت همان برنامه‌ی مدنظر شما جهت پیاده سازی است: <small><a href="https://developers.basalam.com/authorization#%D8%A7%DB%8C%D8%AC%D8%A7%D8%AF-%DA%A9%D9%84%D8%A7%DB%8C%D9%86%D8%AA" target="_blank">(راهنما)</a></small>
  <br>
  <ul dir="rtl">
    <li>روی دکمه <b style="font-weight:bold">ایجاد کلاینت</b> کلیک کنید.</li>
    <li><b style="font-weight:bold">name:</b> نام کلاینت (برنامه) خود را وارد کنید.</li>
    <li><b style="font-weight:bold">redirect_url:</b> آدرسی از برنامهٔ شما که کاربر بعد از صدور (یا رد) اجازه‌های درخواستی به آن هدایت شود. <small><a href="https://developers.basalam.com/authorization#%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%AF%D8%B3%D8%AA%D8%B1%D8%B3%DB%8C-%D8%A7%D8%B2-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1" target="_blank">(توضیحات بیشتر)</a></small></li>
  </ul>
  </p>
  <p>
  بعد از ایجاد کلاینت خود، برای احراز هویت کاربران و گرفتن توکن کاربر لازم است دکمه ای در برنامه‌ی خود ایجاد کنید که کاربران را به لینکی با ساختار زیر هدایت میکند:<br>
  <div style="text-align:left;" dir="ltr">
  <code dir="ltr">https://basalam.com/accounts/sso?client_id=[client_id]&scope=[scope]&redirect_uri=[client_redirect_uri]&state=[state]</code>
  </div>
  <ul dir="rtl">
    <li><b style="font-weight:bold">client_id:</b> آی دی کلاینتی که ایجاد کردید. در <a href="https://developers.basalam.com/clients" target="_new">این صفحه</a> قابل مشاهده است.</li>
    <li><b style="font-weight:bold">scope:</b> رشته‌ای از <a href="https://developers.basalam.com/scopes" target="_blank">دسترسی‌های</a> درخواستی که با کاما "," یا فاصله جدا شده‌اند.</li>
    <li><b style="font-weight:bold">redirect_uri:</b>  آدرسی که کاربر بعد از اعطای دسترسی به آن هدایت می‌شود، این آدرس باید همان آدرسی باشد که در ایجاد کلاینت قرار داده‌اید.</li>
    <li><b style="font-weight:bold">state:</b> یک رشته دلخواه که در درخواست‌های بعدی به کلاینت شما ارسال می‌شود که براساس آن کاربر بعد از ورود موفق به صفحه‌ی خاصی از برنامه شما هدایت شود یا اکشن خاصی برای کاربر انجام شود. (این پارامتر اختیاری است)</li>
  </ul>
  </p>
  <p>
  در مرحله بعد که کاربر به لینک redirect_uri شما هدایت شد، اگر اجازه دسترسی را تایید کرده باشد دو پارامتر زیر برای شما ارسال می شود:
  <ul dir="rtl">
    <li><b style="font-weight:bold">code:</b> کد یک‌بار مصرف ایجاد شده توسط سرویس احراز هویت به منظور دریافت توکن</li>
    <li><b style="font-weight:bold">state:</b>  مقدار دلخواهی که در مرحله قبل ارسال کرده‌اید</li>
  </ul>
  حالا باید با استفاده از code دریافتی ریکوئستی به فرمت زیر ارسال کنید که توکن کاربر را دریافت کنید:
  <br>
  <div style="text-align:left;direction: ltr;" dir="ltr">
  <pre dir="ltr"><code dir="ltr">curl --request POST \
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
  </code></pre>
  </div>
  <ul dir="rtl">
    <li><b style="font-weight:bold">client_id:</b> آی دی کلاینتی که ایجاد کردید. در <a href="https://developers.basalam.com/clients" target="_new">این صفحه</a> قابل مشاهده است.</li>
    <li><b style="font-weight:bold">client_secret:</b>  رمز اختصاص داده شده به کلاینت. در <a href="https://developers.basalam.com/clients" target="_new">این صفحه</a> قابل مشاهده است.</li>
    <li><b style="font-weight:bold">redirect_uri:</b>  آدرسی که کاربر بعد از اعطای دسترسی به آن هدایت می‌شود، این آدرس باید همان آدرسی باشد که در ایجاد کلاینت قرار داده‌اید.</li>
    <li><b style="font-weight:bold">code:</b> کد یکبار مصرفی که به آدرس ریدارکت شما ارسال شده است.</li>
  </ul>
  در صورت صحیح بودن اطلاعات، پاسخ دریافتی به صورت زیر است:
  <div style="text-align:left;direction: ltr;" dir="ltr">
  <pre><code>{
    "token_type": "Bearer",
    "expires_in": 31622400,
    "access_token": "...",
    "refresh_token": "..."
  }
  </code></pre>
  </div>
  <ul dir="rtl">
    <li><b style="font-weight:bold">token_type:</b> نوع توکن برگشتی، که نوع Bearer هست.</li>
    <li><b style="font-weight:bold">expires_in:</b> زمان معتبر بودن توکن به ثانیه</li>
    <li><b style="font-weight:bold">access_token:</b> توکن کاربر</li>
    <li><b style="font-weight:bold">refresh_token:</b> توکنی برای دریافت توکن جدید زمانی که توکن کاربر منقضی شده</li>
  </ul>
  پس از دریافت توکن، آن را نزد خود ذخیره کنید و برای درخواست های بعدی آنرا در هدر Authorization ارسال کنید. 
  برای اطلاعات بیشتر <a href="https://developers.basalam.com/authorization#%D9%85%D8%B1%D8%AD%D9%84%D9%87-%D8%B3%D9%88%D9%85-%D8%AF%D8%B1%DB%8C%D8%A7%D9%81%D8%AA-%D8%A7%D8%B7%D9%84%D8%A7%D8%B9%D8%A7%D8%AA-%DA%A9%D8%A7%D8%B1%D8%A8%D8%B1" target="_blank">این صفحه</a> را مشاهده کنید.
  </p>

  <h2>دریافت اطلاعات کاربر</h2>
  <p dir="rtl">
  پس از دریافت توکن کاربر، اولین قدم این است که اطلاعات کاربر را دریافت کنید و موارد مورد نیاز مانند شناسه کاربر (id) و شناسه غرفه کاربر (vendor->id) را برای درخواست های بعدی ذخیره کنید:

  <pre dir="ltr"><code dir="ltr">curl --request GET \
    --url https://core.basalam.com/v3/users/me \
    --header 'Accept: application/json'
    --header 'Authorization: Bearer [TOKEN]'
  </code></pre>

  بجای <code>[TOKEN]</code> باید توکن کاربر را که در مراحل قبل بعد از تایید دسترسی توسط کاربر دریافت کردید را قرار دهید.
  <br>
  نمونه ریسپانس:
  <pre dir="ltr"><code dir="ltr">{
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
  </code></pre>
  </p>

  <h2>لیست APIها</h2>
  <p dir="rtl">
  <span>معماری باسلام براساس میکروسرویس است و هر بخش آن وبسرویس‌های مجزای خود را دارد که در لیست زیر دردسترس هستند:</span>
  <ul dir="rtl">
    <li><a href="https://developers.basalam.com/services#-%D9%87%D8%B3%D8%AA%D9%87-core" target="_blank">Core (هسته)</a></li>
    <li><a href="https://developers.basalam.com/services#-%DA%A9%DB%8C%D9%81-%D9%BE%D9%88%D9%84-wallet" target="_blank">Wallet (کیف پول)</a></li>
    <li><a href="https://developers.basalam.com/services#-%D8%B3%D9%81%D8%A7%D8%B1%D8%B4-order" target="_blank">Order (سفارش)</a></li>
    <li><a href="https://developers.basalam.com/services#-%D8%B1%D9%87%DA%AF%DB%8C%D8%B1%DB%8C-%D8%B3%D9%81%D8%A7%D8%B1%D8%B4-order-processing" target="_blank">Order Processing (رهگیری سفارش)</a></li>
    <li><a href="https://developers.basalam.com/services#-%D8%AC%D8%B3%D8%AA%D8%AC%D9%88-search" target="_blank">Search (جستجو)</a></li>
  </ul>
  </p>


</div>

<!-- <script>hljs.highlightAll();</script> -->





