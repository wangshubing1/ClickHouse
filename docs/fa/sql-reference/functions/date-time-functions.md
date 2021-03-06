---
machine_translated: true
machine_translated_rev: 72537a2d527c63c07aa5d2361a8829f3895cf2bd
toc_priority: 39
toc_title: "\u06A9\u0627\u0631 \u0628\u0627 \u062A\u0627\u0631\u06CC\u062E \u0648\
  \ \u0632\u0645\u0627\u0646"
---

# توابع برای کار با تاریخ و زمان {#functions-for-working-with-dates-and-times}

پشتیبانی از مناطق زمانی

همه توابع برای کار با تاریخ و زمان است که یک استفاده منطقی برای منطقه زمانی می تواند یک زمان اختیاری استدلال منطقه دوم قبول. مثال: اسیا/یکاترینبورگ. در این مورد از منطقه زمانی مشخص شده به جای محلی (پیش فرض) استفاده می کنند.

``` sql
SELECT
    toDateTime('2016-06-15 23:00:00') AS time,
    toDate(time) AS date_local,
    toDate(time, 'Asia/Yekaterinburg') AS date_yekat,
    toString(time, 'US/Samoa') AS time_samoa
```

``` text
┌────────────────time─┬─date_local─┬─date_yekat─┬─time_samoa──────────┐
│ 2016-06-15 23:00:00 │ 2016-06-15 │ 2016-06-16 │ 2016-06-15 09:00:00 │
└─────────────────────┴────────────┴────────────┴─────────────────────┘
```

فقط مناطق زمانی که از مجموعه مقالات توسط تعداد کل ساعت متفاوت پشتیبانی می شوند.

## توتیمزون {#totimezone}

تبدیل زمان یا تاریخ و زمان به منطقه زمانی مشخص شده است.

## اسباب بازی {#toyear}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد اوینت16 حاوی شماره سال (میلادی).

## فهرست توزیع جدید {#toquarter}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد کوچک8 حاوی شماره سه ماهه.

## تامونت {#tomonth}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد کوچک8 حاوی شماره ماه (1-12).

## سال {#todayofyear}

تبدیل یک تاریخ و یا تاریخ با گذشت زمان به یک UInt16 تعداد شامل تعداد روز از سال (1-366).

## تودیفمون {#todayofmonth}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد اوینت8 حاوی تعداد روز از ماه (1-31).

## تدیفوک {#todayofweek}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد اوینت8 حاوی تعداد روز هفته (دوشنبه است 1, و یکشنبه است 7).

## تمام {#tohour}

تبدیل تاریخ با هم به یک UInt8 شماره حاوی تعداد ساعت در زمان 24 ساعته (0-23).
This function assumes that if clocks are moved ahead, it is by one hour and occurs at 2 a.m., and if clocks are moved back, it is by one hour and occurs at 3 a.m. (which is not always true – even in Moscow the clocks were twice changed at a different time).

## تامینوت {#tominute}

تبدیل تاریخ با هم به یک UInt8 شماره حاوی تعداد دقیقه از ساعت (0-59).

## جای خالی {#tosecond}

تبدیل تاریخ با هم به یک UInt8 شماره حاوی شماره دوم در دقیقه (0-59).
ثانیه جهش برای به حساب نمی.

## تیونیتیمستمپ {#to-unix-timestamp}

برای استدلال حسگر ناحیه رنگی: تبدیل ارزش به نمایندگی عددی داخلی خود (برچسب زمان یونیکس).
برای استدلال رشته: تاریخ ساعت پارسه از رشته با توجه به منطقه زمانی (بحث دوم اختیاری, منطقه زمانی سرور به طور پیش فرض استفاده می شود) و مربوط برچسب زمان یونیکس می گرداند.
برای استدلال تاریخ: رفتار نامشخص است.

**نحو**

``` sql
toUnixTimestamp(datetime)
toUnixTimestamp(str, [timezone])
```

**مقدار بازگشتی**

-   زمان یونیکس را برمی گرداند.

نوع: `UInt32`.

**مثال**

پرسوجو:

``` sql
SELECT toUnixTimestamp('2017-11-05 08:07:47', 'Asia/Tokyo') AS unix_timestamp
```

نتیجه:

``` text
┌─unix_timestamp─┐
│     1509836867 │
└────────────────┘
```

## سال نو {#tostartofyear}

دور یک تاریخ یا تاریخ با زمان به روز اول سال.
تاریخ را برمی گرداند.

## تاستارتوفیزیر {#tostartofisoyear}

دور کردن تاریخ یا تاریخ با زمان به روز اول سال ایزو.
تاریخ را برمی گرداند.

## تاستارتوفارتر {#tostartofquarter}

دور یک تاریخ یا تاریخ با زمان به روز اول سه ماهه.
اولین روز از سه ماهه است یا 1 ژانویه, 1 مارس, 1 جولای, یا 1 اکتبر.
تاریخ را برمی گرداند.

## ماهی تابه {#tostartofmonth}

دور پایین تاریخ یا تاریخ با زمان به روز اول ماه.
تاریخ را برمی گرداند.

!!! attention "توجه"
    رفتار تجزیه تاریخ نادرست اجرای خاص است. تاتر ممکن است صفر تاریخ بازگشت, پرتاب یک استثنا و یا انجام “natural” سرریز کردن.

## روز قیامت {#tomonday}

دور کردن یک تاریخ یا تاریخ با زمان به نزدیکترین دوشنبه.
تاریخ را برمی گرداند.

## تستارتوفک (تی \[, حالت\]) {#tostartofweektmode}

دور یک تاریخ یا تاریخ را با زمان به نزدیکترین یکشنبه یا دوشنبه با حالت.
تاریخ را برمی گرداند.
استدلال حالت کار می کند دقیقا مانند استدلال حالت به یدک کش (). برای نحو تک استدلال, ارزش حالت 0 استفاده شده است.

## روزهای سه بعدی {#tostartofday}

دور پایین تاریخ با زمان به شروع روز.

## تاستارتوفهور {#tostartofhour}

دور پایین تاریخ با زمان به شروع ساعت.

## حفاظت {#tostartofminute}

دور پایین تاریخ با زمان به شروع دقیقه.

## تستارتوفیفومینوت {#tostartoffiveminute}

دور پایین تاریخ با زمان به شروع فاصله پنج دقیقه.

## حفاظت {#tostartoftenminutes}

دور پایین تاریخ با زمان به شروع فاصله ده دقیقه.

## حفاظت از محیط زیست {#tostartoffifteenminutes}

دور پایین تاریخ با زمان به شروع فاصله پانزده دقیقه.

## toStartOfInterval(time_or_data فاصله x واحد \[, time_zone\]) {#tostartofintervaltime-or-data-interval-x-unit-time-zone}

این یک تعمیم توابع دیگر به نام است `toStartOf*`. به عنوان مثال,
`toStartOfInterval(t, INTERVAL 1 year)` همان را برمی گرداند `toStartOfYear(t)`,
`toStartOfInterval(t, INTERVAL 1 month)` همان را برمی گرداند `toStartOfMonth(t)`,
`toStartOfInterval(t, INTERVAL 1 day)` همان را برمی گرداند `toStartOfDay(t)`,
`toStartOfInterval(t, INTERVAL 15 minute)` همان را برمی گرداند `toStartOfFifteenMinutes(t)` و غیره

## & تمام کردن {#totime}

تبدیل یک تاریخ با زمان به یک تاریخ ثابت خاص, در حالی که حفظ زمان.

## ترلتیویینوم {#torelativeyearnum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد سال, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیواارترن {#torelativequarternum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد سه ماهه, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیومنتنوم {#torelativemonthnum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد ماه, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیواکنام {#torelativeweeknum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد هفته, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیدینوم {#torelativedaynum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد روز, با شروع از یک نقطه ثابت خاص در گذشته.

## تورلاتویورنام {#torelativehournum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد ساعت, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیومینوتنوم {#torelativeminutenum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد دقیقه, با شروع از یک نقطه ثابت خاص در گذشته.

## ترلتیویسکنندوم {#torelativesecondnum}

تبدیل یک تاریخ با زمان و یا تاریخ به تعداد دوم, با شروع از یک نقطه ثابت خاص در گذشته.

## ریز ریز کردن {#toisoyear}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد اوینت16 حاوی شماره سال ایزو.

## هشدار داده می شود {#toisoweek}

تبدیل یک تاریخ و یا تاریخ با گذشت زمان به یک UInt8 تعداد شامل ISO هفته شماره.

## تاریخ \[, حالت\]) {#toweekdatemode}

این تابع تعداد هفته برای تاریخ و یا تاریخ ساعت می گرداند. فرم دو برهان یدک کش () شما را قادر به مشخص کنید که هفته در روز یکشنبه یا دوشنبه شروع می شود و چه مقدار بازگشتی باید در محدوده 0 تا 53 یا از 1 به 53 باشد. اگر استدلال حالت حذف شده است, حالت پیش فرض است 0.
`toISOWeek()`یک تابع سازگاری است که معادل است `toWeek(date,3)`.
جدول زیر توضیح می دهد که چگونه استدلال حالت کار می کند.

| حالت | اولین روز هفته | گستره | Week 1 is the first week …  |
|------|----------------|-------|-----------------------------|
| 0    | یکشنبه         | 0-53  | با یکشنبه در این سال        |
| 1    | دوشنبه         | 0-53  | با 4 یا چند روز در سال جاری |
| 2    | یکشنبه         | 1-53  | با یکشنبه در این سال        |
| 3    | دوشنبه         | 1-53  | با 4 یا چند روز در سال جاری |
| 4    | یکشنبه         | 0-53  | با 4 یا چند روز در سال جاری |
| 5    | دوشنبه         | 0-53  | با دوشنبه در این سال        |
| 6    | یکشنبه         | 1-53  | با 4 یا چند روز در سال جاری |
| 7    | دوشنبه         | 1-53  | با دوشنبه در این سال        |
| 8    | یکشنبه         | 1-53  | شامل ژانویه 1               |
| 9    | دوشنبه         | 1-53  | شامل ژانویه 1               |

برای مقادیر حالت با معنی “with 4 or more days this year,” هفته ها با توجه به ایزو شماره 8601: 1988:

-   اگر هفته حاوی ژانویه 1 است 4 یا چند روز در سال جدید, هفته است 1.

-   در غیر این صورت, این هفته گذشته سال گذشته است, و هفته بعد هفته است 1.

برای مقادیر حالت با معنی “contains January 1”, هفته شامل ژانویه 1 هفته است 1. مهم نیست که چند روز در سال جدید هفته شامل, حتی اگر شامل تنها یک روز.

``` sql
toWeek(date, [, mode][, Timezone])
```

**پارامترها**

-   `date` – Date or DateTime.
-   `mode` – Optional parameter, Range of values is \[0,9\], default is 0.
-   `Timezone` – Optional parameter, it behaves like any other conversion function.

**مثال**

``` sql
SELECT toDate('2016-12-27') AS date, toWeek(date) AS week0, toWeek(date,1) AS week1, toWeek(date,9) AS week9;
```

``` text
┌───────date─┬─week0─┬─week1─┬─week9─┐
│ 2016-12-27 │    52 │    52 │     1 │
└────────────┴───────┴───────┴───────┘
```

## تاریخ \[, حالت\]) {#toyearweekdatemode}

را برمی گرداند سال و هفته برای تاریخ. سال در نتیجه ممکن است متفاوت از سال در بحث تاریخ برای اولین و هفته گذشته سال.

استدلال حالت کار می کند دقیقا مانند استدلال حالت به یدک کش (). برای نحو تک استدلال, ارزش حالت 0 استفاده شده است.

`toISOYear()`یک تابع سازگاری است که معادل است `intDiv(toYearWeek(date,3),100)`.

**مثال**

``` sql
SELECT toDate('2016-12-27') AS date, toYearWeek(date) AS yearWeek0, toYearWeek(date,1) AS yearWeek1, toYearWeek(date,9) AS yearWeek9;
```

``` text
┌───────date─┬─yearWeek0─┬─yearWeek1─┬─yearWeek9─┐
│ 2016-12-27 │    201652 │    201652 │    201701 │
└────────────┴───────────┴───────────┴───────────┘
```

## حالا {#now}

قبول صفر استدلال و بازده زمان فعلی در یکی از لحظات اجرای درخواست.
این تابع ثابت می گرداند, حتی اگر درخواست زمان طولانی برای تکمیل.

## امروز {#today}

قبول صفر استدلال و بازده تاریخ جاری در یکی از لحظات اجرای درخواست.
همان ‘toDate(now())’.

## دیروز {#yesterday}

قبول صفر استدلال و بازده تاریخ دیروز در یکی از لحظات اجرای درخواست.
همان ‘today() - 1’.

## بازه زمانی {#timeslot}

دور زمان به نیم ساعت.
این تابع خاص به یاندکس است.متریکا, از نیم ساعت حداقل مقدار زمان برای شکستن یک جلسه به دو جلسه است اگر یک تگ ردیابی نشان می دهد تعداد صفحات متوالی یک کاربر که در زمان به شدت بیش از این مقدار متفاوت. این به این معنی است که تاپل (شناسه برچسب, شناسه کاربری, و شکاف زمان) را می توان مورد استفاده قرار گیرد به جستجو برای تعداد صفحات که در جلسه مربوطه شامل.

## ستاره فیلم سکسی {#toyyyymm}

تبدیل یک تاریخ یا تاریخ با زمان به یک عدد اوینت32 حاوی تعداد سال و ماه (یی \* 100 + میلی متر).

## ستاره فیلم سکسی {#toyyyymmdd}

تبدیل یک تاریخ یا تاریخ با زمان به تعداد اوینت32 حاوی سال و ماه شماره (یی \* 10000 + میلی متر \* 100 + دی.دی.

## اطلاعات دقیق {#toyyyymmddhhmmss}

تبدیل یک تاریخ و یا تاریخ با گذشت زمان به یک UInt64 تعداد شامل سال و ماه شماره (YYYY \* 10000000000 + MM \* 100000000 + DD \* 1000000 + hh \* 10000 + mm \* 100 + ss) است.

## addYears, addMonths, addWeeks, addDays, addHours, addMinutes, addSeconds, addQuarters {#addyears-addmonths-addweeks-adddays-addhours-addminutes-addseconds-addquarters}

تابع می افزاید: یک تاریخ/فاصله زمانی به یک تاریخ/تاریخ ساعت و سپس بازگشت تاریخ / تاریخ ساعت. به عنوان مثال:

``` sql
WITH
    toDate('2018-01-01') AS date,
    toDateTime('2018-01-01 00:00:00') AS date_time
SELECT
    addYears(date, 1) AS add_years_with_date,
    addYears(date_time, 1) AS add_years_with_date_time
```

``` text
┌─add_years_with_date─┬─add_years_with_date_time─┐
│          2019-01-01 │      2019-01-01 00:00:00 │
└─────────────────────┴──────────────────────────┘
```

## subtractYears, subtractMonths, subtractWeeks, subtractDays, subtractHours, subtractMinutes, subtractSeconds, subtractQuarters {#subtractyears-subtractmonths-subtractweeks-subtractdays-subtracthours-subtractminutes-subtractseconds-subtractquarters}

تابع تفریق یک تاریخ/فاصله زمانی به تاریخ/تاریخ ساعت و سپس بازگشت تاریخ / تاریخ ساعت. به عنوان مثال:

``` sql
WITH
    toDate('2019-01-01') AS date,
    toDateTime('2019-01-01 00:00:00') AS date_time
SELECT
    subtractYears(date, 1) AS subtract_years_with_date,
    subtractYears(date_time, 1) AS subtract_years_with_date_time
```

``` text
┌─subtract_years_with_date─┬─subtract_years_with_date_time─┐
│               2018-01-01 │           2018-01-01 00:00:00 │
└──────────────────────────┴───────────────────────────────┘
```

## dateDiff {#datediff}

بازگرداندن تفاوت بین دو تاریخ و یا تاریخ ساعت ارزش.

**نحو**

``` sql
dateDiff('unit', startdate, enddate, [timezone])
```

**پارامترها**

-   `unit` — Time unit, in which the returned value is expressed. [رشته](../syntax.md#syntax-string-literal).

        Supported values:

        | unit   |
        | ---- |
        |second  |
        |minute  |
        |hour    |
        |day     |
        |week    |
        |month   |
        |quarter |
        |year    |

-   `startdate` — The first time value to compare. [تاریخ](../../sql-reference/data-types/date.md) یا [DateTime](../../sql-reference/data-types/datetime.md).

-   `enddate` — The second time value to compare. [تاریخ](../../sql-reference/data-types/date.md) یا [DateTime](../../sql-reference/data-types/datetime.md).

-   `timezone` — Optional parameter. If specified, it is applied to both `startdate` و `enddate`. اگر مشخص نشده, زمان از `startdate` و `enddate` استفاده می شود. در صورتی که یکسان نیست, نتیجه نامشخص است.

**مقدار بازگشتی**

تفاوت بین `startdate` و `enddate` بیان شده در `unit`.

نوع: `int`.

**مثال**

پرسوجو:

``` sql
SELECT dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'));
```

نتیجه:

``` text
┌─dateDiff('hour', toDateTime('2018-01-01 22:00:00'), toDateTime('2018-01-02 23:00:00'))─┐
│                                                                                     25 │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

## زمانهای(StartTime, مدت,\[, اندازه\]) {#timeslotsstarttime-duration-size}

برای یک بازه زمانی شروع در ‘StartTime’ و در ادامه برای ‘Duration’ ثانیه, این مجموعه ای از لحظات در زمان گرداند, متشکل از نقاط از این فاصله به گرد ‘Size’ در عرض چند ثانیه ‘Size’ یک پارامتر اختیاری است: یک ثابت اوینت32, مجموعه ای به 1800 به طور پیش فرض.
به عنوان مثال, `timeSlots(toDateTime('2012-01-01 12:20:00'), 600) = [toDateTime('2012-01-01 12:00:00'), toDateTime('2012-01-01 12:30:00')]`.
این برای جستجوی صفحات در جلسه مربوطه ضروری است.

## formatDateTime(زمان فرمت \[منطقه زمانی\]) {#formatdatetime}

Function formats a Time according given Format string. N.B.: Format is a constant expression, e.g. you can not have multiple formats for single result column.

اصلاح کننده های پشتیبانی شده برای فرمت:
(“Example” ستون نتیجه قالب بندی برای زمان را نشان می دهد `2018-01-02 22:33:44`)

| تغییردهنده | توصیف                                                                       | مثال       |
|------------|-----------------------------------------------------------------------------|------------|
| %C         | سال تقسیم بر 100 و کوتاه به عدد صحیح (00-99)                                | 20         |
| # د       | روز از ماه, صفر خالی (01-31)                                                | 02         |
| %D         | کوتاه میلی متر/دی دی/یی تاریخ, معادل %متر/%د / %و                           | 01/02/18   |
| # ا       | روز از ماه, فضا خالی ( 1-31)                                                | 2          |
| %F         | کوتاه تاریخ یی-میلی متر-دی دی, معادل%و-%متر - % د                           | 2018-01-02 |
| %H         | ساعت در فرمت 24 ساعت (00-23)                                                | 22         |
| %I         | ساعت در فرمت 12 ساعت (01-12)                                                | 10         |
| # ج       | روز سال (001-366)                                                           | 002        |
| % متر      | ماه به عنوان یک عدد اعشاری (01-12)                                          | 01         |
| %M         | دقیقه (00-59)                                                               | 33         |
| % ن        | شخصیت جدید خط (")                                                           |            |
| # پ       | هستم یا بعد از ظهر تعیین                                                    | PM         |
| %R         | 24-ساعت ساعت ساعت: زمان میلی متر, معادل %ساعت: % متر                        | 22:33      |
| %S         | دوم (00-59)                                                                 | 44         |
| % تی       | شخصیت افقی تب (')                                                           |            |
| %T         | ایزو 8601 فرمت زمان (ساعت:میلی متر:اس اس), معادل %ساعت:%متر:%بازدید کنندگان | 22:33:44   |
| # تو      | ایزو 8601 روز هفته به عنوان شماره با دوشنبه به عنوان 1 (1-7)                | 2          |
| %V         | ایزو 8601 هفته شماره (01-53)                                                | 01         |
| # وات     | روز هفته به عنوان یک عدد اعشاری با یکشنبه به عنوان 0 (0-6)                  | 2          |
| #...      | سال گذشته دو رقم (00-99)                                                    | 18         |
| %Y         | سال                                                                         | 2018       |
| %%         | یک % نشانه                                                                  | %          |

[مقاله اصلی](https://clickhouse.tech/docs/en/query_language/functions/date_time_functions/) <!--hide-->
