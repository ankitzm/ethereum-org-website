---
title: آینده‌نگری در اتریوم
description: این ارتقاها اتریوم را به عنوان لایه پایه مقاوم و غیرمتمرکز برای هرآنچه در آینده پیش آید تقویت می‌کند.
lang: fa
image: /images/roadmap/roadmap-future.png
alt: "نقشه‌ راه اتریوم"
template: roadmap
---

برای مقیاس‌پذیری یا ایمن‌سازی اتریوم در کوتاه‌مدت، به برخی از بخش‌های نقشۀ راه الزاماً نیازی نیست، ولی این بخش‌ها می‌توانند ثبات و قابلیت اطمینان را در اتریوم برای آینده تقویت کنند.

## مقاومت کوانتومی {#quantum-resistance}

زمانی که محاسبات کوانتومی به واقعیت تبدیل شود، برخی از [رمزنگاری‌های](/glossary/#cryptography) کنونی که اتریوم را ایمن ساخته‌اند به خطر می‌افتند. اگرچه احتمالاً ده‌ها سال طول بکشد تا کامپیوترهای کوانتومی تهدیدی واقعی برای رمزنگاری مدرن به‌شمار آیند، اتریوم در طول این مدت به گونه‌ای ساخته می‌شود که برای قرن‌های آتی ایمن باشد. این بدین معنی است که [مقاومت کوانتومی اتریوم](https://consensys.net/blog/developers/how-will-quantum-supremacy-affect-blockchain/) به زودی محتمل خواهد بود.

چالش پیش روی توسعه دهندگان اتریوم این است که پروتکل [اثبات سهام](/glossary/#pos) کنونی بر یک طرح امضای بسیار کارآمد به نام BLS برای گردآوری آرا در [بلوک](/glossary/#block) معتبر متکی است. این مدل امضا در برابر کامپیوترهای کوانتومی شکننده است، اما جایگزین‌های مقاوم در برابر کوانتوم نیز آنچنان کارآمد نیستند.

[مدل‌های تعهدی KZG‏](/roadmap/danksharding/#what-is-kzg) که در چندین جا در سرتاسر شبکۀ اتریوم برای تولید رازهای رمزنگاری‌شده استفاده می‌شوند از جمله مدل‌هایی هستند که آسیب‌پذیریشان در برابر کوانتوم شناخته‌شده است. درحال حاضر، این مسئله با استفاده از «تنظیمات قابل اعتماد» دور زده می‌شود، یعنی جایی که در آن بسیاری از کاربران قابلیت انتخاب تصادفی را ایجاد می‌کنند و انجام مهندسی معکوس روی این قابلیت توسط کامپیوترهای کوانتومی امکان‌پذیر نیست. با این حال، راه‌حل ایده‌آل این است که خیلی ساده به جای این روش‌ها از رمزنگاری ایمن کوانتومی استفاده شود. دو رویکرد پیشرو در این زمینه وجود دارند که می‌توانند جایگزین‌های کارآمدی برای مدل BLS باشند: مدل‌های امضا به نام‌های [STARK-based](https://hackmd.io/@vbuterin/stark_aggregation) و [lattice-based](https://medium.com/asecuritysite-when-bob-met-alice/so-what-is-lattice-encryption-326ac66e3175). **اینها هنوز در مرحله تحقیق و نمونه سازی هستند**.

<ButtonLink variant="outline-color" href="/roadmap/danksharding#what-is-kzg"> درباره KZG و تنظیمات مورد اعتماد بخوانید</ButtonLink>

## شبکۀ اتریومِ ساده‌تر و کارآمدتر {#simpler-more-efficient-ethereum}

پیچیدگیِ یک شبکه فرصت‌های زیادی برای انواع باگ‌ها یا آسیب‌پذیری‌ها ایجاد می‌کند که می‌تواند سبب سوءاستفاده مهاجمان شود. بنابراین، بخشی از نقشۀ راه را ساده‌سازیِ شبکۀ اتریوم و حذف کدهایی تشکیل می‌دهد که از طریق به‌روزرسانی‌های مختلف گریبان‌گیر شبکه شده‌اند ولی دیگر نه مورد نیاز هستند و نه می‌توان آنها را بهبود بخشید. نگهداری و استدلال یک پایگاه کد کوچک‌تر و ساده‌تر برای توسعه‌دهندگان آسان‌تر است.

چندین به‌روزرسانی در راه است تا روی [ماشین مجازی اتریوم (EVM)](/developers/docs/evm) اعمال شود و آن را ساده‌تر و کارآمدتر کند. یکی از این به‌روزرسانی‌ها [حذف کد عملیاتی SELFDESTRUCT‏](https://hackmd.io/@vbuterin/selfdestruct) است – دستوری که به ندرت مورد استفاده قرار می‌گیرد و دیگر مورد نیاز نیست و حتی در برخی از شرایط استفاده از آن می‌تواند خطرناک هم باشد، مخصوصاً زمانی که با سایر ارتقاهای مدل‌های ذخیره‌سازی اتریوم در آینده ترکیب شود. [کاربرهای اتریوم](/glossary/#consensus-client) همچنین از برخی از انواع تراکنش‌های قدیمی پشتیبانی می‌کنند که اکنون می‌توانند به طور کامل حذف شوند. نحوه محاسبه [گس](/glossary/#gas) نیز می تواند بهبود یابد و روش های کارآمدتری برای محاسبات زیربنای برخی عملیات رمزنگاری ارائه شود.

به همین ترتیب، به‌روزرسانی‌هایی وجود دارند که می‌توانند برای بخش‌های دیگری از کلاینت‌های امروزی اتریوم اعمال شوند. یک مثال در رابطه با این موضوع این است که در حال حاضر کلاینت‌های اجرا و اجماع از نوع متفاوتی از فشرده‌سازی داده‌ها استفاده می‌کنند. هنگامی که یکپارچه‌سازیِ طرح فشرده‌سازی در کل شبکه انجام بگیرد، اشتراک‌گذاریِ داده‌ها بین کلاینت‌ها بسیار ساده‌تر و شهودی‌تر خواهد شد.

## پیشرفت فعلی {#current-progress}

بسیاری از ارتقاهای مورد نیاز برای اتریومِ مقاوم در آینده **هنوز در مرحله تحقیقاتی هستند و ممکن است چندین سال تا اجرای آن فاصله داشته باشد**. به‌روزرسانی‌هایی مانند حذف SELFDESTRUCT و هماهنگ کردن طرح فشرده‌سازی مورد استفاده در کاربرهای لایه‌های اجرا و اجماع احتمالاً زودتر از رمزنگاری مقاوم در برابر کوانتوم انجام می‌شوند.

**بیشتر بخوانید**

- [گاز](/developers/docs/gas)
- [ماشین مجازی اتریوم (EVM)](/developers/docs/evm)
- [ساختارهای داده](/developers/docs/data-structures-and-encoding)
