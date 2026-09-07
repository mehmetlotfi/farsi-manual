<div dir="rtl" lang="fa" style="text-align: right;">

# آشنایی کامل با دستور wget در لینوکس

# <u>سخن مولف</u>

**در راستای صفحه‌آرایی و تدوین این مقاله، از نرم‌افزار آزاد و متن‌بازِ GNU TeXMacs ذیل پروانه عمومی همگانی گنو GNU General Public License (GNU GPL) نسخه ۳ استفاده گردیده است و خود این اثر نیز تحت پروانه مستندات آزاد گنو (GNU GFDL) نسخه 1.3 و بالاتر منتشر خواهد گردید.**

**بر اساس اعتقاد راسخ قلبی به فلسفه نرم‌افزار آزاد و با هدف حمایت و ترویج عملیِ استفاده از این نرم‌افزارها به‌جای بدیل‌های غیرآزاد و انحصاری، تعیین و اعلام ابزارهای دخیل در تولید یک اثر علمی، دیگر صرفاً یک گزاره فنی یا تشریفاتی نیست، بلکه بیانی روشن از تعهد اخلاقی، مسئولیت اجتماعی و انتخاب آگاهانه مؤلف به‌شمار می‌آید. فلسفه نرم‌افزار آزاد، فراتر از دسترسی رایگان، بر چهار آزادی اساسی استوار است: آزادی اجرا برای هر هدف، آزادی مطالعه کد منبع، آزادی توزیع نسخه‌های اصلی و آزادی انتشار نسخه‌های بهبودیافته — که همگی زمینه‌ساز شفافیت، همکاری و پیشرفت جمعی در عرصه دانش هستند. نرم‌افزار مذکور در این مقاله، یعنی GNU TeXMacs، با تکیه بر شروط صریح پروانه عمومی همگانی گنو (GNU GPL) نسخه۳، این تضمین را ارائه می‌دهد که کاربریِ آن نه‌تنها مستلزم پرداخت هیچ‌گونه هزینه مالکیت فکری یا حق‌الامتیازی نیست، بلکه مؤلف را در عین حال ملزم به رعایت شرط بنیادین «همگانی‌سازی مشتق» (Copyleft) در صورت انتشار دوباره یا تغییر اثر می‌سازد؛ شرطی که از انحصارگرایی مجدد جلوگیری کرده و زنجیره اشتراک دانش را استمرار می‌بخشد. تصریح به نسخه خاص مجوز، افزون بر افزایش شفافیت فرایند پژوهش برای خواننده، داوران علمی و ناشران، هرگونه ابهام درباره اصالت، امنیت و قابلیت استناد به ابزار به‌کاررفته را از میان می‌برد و امکان بازتولید دقیق نتایج را برای سایر پژوهشگران فراهم می‌آورد. بدین‌ترتیب، نگارش این بند در مقدمه، به‌منزله اعلامِ تعهدِ روش‌شناختی مؤلف به استفاده از بسترهای آزاد، رایگان و غیرانحصاری در تمام مراحل صفحه‌آرایی و تدوین است؛ رویکردی که نه‌تنها از لحاظ فنی کارآمد، بلکه از حیث اخلاقی در راستای عدالت علمی و مقابله با وابستگی به نرم‌افزارهای بسته و تصمیم‌گیری‌های پشت‌درِ شرکت‌های تجاری قرار می‌گیرد.**

### امیرمحمد لطفی‌خورشید
## شهریور ماه 1405

### حمایت از پروژه

اگر این مطالب برایتان مفید بود، خوشحال می‌شویم که از پروژه حمایت کنید. حمایت شما می‌تواند به‌صورت **مشارکت در نوشتن راهنماهای جدید، گزارش اشکالات، پیشنهاد بهبود، یا حتی معرفی این مخزن به دیگران** باشد. همچنین در صورت تمایل به دونیت، می‌توانید از طریق [این لینک](https://github.com/mehmetlotfi) اقدام فرمایید. هرگونه حمایت، هرچند کوچک، به ما انگیزه می‌دهد تا این مسیر را با کیفیت بیشتری ادامه دهم.

از همراهی شما سپاسگزاریم.

---

### <u>پیش‌گفتار</u>

دانلود یک فایل از خط فرمان در ظاهر کار ساده‌ای است، اما دنیای واقعی خیلی زود پیچیده‌تر می‌شود: اتصال ممکن است نیمه‌کاره قطع شود، فایل بزرگی نیاز به ادامه‌ی دانلود داشته باشد، سرور تغییر مسیر بدهد، گواهی TLS مشکل داشته باشد، صدها نشانی در یک فهرست باشند یا بخواهیم نسخه‌ای آفلاین از چند صفحه‌ی یک وب‌سایت مجاز تهیه کنیم. GNU Wget برای حل همین مسائل ساخته شده است.

Wget یک دریافت‌کننده‌ی غیرتعاملی شبکه است؛ یعنی برای کار کردن به رابط گرافیکی یا حضور دائمی کاربر نیاز ندارد. این ویژگی آن را برای اسکریپت، cron، سرور و نشست‌های راه دور مناسب می‌کند. Wget از HTTP، HTTPS، FTP و در نسخه‌های جدید از FTPS پشتیبانی می‌کند، دانلود را ادامه می‌دهد، retry و timeout دارد، لینک‌ها را دنبال می‌کند و می‌تواند ساختار فایل‌ها را برای مرور آفلاین بازسازی کند.

قدرت دانلود بازگشتی Wget باید مسئولانه استفاده شود. یک فرمان نامناسب می‌تواند هزاران درخواست بفرستد، محتوای عظیمی دریافت کند، از دامنه‌ی هدف خارج شود یا اطلاعاتی را ذخیره کند که اجازه‌ی نگهداری آن‌ها را ندارید. پیش از mirror کردن، مجوز، شرایط استفاده، robots، نرخ درخواست، فضای دیسک و محدوده‌ی دامنه را بررسی کنید.

این کتاب بر GNU Wget نسخه‌ی ۱ تمرکز دارد. Wget2 پروژه‌ای جداگانه با معماری و بعضی گزینه‌های متفاوت است؛ curl نیز ابزار دیگری با فلسفه و دامنه‌ی کاربرد متفاوت محسوب می‌شود. صفحه‌ی man و خروجی help نسخه‌ی نصب‌شده، مرجع نهایی گزینه‌ها هستند.

### این کتاب برای چه کسانی مناسب است

این راهنما برای کاربران تازه‌کار خط فرمان، مدیران سیستم، توسعه‌دهندگان، پژوهشگران و کسانی نوشته شده که می‌خواهند دانلودهای تکرارپذیر و قابل‌کنترل بسازند. مطالب از یک دانلود ساده شروع می‌شوند و تا احراز هویت، TLS، proxy، mirror، WARC و اسکریپت‌نویسی پیش می‌روند.

### در این کتاب چه چیزی خواهید یافت

در فصل ۱، Wget را نصب می‌کنیم، نخستین فایل را می‌گیریم و خروجی، URL و کد بازگشتی را می‌شناسیم.

در فصل ۲، نام و محل فایل، stdout، جلوگیری از بازنویسی، timestamping و ادامه‌ی دانلود را مدیریت می‌کنیم.

در فصل ۳، timeout، retry، محدودیت سرعت، سهمیه، IPv4/IPv6، گزارش سرور و دانلود پس‌زمینه را بررسی می‌کنیم.

در فصل ۴، چند URL، فایل ورودی، header، User-Agent، درخواست POST و cookieها را می‌آموزیم.

در فصل ۵، HTTPS، گواهی، HSTS، احراز هویت، proxy، FTP و FTPS را با ملاحظات امنیتی می‌بینیم.

در فصل ۶، دانلود بازگشتی، requisites صفحه، تبدیل لینک، محدود کردن دامنه و ساخت mirror مسئولانه را پوشش می‌دهیم.

در فصل ۷، فایل‌های پیکربندی wgetrc، logging، WARC، نام‌های بین‌المللی و حریم خصوصی را بررسی می‌کنیم.

در فصل ۸، الگوهای اسکریپت‌نویسی، hash، امضا، خطاها و انتخاب میان wget و ابزارهای مکمل را جمع‌بندی می‌کنیم.

### آنچه لازم دارید

یک سیستم لینوکس یا شبه‌یونیکس، ترمینال، فضای دیسک کافی و دسترسی مجاز به URL هدف لازم است. بعضی مثال‌ها از ابزارهای مکمل مانند sha256sum، gpg و tar استفاده می‌کنند. نمونه‌دامنه‌ی example.com برای آموزش است؛ برای دانلود واقعی، URL مجاز خودتان را جایگزین کنید.

### قراردادهای این کتاب

علامت $ فقط prompt است. مقادیر بزرگ مانند URL، نام فایل، token و مسیر باید با مقدار واقعی جایگزین شوند. دستورها و خروجی‌ها در بلوک چپ‌به‌راست قرار می‌گیرند:

</div>

<div style="text-align:left;">

```
$ wget https://example.com/file.tar.gz
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

گزینه‌ها بر اساس GNU Wget نوشته شده‌اند. هرجا محتوای موجود ممکن است بازنویسی شود یا داده‌ی حساس در خط فرمان قرار گیرد، خطر آن صریحاً توضیح داده خواهد شد.

## فصل ۱

### <u>آشنایی و نخستین دانلود</u>

### ۱.۱ Wget چیست؟

Wget ورودی را از URL می‌گیرد و در حالت عادی بدنه‌ی پاسخ را در فایلی محلی ذخیره می‌کند. نام فایل معمولاً از آخرین بخش مسیر URL به دست می‌آید. برخلاف مرورگر، رابط تعاملی ندارد و می‌تواند حتی پس از خروج کاربر یا در jobهای زمان‌بندی‌شده اجرا شود.

نام Wget از World Wide Web و واژه‌ی get آمده است. نسخه‌ی GNU آن نرم‌افزار آزاد و بخشی از اکوسیستم گنو است.

### ۱.۲ نصب و نسخه

</div>

<div style="text-align:left;">

```
$ command -v wget
$ wget --version
$ wget --help
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

در Debian و Ubuntu:

</div>

<div style="text-align:left;">

```
$ sudo apt install wget
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

در Fedora:

</div>

<div style="text-align:left;">

```
$ sudo dnf install wget
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

### ۱.۳ دانلود یک فایل

</div>

<div style="text-align:left;">

```
$ wget https://example.com/downloads/archive.tar.gz
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

Wget ابتدا DNS، سپس اتصال و TLS را انجام می‌دهد، وضعیت HTTP را گزارش می‌کند و فایل را با نام archive.tar.gz در دایرکتوری جاری می‌نویسد. موفق بودن فرمان را با وجود فایل به‌تنهایی نسنجید؛ کد بازگشتی و در صورت اهمیت، hash یا امضای منتشرشده را بررسی کنید.

### ۱.۴ خواندن خروجی

خروجی معمولاً URL، نشانی مقصد، کد وضعیت، طول پاسخ، نام فایل محلی، نوار پیشرفت، سرعت و زمان را نشان می‌دهد. redirectها نیز در مسیر نمایش داده می‌شوند. گزینه‌ی ‪`-S`‬ headerهای پاسخ سرور را چاپ می‌کند:

</div>

<div style="text-align:left;">

```
$ wget -S https://example.com/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

### ۱.۵ quiet، no-verbose و debug

</div>

<div style="text-align:left;">

```
$ wget -q https://example.com/file.txt
$ wget -nv https://example.com/file.txt
$ wget -d https://example.com/file.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-q`‬ تقریباً همه‌ی پیام‌ها را پنهان می‌کند، ‪`-nv`‬ خلاصه‌تر از حالت عادی است و ‪`-d`‬ اطلاعات فراوان اشکال‌زدایی می‌دهد. debug ممکن است header، cookie یا جزئیات حساس را آشکار کند؛ خروجی آن را بی‌بررسی منتشر نکنید.

### ۱.۶ بررسی بدون دانلود با spider

</div>

<div style="text-align:left;">

```
$ wget --spider -S https://example.com/file.tar.gz
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

حالت spider بررسی می‌کند منبع قابل دسترسی به نظر می‌رسد، اما سرورها ممکن است به HEAD و GET متفاوت پاسخ دهند و لینک محافظت‌شده یا پویا رفتار دیگری داشته باشد. این یک health check کامل نیست.

### ۱.۷ کدهای بازگشتی

کد صفر موفقیت است. GNU Wget برای انواع خطا کدهای جداگانه دارد: خطای عمومی، parse گزینه، I/O محلی، شبکه، بررسی TLS، احراز هویت، پروتکل و پاسخ خطای سرور. اگر چند مشکل رخ دهد، قواعد اولویت Wget تعیین می‌کند کدام کد بازگردد. مقدار را بلافاصله ببینید:

</div>

<div style="text-align:left;">

```
$ wget --spider -q https://example.com/
$ echo $?
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

برای منطق قابل‌حمل، صفر را موفق و هر مقدار دیگر را شکست بدانید؛ اگر تفکیک دقیق لازم است man نسخه‌ی خود را مرجع قرار دهید.

### ۱.۸ حالا چه؟

اکنون یک دانلود ساده و بررسی بدون ذخیره را می‌شناسید. فصل بعد تعیین می‌کند داده دقیقاً کجا و با چه سیاستی نوشته شود.

### برای مرجع بعدی

| دستور | کاربرد |
|---|---|
| wget URL | دانلود با نام برگرفته از URL |
| wget -S URL | نمایش پاسخ سرور |
| wget --spider URL | بررسی بدون ذخیره‌ی بدنه |
| wget -q URL | اجرای ساکت |
| wget -nv URL | خروجی خلاصه |
| wget -d URL | اشکال‌زدایی پرجزئیات |

## فصل ۲

### <u>نام فایل، دایرکتوری و ادامه‌ی دانلود</u>

### ۲.۱ تعیین نام خروجی با ‪-O‬

</div>

<div style="text-align:left;">

```
$ wget -O package.tar.gz 'https://example.com/download?id=42'
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-O`‬ همه‌ی اسناد دریافت‌شده را مانند یک جریان در فایل تعیین‌شده می‌نویسد؛ فقط «تغییر نام پس از دانلود» نیست. اگر چند URL بدهید، محتوای آن‌ها در همان فایل ترکیب می‌شود. فایل ممکن است پیش از موفقیت کامل truncate شود، پس برای فایل مهم از مسیر موقت و سپس جابه‌جایی اتمی استفاده کنید.

### ۲.۲ نوشتن روی stdout

</div>

<div style="text-align:left;">

```
$ wget -qO- https://example.com/data.txt
$ wget -qO- https://example.com/data.txt | less
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

علامت خط تیره به معنی stdout است. داده‌ی ناشناخته را مستقیماً به shell یا interpreter pipe نکنید. الگوی «دانلود و اجرا» فرصت بررسی hash، امضا و محتوا را از بین می‌برد.

### ۲.۳ انتخاب دایرکتوری با ‪-P‬

</div>

<div style="text-align:left;">

```
$ wget -P downloads/ https://example.com/file.iso
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-P`‬ پیشوند دایرکتوری را تعیین می‌کند و در دانلود بازگشتی نیز بر ریشه‌ی ساختار محلی اثر می‌گذارد.

### ۲.۴ ادامه‌ی دانلود با ‪-c‬

</div>

<div style="text-align:left;">

```
$ wget -c https://example.com/large.iso
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

اگر فایل محلی ناقص باشد و سرور Range را پشتیبانی کند، دانلود از انتهای آن ادامه می‌یابد. Wget تضمین نمی‌کند فایل محلی بخشی از همان نسخه‌ی فعلی سرور باشد؛ اگر محتوای راه دور عوض شده باشد، نتیجه می‌تواند خراب شود. پس از اتمام hash را بررسی کنید.

### ۲.۵ جلوگیری از بازنویسی با ‪-nc‬

</div>

<div style="text-align:left;">

```
$ wget -nc https://example.com/report.pdf
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`--no-clobber`‬ اگر فایل هم‌نام وجود داشته باشد دانلود را رد می‌کند. آن را با ‪`-O`‬ یا timestamping بدون شناخت رفتار ترکیب نکنید؛ این گزینه‌ها هدف‌های متفاوتی دارند.

### ۲.۶ timestamping با ‪-N‬

</div>

<div style="text-align:left;">

```
$ wget -N https://example.com/releases/checksums.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

Wget با Last-Modified و اندازه یا درخواست شرطی تصمیم می‌گیرد فایل را دوباره بگیرد یا نه. timestamping به رفتار درست سرور وابسته است و با نام خروجی اجباری ‪`-O`‬ سازگاری مفهومی خوبی ندارد.

### ۲.۷ نام برگرفته از Content-Disposition

</div>

<div style="text-align:left;">

```
$ wget --content-disposition 'https://example.com/download?id=42'
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این گزینه‌ی GNU Wget هنوز experimental معرفی می‌شود. نام پیشنهادی سرور داده‌ی غیرقابل اعتماد است؛ در محیط حساس نام و مسیر فایل نهایی را کنترل کنید.

### ۲.۸ فایل موقت و انتشار اتمی

در اسکریپت، ابتدا به فایل تازه دانلود و پس از موفقیت و اعتبارسنجی آن را جایگزین کنید:

</div>

<div style="text-align:left;">

```
tmp_file=$(mktemp ./artifact.XXXXXX)
if wget -qO "$tmp_file" https://example.com/artifact.bin; then
    mv -- "$tmp_file" artifact.bin
else
    rm -f -- "$tmp_file"
    exit 1
fi
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

در اسکریپت واقعی trap برای پاک‌سازی هنگام signal اضافه کنید. mv فقط وقتی در همان filesystem باشد جایگزینی اتمی معمول را فراهم می‌کند.

### ۲.۹ حالا چه؟

اکنون می‌توانید از فایل ناقص، بازنویسی ناخواسته و نام مبهم جلوگیری کنید. فصل بعد رفتار Wget را در شبکه‌ی کند یا ناپایدار کنترل می‌کند.

### برای مرجع بعدی

| گزینه | کاربرد |
|---|---|
| -O FILE | نوشتن جریان در فایل مشخص |
| -O- | نوشتن روی stdout |
| -P DIR | پیشوند دایرکتوری |
| -c | ادامه‌ی فایل ناقص |
| -nc | عدم بازنویسی فایل موجود |
| -N | دریافت فقط در صورت جدیدتر بودن |
| --content-disposition | استفاده از نام پیشنهادی پاسخ |

## فصل ۳

### <u>کنترل زمان، تلاش مجدد و پهنای باند</u>

### ۳.۱ timeout کلی و تفکیکی

</div>

<div style="text-align:left;">

```
$ wget -T 20 https://example.com/file.bin
$ wget --dns-timeout=5 --connect-timeout=10 --read-timeout=30 URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-T`‬ timeoutهای شبکه را یکجا تعیین می‌کند. timeout خواندن معمولاً دوره‌ی بی‌داده را محدود می‌کند، نه زمان کل دانلود. برای سقف قطعی کل فرایند می‌توان در GNU/Linux از timeout بیرونی استفاده کرد.

### ۳.۲ تعداد تلاش‌ها

</div>

<div style="text-align:left;">

```
$ wget --tries=5 --waitretry=10 https://example.com/file.bin
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

صفر برای tries می‌تواند به معنی تلاش نامحدود باشد و در job خودکار خطر گیر کردن دارد. تعداد و زمان را محدود کنید. Wget همه‌ی خطاها را به‌طور پیش‌فرض retry نمی‌کند.

### ۳.۳ retry برای خطاهای مشخص

</div>

<div style="text-align:left;">

```
$ wget --retry-connrefused --retry-on-http-error=429,500,502,503,504 \
    --tries=5 --waitretry=15 URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

retry بی‌قاعده می‌تواند بار سرور را بیشتر کند. headerهایی مانند Retry-After و سیاست سرویس را رعایت کنید و برای درخواست‌های غیر idempotent، به‌ویژه POST، خطر تکرار عملیات را جدی بگیرید.

### ۳.۴ فاصله میان چند دانلود

</div>

<div style="text-align:left;">

```
$ wget --wait=3 --random-wait -i urls.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

random-wait جایگزین مجوز یا رعایت rate limit نیست. در دانلود بازگشتی نرخ محافظه‌کارانه انتخاب کنید.

### ۳.۵ محدود کردن سرعت و سهمیه

</div>

<div style="text-align:left;">

```
$ wget --limit-rate=500k URL
$ wget --quota=2g -i urls.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

quota معمولاً پس از کامل شدن یک فایل بررسی می‌شود و ممکن است کمی از حد عبور کند. فضای آزاد دیسک را جداگانه پایش کنید.

### ۳.۶ انتخاب IPv4 یا IPv6

</div>

<div style="text-align:left;">

```
$ wget -4 URL
$ wget -6 URL
$ wget --prefer-family=IPv4 URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

دو گزینه‌ی اول خانواده را اجبار می‌کنند؛ prefer-family فقط اولویت را تغییر می‌دهد. این جداسازی برای عیب‌یابی route یا DNS مفید است.

### ۳.۷ bind کردن نشانی محلی و proxy

</div>

<div style="text-align:left;">

```
$ wget --bind-address=192.168.1.20 URL
$ wget --no-proxy URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

نشانی bind باید روی سیستم موجود باشد. no-proxy تنظیمات proxy محیط یا پیکربندی Wget را برای همان اجرا کنار می‌گذارد.

### ۳.۸ اجرای پس‌زمینه

</div>

<div style="text-align:left;">

```
$ wget -b https://example.com/large.iso
$ tail -f wget-log
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

حالت background به‌طور پیش‌فرض در wget-log گزارش می‌نویسد. در سامانه‌های امروزی برای job مهم، systemd، tmux یا scheduler مدیریت‌پذیرتر از رها کردن پردازش است.

### ۳.۹ حالا چه؟

با timeout، retry و rate limit می‌توان دانلود را نسبت به خطا مقاوم کرد، بدون آن‌که نامحدود یا آزاردهنده شود. فصل بعد درخواست و ورودی را سفارشی می‌کند.

### برای مرجع بعدی

| گزینه | کاربرد |
|---|---|
| -T N | تنظیم timeoutهای شبکه |
| --tries=N | تعداد تلاش |
| --waitretry=N | مکث تصاعدی تا سقف تعیین‌شده |
| --wait=N | فاصله بین دریافت‌ها |
| --random-wait | تصادفی کردن wait |
| --limit-rate=RATE | محدودیت سرعت |
| --quota=SIZE | سهمیه‌ی کل |
| -4 / -6 | اجبار خانواده‌ی IP |
| -b | اجرای پس‌زمینه |

## فصل ۴

### <u>چند URL، header، cookie و روش HTTP</u>

### ۴.۱ دانلود چند URL

</div>

<div style="text-align:left;">

```
$ wget https://example.com/a.txt https://example.com/b.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

Wget آن‌ها را به‌ترتیب دریافت می‌کند. GNU Wget 1 دانلود موازی داخلی عمومی مانند ابزارهای تخصصی ندارد.

### ۴.۲ خواندن URLها از فایل

</div>

<div style="text-align:left;">

```
$ wget -i urls.txt
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

فایل URL را مانند ورودی غیرقابل اعتماد بررسی کنید؛ ممکن است مقصد داخلی، فایل بسیار بزرگ یا URL دارای credential در آن باشد.

### ۴.۳ فایل HTML محلی و base URL

</div>

<div style="text-align:left;">

```
$ wget -i links.html -F -B https://example.com/docs/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-F`‬ ورودی را HTML و ‪`-B`‬ مبنای لینک‌های نسبی را تعیین می‌کند.

### ۴.۴ افزودن header

</div>

<div style="text-align:left;">

```
$ wget --header='Accept: application/json' -O data.json URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

می‌توان گزینه‌ی header را چند بار تکرار کرد. token را مستقیم در خط فرمان نگذارید، چون ممکن است در history و فهرست پردازش‌ها دیده شود. فایل پیکربندی نیز باید دسترسی محدود داشته باشد.

### ۴.۵ User-Agent و Referer

</div>

<div style="text-align:left;">

```
$ wget --user-agent='ExampleFetcher/1.0 (admin@example.test)' URL
$ wget --referer='https://example.com/page' URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

جعل هویت مرورگر راه‌حل محدودیت دسترسی یا مجوز نیست. برای crawler مجاز، User-Agent شفاف و اطلاعات تماس مفیدتر است.

### ۴.۶ cookieها

</div>

<div style="text-align:left;">

```
$ wget --load-cookies=cookies.txt URL
$ wget --save-cookies=cookies.txt --keep-session-cookies URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

فایل cookie ممکن است session فعال و اطلاعات حساس داشته باشد. دسترسی آن را محدود کنید، وارد Git نکنید و پس از نیاز حذف یا منقضی کنید. تبدیل cookie مرورگر همیشه مستقیم و ایمن نیست.

### ۴.۷ POST و body سفارشی

</div>

<div style="text-align:left;">

```
$ wget --post-data='name=value' -O response.txt https://example.com/form
$ wget --method=PUT --body-file=payload.json \
    --header='Content-Type: application/json' -O response.json URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

Wget ابزار اصلی طراحی API نیست. برای JSON، auth پیچیده، مشاهده‌ی status و کنترل بهتر headerها معمولاً curl مناسب‌تر است. retry کردن درخواست تغییردهنده ممکن است عملیات را تکرار کند.

### ۴.۸ فشرده‌سازی HTTP

</div>

<div style="text-align:left;">

```
$ wget --compression=auto URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این گزینه فشرده‌سازی انتقال HTTP را مذاکره می‌کند و با دانلود یک فایل .gz یا فشرده‌سازی محلی فرق دارد.

### ۴.۹ حالا چه؟

اکنون Wget می‌تواند درخواست‌های قابل‌کنترل‌تری بسازد. فصل بعد حفاظت credential و اعتبار اتصال TLS را بررسی می‌کند.

### برای مرجع بعدی

| گزینه | کاربرد |
|---|---|
| -i FILE | URLها از فایل |
| -F | تفسیر ورودی به‌عنوان HTML |
| -B URL | base لینک نسبی |
| --header=TEXT | header سفارشی |
| -U AGENT | User-Agent |
| --load-cookies=FILE | بارگذاری cookie |
| --post-data=TEXT | درخواست POST |
| --method=METHOD | روش HTTP سفارشی |

## فصل ۵

### <u>HTTPS، احراز هویت، proxy و FTP</u>

### ۵.۱ اعتبارسنجی TLS

در HTTPS، Wget باید زنجیره‌ی گواهی، تاریخ اعتبار و تطابق نام میزبان را بررسی کند. شکست این بررسی می‌تواند از ساعت غلط سیستم، CAهای قدیمی، proxy بازرسی‌کننده، نام اشتباه یا حمله ناشی شود. علت را رفع کنید، نه این‌که حفاظت را حذف کنید.

### ۵.۲ خطر ‪--no-check-certificate‬

</div>

<div style="text-align:left;">

```
$ wget --no-check-certificate https://example.com/file
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این گزینه اعتبار هویت مقصد را بررسی نمی‌کند و راه را برای حمله‌ی مرد میانی باز می‌گذارد. وجودش در مثال‌های اینترنتی آن را امن نمی‌کند. فقط در آزمایش کاملاً کنترل‌شده و با درک پیامد استفاده شود؛ راه درست معمولاً نصب CA معتبر با ‪`--ca-certificate`‬ یا اصلاح گواهی است.

### ۵.۳ CA و certificate سمت client

</div>

<div style="text-align:left;">

```
$ wget --ca-certificate=organization-ca.pem URL
$ wget --certificate=client.pem --private-key=client-key.pem URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

کلید خصوصی را با دسترسی سخت‌گیرانه نگه دارید و از قرار دادن آن در مخزن خودداری کنید. نوع PEM/DER و engine TLS build می‌تواند بر گزینه‌ها اثر بگذارد.

### ۵.۴ HSTS و pinning

GNU Wget می‌تواند HSTS را در پایگاه محلی نگه دارد و HTTP را برای میزبان شناخته‌شده به HTTPS ارتقا دهد. گزینه‌ی ‪`--pinnedpubkey`‬ کلید عمومی را با فایل یا hash تعیین‌شده تطبیق می‌دهد. pinning مدیریت چرخه‌ی تعویض کلید را دشوار می‌کند و باید با برنامه‌ی rotation استفاده شود.

### ۵.۵ نام کاربری و رمز عبور

</div>

<div style="text-align:left;">

```
$ wget --user=alice --ask-password https://example.com/private/file
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`--ask-password`‬ بهتر از نوشتن رمز در آرگومان است. گزینه‌ی ‪`--password`‬ می‌تواند secret را در history یا process list آشکار کند. Basic Auth باید فقط روی HTTPS معتبر استفاده شود.

### ۵.۶ فایل netrc

Wget می‌تواند credential را از ‪~/.netrc‬ بخواند. فایل باید فقط برای کاربر قابل خواندن باشد:

</div>

<div style="text-align:left;">

```
$ chmod 600 ~/.netrc
$ wget https://example.com/private/file
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`--no-netrc`‬ استفاده از آن را غیرفعال می‌کند. netrc متن ساده است؛ حفاظت filesystem و مدیریت secret ضروری است.

### ۵.۷ proxy

Wget تنظیمات proxy را از محیط یا wgetrc می‌خواند:

</div>

<div style="text-align:left;">

```
$ export https_proxy='http://proxy.example.test:3128/'
$ wget https://example.com/file
$ wget --no-proxy https://example.com/file
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

credential را در URL متغیر محیطی قرار ندهید؛ محیط ممکن است در ابزارهای تشخیصی یا لاگ آشکار شود. سیاست proxy سازمان را رعایت کنید.

### ۵.۸ FTP و FTPS

</div>

<div style="text-align:left;">

```
$ wget ftp://ftp.example.test/pub/file.tar.gz
$ wget --ftps-implicit ftps://ftp.example.test/file.tar.gz
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

FTP عادی credential و داده را رمزگذاری نمی‌کند. FTPS با SFTP یکی نیست؛ SFTP بخشی از SSH است و Wget از آن پشتیبانی نمی‌کند. برای SFTP از sftp، scp یا curl با build مناسب استفاده کنید. گزینه‌های fallback یا clear-data می‌توانند امنیت را تضعیف کنند.

### ۵.۹ حالا چه؟

اتصال موفق بدون اعتبارسنجی هویت کافی نیست. پس از ایمن کردن انتقال، فصل بعد محدوده‌ی دانلود بازگشتی را مهار می‌کند.

### برای مرجع بعدی

| نیاز | گزینه/ابزار |
|---|---|
| CA سازمانی | --ca-certificate=FILE |
| گواهی client | --certificate و --private-key |
| درخواست امن رمز | --ask-password |
| نادیده گرفتن netrc | --no-netrc |
| کنار گذاشتن proxy | --no-proxy |
| SFTP | sftp یا scp، نه wget |

## فصل ۶

### <u>دانلود بازگشتی و mirror وب</u>

### ۶.۱ recursion با ‪-r‬ و عمق با ‪-l‬

</div>

<div style="text-align:left;">

```
$ wget -r -l 2 https://example.com/docs/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

عمق صفر یا inf می‌تواند نامحدود باشد. همیشه ابتدا عمق، دامنه، مسیر و quota محدود تعیین کنید. لینک‌های تولیدشونده‌ی بی‌نهایت، calendarها و query stringها می‌توانند crawl را منفجر کنند.

### ۶.۲ یک صفحه با ملزوماتش

</div>

<div style="text-align:left;">

```
$ wget -p -k -E https://example.com/guide/page.html
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-p`‬ تصاویر و CSS لازم، ‪`-k`‬ تبدیل لینک‌ها برای مشاهده‌ی محلی و ‪`-E`‬ پسوند مناسب HTML/CSS را درخواست می‌کند. برنامه‌های JavaScript پویا الزاماً با این روش آفلاین نمی‌شوند.

### ۶.۳ mirror با ‪-m‬

</div>

<div style="text-align:left;">

```
$ wget -m --wait=2 --limit-rate=500k https://example.com/docs/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-m`‬ میان‌بری برای recursion نامحدود، timestamping و حفظ listingهای FTP است. به همین دلیل به‌تنهایی فرمان محافظه‌کارانه‌ای نیست؛ محدودیت‌های دیگر را حتماً اضافه کنید.

### ۶.۴ جلوگیری از صعود با ‪-np‬

</div>

<div style="text-align:left;">

```
$ wget -r -l 3 -np https://example.com/docs/manual/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

no-parent اجازه نمی‌دهد crawl از hierarchy مسیر آغازین بالاتر برود، ولی به‌تنهایی همه‌ی URLهای ناخواسته را حذف نمی‌کند.

### ۶.۵ محدود کردن دامنه و host

</div>

<div style="text-align:left;">

```
$ wget -r -l 2 -D example.com,static.example.com -H URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-H`‬ دنبال کردن hostهای خارجی را فعال می‌کند و بدون allowlist خطر گسترش crawl دارد. ‪`-D`‬ دامنه‌های پذیرفته را مشخص می‌کند. CDN لازم ممکن است host جدا داشته باشد؛ آن را آگاهانه اضافه کنید.

### ۶.۶ فیلتر پسوند و مسیر

</div>

<div style="text-align:left;">

```
$ wget -r -l 3 -A pdf,epub -np URL
$ wget -r -l 3 -R zip,iso URL
$ wget -r -I /docs,/assets -X /private,/tmp URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

پذیرش فقط یک پسوند می‌تواند مانع دریافت HTML لازم برای کشف لینک‌های بعدی شود. accept/reject روی URL و نام‌ها اعمال می‌شود و MIME type را به‌تنهایی تضمین نمی‌کند.

### ۶.۷ ساختار دایرکتوری محلی

- ‪`-nd`‬ همه‌ی فایل‌ها را بدون دایرکتوری ذخیره می‌کند و خطر برخورد نام دارد.
- ‪`-x`‬ ساخت دایرکتوری را اجبار می‌کند.
- ‪`-nH`‬ پوشه‌ی نام host را حذف می‌کند.
- ‪`--cut-dirs=N`‬ چند جزء ابتدایی مسیر را کنار می‌گذارد.
- ‪`-P DIR`‬ ریشه‌ی محلی را تعیین می‌کند.

### ۶.۸ robots، مجوز و بار سرور

GNU Wget در recursion رفتار robots را در نظر می‌گیرد، اما این جای اجازه، شرایط استفاده و قانون را نمی‌گیرد. robots یک سازوکار کنترل دسترسی نیست. نرخ را کم، User-Agent را شفاف، دامنه را محدود و زمان اجرا را هماهنگ کنید. محتوای شخصی، دارای حق نشر یا پشت احراز هویت نیازمند مجوز و سیاست نگهداری روشن است.

### ۶.۹ دستور محافظه‌کارانه‌ی نمونه

</div>

<div style="text-align:left;">

```
$ wget -r -l 2 -np -H -D example.com,static.example.com \
    --wait=2 --random-wait --limit-rate=300k --quota=500m \
    -P offline-copy https://example.com/docs/
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این فقط الگوست؛ پیش از اجرا دامنه‌ها، حجم احتمالی و اجازه را بررسی کنید.

### ۶.۱۰ حالا چه؟

دانلود بازگشتی زمانی قابل‌کنترل است که چند محدودیت مستقل داشته باشد. فصل بعد پیکربندی، لاگ و بایگانی پژوهشی را معرفی می‌کند.

### برای مرجع بعدی

| گزینه | کاربرد |
|---|---|
| -r | دانلود بازگشتی |
| -l N | عمق recursion |
| -p | ملزومات یک صفحه |
| -k | تبدیل لینک محلی |
| -E | تنظیم پسوند HTML/CSS |
| -m | حالت mirror |
| -np | عدم صعود به parent |
| -H / -D | host خارجی / allowlist دامنه |
| -A / -R | پذیرش / رد الگوها |
| -I / -X | include / exclude مسیر |

## فصل ۷

### <u>پیکربندی، گزارش‌گیری و بایگانی</u>

### ۷.۱ فایل‌های wgetrc

GNU Wget ابتدا پیکربندی سیستمی و سپس پیکربندی کاربر را می‌خواند. مسیر دقیق در ‪`wget --version`‬ و man آمده است. نمونه‌ی کاربر معمولاً ‪~/.wgetrc‬ است:

</div>

<div style="text-align:left;">

```
timeout = 30
tries = 4
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

گزینه‌ی ‪`--no-config`‬ همه‌ی فایل‌های پیکربندی را کنار می‌گذارد و ‪`--config=FILE`‬ فایل مشخصی را می‌خواند. این قابلیت برای اجرای تکرارپذیر مفید است.

### ۷.۲ تنظیم یک‌باره با ‪-e‬

</div>

<div style="text-align:left;">

```
$ wget -e robots=off URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این مثال نحو را نشان می‌دهد، نه توصیه را: خاموش کردن robots فقط وقتی مجاز است که مالک سایت هستید یا اجازه‌ی صریح دارید. ‪`-e`‬ فرمان‌های سبک wgetrc را برای همان اجرا اعمال می‌کند.

### ۷.۳ فایل log

</div>

<div style="text-align:left;">

```
$ wget -o download.log URL
$ wget -a download.log URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

‪`-o`‬ فایل را جایگزین و ‪`-a`‬ به آن اضافه می‌کند. لاگ ممکن است URL query، نام کاربری، مسیر داخلی و پاسخ سرور را داشته باشد؛ دسترسی و retention آن را مدیریت کنید.

### ۷.۴ WARC برای بایگانی وب

</div>

<div style="text-align:left;">

```
$ wget --warc-file=research-capture -r -l 1 URL
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

WARC درخواست و پاسخ را برای بایگانی نگه می‌دارد و می‌تواند بسیار بزرگ و حاوی اطلاعات حساس باشد. نام گزینه معمولاً بدون پسوند نهایی داده می‌شود و Wget فایل فشرده‌ی WARC می‌سازد. quota، مجوز، hash و سیاست نگهداری لازم‌اند.

### ۷.۵ IRI و نام‌های بین‌المللی

GNU Wget می‌تواند IRI و تبدیل encoding را مدیریت کند. ‪`--local-encoding`‬ و ‪`--remote-encoding`‬ هنگام تشخیص نادرست مفیدند و ‪`--no-iri`‬ این قابلیت را خاموش می‌کند. نام فایل روی سیستم‌عامل‌های مختلف ممکن است نیازمند ‪`--restrict-file-names`‬ باشد.

### ۷.۶ xattr و metadata

‪`--xattr`‬ می‌تواند metadataهایی مانند URL مبدأ را در extended attribute ذخیره کند. filesystem یا ابزار کپی شاید آن‌ها را حفظ نکند. URL مبدأ نیز می‌تواند حساس باشد؛ پیش از انتشار فایل، xattrها را بررسی کنید.

### ۷.۷ خروجی تکرارپذیر

برای job قابل بازتولید، نسخه‌ی Wget، URL نهایی، پیکربندی، زمان، hash و کد بازگشتی را ثبت کنید. redirect یا محتوای mutable می‌تواند دو اجرای یک فرمان را متفاوت کند. در artifactهای انتشار، URL نسخه‌دار و checksum رسمی بهتر از latest است.

### ۷.۸ حالا چه؟

اکنون رفتار پنهان پیکربندی و داده‌های جانبی دانلود را می‌شناسید. فصل آخر این اجزا را در اسکریپت‌های ایمن‌تر کنار هم می‌گذارد.

### برای مرجع بعدی

| گزینه | کاربرد |
|---|---|
| --no-config | نخواندن wgetrc |
| --config=FILE | پیکربندی مشخص |
| -e COMMAND | تنظیم یک‌باره |
| -o FILE | جایگزینی log |
| -a FILE | افزودن به log |
| --warc-file=NAME | ساخت بایگانی WARC |
| --restrict-file-names=OS | محدودسازی نام فایل |
| --xattr | ذخیره‌ی metadata در xattr |

## فصل ۸

### <u>اسکریپت‌نویسی، اعتبارسنجی و عیب‌یابی</u>

### ۸.۱ دانلود امن‌تر به فایل موقت

</div>

<div style="text-align:left;">

```
#!/usr/bin/env bash
set -u

url='https://example.com/releases/app.tar.gz'
destination='app.tar.gz'
tmp_file=$(mktemp './app.tar.gz.part.XXXXXX') || exit 1
trap 'rm -f -- "$tmp_file"' EXIT HUP INT TERM

if wget --tries=4 --timeout=30 -O "$tmp_file" "$url"; then
    mv -- "$tmp_file" "$destination"
    trap - EXIT HUP INT TERM
else
    echo 'download failed' >&2
    exit 1
fi
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

این الگو فایل قبلی را تا موفقیت دانلود حفظ می‌کند. برای artifact حساس، پیش از mv بررسی hash یا امضا را نیز انجام دهید.

### ۸.۲ بررسی SHA-256

</div>

<div style="text-align:left;">

```
$ wget https://example.com/app.tar.gz
$ wget https://example.com/app.tar.gz.sha256
$ sha256sum -c app.tar.gz.sha256
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

اگر فایل و checksum از همان کانال قابل جعل بیایند، hash فقط خرابی تصادفی را خوب تشخیص می‌دهد و اصالت مستقل نمی‌سازد. checksum را از کانال معتبر یا امضاشده بگیرید.

### ۸.۳ بررسی امضای GPG

</div>

<div style="text-align:left;">

```
$ wget https://example.com/app.tar.gz
$ wget https://example.com/app.tar.gz.sig
$ gpg --verify app.tar.gz.sig app.tar.gz
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

نتیجه فقط وقتی معتبر است که fingerprint کلید امضاکننده را از مسیر مستقل و قابل اعتماد تأیید کرده باشید.

### ۸.۴ بررسی وجود منبع در شرط

</div>

<div style="text-align:left;">

```
if wget --spider -q --timeout=10 --tries=2 "$url"; then
    echo 'resource appears reachable'
else
    echo 'resource check failed' >&2
fi
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

عبارت «به نظر قابل دسترسی است» دقیق‌تر از «فایل قطعاً موجود است» است، چون HEAD، auth و رفتار پویا می‌توانند نتیجه را تغییر دهند.

### ۸.۵ خطاهای رایج

- ‪`Temporary failure in name resolution`‬: DNS یا resolver را بررسی کنید.
- ‪`Connection refused`‬: اتصال به مقصد رسیده ولی پورت اتصال را نپذیرفته است.
- timeout: مسیر، firewall، ازدحام یا سرور کند ممکن‌اند.
- ‪`404 Not Found`‬: مسیر منبع از دید سرور وجود ندارد.
- ‪`403 Forbidden`‬: سرور درخواست را فهمیده ولی اجازه نداده است؛ دور زدن کنترل دسترسی راه‌حل نیست.
- خطای certificate: ساعت، نام، زنجیره‌ی CA و proxy را اصلاح کنید.
- ‪`No space left on device`‬: فضای دیسک و inode را بررسی و دانلود ناقص را مدیریت کنید.
- فایل HTML به‌جای artifact: redirect، صفحه‌ی login یا پاسخ خطا را با ‪`-S`‬ و file بررسی کنید.

### ۸.۶ عیب‌یابی مرحله‌به‌مرحله

</div>

<div style="text-align:left;">

```
$ getent ahosts example.com
$ wget --spider -S -4 https://example.com/file
$ wget --spider -S -6 https://example.com/file
$ wget -d --spider https://example.com/file
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

debug ممکن است اطلاعات حساس چاپ کند. برای بررسی HTTP پیچیده، ‪`curl -v`‬ و برای TLS، ‪`openssl s_client`‬ دید متفاوتی می‌دهند.

### ۸.۷ wget یا curl؟

Wget برای دانلود غیرتعاملی فایل، ادامه، timestamping و recursion بسیار مناسب است. curl از پروتکل‌های بیشتری پشتیبانی می‌کند، برای API، headerها، upload، status و نوشتن اسکریپت‌های HTTP دقیق‌تر معمولاً انعطاف بیشتری دارد. هیچ‌کدام ذاتاً جای مرورگر headless برای برنامه‌ی JavaScriptمحور نیستند.

### ۸.۸ ابزارهای مکمل

| ابزار | کاربرد |
|---|---|
| curl | API، HTTP دقیق، upload و پروتکل‌های بیشتر |
| aria2 | دانلود چندمنبعی و قطعه‌ای |
| rsync | همگام‌سازی افزایشی با مقصد پشتیبان |
| scp / sftp | انتقال روی SSH |
| sha256sum | بررسی یکپارچگی |
| gpg | تأیید امضای ناشر |
| file | تشخیص نوع محتوای دانلودشده |
| tar / unzip | استخراج پس از اعتبارسنجی |

### ۸.۹ استخراج خودکار نکنید

آرشیو دانلودشده می‌تواند مسیر مطلق، ‪`../`‬، symlink یا فایل مخرب داشته باشد. ابتدا نوع، hash، امضا و فهرست محتوا را بررسی کنید و در دایرکتوری کنترل‌شده استخراج نمایید:

</div>

<div style="text-align:left;">

```
$ file archive.tar.gz
$ tar tzf archive.tar.gz | less
```
</div>
<div dir="rtl" lang="fa" style="text-align: right;">

### ۸.۱۰ حالا چه؟

در این کتاب از یک دانلود ساده تا ادامه‌ی فایل ناقص، سیاست بازنویسی، retry، timeout، نرخ، cookie، درخواست HTTP، TLS، احراز هویت، proxy، FTP، mirror، WARC و اسکریپت‌نویسی پیش رفتیم. مهم‌ترین اصل این است که «دانلود موفق» با «فایل معتبر و قابل اعتماد» یکسان نیست؛ منبع، TLS، hash یا امضا و نوع محتوا باید متناسب با ریسک بررسی شوند.

برای استفاده‌ی روزمره، فرمان را محدود نگه دارید. برای recursion چند مرز مستقل بگذارید. secret را در آرگومان ننویسید. خطای TLS را با خاموش کردن بررسی گواهی پنهان نکنید. و هیچ محتوای دانلودشده‌ای را بدون بازبینی مستقیم اجرا یا استخراج نکنید.

### برای مرجع بعدی

### دانلود و نام فایل

| دستور | توضیح |
|---|---|
| wget URL | دانلود عادی |
| wget -O FILE URL | نوشتن در فایل مشخص |
| wget -P DIR URL | ذخیره زیر دایرکتوری |
| wget -c URL | ادامه‌ی دانلود ناقص |
| wget -nc URL | عدم بازنویسی |
| wget -N URL | timestamping |

### پایداری و کنترل منابع

| گزینه | توضیح |
|---|---|
| --tries=N | تعداد تلاش |
| --timeout=N | timeoutهای شبکه |
| --waitretry=N | مکث retry |
| --wait=N | فاصله‌ی دانلودها |
| --limit-rate=RATE | سقف سرعت |
| --quota=SIZE | سقف تقریبی دریافت |
| -4 / -6 | اجبار IPv4/IPv6 |

### HTTP و امنیت

| گزینه | توضیح |
|---|---|
| -S | header پاسخ سرور |
| --spider | بررسی بدون دانلود بدنه |
| --header=TEXT | header سفارشی |
| --load-cookies=FILE | cookie ورودی |
| --ask-password | درخواست تعاملی رمز |
| --ca-certificate=FILE | CA سفارشی معتبر |
| --no-check-certificate | غیرفعال کردن اعتبارسنجی؛ ناامن |

### دانلود بازگشتی

| گزینه | توضیح |
|---|---|
| -r | recursion |
| -l N | عمق |
| -p | requisites صفحه |
| -k | تبدیل لینک‌ها |
| -m | mirror |
| -np | جلوگیری از parent |
| -D LIST | allowlist دامنه |
| -A / -R | پذیرش / رد فایل |
| -I / -X | include / exclude دایرکتوری |

### قواعد طلایی

| قاعده | دلیل |
|---|---|
| ابتدا با --spider و محدودیت بررسی کنید | از دریافت ناخواسته جلوگیری می‌کند |
| retry، timeout و quota را محدود کنید | job از کنترل خارج نمی‌شود |
| TLS را معتبر نگه دارید | هویت و محرمانگی مسیر حفظ می‌شود |
| hash یا امضا را بررسی کنید | موفقیت انتقال اصالت فایل نیست |
| recursion را به دامنه و مسیر محدود کنید | از crawl بی‌مرز جلوگیری می‌شود |
| secret را در command line نگذارید | history و process list آن را فاش می‌کنند |
| دانلود را مستقیماً اجرا نکنید | فرصت اعتبارسنجی و بازبینی از بین می‌رود |

</div>
