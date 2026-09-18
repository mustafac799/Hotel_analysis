![alt text](<Images/Hotel_dashboard_page 1.png>)
![alt text](<Images/Hotel_dashboard_page 2.png>)


# 🏨 Hotel Historical Dashboard

**A Power BI analytics project analyzing 3 years of hotel booking data to answer real operational and financial questions for hotel management.**

---

## 🇬🇧 Project Overview

This project transforms raw hotel booking data (2018–2020, ~142,000 reservations across two hotels) into an interactive Power BI dashboard designed to answer three core business questions:

1. **Is revenue growing?**
2. **Do we need to increase parking capacity?**
3. **What operational and booking trends should management be aware of?**

### Data Sources

- `2018.csv`, `2019.csv`, `2020.csv` — raw booking-level data (32 fields per booking: dates, stay length, ADR, market segment, cancellation status, guest details, etc.)
- `market_segment.csv` — discount rate applied per market segment
- `meal_cost.csv` — per-meal cost by meal plan (BB, HB, FB, SC)

### Methodology

Revenue logic was not assumed — it was **validated against source data and confirmed with the hotel's accounting team** before being finalized. Key methodological decisions:

- **Revenue = nights × (ADR × (1 - discount) + meal cost)**, where:
  - ADR is confirmed to exclude both meal cost and discount (verified with hotel accounting)
  - Meal cost is charged per meal ordered, and therefore scales with length of stay
  - Discount is applied to the room rate, varies by market segment, and applies uniformly across room types
- **Realized Revenue** is filtered to non-canceled bookings only, since a canceled reservation never generates actual income
- **Total (Supposed) Revenue** is reported separately to quantify the gap between what was booked and what was actually earned — a standard gross-vs-net revenue reconciliation, adapted here to also isolate cancellation impact by market segment

All core measures were built in both SQL (for data preparation/views) and DAX (for the Power BI model), and cross-validated against raw CSV calculations to confirm consistency before being surfaced on the dashboard.

### Key Findings

| Metric | Value |
|---|---|
| Total Booked Revenue | ~$44.7M |
| Realized Revenue | ~$27.5M |
| Revenue Lost to Cancellations | ~$17.2M |
| Total Discounts (realized bookings) | ~$7.59M |
| Total Meal Revenue (realized bookings) | ~$4.58M |
| Non-canceled Bookings | 89,108 (63%) |
| Canceled Bookings | 52,839 (37%) |

**Headline insight:** Cancellation rate varies dramatically by market segment — from 12% (Complementary) to **62% (Groups)**, the highest of any segment.

### Dashboard Structure

- **Page 1 — Revenue:** Growth over time (normalized by month to account for partial-year data), revenue by hotel/segment/channel/meal/customer type, discount analysis
- **Page 2 — Operational Insights:** Cancellation vs. fulfillment rate by segment, parking demand trends, guest type breakdown, repeat guest ratio, deposit type analysis

### Known Limitations

- Parking demand is tracked, but the dataset contains no parking **capacity** figure, so the dashboard quantifies demand trends rather than issuing a capacity recommendation.
- 2018 and 2020 contain partial-year data (6 and 8 months respectively vs. 12 for 2019); charts are labeled and normalized accordingly to avoid misleading year-over-year comparisons.
- Cancellation loss assumes canceled rooms went unsold; actual loss may be lower where rooms were resold, particularly for long-lead-time cancellations.

### Tools Used

`SQL` (data modeling & views) · `Power BI` (data model, DAX, visualization) ·

---

## 🇸🇦 نظرة عامة على المشروع

يحوّل هذا المشروع بيانات حجوزات فندقية خامة (2018–2020، حوالي 142,000 حجز في فندقين) إلى لوحة معلومات تفاعلية في Power BI، مصممة للإجابة على ثلاثة أسئلة أساسية تهم إدارة الفندق:

1. **هل الإيرادات في نمو؟**
2. **هل نحتاج لزيادة سعة مواقف السيارات؟**
3. **ما هي الاتجاهات التشغيلية وأنماط الحجز التي يجب أن تكون الإدارة على دراية بها؟**

### مصادر البيانات

- `2018.csv`، `2019.csv`، `2020.csv` — بيانات الحجوزات الخام (32 حقلًا لكل حجز: التواريخ، مدة الإقامة، السعر اليومي، شريحة السوق، حالة الإلغاء، بيانات النزيل، إلخ)
- `market_segment.csv` — نسبة الخصم المطبّقة على كل شريحة سوق
- `meal_cost.csv` — تكلفة كل وجبة حسب نوع الخطة (إفطار فقط، نصف إقامة، إقامة كاملة، بدون وجبات)

### المنهجية

لم تُفترض صيغة الإيراد اعتباطًا، بل **تم التحقق منها مقابل البيانات المصدرية وتأكيدها من قسم المحاسبة في الفندق** قبل اعتمادها بشكل نهائي. أبرز القرارات المنهجية:

- **الإيراد = عدد الليالي × (السعر اليومي × (1 - الخصم) + تكلفة الوجبة)**، حيث:
  - تم التأكد أن السعر اليومي (ADR) لا يشمل تكلفة الوجبة ولا الخصم (تم التحقق من ذلك من قسم المحاسبة)
  - تُحتسب تكلفة الوجبة حسب كل وجبة يطلبها النزيل، وبالتالي تتناسب مع مدة الإقامة
  - يُطبّق الخصم على سعر الغرفة، ويختلف حسب شريحة السوق، ويُطبّق بشكل موحّد على جميع أنواع الغرف
- **الإيراد المحقق** يُحتسب فقط للحجوزات غير الملغاة، لأن الحجز الملغى لا يُولّد دخلًا فعليًا أبدًا
- يُعرض **إجمالي الإيراد (المفترض)** بشكل منفصل لقياس الفجوة بين ما تم حجزه وما تحقق فعليًا — وهو مبدأ محاسبي قياسي (الإجمالي مقابل الصافي)، تم تطويعه هنا أيضًا لعزل أثر الإلغاء حسب شريحة السوق

تم بناء جميع المقاييس الأساسية في كل من SQL (لتجهيز البيانات وإنشاء الـ Views) وDAX (لنموذج Power BI)، وتم التحقق من تطابقها مع حسابات مباشرة على ملفات CSV الخام لضمان الاتساق قبل عرضها في اللوحة.

### أبرز النتائج

| المؤشر | القيمة |
|---|---|
| إجمالي الإيراد المحجوز | ~44.7 مليون$ |
| الإيراد المحقق | ~27.5 مليون$ |
| الإيراد المفقود بسبب الإلغاءات | ~17.2 مليون$ |
| إجمالي الخصومات (للحجوزات المحققة) | ~7.59 مليون$ |
| إجمالي إيراد الوجبات (للحجوزات المحققة) | ~4.58 مليون$ |
| الحجوزات غير الملغاة | 89,108 (63%) |
| الحجوزات الملغاة | 52,839 (37%) |

**أبرز رؤية:** تتفاوت نسبة الإلغاء بشكل كبير حسب شريحة السوق — من 12% (Complementary) إلى **62% (Groups)**، وهي الأعلى على الإطلاق.

### هيكل اللوحة

- **الصفحة الأولى — الإيرادات:** النمو عبر الزمن (مُطبَّع شهريًا لمراعاة البيانات غير المكتملة لبعض السنوات)، الإيراد حسب الفندق/الشريحة/القناة/الوجبة/نوع العميل، تحليل الخصومات
- **الصفحة الثانية — الرؤى التشغيلية:** نسبة الإلغاء مقابل الإتمام حسب الشريحة، اتجاهات الطلب على المواقف، توزيع أنواع النزلاء، نسبة النزلاء المتكررين، تحليل نوع العربون

### قيود معروفة

- يتم تتبّع الطلب على مواقف السيارات، لكن لا تحتوي البيانات على رقم يوضّح **السعة الفعلية** للموقف، لذا تعرض اللوحة اتجاهات الطلب فقط دون إصدار توصية بشأن السعة.
- تحتوي بيانات 2018 و2020 على سنوات غير مكتملة (6 و8 أشهر على التوالي مقابل 12 شهرًا في 2019)؛ تم تصنيف الرسوم البيانية وتطبيعها وفقًا لذلك لتجنّب أي مقارنة مضلّلة بين السنوات.
- تفترض "خسارة الغرف الملغاة" أن الغرف الملغاة بقيت شاغرة؛ قد تكون الخسارة الفعلية أقل في حال إعادة بيع تلك الغرف، خاصة في حالات الإلغاء المبكر.

### الأدوات المستخدمة

`SQL` (تصميم البيانات والـ Views) · `Power BI` (نموذج البيانات، DAX، التصور) ·
